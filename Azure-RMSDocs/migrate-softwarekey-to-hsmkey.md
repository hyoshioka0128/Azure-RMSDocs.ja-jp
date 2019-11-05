---
title: ソフトウェアで保護されているキーから HSM で保護されているキーへの移行 - AIP
description: この手順は、AD RMS から Azure Information Protection への移行パスの一部であり、AD RMS キーが HSM で保護されているときに Azure Key Vault 内のソフトウェアで保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bb23ceb2721e18f8028ec5b0bb19a2c7230d9c1f
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559173"
---
# <a name="step-2-software-protected-key-to-hsm-protected-key-migration"></a>手順 2. ソフトウェアで保護されているキーから HSM で保護されているキーへの移行

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*


この手順は、[AD RMS から Azure Information Protection への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーが HSM で保護されているときに Azure Key Vault 内のソフトウェアで保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。 

これが選択した構成シナリオでない場合は、[手順4に戻ります。構成データを AD RMS からエクスポートし、Azure RMS にインポート](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection)して、別の構成を選択します。

これは、AD RMS 構成を Azure Information Protection にインポートする 4 段階の手順で、結果は Azure Key Vault でお客様が管理 (BYOK) する Azure Information Protection テナント キーです。

まず、AD RMS 構成データからサーバーライセンサー証明書 (SLC) キーを抽出し、キーをオンプレミスの nCipher HSM に転送し、次に HSM キーをパッケージ化して Azure Key Vault に転送してから、Azure Rights Management サービスを承認する必要があります。キーコンテナーへのアクセスを Azure Information Protection し、構成データをインポートします。

Azure Information Protection テナント キーは Azure Key Vault によって格納され管理されるので、移行のこの部分では、Azure Information Protection だけでなく、Azure Key Vault での管理も必要です。 Azure Key Vault が組織で自分以外の管理者によって管理されている場合は、その管理者と調整し、連携してこれらの手順を完了する必要があります。

作業を開始する前に、Azure Key Vault で作成されたキー コンテナーが組織に存在すること、さらに HSM で保護されたキーがサポートされていることを確認します。 必須ではありませんが、Azure Information Protection に専用のキー コンテナーを用意することをお勧めします。 このキー コンテナーは、Azure Information Protection からの Azure Rights Management サービスによるアクセスを許可するように構成されます。結果、このキー コンテナーに格納されるキーは、Azure Information Protection キーのみに限定される必要があります。


> [!TIP]
> Azure Key Vault の構成手順を実行中で、この Azure サービスに慣れていない方は、最初に「[Azure Key Vault の概要](/azure/key-vault/key-vault-get-started)」を参照することをお勧めします。 


## <a name="part-1-extract-your-slc-key-from-the-configuration-data-and-import-the-key-to-your-on-premises-hsm"></a>パート 1: 構成データから SLC キーを抽出し、オンプレミス HSM にキーをインポートする

1.  Azure Key Vault 管理者: Azure Key Vault で格納するエクスポート済みの各 SLC キーに対して、Azure Key Vault のドキュメントの「[Azure Key Vault の独自のキー (BYOK) の実装](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault)」セクションに記載された次の手順を実行します。

    -   **キーを生成して HSM Azure Key Vault に転送する**:[手順 1: インターネット接続ワークステーションを準備](/azure/key-vault/key-vault-hsm-protected-keys#step-1-prepare-your-internet-connected-workstation)する

    -   **テナントキーを生成して転送する–インターネット経由**:[手順 2: 未接続ワークステーションを準備する](/azure/key-vault/key-vault-hsm-protected-keys#step-2-prepare-your-disconnected-workstation)

    手順に従ってテナント キーを生成しないでください。既に、エクスポートされた構成データ (.xml) ファイルに同等のものがあります。 代わりに、ツールを実行してファイルからこのキーを抽出し、オンプレミス HSM にインポートします。 ツールを実行すると、次の 2 つのファイルが作成されます。

    - キーを使用しない新しい構成データ ファイル。Azure Information Protection テナントにインポートする準備ができています。

    - キーを使用する PEM ファイル (キー コンテナー)。オンプレミスの HSM にインポートする準備ができています。

2. Azure Information Protection 管理者または Azure Key Vault 管理者: 未接続のワークステーションで、[Azure RMS 移行ツールキット](https://go.microsoft.com/fwlink/?LinkId=524619)から TpdUtil ツールを実行します。 たとえば、ContosoTPD.xml という名前の構成データ ファイルをコピーする E ドライブにツールがインストールされている場合:

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

3. 同じ未接続のワークステーションで、nCipher のドキュメントに従って、nCipher HSM をアタッチして構成します。 次のコマンドを使用して、接続されている nCipher HSM にキーをインポートできるようになりました。その場合は、独自のファイル名を Contosotpd.pem に置き換える必要があります。

        generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA

    > [!NOTE]
    >ファイルが複数ある場合は、移行後にコンテンツを保護するために Azure RMS で使用する HSM キーに対応するファイルを選択します。

    これにより、次のような出力表示が生成されます。

    **キーの生成パラメーター:**

    **operation &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 実行する操作 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; インポート**

    **application &nbsp;&nbsp;&nbsp;&nbsp;アプリケーション&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; シンプル**

    **verify &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 構成キーのセキュリティの検証&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; はい**

    **type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; キーの種類 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; RSA キーを含む PEM ファイル &nbsp;&nbsp; e:\ContosoTPD.pem**

    **ident &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; キー識別子 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; キー名 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **キーは正常にインポートされました。**

    **キーへのパス: C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

この出力は、キーに保存された暗号化コピーを使用して、秘密キーがオンプレミスの nCipher HSM デバイスに移行されたことを確認します (この例では "key_simple_contosobyok")。 

SLC キーが抽出され、オンプレミスの HSM にインポートされたので、HSM で保護されたキーをパッケージ化し、Azure Key Vault に転送することができます。

> [!IMPORTANT]
> この手順を完了したら、未接続のワークステーションからこれらの PEM ファイルを確実に消去して、不正ユーザーがアクセスできないようにしてください。 たとえば、E: ドライブからすべてのファイルを確実に削除するには、"cipher /w: E" を実行します。

## <a name="part-2-package-and-transfer-your-hsm-key-to-azure-key-vault"></a>パート 2: HSM キーをパッケージ化して Azure Key Vault に転送する

Azure Key Vault 管理者: Azure Key Vault で格納するエクスポート済みの各 SLC キーに対して、Azure Key Vault のドキュメントの「[Azure Key Vault の独自のキー (BYOK) の実装](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault)」セクションに記載された次の手順を実行します。

- [手順 4: キーの転送を準備する](/azure/key-vault/key-vault-hsm-protected-keys#step-4-prepare-your-key-for-transfer)

- [手順 5: Azure Key Vault にキーを転送する](/azure/key-vault/key-vault-hsm-protected-keys#step-5-transfer-your-key-to-azure-key-vault)

キー ペアを生成する手順は実行しないでください。キーは既にあります。 代わりに、オンプレミスの HSM からこのキーを転送するコマンドを実行します (例では、KeyIdentifier パラメーターに "contosobyok" を使用しています)。

権限が制限されたキーのコピーを作成したとき (手順 4.1) およびキーを暗号化したとき (手順 4.3) に、KeyTransferRemote.exe ユーティティが **: SUCCESS**を返していることを確認してから、Azure Key Vault へのキーの転送を行ってください。

Azure Key Vault にキーがアップロードされるとき、表示されたキーのプロパティ (キーの ID が含まれている) を確認できます。 出力は、 **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** のようになります。 この URL をメモしてください。Azure Information Protection の管理者は、Azure Information Protection からの Azure Rights Management サービスにそのテナント キーとしてこのキーを使用するように指示するときに、この URL を使用する必要があります。

次に、 [AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)コマンドレットを使用して、key vault にアクセスするための Azure Rights Management サービスプリンシパルを承認します。 必要な権限は、decrypt、encrypt、unwrapkey、wrapkey、verify、および sign です。

たとえば、Azure Information Protection 用に作成したキー コンテナーの名前が contosorms-byok-kv、リソース グループの名前が contosorms-byok-rg である場合は、次のコマンドを実行します。
    
    Set-AzKeyVaultAccessPolicy -VaultName "contosorms-byok-kv" -ResourceGroupName "contosorms-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

これで、HSM キーが Azure Key Vault に転送されたので、AD RMS 構成データをインポートできます。

## <a name="part-3-import-the-configuration-data-to-azure-information-protection"></a>パート 3: 構成データを Azure Information Protection にインポートする

1. Azure Information Protection 管理者: インターネットに接続されたワークステーションと PowerShell セッションで、TpdUtil ツールを実行した後に、SLC キーが削除されている新しい構成データファイル (.xml) をコピーします。

2. [Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)コマンドレットを使用して、各 .xml ファイルをアップロードします。 たとえば、暗号化モード 2 用に AD RMS クラスターをアップグレードした場合、少なくとも 1 つの追加ファイルが必要です。

    このコマンドレットを実行するには、各構成データ ファイルに対して以前指定したパスワードと前の手順で指定したキーの URL が必要です。

    たとえば、C:\contoso_keyless.xml の構成データ ファイルと前の手順で取得したキーの URL 値を使用して、まず以下を実行してパスワードを格納します。
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
   指定したパスワードを入力して構成データ ファイルをエクスポートします。 次に、以下のコマンドを実行して、この操作を行うことを確認します。

    ```
    Import-AipServiceTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```

    このインポート処理の一部として、SLC キーがインポートされ、自動でアーカイブ済みに設定されます。

3. 各ファイルをアップロードしたら、 [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)を実行して、AD RMS クラスター内の現在アクティブな SLC キーと一致するインポートされたキーを指定します。

4. [Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice)コマンドレットを使用して、Azure Rights Management サービスとの接続を切断します。

    ```
    Disconnect-AipServiceService
    ```

Azure Information Protection テナントキーが Azure Key Vault で使用しているキーを後で確認する必要がある場合は、 [Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) Azure RMS コマンドレットを使用します。


これで、手順 5. に進むことができ[ます。Azure Rights Management サービスをアクティブ化](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)します。


