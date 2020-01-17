---
title: HSM で保護されているキーから HSM で保護されているキーへの移行 - AIP
description: AD RMS から Azure Information Protection への移行パスの一部であり、AD RMS キーが HSM で保護されていて、Azure Key Vault 内の HSM で保護されているテナントキーを使用して Azure Information Protection に移行する場合にのみ適用される手順。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/11/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 888da129f3b6897303cb2731d23afc52f6261cce
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117954"
---
# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>手順 2. HSM で保護されているキーから HSM で保護されているキーへの移行

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*


この手順は、[AD RMS から Azure Information Protection への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーが HSM で保護されているときに Azure Key Vault 内の HSM で保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。 

これが選択した構成シナリオでない場合は、[手順4に戻ります。構成データを AD RMS からエクスポートし、Azure RMS にインポート](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection)して、別の構成を選択します。

> [!NOTE]
> これらの手順は、AD RMS キーがモジュールで保護されていることを前提としています。 これは、最も一般的なケースです。 

これは、HSM キーと AD RMS 構成を Azure Information Protection にインポートする 2 段階の手順で、結果はお客様が管理 (BYOK) する Azure Information Protection テナント キーです。

Azure Information Protection テナント キーは Azure Key Vault によって格納され管理されるので、移行のこの部分では、Azure Information Protection だけでなく、Azure Key Vault での管理も必要です。 Azure Key Vault が組織で自分以外の管理者によって管理されている場合は、その管理者と調整し、連携してこれらの手順を完了する必要があります。

作業を開始する前に、Azure Key Vault で作成されたキー コンテナーが組織に存在すること、さらに HSM で保護されたキーがサポートされていることを確認します。 必須ではありませんが、Azure Information Protection に専用のキー コンテナーを用意することをお勧めします。 このキー コンテナーは、Azure Rights Management サービスからのアクセスを許可するように構成されます。結果、このキー コンテナーに格納されるキーは、Azure Information Protection キーのみに限定される必要があります。


> [!TIP]
> Azure Key Vault の構成手順を実行中で、この Azure サービスに慣れていない方は、最初に「[Azure Key Vault の概要](/azure/key-vault/key-vault-get-started)」を参照することをお勧めします。 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>パート 1: Azure Key Vault に HSM キーを転送する

これらの手順は、Azure Key Vault の管理者によって実行されます。

1. Azure Key Vault で格納するエクスポート済みの各 SLC キーに対して、Azure Key Vault のドキュメントの「[Azure Key Vault の Bring Your Own Key (BYOK) の実装](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault)」に記載された手順に従います。ただし、次の例外があります。

   - 「**テナント キーを生成する**」の手順を実行しないでください。それと同等のものが、既に AD RMS のデプロイメントから取得されています。 代わりに、nCipher インストールから AD RMS サーバーが使用するキーを特定し、それらのキーを転送用に準備してから、Azure Key Vault に転送します。 
        
        NCipher の暗号化されたキーファイルの名前は、サーバー上のローカルの **<em>keyappname</em>> _ <<em>keyappname</em>>に key_ <** ます。 たとえば、 `C:\Users\All Users\nCipher\Key Management Data\local\key_mscapi_f829e3d888f6908521fe3d91de51c25d27116a54`のように指定します。 KeyTransferRemote コマンドを実行して、アクセス許可が制限されたキーのコピーを作成する場合は、keyAppName として**mscapi**値を指定し、キー識別子に独自の値を指定する必要があります。
        
        Azure Key Vault にキーがアップロードされるとき、表示されたキーのプロパティ (キーの ID が含まれている) を確認できます。 これは、https\://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 のようになります。 この URL をメモしてください。Azure Information Protection の管理者は、Azure Rights Management サービスにそのテナント キーとしてこのキーを使用するように指示するときに、この URL を使用する必要があります。

2. インターネットに接続されたワークステーションの PowerShell セッションで、 [AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)コマンドレットを使用して、Azure Information Protection テナントキーを格納する key vault にアクセスするように Azure Rights Management サービスプリンシパルを承認します。 必要な権限は、decrypt、encrypt、unwrapkey、wrapkey、verify、および sign です。
    
    たとえば、Azure Information Protection 用に作成したキー コンテナーの名前が contoso-byok-ky、リソース グループの名前が contoso-byok-rg である場合は、次のコマンドを実行します。
    
        Set-AzKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get


これで、Azure Information Protection から Azure Rights Management サービスに対して Azure Key Vault の HSM キーが準備されたので、AD RMS 構成データをインポートできます。

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>パート 2: 構成データを Azure Information Protection にインポートする

これらの手順は、Azure Information Protection の管理者によって実行されます。

1. インターネット接続ワークステーションと PowerShell セッションで、 [connect-AipService](/powershell/module/aipservice/connect-aipservice)コマンドレットを使用して Azure Rights Management サービスに接続します。
    
    次に、 [Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)コマンドレットを使用して、信頼された発行ドメイン (.xml) ファイルをアップロードします。 たとえば、暗号化モード 2 用に AD RMS クラスターをアップグレードした場合、少なくとも 1 つの追加ファイルが必要です。
    
    このコマンドレットを実行するには、各構成データ ファイルに対して以前指定したパスワードと前の手順で指定したキーの URL が必要です。
    
    たとえば、\contoso-tpd1.xml の構成データ ファイルと前の手順で取得したキーの URL 値を使用し、まず以下を実行してパスワードを格納します。
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
    指定したパスワードを入力して構成データ ファイルをエクスポートします。 次に、以下のコマンドを実行して、この操作を行うことを確認します。
    
    ```
    Import-AipServiceTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword $TPD_Password –KeyVaultKeyUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```
    
    このインポート処理の一部として、SLC キーがインポートされ、自動でアーカイブ済みに設定されます。

2.  各ファイルをアップロードしたら、 [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)を実行して、AD RMS クラスター内の現在アクティブな SLC キーと一致するインポートされたキーを指定します。 このキーは、Azure Rights Management サービスのアクティブなテナント キーとなります。

3.  [Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice)コマンドレットを使用して、Azure Rights Management サービスとの接続を切断します。

    ```
    Disconnect-AipServiceService
    ```

Azure Information Protection テナントキーが Azure Key Vault で使用しているキーを後で確認する必要がある場合は、 [Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) Azure RMS コマンドレットを使用します。

これで、手順 5. に進むことができ[ます。Azure Rights Management サービスをアクティブ化](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)します。


