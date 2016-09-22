---
title: "手順 2.&colon; ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行 | Azure RMS"
description: "AD RMS から Azure Rights Management への移行パスの一部であり、AD RMS キーがソフトウェアで保護されているときにソフトウェアで保護されているテナント キーを持つ Azure Rights Management に移行する場合にのみ適用される手順です。"
author: cabailey
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 459cbe65741ea415defced844034f62cfd4654ed
ms.openlocfilehash: 2bd9abcac99a06a29e5dacdd014e660358840adc


---


# 手順 2. ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行

>*適用対象: Active Directory Rights Management サービス、Azure Rights Management*


これらの手順は [AD RMS から Azure Rights Management への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーがソフトウェアで保護されているときにソフトウェアで保護されているテナント キーを持つ Azure Rights Management に移行する場合にのみ適用されます。 

選択した構成シナリオでない場合、[手順 2 に戻ってください。AD RMS から構成データをエクスポートし、それを Azure RMS にインポートし](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)、別の構成を選択します。

AD RMS 構成を Azure RMS にインポートするには次の手順を使用します。結果は Microsoft 管理の Azure RMS テナント キーです。

## 構成データを Azure RMS にインポートするには

1.  インターネットに接続されたワークステーションで、Windows PowerShell module for Azure RMS (バージョン 2.5.0.0 以降) をダウンロードしてインストールします。[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) コマンドレットが含まれます。

    > [!TIP]
    > 事前にモジュールをダウンロードしてインストールしてある場合は、次のコマンドレットを実行してバージョン番号を確認します。 `(Get-Module aadrm -ListAvailable).Version`

    インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

2.  [ **管理者として実行** ] オプションを選択して Windows PowerShell を起動し、 [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) コマンドレットを使用して Azure RMS サービスに接続します。

    ```
    Connect-AadrmService
    ```
    プロンプトが表示されたら、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] のテナント管理者資格情報を入力します (通常は、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使用します)。

3.  [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) コマンドレットを使用して、最初にエクスポートした信頼された発行ドメイン (.xml) ファイルをアップロードします。 信頼された発行ドメインが複数あるために複数の .xml ファイルがある場合は、移行後にコンテンツを保護するために Azure RMS で使用するエクスポートされた信頼された発行ドメインが含まれるファイルを選択します。 次のコマンドを使用します。

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    [ConvertTo-SecureString -AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) または [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) を使用し、セキュリティで保護された文字列としてパスワードを指定します。 ConvertTo-SecureString を使用する場合で、パスワードに特殊文字が含まれているときは、単一引用符の間にパスワードを入力するか、特殊文字をエスケープします。
    
    例: まず **$TPD_Password = Read-Host -AsSecureString** を実行し、上記の手順で指定したパスワードを入力します。 次に **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose** を実行します。 メッセージが表示されたら、この操作を実行することを確認します。
    
4.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 3 を繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。 例: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

5.  [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) コマンドレットを使用して Azure RMS サービスから切断します。

    ```
    Disconnect-AadrmService
    ```


以上で「[手順 3. RMS テナントをアクティブ化する](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)」に進む準備が完了しました。





<!--HONumber=Sep16_HO2-->


