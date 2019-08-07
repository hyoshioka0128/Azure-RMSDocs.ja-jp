---
title: ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行 - AIP
description: この手順は、AD RMS から Azure Information Protection への移行パスの一部であり、AD RMS キーがソフトウェアで保護されているときにソフトウェアで保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5bbf064cb019b663b62a779bf58322e0b23302e8
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68790548"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>手順 2:ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


この手順は、[AD RMS から Azure Information Protection への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーがソフトウェアで保護されているときにソフトウェアで保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。 

選択した構成シナリオでない場合、[手順 4 に戻り、AD RMS から構成データをエクスポートし、それを Azure RMS にインポートし](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection)、別の構成を選択します。

以下の手順を使用して、AD RMS 構成を Azure Information Protection にインポートします。結果は Microsoft が管理する Azure Information Protection テナント キーです。

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>構成データを Azure Information Protection にインポートするには

1. インターネットに接続されたワークステーションで、 [connect-AipService](/powershell/module/aipservice/connect-aipservice)コマンドレットを使用して、Azure Rights Management サービスに接続します。

    ```
    Connect-AipService
    ```
    プロンプトが表示されたら、Azure Rights Management テナント管理者の資格情報を入力します (通常は、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使います)。

2. [Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)コマンドレットを使用して、エクスポートされた各信頼された発行ドメイン (.xml) ファイルをアップロードします。 たとえば、暗号化モード 2 用に AD RMS クラスターをアップグレードした場合、少なくとも 1 つの追加ファイルが必要です。 
    
    このコマンドレットを実行するには、各構成データ ファイルに対して以前指定したパスワードが必要です。 
    
    たとえば、最初に以下を実行してパスワードを格納します。
    
        $TPD_Password = Read-Host -AsSecureString
    
    指定したパスワードを入力して、最初の構成データ ファイルをエクスポートします。 次に、構成ファイルの例として E:\contosokey1.xml を使用して次のコマンドを実行し、この操作の実行を確定します。
    ```
    Import-AipServiceTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. 各ファイルをアップロードしたら、 [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)を実行して、AD RMS で現在アクティブになっている SLC キーと一致するインポートされたキーを識別します。 このキーは、Azure Rights Management サービスのアクティブなテナント キーとなります。

4.  [Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice)コマンドレットを使用して、Azure Rights Management サービスとの接続を切断します。

    ```
    Disconnect-AipServiceService
    ```

以上で「[手順 5. Azure Rights Management サービスをアクティブにする](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)」に進む準備ができました。


