---
title: HSM で保護されているキーから HSM で保護されているキーへの移行 - AIP
description: この手順は、AD RMS から Azure Information Protection への移行パスの一部であり、AD RMS キーが HSM で保護されているときに Azure Key Vault 内の HSM で保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/19/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c8ed0fd3e8daa2c03f179cf71c0c258b8ef79901
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>手順 2. HSM で保護されているキーから HSM で保護されているキーへの移行

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*


この手順は、[AD RMS から Azure Information Protection への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーが HSM で保護されているときに Azure Key Vault 内の HSM で保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。 

選択した構成シナリオでない場合、[手順 4 に戻り、AD RMS から構成データをエクスポートし、それを Azure RMS にインポートし](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection)、別の構成を選択します。

> [!NOTE]
> これらの手順は、AD RMS キーがモジュールで保護されていることを前提としています。 これは、最も一般的なケースです。 

これは、HSM キーと AD RMS 構成を Azure Information Protection にインポートする 2 段階の手順で、結果はお客様が管理 (BYOK) する Azure Information Protection テナント キーです。

Azure Information Protection テナント キーは Azure Key Vault によって格納され管理されるので、移行のこの部分では、Azure Information Protection だけでなく、Azure Key Vault での管理も必要です。 Azure Key Vault が組織で自分以外の管理者によって管理されている場合は、その管理者と調整し、連携してこれらの手順を完了する必要があります。

作業を開始する前に、Azure Key Vault で作成されたキー コンテナーが組織に存在すること、さらに HSM で保護されたキーがサポートされていることを確認します。 必須ではありませんが、Azure Information Protection に専用のキー コンテナーを用意することをお勧めします。 このキー コンテナーは、Azure Rights Management サービスからのアクセスを許可するように構成されます。結果、このキー コンテナーに格納されるキーは、Azure Information Protection キーのみに限定される必要があります。


> [!TIP]
> Azure Key Vault の構成手順を実行中で、この Azure サービスに慣れていない方は、最初に「[Azure Key Vault の概要](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)」を参照することをお勧めします。 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>パート 1: Azure Key Vault に HSM キーを転送する

これらの手順は、Azure Key Vault の管理者によって実行されます。

1. Azure Key Vault で格納するエクスポート済みの各 SLC キーに対して、Azure Key Vault のドキュメントの「[Azure Key Vault の Bring Your Own Key (BYOK) の実装](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azurekey-vault)」に記載された手順に従います。ただし、次の例外があります。

    - 「**テナント キーを生成する**」の手順を実行しないでください。それと同等のものが、既に AD RMS のデプロイメントから取得されています。 Thales のインストールから AD RMS サーバーで使用されるキーを識別し、移行中にこのキーを使用する必要があります。 Thales で暗号化されたキー ファイルの名前は通常、サーバー上のローカルな **key<*keyAppName*><*keyIdentifier*>** です。

    Azure Key Vault にキーがアップロードされるとき、表示されたキーのプロパティ (キーの ID が含まれている) を確認できます。 出力は、https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 のようになります。 この URL をメモしてください。Azure Information Protection の管理者は、Azure Rights Management サービスにそのテナント キーとしてこのキーを使用するように指示するときに、この URL を使用する必要があります。

2. インターネットに接続されたワークステーションの PowerShell セッションで、[Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) コマンドレットを使って、Azure Information Protection テナント キーを保存するキー コンテナーに Azure Rights Management サービス プリンシパルがアクセスするのを承認します。 必要な権限は、decrypt、encrypt、unwrapkey、wrapkey、verify、および sign です。
    
    たとえば、Azure Information Protection 用に作成したキー コンテナーの名前が contoso-byok-ky、リソース グループの名前が contoso-byok-rg である場合は、次のコマンドを実行します。
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get


これで、Azure Information Protection から Azure Rights Management サービスに対して Azure Key Vault の HSM キーが準備されたので、AD RMS 構成データをインポートできます。

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>パート 2: 構成データを Azure Information Protection にインポートする

これらの手順は、Azure Information Protection の管理者によって実行されます。

1. インターネットに接続されたワークステーションでの PowerShell セッションで、[Connnect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) コマンドレットを使用して Azure Rights Management サービスに接続します。
    
    [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) コマンドレットを使用して、各信頼された発行ドメイン (.xml) ファイルをアップロードします。 たとえば、暗号化モード 2 用に AD RMS クラスターをアップグレードした場合、少なくとも 1 つの追加ファイルが必要です。
    
    このコマンドレットを実行するには、各構成データ ファイルに対して以前指定したパスワードと前の手順で指定したキーの URL が必要です。
    
    たとえば、\contoso-tpd1.xml の構成データ ファイルと前の手順で取得したキーの URL 値を使用し、まず以下を実行してパスワードを格納します。
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
    指定したパスワードを入力して構成データ ファイルをエクスポートします。 次に、以下のコマンドを実行して、この操作を行うことを確認します。
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```
    
    このインポート処理の一部として、SLC キーがインポートされ、自動でアーカイブ済みに設定されます。

2.  各ファイルをアップロードしたら [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) を実行して、AD RMS クラスターで現在アクティブな SLC キーと一致するインポート済みのキーを指定します。 このキーは、Azure Rights Management サービスのアクティブなテナント キーとなります。

3.  [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) コマンドレットを使用して Azure Rights Management サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

Azure Key Vault で Azure Information Protection テナント キーが使用しているキーを後で確認する必要がある場合は、Azure RMS コマンドレット [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) を使用します。

以上で「[手順 5. Azure Rights Management サービスをアクティブにする](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)」に進む準備ができました。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

