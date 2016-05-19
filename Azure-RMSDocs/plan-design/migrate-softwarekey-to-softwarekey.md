---
# required metadata

title: 手順 2. ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# 手順 2. ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行

これらの手順は [AD RMS から Azure Rights Management への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーがソフトウェアで保護されているときにソフトウェアで保護されているテナント キーを持つ Azure Rights Management に移行する場合にのみ適用されます。 

これが目的の構成シナリオでない場合は、「[Step 2.Export configuration data from AD RMS and import it to Azure RMS (手順 2. AD RMS から構成データをエクスポートし、それを Azure RMS にインポートする)](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)」に戻り、別の構成を選択してください。

AD RMS 構成を Azure RMS にインポートするには次の手順を使用します。結果は Microsoft 管理の Azure RMS テナント キーです。

## 構成データを Azure RMS にインポートするには

1.  インターネットに接続されたワークステーションで、Windows PowerShell module for Azure RMS (バージョン 2.1.0.0 以降) をダウンロードしてインストールします。[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) コマンドレットが含まれます。

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
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    例: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    プロンプトが表示されたら、前に指定したパスワードを入力し、この操作を実行することを確認します。

4.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 3 を繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。 例: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) コマンドレットを使用して Azure RMS サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

以上で「[Step 3. Activate your RMS tenant (手順 3. RMS テナントをアクティブ化する)](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration)」に進む準備が完了しました。



<!--HONumber=Apr16_HO3-->


