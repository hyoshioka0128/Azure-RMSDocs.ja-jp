---
title: "手順 2.&colon; HSM で保護されているキーから HSM で保護されているキーへの移行 | Azure Information Protection"
description: "この手順は、AD RMS から Azure Information Protection への移行パスの一部であり、AD RMS キーが HSM で保護されているときに Azure Key Vault 内の HSM で保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。"
author: cabailey
manager: mbaldwin
ms.date: 10/14/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bad084502b9b7e55c6e80dccfbd66c3f34b63c7c
ms.openlocfilehash: 8d9538cb2663edce5fc343ed9710032505c15293


---

# 手順 2. HSM で保護されているキーから HSM で保護されているキーへの移行

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection*


この手順は、[AD RMS から Azure Information Protection への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーが HSM で保護されているときに Azure Key Vault 内の HSM で保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。 

選択した構成シナリオでない場合、[手順 2 に戻ってください。AD RMS から構成データをエクスポートし、それを Azure RMS にインポートし](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)、別の構成を選択します。

> [!NOTE]
> これらの手順は、AD RMS キーがモジュールで保護されていることを前提としています。 これは、最も一般的なケースです。 

これは、HSM キーと AD RMS 構成を Azure Information Protection にインポートする 2 段階の手順で、結果はお客様が管理 (BYOK) する Azure Information Protection テナント キーです。

Azure Information Protection テナント キーは Azure Key Vault によって格納され管理されるので、移行のこの部分では、Azure Information Protection だけでなく、Azure Key Vault での管理も必要です。 Azure Key Vault が組織で自分以外の管理者によって管理されている場合は、その管理者と調整を行い連携してこれらの手順を完了する必要があります。

作業を開始する前に、Azure Key Vault で作成されたキー コンテナーが組織に存在すること、さらに HSM で保護されたキーがサポートされていることを確認します。 必須ではありませんが、Azure Information Protection に専用のキー コンテナーを用意することをお勧めします。 このキー コンテナーは、Azure Rights Management サービスからのアクセスを許可するように構成されます。結果、このキー コンテナーに格納されるキーは、Azure Information Protection キーのみに限定される必要があります。


> [!TIP]
> Azure Key Vault の構成手順を実行する予定であるが、この Azure サービスに慣れていない場合は、最初に「[Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)」 (Azure Key Vault の概要) を参照することをお勧めします。 


## パート 1: Azure Key Vault に HSM キーを転送する

これらの手順は、Azure Key Vault の管理者によって実行されます。

1.  Azure Key Vault のドキュメントの「[Azure Key Vault の独自のキー (BYOK) の実装](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault)」に記載された手順に従います。ただし、次の例外があります。

    - 「**テナント キーを生成する**」の手順を実行しないでください。それと同等のものが、既に AD RMS のデプロイメントから取得されています。 Thales のインストールから AD RMS サーバーで使用されるキーを識別し、移行中にこのキーを使用する必要があります。 Thales で暗号化されたキー ファイルの名前は通常、サーバー上のローカルな **key<*keyAppName*><*keyIdentifier*>** です。

    Azure Key Vault にキーがアップロードされるとき、表示されたキーのプロパティ (キーの ID が含まれている) を確認できます。 https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 のようになります。 この URL をメモしてください。Azure Information Protection の管理者は、Azure Rights Management サービスにそのテナント キーとしてこのキーを使用するように指示するときに、この URL を使用する必要があります。

2. インターネットに接続されたワークステーションでの PowerShell セッションで、[Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/en-us/library/mt603625(v=azure.300\).aspx) コマンドレットを使用して、Azure Information Protection テナント キーを保存するキー コンテナーへの Microsoft.Azure.RMS という名前のサービス プリンシパルによるアクセスを承認します。 必要な権限は、decrypt、encrypt、unwrapkey、wrapkey、verify、および sign です。
    
    たとえば、Azure Information Protection 用に作成したキー コンテナーの名前が contoso-byok-ky、リソース グループの名前が contoso-byok-rg である場合は、次のコマンドを実行します。
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get


これで、Azure Information Protection から Azure Rights Management サービスに対して Azure Key Vault の HSM キーが準備されたので、AD RMS 構成データをインポートできます。

## パート 2: 構成データを Azure Information Protection にインポートする

これらの手順は、Azure Information Protection の管理者によって実行されます。

1.  インターネットに接続されたワークステーションでの PowerShell セッションで、[Connnect-AadrmService](https://msdn.microsoft.com/library/dn629415.aspx) コマンドレットを使用して Azure Rights Management サービスに接続します。
    
    [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx) コマンドレットを使用して、最初にエクスポートした信頼された発行ドメイン (.xml) ファイルをアップロードします。 信頼された発行ドメインが複数あるために複数の .xml ファイルがある場合は、移行後にコンテンツを保護するために Azure RMS で使用する HSM キーに対応するエクスポートされた信頼された発行ドメインが含まれるファイルを選択します。 
    
    このコマンドレットを実行するには、前の手順で識別されたキーの URL が必要です。
    
    たとえば、前の手順で取得したキーの URL 値と、C:\contoso-tpd1.xml の TPD ファイルを使用して、次を実行します。
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```
    
    プロンプトが表示されたら、前に指定したパスワードを入力し、この操作を実行することを確認します。

2.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 1 を繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。  

3.  [Disconnect-AadrmService](https://msdn.microsoft.com/library/azure/dn629416.aspx) コマンドレットを使用して Azure Rights Management サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Azure Key Vault で Azure Information Protection テナント キーが使用しているキーを後で確認する必要がある場合は、Azure RMS コマンドレット [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) を使用します。

以上で「[手順 3. Azure Information Protection テナントをアクティブ化する](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)」に進む準備ができました。




<!--HONumber=Oct16_HO3-->


