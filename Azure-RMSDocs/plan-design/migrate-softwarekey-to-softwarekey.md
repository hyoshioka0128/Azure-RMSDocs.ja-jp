---
title: "ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行 - AIP"
description: "この手順は、AD RMS から Azure Information Protection への移行パスの一部であり、AD RMS キーがソフトウェアで保護されているときにソフトウェアで保護されているテナント キーを持つ Azure Information Protection に移行する場合にのみ適用されます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 60370cc34184b28f5cdecf6ad51f9ba58dd4816a
ms.sourcegitcommit: 77b0936bea2700eb12b580e5738e077d447d5686
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

2. [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) コマンドレットを使用して、最初にエクスポートした信頼された発行ドメイン (.xml) ファイルをアップロードします。 信頼された発行ドメインが複数あるために複数の .xml ファイルがある場合は、移行後にコンテンツを保護するために Azure Information Protection で使用するエクスポートされた信頼された発行ドメインが含まれるファイルを選択します。 次のコマンドを使用します。

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    [ConvertTo-SecureString -AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) または [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) を使用し、セキュリティで保護された文字列としてパスワードを指定します。 ConvertTo-SecureString を使用する場合で、パスワードに特殊文字が含まれているときは、単一引用符の間にパスワードを入力するか、特殊文字をエスケープします。
    
    例: まず **$TPD_Password = Read-Host -AsSecureString** を実行し、上記の手順で指定したパスワードを入力します。 次に **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose** を実行します。 メッセージが表示されたら、この操作を実行することを確認します。
    
3.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 3 を繰り返します。 たとえば、暗号化モード 2 用に AD RMS クラスターをアップグレードした場合、少なくとも 1 つの追加ファイルが必要です。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。 例: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

4.  [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) コマンドレットを使用して Azure Rights Management サービスから切断します。

    ```
    Disconnect-AadrmService
    ```


以上で「[手順 5. Azure Information Protection テナントをアクティブ化する](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)」に進む準備ができました。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

