---
title: "手順 2.&colon; ソフトウェアで保護されているキーから HSM で保護されているキーへの移行 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7a9c8b531ec342e7d5daf0cbcacd6597a79e6a55
ms.openlocfilehash: 173641b9dada2673b48a1c210419cb933cdd9f13


---

# 手順 2. ソフトウェアで保護されているキーから HSM で保護されているキーへの移行

*適用対象: Active Directory Rights Management サービス、Azure Rights Management*


これらの手順は [AD RMS から Azure Rights Management への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーがソフトウェアで保護されているときに HSM で保護されているテナント キーを持つ Azure Rights Management に移行する場合にのみ適用されます。 

選択した構成シナリオでない場合、[手順 2 に戻ってください。AD RMS から構成データをエクスポートし、それを Azure RMS にインポートし](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)、別の構成を選択します。

3 段階の手順で AD RMS 構成を Azure RMS にインポートし、結果は顧客管理 (BYOK) の Azure RMS テナント キーです。

最初にサーバー ライセンサー証明書 (SLC) キーを構成データから抽出し、キーをオンプレミス Thales HSM に転送した後、HSM キーをパッケージ化して Azure RMS に転送し、構成データをインポートします。

## パート 1: 構成データから SLC を抽出し、オンプレミス HSM にキーをインポートする

1.  「[Azure Rights Management テナント キーを計画して実装する](plan-implement-tenant-key.md)」の「[BYOK (Bring Your Own Key) の実装](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key)」セクションの手順に従います。その際、「**テナント キーを生成して転送する – インターネット経由**」の手順を使用します。例外を次に示します。

    -   **テナント キーを生成して転送する – インターネット経由**: **インターネット接続ワークステーションを準備する**

    -   **テナント キーを生成して転送する – インターネット経由**: **未接続ワークステーションを準備する**

    手順に従ってテナント キーを生成しないでください。既に、エクスポートされた構成データ (.xml) ファイルに同等のものがあります。 代わりに、コマンドを実行してファイルからこのキーを抽出し、オンプレミス HSM にインポートします。

2.  切断されているワークステーションで、次のコマンドを実行します。

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    北米の場合: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    追加情報:

    -   ImportRmsCentrallyManagedKey パラメーターは、操作が SLC キーのインポートであることを示します。

    -   パスワードをコマンドで指定しないと、指定するように求められます。

    -   KeyIdentifier パラメーターは、キー ファイルの名前を作成するキーのフレンドリ名です。 子文字の ASCII 文字のみを使用する必要があります。

    -   ExchangeKeyPackage パラメーターは、名前の先頭に BYOK-KEK-pkg- が付く地域固有のキー交換キー (KEK) パッケージを指定します。

    -   NewSecurityWorldPackage パラメーターは、名前の先頭に BYOK-SecurityWorld-pkg- が付く地域固有のセキュリティ ワールド パッケージを指定します。

    このコマンドの結果は次のようになります。

    -   HSM のキー ファイル: %NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   SLC が除去された RMS 構成データ ファイル: %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  RMS 構成データ ファイルが複数ある場合は、残りのファイルに手順 2. を繰り返します。

SLC を HSM ベースのキーとして抽出したので、パッケージ化して Azure RMS に転送できます。

## パート 2:HSM キーをパッケージ化して Azure RMS に転送する

1.  「[Azure Rights Management テナント キーを計画して実装する](plan-implement-tenant-key.md)」の「[BYOK (Bring Your Own Key) の実装](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key)」セクションの次の手順を使用します。

    -   **テナント キーを生成して転送する – インターネット経由**: **テナント キーの転送を準備する**

    -   **テナント キーを生成して転送する – インターネット経由**: **テナント キーの Azure RMS への転送**

これで、HSM キーを Azure RMS に転送しました。AD RMS 構成データをインポートする準備が整いました。構成データには新しく転送されたテナント キーへのポインターのみが含まれます。

## パート 3:構成データを Azure RMS にインポートする

1.  インターネットに接続されたワークステーションと Windows PowerShell セッションのままで、SLC が除去された RMS 構成ファイルをコピーします (切断されたワークステーションから、%NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  最初のファイルをアップロードします。 信頼された発行ドメインが複数あるために複数の .xml ファイルがある場合は、移行後にコンテンツを保護するために Azure RMS で使用する HSM キーに対応するエクスポートされた信頼された発行ドメインが含まれるファイルを選択します。 次のコマンドを使用します。

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    例: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    プロンプトが表示されたら、前に指定したパスワードを入力し、この操作を実行することを確認します。

3.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 2 を繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。 例: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) コマンドレットを使用して Azure RMS サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

以上で「[手順 3. RMS テナントをアクティブ化する](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)」に進む準備が完了しました。





<!--HONumber=Jul16_HO3-->


