---
title: "手順 2.&colon; ソフトウェアで保護されているキーから HSM で保護されているキーへの移行 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 437afd88efebd9719a3db98f8ab0ae07403053f7
ms.openlocfilehash: bd93e781da7dc34c18e236a90a03dbc8fb012a1c


---

# 手順 2. ソフトウェアで保護されているキーから HSM で保護されているキーへの移行

*適用対象: Active Directory Rights Management サービス、Azure Rights Management*


これらの手順は [AD RMS から Azure Rights Management への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーがソフトウェアで保護されているときに Azure Key Vault 内の HSM で保護されているテナント キーを持つ Azure Rights Management に移行する場合にのみ適用されます。 

選択した構成シナリオでない場合、[手順 2 に戻ってください。AD RMS から構成データをエクスポートし、それを Azure RMS にインポートし](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)、別の構成を選択します。

4 段階の手順で AD RMS 構成を Azure RMS にインポートします。これにより、Azure RMS テナント キーは Azure Key Vault で BYOK によって管理されるようになります。

最初にサーバー ライセンサー証明書 (SLC) キーを AD RMS 構成データから抽出し、キーをオンプレミスの Thales HSM に転送します。次に、HSM キーをパッケージ化して Azure Key Vault に転送し、キー コンテナーへの Azure RMS のアクセスを承認し、構成データをインポートします。

Azure RMS テナント キーは Azure Key Vault によって格納され管理されるので、移行のこの部分では、Azure Key RMS だけでなく、Azure Key Vault での管理も必要です。 Azure Key Vault が組織で自分以外の管理者によって管理されている場合は、その管理者と調整を行い連携してこれらの手順を完了する必要があります。

作業を開始する前に、Azure Key Vault で作成されたキー コンテナーが組織に存在すること、さらに HSM で保護されたキーがサポートされていることを確認します。 必須ではありませんが、Azure RMS に専用のキー コンテナーを用意することをお勧めします。 このキー コンテナーは、Azure RMS からのアクセスを許可するように構成されます。結果、このキー コンテナーに格納されるキーは、Azure RMS キーのみに限定される必要があります。


> [!TIP]
> Azure Key Vault の構成手順を実行する予定であるが、この Azure サービスに慣れていない場合は、最初に「[Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)」 (Azure Key Vault の概要) を参照することをお勧めします。 


## パート 1: 構成データから SLC キーを抽出し、オンプレミス HSM にキーをインポートする

1.  Azure Key Vault 管理者: Azure Key Vault のドキュメントの「[Azure Key Vault の独自のキー (BYOK) の実装](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault)」セクションに記載された次の手順を使用します。

    -   **キーを生成し、Azure Key Vault HSM に転送する**: [手順 1: インターネット接続ワークステーションを準備する](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **テナント キーを生成して転送する – インターネット経由**: [手順 2: 未接続ワークステーションを準備する](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

    手順に従ってテナント キーを生成しないでください。既に、エクスポートされた構成データ (.xml) ファイルに同等のものがあります。 代わりに、ツールを実行してファイルからこのキーを抽出し、オンプレミス HSM にインポートします。 ツールを実行すると、次の 2 つのファイルが作成されます。

    - キーを使用しない新しい構成データ ファイル。Azure RMS テナントにインポートする準備ができています。

    - キーを使用する PEM ファイル (キー コンテナー)。オンプレミスの HSM にインポートする準備ができています。

2. Azure RMS 管理者または Azure Key Vault 管理者: 未接続のワークステーションで、[Azure RMS 移行ツールキット](https://go.microsoft.com/fwlink/?LinkId=524619)から TpdUtil ツールを実行します。 たとえば、ContosoTPD.xml という名前の構成データ ファイルをコピーする E ドライブにツールがインストールされている場合:

    ```
        E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    RMS 構成データ ファイルが複数ある場合は、残りのファイルに対してこのツールを実行します。

    このツールのヘルプ (説明、使用状況、および例が含まれている) を表示するには、パラメーターなしで TpdUtil.exe を実行します。

    このコマンドの追加情報:

    - **/tpd**: エクスポートした AD RMS 構成データ ファイルのフル パスと名前を指定します。 完全なパラメーター名は **TpdFilePath** です。

    - **/otpd**: キーを使用しないで構成データ ファイルの出力ファイル名を指定します。 完全なパラメーター名は **OutPfxFile** です。 このパラメーターを指定しない場合、既定では出力ファイルの名前にサフィックス **_keyless** が付けられ、ファイルは現在のフォルダーに格納されます。

    - **/opem**: PEM ファイルの出力ファイル名を指定します。これには、抽出されたキーが含まれます。 完全なパラメーター名は **OutPemFile** です。 このパラメーターを指定しない場合、既定では出力ファイルの名前にサフィックス **_key** が付けられ、ファイルは現在のフォルダーに格納されます。

    - このコマンドを実行するときに、**TpdPassword** の完全なパラメーター名または **pwd** の短いパラメーター名を使用してパスワードを指定しなかった場合は、パスワードを指定するように求められます。

3. 同じ未接続のワークステーションで、Thales のドキュメントに従って Thales HSM をアタッチして構成します。 次のコマンドを使用することで、アタッチした Thales HSM にキーをインポートできるようになりました。この場合は、独自のファイル名を ContosoTPD.pem に置換する必要があります。

        generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA

    > [!NOTE]
    >ファイルが複数ある場合は、移行後にコンテンツを保護するために Azure RMS で使用する HSM キーに対応するファイルを選択します。

    これにより、次のような出力表示が生成されます。

    **キーの生成パラメーター:**

    **operation &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 実行する操作 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; インポート**

    **application &nbsp;&nbsp;&nbsp;&nbsp;アプリケーション&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; シンプル**

    **verify &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 構成キーのセキュリティの検証 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; はい**

    **type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; キーの種類 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; RSA キーを含む PEM ファイル &nbsp;&nbsp; e:\ContosoTPD.pem**

    **ident &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; キー識別子 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; キー名 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **キーは正常にインポートされました。**

    **キーへのパス: C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

次の出力により、キー (この例では、"key_simple_contosobyok") に保存されている暗号化されたコピーを使用して秘密キーがオンプレミスの Thales HSM デバイスに移行されたことを確認できます。 

SLC キーが抽出され、オンプレミスの HSM にインポートされたので、HSM で保護されたキーをパッケージ化し、Azure Key Vault に転送することができます。

> [!IMPORTANT]
> この手順を完了したら、未接続のワークステーションからこれらの PEM ファイルを確実に消去して、不正ユーザーがアクセスできないようにしてください。 たとえば、E: ドライブからすべてのファイルを確実に削除するには、"cipher /w:E" を実行します。

## パート 2: HSM キーをパッケージ化して Azure Key Vault に転送する

1.  Azure Key Vault 管理者: Azure Key Vault のドキュメントの「[Azure Key Vault の独自のキー (BYOK) の実装](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault)」セクションに記載された次の手順を使用します。

    -   [手順 4: キーの転送を準備する](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

    -   [手順 5: Azure Key Vault にキーを転送する](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azure-key-vault)

    キー ペアを生成する手順は実行しないでください。キーは既にあります。 代わりに、オンプレミスの HSM からこのキーを転送するコマンドを実行します (例では、KeyIdentifier パラメーターに "contosobyok" を使用しています)。

    権限が制限されたキーのコピーを作成したとき (手順 4.1) およびキーを暗号化したとき (手順 4.3) に、KeyTransferRemote.exe ユーティティが**: SUCCESS**を返していることを確認してから、Azure Key Vault へのキーの転送を行ってください。

    Azure Key Vault にキーがアップロードされるとき、表示されたキーのプロパティ (キーの ID が含まれている) を確認できます。 **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** のようになります。 この URL をメモしてください。Azure RMS の管理者は、Azure RMS にそのテナント キーとしてこのキーを使用するように指示するときに、この URL を使用する必要があります。

    これで、HSM キーが Azure Key Vault に転送されたので、AD RMS 構成データをインポートできます。

## パート 3:構成データを Azure RMS にインポートする

1.  Azure RMS 管理者: インターネットに接続されたワークステーションでの PowerShell セッションで、TpdUtil ツールの実行後に、SLC キーが削除されている新しい構成データ ファイル (.xml) をコピーしてください。

2. [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx) コマンドレットを使用して最初の .xml ファイルをアップロードします。 信頼された発行ドメインが複数存在したためにこれらのファイルが複数ある場合は、移行後にコンテンツを保護するために Azure RMS で使用する HSM キーに対応するファイルを選択します。

    このコマンドレットを実行するには、前の手順で識別されたキーの URL が必要です。

    たとえば、前の手順で取得したキーの URL 値と、C:\contoso_keyless.xml の構成データ ファイルを使用して、次を実行します。

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```

    プロンプトが表示されたら、構成データ ファイルに対して前に指定したパスワードを入力し、この操作を実行することを確認します。

    構成データ ファイルが複数ある場合は、残りのファイルに対してこのコマンドを繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。



3.  [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) コマンドレットを使用して Azure RMS サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Azure Key Vault で Azure RMS テナント キーが使用しているキーを後で確認する必要がある場合は、Azure RMS コマンドレット [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) を使用します。


以上で「[手順 3. RMS テナントをアクティブ化する](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)」に進む準備が完了しました。






<!--HONumber=Aug16_HO3-->


