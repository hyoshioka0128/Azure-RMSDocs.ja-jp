---
title: "ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行 - AIP"
description: "この手順は、AD RMS から Azure Information Protection への移行パスの一部であり、AD RMS キーがソフトウェアで保護されているときにソフトウェアで保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ef3b3f08dfc73703f2bb05943645176c22134a02
ms.sourcegitcommit: 237ce3a0cc4921da5a08ed5753e6491403298194
translationtype: HT
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>手順 2. ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*


この手順は、[AD RMS から Azure Information Protection への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーがソフトウェアで保護されているときにソフトウェアで保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。 

選択した構成シナリオでない場合、[手順 4 に戻り、AD RMS から構成データをエクスポートし、それを Azure RMS にインポートし](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection)、別の構成を選択します。

以下の手順を使用して、AD RMS 構成を Azure Information Protection にインポートします。結果は Microsoft が管理する Azure Information Protection テナント キーです。

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>構成データを Azure Information Protection にインポートするには

1. インターネットに接続されたワークステーションで、[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) コマンドレットを使って Azure Rights Management サービスに接続します。

    ```
    Connect-AadrmService
    ```
    プロンプトが表示されたら、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] のテナント管理者資格情報を入力します (通常は、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使用します)。

2. [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) コマンドレットを使用して、エクスポートした各信頼された発行ドメイン (.xml) ファイルをアップロードします。 たとえば、暗号化モード 2 用に AD RMS クラスターをアップグレードした場合、少なくとも 1 つの追加ファイルが必要です。 
    
    このコマンドレットを実行するには、各構成データ ファイルに対して以前指定したパスワードが必要です。 
    
    たとえば、最初に以下を実行してパスワードを格納します。
    
        $TPD_Password = Read-Host -AsSecureString
    
    指定したパスワードを入力して、最初の構成データ ファイルをエクスポートします。 次に、構成ファイルの例として E:\contosokey1.xml を使用して次のコマンドを実行し、この操作の実行を確定します。
    ```
    Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. 各ファイルをアップロードしたら [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) を実行し、AD RMS で現在アクティブな SLC キーと一致するインポート済みのキーを指定します。 このキーは、Azure Rights Management サービスのアクティブなテナント キーとなります。

4.  [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) コマンドレットを使用して Azure Rights Management サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

以上で「[手順 5. Azure Rights Management サービスをアクティブにする](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)」に進む準備ができました。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

