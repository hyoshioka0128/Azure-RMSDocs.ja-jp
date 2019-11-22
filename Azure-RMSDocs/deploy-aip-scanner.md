---
title: Deploy the Azure Information Protection scanner - AIP
description: Instructions to install, configure, and run the current version of the Azure Information Protection scanner to discover, classify, and protect files on data stores.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/21/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bc49fc0721ad3b3fff09856a84fdc91718d0a1d0
ms.sourcegitcommit: d9442efe61b55bb158bd50ee69873c028234842d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297628"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2*
>
> [!NOTE]
> This article is for the current general availability version of the Azure Information Protection scanner with the Azure Information Protection client (classic), and the preview version of the scanner for the current general availability version of the Azure Information Protection unified labeling client.
> 
> If you have previously installed the scanner and want to upgrade it, use the following upgrade instructions and then use the instructions on this page, omitting the step to install the scanner:
> - For the classic client: [Upgrading the Azure Information Protection scanner](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> - For the unified labeling client: [Upgrading the Azure Information Protection scanner](./rms-client/clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> 
> If you have a version of the scanner that is older than 1.48.204.0 and you're not ready to upgrade it, see [Deploying previous versions of the Azure Information Protection scanner to automatically classify and protect files](deploy-aip-scanner-previousversions.md).


この情報を使用して、Azure Information Protection スキャナーについて説明し、正常にインストール、構成、および実行する方法について説明します。

このスキャナーは、Windows Server でサービスとして実行され、次のデータ ストア上のファイルを検出、分類、および保護することができます。

- スキャナーを実行する Windows Server コンピューター上のローカル フォルダー。

- サーバー メッセージ ブロック (SMB) プロトコルを使用するネットワーク共有の UNC パス。

- Document libraries and folders for SharePoint Server 2019 through SharePoint Server 2013. [このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様向けに SharePoint 2010 もサポートされています。

クラウド リポジトリ上のファイルをスキャンおよびラベル付けするには、スキャナーの代わりに [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) を使用します。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの概要

When you have configured labels that apply automatic classification, files that this scanner discovers can then be labeled. ラベルは分類を適用し、必要に応じて、保護を適用または保護を解除します。

![Azure Information Protection スキャナーのアーキテクチャの概要](./media/infoprotect-scanner.png)

スキャナーは、コンピューターにインストールされている IFilters を使うことで、Windows によってインデックス化できるすべてのファイルを検証できます。 そして、ファイルでラベル付けが必要かどうかを判断するため、スキャナーで Office 365 に組み込まれたデータ損失防止 (DLP) の機密情報の種類とパターン検出、または Office 365 の正規表現パターンが使われます。 Because the scanner uses the Azure Information Protection client (the classic client or unified labeling client), the scanner can classify and protect the same file types:

- The classic client: [File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)

- The unified labeling  client: [File types supported by the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-file-types.md)

スキャナーを実行できるのは検索モードでのみです。この場合、レポートを使用して、ファイルがラベル付けされた場合に何が発生するかをチェックします。 またはスキャナーを実行して、自動的にラベルを適用できます。 機密情報の種類を含んだファイルを検出するためにスキャナーを実行することもできます (自動分類を適用する条件用にラベルを構成する必要はありません)。

スキャナーは検出せず、リアルタイムでラベル付けしないことに注意してください。 スキャナーは指定したデータ ストア上のファイルを体系的にクロールします。この実行サイクルは、1 回限りまたは繰り返しに設定することができます。

スキャナーの構成の一部としてファイルの種類の一覧を定義することで、スキャンするファイルの種類、またはスキャンから除外するファイルの種類を指定できます。


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの前提条件
Azure Information Protection スキャナーをインストールする前に、次の要件を満たしていることを確認してください。

|要件|説明を見る|
|---------------|--------------------|
|スキャナー サービスを実行する Windows Server コンピューター:<br /><br />- 4 コア プロセッサ<br /><br />- 8 GB の RAM<br /><br />- 一時ファイルのための空き容量 10 GB (平均)|Windows Server 2019, Windows Server 2016, or Windows Server 2012 R2. <br /><br />注: 非運用環境でテストまたは評価を行う場合、[Azure Information Protection クライアントでサポートされている](requirements.md#client-devices) Windows クライアント オペレーティング システムを使用できます。<br /><br />このコンピューターは、スキャンするデータ ストアへの高速で信頼性の高いネットワーク接続がある物理コンピューターまたは仮想コンピューターにすることができます。<br /><br /> スキャナーは、スキャンする各ファイル用に、コアごとに 4 つの一時ファイルを作成するために、十分なディスク領域を必要とします。 推奨される 10 GB のディスク領域を使用すると、4 コア プロセッサで、それぞれのサイズが 625 MB であるファイルを 16 個スキャンできます。 <br /><br /> If internet connectivity is not possible because of your organization policies, see the [Deploying the scanner with alternative configurations](#deploying-the-scanner-with-alternative-configurations) section. Otherwise, make sure that this computer has internet connectivity that allows the following URLs over HTTPS (port 443):<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com <br /> \*.protection.outlook.com (scanner from the unified labeling client only)|
|スキャナー サービスを実行するサービス アカウント|Windows Server コンピューター上でのスキャナー サービスの実行に加えて、この Windows アカウントは Azure AD で認証され、Azure Information Protection ポリシーをダウンロードします。 このアカウントは Active Directory アカウントであり、かつ Azure AD と同期している必要があります。 組織のポリシーによってこのアカウントを同期できない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />このサービス アカウントには次の要件があります。<br /><br />-  **[Log on locally]\(ローカル ログオン\)** ユーザー権限の割り当て。 この権限は、スキャナーのインストールと構成に必要ですが、操作には必要ありません。 この権限をサービス アカウントに付与する必要がありますが、スキャナーがファイルを検出、分類、保護できることを確認したら、この権限を削除することができます。 組織のポリシーによって、短時間でもこの権限を付与することができない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />-  **[サービスとしてログオン]** ユーザー権限の割り当て。 この権限は、スキャナーのインストール中にサービス アカウントに自動的に付与され、スキャナーのインストール、構成、操作に必要です。 <br /><br />- データ リポジトリへのアクセス許可: ファイルをスキャンして、Azure Information Protection ポリシーの条件を満たすファイルに分類と保護を適用するには、**読み取り**と**書き込み**のアクセス許可を付与する必要があります。 スキャナーを検索モードでのみ実行するには、**読み取り**アクセス許可で十分です。<br /><br />- For labels that reprotect or remove protection: To ensure that the scanner always has access to protected files, make this account a [super user](configure-super-users.md) for Azure Information Protection, and ensure that the super user feature is enabled. さらに、段階的な展開の[オンボーディング制御](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を実装している場合は、このアカウントが構成したオンボーディング制御に含まれていることを確認してください。|
|スキャナーの構成を格納する SQL Server:<br /><br />- ローカルまたはリモート インスタンス<br /><br />- [Case insensitive collation](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15) <br /><br />- スキャナーをインストールする sysadmin ロール|次のエディションでは、SQL Server 2012 が最小バージョンとなります。<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Azure Information Protection スキャナーでは、スキャナーのカスタム プロファイル名を指定するときに同じ SQL Server インスタンス上の複数の構成データベースがサポートされます。 When you use the preview version of the scanner from the unified labeling client, multiple scanners can share the same configuration database.<br /><br />Sysadmin ロールを持つアカウントでスキャナーをインストールすると、インストールのプロセスでスキャナーの構成データベースが自動的に作成され、スキャナーを実行するサービス アカウントに対して必要な db_owner ロールが付与されます。 Sysadmin ロールが付与されない場合や、組織のポリシーがデータベースを手動で作成し構成することを要求している場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」をご覧ください。<br /><br /> For capacity guidance, see [Storage requirements and capacity planning for SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).|
|Either of the following Azure Information Protection clients is installed on the Windows Server computer <br /><br /> - Classic client <br /><br /> - Unified labeling client ([current general availability version only](./rms-client/unifiedlabelingclient-version-release-history.md#version-25330)) |スキャナーに対する完全なクライアントをインストールする必要があります。 PowerShell モジュールだけで、クライアントをインストールしないでください。<br /><br />For installation and upgrade instructions: <br /> - [Classic client](./rms-client/client-admin-guide.md)<br /> - [Unified labeling client](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner) |
|自動分類と、必要に応じて保護を適用する構成済みのラベル|For instructions for the classic client to configure a label for conditions and to apply protection:<br /> - [自動および推奨分類の条件を構成する方法](configure-policy-classification.md)<br /> - [Rights Management による保護でラベルを構成する方法](configure-policy-protection.md) <br /><br />Tip: You can use the instructions from the [tutorial](infoprotect-quick-start-tutorial.md) to test the scanner with a label that looks for credit card numbers in a prepared Word document. ただし、オプション **[このラベルの適用方法を選択]** が **[推奨]** ではなく **[自動]** に設定されるように、ラベルの構成を変更する必要があります。 その後、(適用される場合は) ドキュメントからラベルを削除して、スキャナー用のデータ リポジトリにファイルをコピーします。 簡単なテストの場合、これにはスキャナー コンピューター上のローカル フォルダーを使用できます。<br /><br /> For instructions for the unified labeling client to configure a label for auto-labeling and to apply protection:<br /> - [Apply a sensitivity label to content automatically](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)<br /> - [Restrict access to content by using encryption in sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)<br /><br /> 自動分類を適用するラベルを構成していない場合でもスキャナーを実行できますが、このシナリオについては、これらの手順では説明されていません。 [詳細情報](#using-the-scanner-with-alternative-configurations)|
|For SharePoint document libraries and folders to be scanned:<br /><br />- SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|スキャナーでは SharePoint の他のバージョンはサポートされていません。<br /><br />When you use [versioning](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), the scanner inspects and labels the last published version. If the scanner labels a file and [content approval](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) is required, that labeled file must be approved to be available for users. <br /><br />大規模な SharePoint ファームの場合は、スキャナーがすべてのファイルにアクセスするために、リスト ビューのしきい値 (既定では 5,000) を増やす必要があるかどうかを確認します。 For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|スキャンされる Office ドキュメントの場合:<br /><br />- Word、Excel、PowerPoint の 97-2003 ファイル形式および Office Open XML 形式|For more information about the file types that the scanner supports for these file formats, see the following information: <br />- Classic client: [File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)<br />- Unified labeling client: [File types supported by the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-file-types.md)|
|長いパスの場合:<br /><br />- 最大 260 文字 (スキャナーが Windows 2016 にインストールされていて、コンピューターが長いパスをサポートするように構成されているのでない場合)|Windows 10 and Windows Server 2016 support path lengths greater than 260 characters with the following [group policy setting](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/): **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **All Settings** > **Enable Win32 long paths**<br /><br /> 長いファイルのパスのサポートについて詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

If you can't meet all the requirements in the table because they are prohibited by your organization policies, see the [alternative configurations](#deploying-the-scanner-with-alternative-configurations) section.

When you deploy the scanner in production, or you're testing the performance for multiple scanners, see the next section for capacity planning guidance for SQL Server.

However, if you're ready to start deploying the scanner, go straight to [configuring the scanner section](#configure-the-scanner-in-the-azure-portal).

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Storage requirements and capacity planning for SQL Server

The amount of disk space required for the scanner's configuration database and the specification of the computer running SQL Server can vary for each environment, so we encourage you to do your own testing. However, you can use the following guidance as a starting point.

See the [Optimizing the performance of the scanner](#optimizing-the-performance-of-the-scanner) section for additional information.

##### <a name="scanner-from-the-classic-client"></a>Scanner from the classic client:

- **Disk size**: The size of the configuration database will vary for each deployment but we recommend you allocate 500 MB for every 1,000,000 files that you want to scan.

- **For each scanner**: 4 core processors; 8 GB RAM recommended (4 GB minimum).

##### <a name="scanner-from-the-unified-labeling-client"></a>Scanner from the unified labeling client:

- **Disk size**: Although the size of the scanner configuration database will vary for each deployment, you can use the following equation as guidance: `100 KB + <file count> *(1000 + 4*<average file name length>)`. 
    
    For example, to scan 1 million files that have an average file name length of 250 bytes, allocate 2 GB disk space.

- **For multiple scanners, up to 12**: 4 core processors; 8 GB RAM recommended (4 GB minimum).

- **For multiple scanners more than 12 (maximum 40)** : 8 core processes; 16 GB RAM recommended (8 GB minimum).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーのデプロイ

テーブルに一覧表示されている前提条件は、スキャナーの既定の要件であり、推奨されます。何故なら、これらはスキャナーをデプロイするための最も簡単な構成であるためです。 これらは、スキャナーの機能を確認するための最初のテスト用に適しています。 ただし、運用環境では、次の制限の 1 つ以上に該当するために組織のポリシーによって既定の要件が禁止される場合があります。

- Servers are not allowed internet connectivity

- Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

- サービス アカウントに**ローカル ログオン**権限を付与できない

- Service accounts cannot be synchronized to Azure Active Directory but servers have internet connectivity

スキャナーをこれらの制限に対応させることは可能ですが、追加構成が必要です。


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction: The scanner server cannot have internet connectivity

Follow the instructions from the admin guides to support a disconnected computer:

- For the classic client: [Support for disconnected computers](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)
    
    In this configuration, the scanner from the classic client cannot apply protection, remove protection, or inspect protected files by using your organization's cloud-based key. Instead, the scanner is limited to using labels that apply classification only, or apply protection that uses [HYOK](configure-adrms-restrictions.md)

- For the unified labeling client: [Support for disconnected computers](./rms-client/clientv2-admin-guide-customizations.md#support-for-disconnected-computers)
    
    In this configuration, the scanner from the unified labeling client can apply protection, remove protection, and inspect protected files by using the *DelegatedUser* parameter with the [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) cmdlet.

次に、以下の操作を行います。

1. スキャナーのプロファイルを作成して、Azure portal でスキャナーを構成します。 この手順に関してサポートが必要な場合は、「[Azure portal でスキャナーを構成する](#configure-the-scanner-in-the-azure-portal)」をご覧ください。

2. Export your scanner profile from the **Azure Information Protection - Profiles** pane, by using the **Export** option.

3. 最後に、PowerShell セッションで、[Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) を実行し、エクスポートされた設定を含んでいるファイルを指定します。

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

スキャナーをインストールするために一時的に Sysadmin ロールが付与される場合、スキャナーのインストールが完了したらこのロールを削除できます。 この構成を使用すると、データベースが自動的に作成され、スキャナー用のサービス アカウントに必要なアクセス許可が自動的に付与されます。 ただし、スキャナーを構成するユーザー アカウントには、スキャナー構成データベースの db_owner ロールが必要です。このロールをユーザー アカウントに手動で付与する必要があります。

If you cannot be granted the Sysadmin role even temporarily, you must ask a user with Sysadmin rights to manually create a database before you install the scanner. For this configuration, the following roles must be assigned:
    
|アカウント|データベースレベルのロール|
|--------------------------------|---------------------|
|スキャナーのサービス アカウント|db_owner|
|スキャナーのインストール用のユーザー アカウント|db_owner|
|スキャナーの構成用のユーザー アカウント |db_owner|

通常、スキャナーのインストールと構成には同じユーザー アカウントを使用します。 ただし、別々のアカウントを使用する場合は、両方にスキャナー構成データベースの db_owner ロールが必要です。

- If you do not specify your own profile name for the scanner (classic client only), the configuration database is named **AIPScanner_\<computer_name>** . 

- If you specify your own profile name, the configuration database is named **AIPScanner_\<profile_name>** (classic client) or **AIPScannerUL_\<profile_name>** (unified labeling client).

To create a user and grant db_owner rights on this database, ask the Sysadmin to run the following SQL script twice. The first time, for the service account that runs the scanner, and the second time for you to install and manage the scanner. Before running the script:
1. Replace *domain\user* with the domain name and user account name of the service account or user account.
2. Replace *DBName* with the name of the scanner configuration database.

SQL script:

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END

さらに、本サービスには以下の規定が適用されます。

- You must be a local administrator on the server that will run the scanner
- The service account that will run the scanner must be granted Full Control permissions to the following registry keys:
    
    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

If, after configuring these permissions, you see an error when you install the scanner, the error can be ignored and you can manually start the scanner service.


#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>制限: スキャナーのサービス アカウントに**ローカル ログオン**権限を付与できない

If your organization policies prohibit the **Log on locally** right for service accounts but allow the **Log on as a batch job** right, use the following instructions:

- For the classic client: See [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.

- For the unified labeling client: Use the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) in that client's admin guide.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction: The scanner service account cannot be synchronized to Azure Active Directory but the server has internet connectivity

スキャナーのサービスを実行するために 1 つのアカウントを持ち、Azure Active Directory を認証するために別のアカウントを使用することができます。

- スキャナーのサービス アカウントのためには、ローカルの Windows アカウントか Active Directory アカウントを使用できます。

- For the Azure Active Directory account, use the following instructions:
    - For the classic client: See [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.
    - For the unified labeling client: Specify your local account for the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) in that client's admin guide.


## <a name="configure-the-scanner-in-the-azure-portal"></a>Azure portal でスキャナーを構成する

Before you install the scanner, or upgrade it from an older general availability version of the scanner, create a profile for the scanner in the Azure portal. スキャナーの設定に関するプロファイルと、スキャンするデータ リポジトリを構成します。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.
    
2. **[スキャナー]** メニュー オプションを見つけて、 **[プロファイル]** を選択します。

3. **[Azure Information Protection] - [プロファイル]** ペインで、 **[追加]** を選択します。
    
    ![Azure Information Protection スキャナーのプロファイルを追加する](./media/scanner-add-profile.png)

4. **[新しいプロファイルを追加する]** ペインで、その構成設定とスキャンするデータ リポジトリを識別するために使うスキャナーの名前を指定します。 たとえば、スキャナーの対象となるデータ リポジトリの地理的な場所を識別するために、**Europe** を指定する場合があります。 後でスキャナーをインストールまたはアップグレードするときに、同じプロファイル名を指定する必要があります。
    
    スキャナーのプロファイル名を識別するために、必要に応じて管理目的の説明を指定します。

5. For this initial configuration, configure the following settings, and then select **Save** but do not close the pane:
    
    For the **Profile settings** section:
    - **Schedule**: Keep the default of **Manual**
    - **Info types to be discovered**: Change to **Policy only**
    - **Configure repositories**: Do not configure at this time because the profile must first be saved.
    
    For the **Policy enforcement** section:
    - **Enforce**: Select **Off**
    - **Label files based on content**: Keep the default of **On**
    - **Default label**: Keep the default of **Policy default**
    - **Relabel files**: Keep the default of **Off**
    
    For the **Configure file settings** section:
    - **Preserve "Date modified", "Last modified" and "Modified by"** : Keep the default of **On**
    - **File types to scan**: Keep the default file types for **Exclude**
    - **Default owner**: Keep the default of **Scanner Account**

6. これでプロファイルの作成と保存が完了したので、 **[リポジトリの構成]** オプションに戻って、スキャンするデータ ストアを指定する準備が整いました。 You can specify local folders, UNC paths, and SharePoint Server URLs for SharePoint on-premises document libraries and folders. 
    
    SharePoint Server 2019, SharePoint Server 2016, and SharePoint Server 2013 are supported for SharePoint. また、SharePoint Server 2010 も、[このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)を受けている場合はサポートされます。
    
    To add your first data store, still on the **Add a new profile** pane, select **Configure repositories** to open the **Repositories** pane:
    
    ![Azure Information Protection スキャナーのデータ リポジトリを構成する](./media/scanner-repositories-bar.png)

7. **[リポジトリ]** ペインで、 **[追加]** を選択します。
    
    ![Azure Information Protection スキャナーのデータ リポジトリを追加する](./media/scanner-repository-add.png)

8. On the **Repository** pane, specify the path for the data repository. 
    
    ワイルドカードはサポートされていません。また、WebDav の場所はサポートされていません。
    
    例:
    
    - ローカル パスの場合: `C:\Folder`
    
    - ネットワーク共有の場合: `C:\Folder\Filename`
    
    - UNC パスの場合: `\\Server\Folder`
    
    - SharePoint ライブラリの場合: `http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > "共有ドキュメント" の SharePoint パスを追加する場合:
    >
     >- 共有ドキュメントのすべてのドキュメントとすべてのフォルダーをスキャンしたい場合は、パスに **Shared Documents** を指定します。 たとえば次のようになります。`http://sp2013/Shared Documents`
     >
     >- 共有ドキュメント下のサブフォルダーのすべてのドキュメントとすべてのフォルダーをスキャンしたい場合は、パスに **Documents** を指定します。 たとえば次のようになります。`http://sp2013/Documents/Sales Reports`
    
    For the remaining settings on this pane, do not change them for this initial configuration, but keep them as **Profile default**. これは、データ リポジトリがスキャナーのプロファイルから設定を継承することを意味します。 
    
    **[保存]** を選択します。

9. 別のデータ リポジトリを追加する場合は、手順 7 と 8 を繰り返します。

10. You can now close **Repositories** pane and your profile pane. Back on the **Azure Information Protection - Profiles** pane, you see your profile name displayed, together with the **SCHEDULE** column showing **Manual** and the **ENFORCE** column is blank.

これで、先ほど作成したスキャナーのプロファイルを使ってスキャナーをインストールする準備ができました。

## <a name="install-the-scanner"></a>スキャナーのインストール

1. スキャナーを実行する Windows Server コンピューターにサインインします。 ローカル管理者権限と SQL Server マスター データベースに書き込むためのアクセス許可を持つアカウントを使用します。

2. **[管理者として実行]** オプションを使用して Windows PowerShell セッションを開きます。

3. Azure Information Protection スキャナー用のデータベースを作成する SQL Server のインスタンスと、前のセクションで指定したスキャナーのプロファイル名を指定して、[Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) コマンドレットを実行します。 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <profile name>
    ```
    
    プロファイル名 **Europe** を使った例:
    
    - 既定のインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - 名前付きインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - SQL Server Express の場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    求められたら、スキャナー サービス アカウントの資格情報 (\<ドメイン\ユーザー名>) とパスワードを指定します。

4. **[管理ツール]**  >  **[サービス]** を使用して、サービスがインストールされたことを確認します。 
    
    インストールされているサービスの名前は **Azure Information Protection スキャナー**で、作成したスキャナー サービス アカウントを使用して実行するように構成されます。

スキャナーをインストールしたら、スキャナーを無人で実行できるように、スキャナー サービス アカウントを認証するための Azure AD トークンを取得する必要があります。 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>スキャナー用の Azure AD トークンを取得する

The Azure AD token lets the scanner authenticate to the Azure Information Protection service.

1. Return to the Azure portal to create two Azure AD applications (just one Azure AD application for the scanner from the unified labeling client) that are needed to specify an access token for authentication. This token lets the scanner run non-interactively.
    
    To create these applications, follow the instructions in the admin guides for the relevant clients:
    
    - For the classic client: [How to label files non-interactively for Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)
    
    - For the unified labeling client: [How to label files non-interactively for Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

2. スキャナーのサービス アカウントにインストール用に**ローカルでログオン**する権限が付与されている場合、Windows Server コンピューターから、このアカウントを使用してサインインし、PowerShell セッションを開始します。 前の手順でコピーした値を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行します。
    
    **For the classic client:**
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    求められたら、Azure AD のサービス アカウントの資格情報のパスワードを指定し、 **[同意する]** をクリックします。
    
    If your scanner service account cannot be granted the **Log on locally** right for the installation see [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.
    
    **For the unified labeling client:**
    
    ```
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
    
    If your scanner service account cannot be granted the **Log on locally** right for the installation, use the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) from that client's admin guide.

The scanner now has a token to authenticate to Azure AD, which is valid for one year, two years, or never expires, according to your configuration of the **Web app /API** (classic client) or client secret (unified labeling client) in Azure AD. トークンが期限切れになったら、手順 1 と 2 を繰り返す必要があります。

これで、最初のスキャンを検索モードで実行する準備ができました。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>探索サイクルの実行とスキャナーのレポートの表示

1. In the Azure portal, on the **Azure Information Protection - Profiles** pane, select your scanner's profile, and then the **Scan now** option:
    
    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)
    
    または、PowerShell セッションで、次のコマンドを実行します。
    
        Start-AIPScan

2. スキャナーのサイクルが完了するまで待ちます。 スキャナーが指定したデータ ストア内のすべてのファイルをクロールし終わると、スキャナー サービスの動作が続いていてもスキャナーは停止します。
    
    - On the **Azure Information Protection - Profiles** pane, use the **Refresh** option and wait until you see values for the **LAST SCAN RESULTS** column and the **LAST SCAN (END TIME)** column.
    
    - PowerShell を使用すると、`Get-AIPScannerStatus` を実行して状態の変化を監視できます。
    
    - Scanner from the classic client only: Check the local Windows **Applications and Services** event log, **Azure Information Protection**. このログでは、スキャナーがスキャンを完了した時刻も、結果の概要と共に報告されます。 情報イベント ID **911** を探します。

3. %*localappdata*%\Microsoft\MSIP\Scanner\Reports に格納されているレポートを確認します。 .txt の概要ファイルには、スキャンにかかった時間、スキャンされたファイルの数、情報の種類と一致したファイルの数が含まれています。 .csv ファイルには各ファイルに関する詳細情報が記載されています。 このフォルダーには、スキャンのサイクルごとに最大 60 のレポートが格納され、必要なディスク領域を最小限に抑えるために最新のもの以外のすべてのレポートが圧縮されます。
    
    > [!NOTE]
    > [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) と共に *ReportLevel* パラメーターを使って、ログ記録のレベルを変更することができます。ただし、レポート フォルダーの場所または名前を変更することはできません。 別のボリュームまたはパーティションにレポートを保存したい場合は、フォルダーに対するディレクトリのジャンクションの使用を検討してください。
    >
    > たとえば、[Mklink](/windows-server/administration/windows-commands/mklink) コマンドを使います。`mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    **[検出する情報の種類]** に対して **[ポリシーのみ]** を設定しているため、自動分類用に設定した条件を満たすファイルのみが詳細レポートに含まれます。 ラベルが適用されていない場合は、ラベルの構成に推奨される分類ではなく自動分類が含まれていることを確認します。
    
    > [!TIP]
    > スキャナーでは 5 分ごとにこの情報が Azure Information Protection に送信されます。このため、Azure portal から結果をほぼリアルタイムで確認することができます。 詳細については、[Azure Information Protection のレポート作成](reports-aip.md)に関するページを参照してください。 
        
    If the results are not as you expect, you might need to reconfigure the conditions that you specified for you labels. その場合は、構成を変更して分類、および必要に応じて保護を適用する準備ができるまで、手順 1 から 3 を繰り返します。 

Azure portal には、最後のスキャンに関する情報のみが表示されます。 前のスキャンの結果を確認する必要がある場合は、スキャナー コンピューターの %*localappdata*%\Microsoft\MSIP\Scanner\Reports フォルダーに格納されているレポートに戻ります。

スキャナーが検出したファイルに自動的にラベル付けする準備ができたら、次の手順に進みます。 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>スキャナーを構成して分類と保護を適用する

これらの手順に従っている場合、スキャナーは、レポートのみモードで 1 回だけ実行されます。 これらの設定を変更するには、スキャナーのプロファイルを編集します。

1. Back on the **Azure Information Protection - Profiles** pane, select the scanner profile to edit it.

2. On the \<**profile name**> pane, change the following two settings, and then select **Save**:
    
   - From the **Profile settings** section: Change the **Schedule** to **Always**
   - From the **Policy enforcement** section: Change **Enforce** to **On**
    
     変更する可能性があるその他の構成があります。 たとえば、ファイル属性を変更するかどうか、またはスキャナーでファイルのラベルを書き換えられるかどうかなどです。 情報のポップアップ ヘルプを使って、各構成設定について詳しく学習してください。

3. Make a note of the current time and start the scanner again from the **Azure Information Protection - Profiles** pane:
    
    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)
    
    または、PowerShell セッションで次のコマンドを実行できます。
    
        Start-AIPScan

4. Scanner from the classic client only: Monitor the event log for the informational type **911** again, with a time stamp later than when you started the scan in the previous step.
    
    次に、レポートをチェックして、ラベル付けされたファイル、各ファイルに適用された分類、それらに保護が適用されたかどうかについての詳細を確認します。 または、Azure portal を使用してより簡単にこの情報を確認します。

スケジュールを継続的に実行するように構成したため、スキャナーはすべてのファイルの作業を完了すると、新しいファイルや変更されたファイルをすべて検出するために新しいサイクルを自動的に開始します。

## <a name="how-files-are-scanned"></a>ファイルをスキャンする方法

スキャナーでは、ファイルをスキャンするとき、次のプロセスが実行されます。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. Determine whether files are included or excluded for scanning 
The scanner automatically skips files that are excluded from classification and protection, such as executable files and system files. For more information, see the following admin guides:

- For the classic client: [File types that are excluded from classification and protection](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- For the unified labeling client: [File types that are excluded from classification and protection](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

スキャンする (またはスキャン対象から除外する) ファイルの種類のリストを定義することで、この動作を変更できます。 スキャナーに対してこのリストを指定し、既定ですべてのデータ リポジトリに適用させることができます。また、データ リポジトリごとに 1 つのリストを指定することができます。 このリストを指定するには、スキャナーのプロファイルの **[スキャンするファイルの種類]** 設定を使います。

![Azure Information Protection スキャナー用にスキャンするファイルの種類を構成する](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2. Inspect and label files

その後、スキャナーでは、フィルターを使用して、サポートされているファイルの種類がスキャンされます。 これらの同じフィルターが、オペレーティング システムによって Windows Search とインデックス作成にも使用されます。 構成を何も追加しなくても、Word、Excel、PowerPoint、PDF ドキュメント、テキスト ファイルに対して使用されるファイルの種類のスキャンに、Windows IFilter が使用されます。

For a full list of file types that are supported by default, and additional information how to configure existing filters that include .zip files and .tiff files, see the following admin guides:

- For the classic client: [File types supported for inspection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)
- For the unified labeling client: [File types supported for inspection](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection)

検査が済むと、ユーザーがラベルに対して指定した条件を使用して、これらのファイルの種類にラベルを付けることができます。 または、検出モードを使用している場合は、ユーザーがラベルに対して指定した条件、またはすべての既知の機密情報の種類を含むように、これらのファイルを報告できます。 

ただし、以下の状況では、スキャナーでファイルにラベルを付けることはできません。

- If the label applies classification and not protection, and the file type does not support classification only by the [classic client](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) or [unified labeling client](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- ラベルで分類と保護が適用されるが、スキャナーでファイルの種類が保護されていない場合。
    
    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 Other file types can be protected when you [change which file types are protected](#change-which-file-types-to-protect) as described in a following section.

たとえば、.txt ファイルの種類では "分類のみ" がサポートされていないため、ファイル名拡張子が .txt であるファイルを検査した後は、分類用にだけ構成されていて保護用には構成されていないラベルを、スキャナーで適用することはできません。 If the label is configured for classification and protection, and the .txt file name extension is included for the scanner to protect, the scanner can label the file. 

> [!TIP]
> このプロセス中にスキャナーが停止し、リポジトリ内の大量のファイルのスキャンが完了しない場合:
> 
> - ファイルをホストしているオペレーティング システムに対し、動的ポートの数を増やす必要がある場合があります。 SharePoint 用にサーバーのセキュリティが強化されている場合、スキャナーが許可されているネットワーク接続の数を超えて、そのために停止する原因の 1 つになる可能性があります。
>     
>     To check whether this is the cause of the scanner stopping, look to see if the following error message is logged for the scanner in %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (zipped if there are multiple logs): **Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port**
>    
>     現在のポート範囲を表示し、範囲を拡大する方法について詳しくは、「[ネットワーク パフォーマンスを向上させるために変更可能な設定](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)」をご覧ください。
> 
> - 大規模な SharePoint ファームの場合、リスト ビューのしきい値 (既定では 5,000) を増やす必要がある場合があります。 For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. Label files that can't be inspected
検査できないファイルの種類に対し、スキャナーでは Azure Information Protection ポリシーの既定のラベル、またはユーザーがスキャナー用に構成した既定のラベルが適用されます。

前のステップと同じように、以下の状況では、スキャナーでファイルにラベルを付けることはできません。

- If the label applies classification and not protection, and the file type does not support classification only by the [classic client](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) or [unified labeling client](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- ラベルで分類と保護が適用されるが、スキャナーでファイルの種類が保護されていない場合。
    
    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 Other file types can be protected when you change which file types to protect, as described next.

## <a name="change-which-file-types-to-protect"></a>Change which file types to protect

By default, the scanner protects Office file types and PDF files only. You can change this behavior so that for example, the scanner protects all file types, which is the same protection behavior as the client. Or, the scanner protects additional file types that you specify, in addition to Office file types and PDF files. 

For configuration instructions, see the following sections.

### <a name="scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected"></a>Scanner from the classic client: Use the registry to change which file types are protected

This section applies to the scanner from the classic client only.

To change the default scanner behavior for protecting file types other than Office files and PDFs, you must edit the registry and specify the additional file types that you want to be protected, and the type of protection (native or generic). 詳しくは、開発者ガイダンスの「[ファイル API の構成](develop/file-api-configuration.md)」をご覧ください。 この開発者向けドキュメントでは、汎用的な保護は "PFile" と呼ばれています。 さらに、スキャナーの場合:

- The scanner has its own default behavior: Only Office file formats and PDF documents are protected by default. レジストリを変更しない場合、その他のファイル形式は、スキャナーによってラベル付けまたは保護されません。

- If you want the same default protection behavior as the Azure Information Protection client, where all files are automatically protected with native or generic protection: Specify the `*` wildcard as a registry key, `Encryption` as the value (REG_SZ), and `Default` as the value data.

レジストリを編集するときには、各ファイル名拡張子のキーと共に、**MSIPC** キーと **FileProtection** キーが存在しない場合には手動で作成します。

たとえば、Office ファイルと PDF だけでなく、TIFF イメージも保護するスキャナーの場合、レジストリの編集後は、次の図のようになります。 イメージ ファイルなので、TIFF ファイルではネイティブ保護がサポートされ、結果としてファイル名拡張子は .ptiff になります。

![保護を適用するためのスキャナーのレジストリの編集](./media/editregistry-scanner.png)

For a list of text and images file types that similarly support native protection but must be specified in the registry, see [Supported file types for classification and protection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection).

ネイティブ保護がサポートされていないファイルの場合は、新しいキーとしてファイル名拡張子を指定し、汎用的な保護のために **PFile** を指定します。 結果として、保護されるファイルのファイル名拡張子は .pfile になります。

### <a name="scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected"></a>Scanner from the unified labeling client: Use PowerShell to change which file types are protected

This section applies to the scanner from the unified labeling client only.

For a label policy that applies to the user account downloading labels for the scanner, specify a PowerShell advanced setting named **PFileSupportedExtensions**. 

> [!NOTE]
> For a scanner that has access to the internet, this user account is the account that you specify for the *DelegatedUser* parameter with the Set-AIPAuthentication command.

Example 1:  PowerShell command for the scanner to protect all file types, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

Example 2: PowerShell command for the scanner to protect .xml files and .tiff files in addition to Office files and PDF files, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}

For detailed instructions, see [Change which file types to protect](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) from the admin guide.


## <a name="when-files-are-rescanned"></a>ファイルが再スキャンされる場合

最初のスキャン サイクルではスキャナーは構成されているデータ ストアのすべてのファイルを検査し、後続のスキャンでは、新しいファイルまたは変更されたファイルのみが検査されます。 

You can force the scanner to inspect all files again from the **Azure Information Protection - Profiles** pane in the Azure portal. Select your scanner profile from the list, and then select the **Rescan all files** option:

![Azure Information Protection スキャナーの再スキャンを開始する](./media/scanner-rescan-files2.png)

すべてのファイルの再検査はレポートにすべてのファイルを含める必要がある場合に役立ち、この構成は通常、検索モードでスキャナーが実行されるときに使用されます。 フル スキャンが完了すると、後続のスキャンで新しいファイルまたは変更されたファイルのみがスキャンされるように、スキャンの種類が自動的に [増分] に変更されます。

In addition, all files are inspected when the scanner from the classic client downloads an Azure Information Protection policy that has new or changed conditions and the scanner from the unified labeling client has new or changed settings for automatic and recommended labeling. 

The scanner refreshes the policy according to the following triggers:

- Scanner from the classic client: Every hour and when the service starts and the policy is older than one hour. 

- Scanner from the unified labeling client: Every four hours and when the service starts. 

> [!TIP]
> If you need to refresh the policy sooner than the default interval, for example, during a testing period: 
>
> - Scanner from the classic client: Manually delete the policy file, **Policy.msip** from **%LocalAppData%\Microsoft\MSIP\Policy.msip**.
>
> - Scanner from the unified labeling client: Manually delete the contents from **%LocalAppData%\Microsoft\MSIP\mip\\<*processname*>\mip**.
>
その後、Azure Information Scanner サービスを再起動します。 If you changed protection settings for your labels, also wait 15 minutes from when you saved the protection settings before you restart the service.


## <a name="editing-in-bulk-for-the-data-repository-settings"></a>データ リポジトリ設定の一括編集

スキャナーのプロファイルに追加したデータ リポジトリに対して、 **[エクスポート]** と **[インポート]** オプションを使って簡単に設定を変更することができます。 たとえば、ご自分の SharePoint データ リポジトリに対して、スキャンから除外する新しいファイルの種類を追加したいことがあります。

Instead of editing each data repository in the Azure portal, use the **Export** option from the **Repositories** pane:

![スキャナーのデータ リポジトリの設定をエクスポートする](./media/export-scanner-repositories.png)

Manually edit the file to make the change, and then use the **Import** option on the same pane.

## <a name="using-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーの使用

There are three alternative scenarios that the Azure Information Protection scanner supports where labels do not need to be configured for any conditions: 

- データ リポジトリ内のすべてのファイルに既定のラベルを適用する。
    
    For this configuration, set **Label files based on content** to **Off**. Then set the **Default label** to **Custom**, and select the label to use.
    
    The contents of the files are not inspected and all unlabeled files in the data repository are labeled according to the default label that you specify for the data repository or the scanner profile. 
    
    For the scanner from the unified labeling client, you can also select **Enforce default label** if you want the default label to be applied on all files, even if they are already labeled.
    

- Remove existing labels from all files in a data repository.
    
    Applicable to the scanner from the unified labeling client only, this configuration lets you remove existing labels, which includes protection if it was applied with that label. Protection that was applied independently from a label is retained. Use this configuration if you need to remove all labels from files in a repository.
    
    次の設定を構成します。
    - **Label files based on content**: **Off**
    - **Default label**: **None**
    - **Relabel files**: **On** with the **Enforce default label** checkbox selected

- すべてのカスタム条件と、既知の機密情報の種類を特定する。
    
    この構成では、 **[検出する情報の種類]** を **[すべて]** に設定します。
    
    For the scanner from the classic client: The scanner uses any custom conditions that you have specified for labels in the Azure Information Protection policy, and the list of information types that are available to specify for labels in the Azure Information Protection policy. 
    
    For the scanner from the unified labeling client: The scanner uses any custom sensitive info types that you have specified and the list of built-in sensitive info types that are available to select in your labeling management center.
    
    この設定は、気付かない可能性がある機密情報を発見するのに役立ちますが、スキャナーのスキャン速度が犠牲になります。
    
    The following quickstart for the scanner uses this configuration: [Quickstart: Find what sensitive information you have](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>スキャナーのパフォーマンスの最適化

スキャナーのパフォーマンスを最適化するには、次のガイダンスを使用します。 However, if your priority is the responsiveness of the scanner computer rather than the scanner performance, you can use an [advanced client setting](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner) to limit the number of threads used by the scanner (classic client only).

スキャナーのパフォーマンスを最大化するには

- **スキャナー コンピューターとスキャンされたデータ ストア間のネットワーク接続を高速かつ信頼性の高い接続にする**
    
    たとえば、同じ LAN 内か、スキャンされたデータ ストアと同じネットワーク セグメント内 (推奨) にスキャナー コンピューターを配置します。
    
    ネットワーク接続の品質は、スキャナーがスキャナー サービスを実行しているコンピューターにファイルのコンテンツを転送してファイルを検査するため、スキャナーのパフォーマンスに影響します。 このデータを移動する必要があるネットワークのホップ数を減らす (削除する) と、ネットワークの負荷も軽減されます。 

- **スキャナー コンピューターに利用可能なプロセッサ リソースがあることを確認する**
    
    ファイルの内容の検査、およびファイルの暗号化と複合化は、プロセッサ負荷の高いアクションです。 プロセッサ リソースの不足がスキャナー パフォーマンスを低下させるかどうかを識別するには、指定したデータ ストアの標準のスキャン サイクルを監視します。
    
- **スキャナー サービスを実行しているコンピューター上のローカル フォルダーをスキャンしない**
    
    Windows Server 上にスキャンするフォルダーがある場合は、別のコンピューター上にスキャナーをインストールし、これらのフォルダーをネットワーク共有として構成してスキャンします。 ファイルをホストする機能とファイルをスキャンする機能の 2 つの機能を分離させると、これらのサービス用のリソースの計算が相互に競合していないことを意味します。

必要に応じて、スキャナーの複数のインスタンスをインストールします。 Azure Information Protection スキャナーでは、スキャナーのカスタム プロファイル名を指定するときに同じ SQL Server インスタンス上の複数の構成データベースがサポートされます。 For the scanner from the unified labeling client, multiple scanners can share the same profile, which results in quicker scanning times.

スキャナーのパフォーマンスに影響するその他の要因

- スキャンするファイルを含むデータ ストアの現在の負荷と応答時間

- スキャナーが検索モードまたは強制モードのどちらで実行されているか
    
    通常、検索モードでは、強制モードよりもスキャン速度が速くなります。これは、発見には単一ファイルの読み取りアクションが必要なのに対して、強制モードでは読み取り/書き込みアクションが必要なためです。

- You change the conditions in the Azure Information Protection policy (classic client) or auto-labeling in the label policy (unified labeling client)
    
    スキャナーがすべてのファイルを検査する必要がある場合、最初のスキャン サイクルには、既定では新規および変更されたファイルのみを検査する後続のスキャン サイクルよりも、長い時間がかかります。 However, if you change the conditions or auto-labeling settings, all files are scanned again, as described in the [preceding section](#when-files-are-rescanned).

- カスタム条件に対する正規表現式の構築
    
    メモリの大量消費とタイムアウト (1 ファイルあたり 15 分) のリスクを回避するには、ご利用の正規表現式を確認して効率的なパターン マッチングが行われているかを確認してください。 たとえば、次のようになります。
    
    - [最長の量指定子](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)を開始します
    
    - `(expression)` ではなく、`(?:expression)` などの非キャプチャ グループを使用します

- 選択したログ レベル
    
    スキャナー レポートに対して **[デバッグ]** 、 **[情報]** 、 **[エラー]** 、 **[オフ]** から選択できます。 **[オフ]** を選択すると、最適なパフォーマンスになります。 **[デバッグ]** は大幅にスキャナーのスピードを低下させるので、トラブルシューティング時にのみ使用してください。 詳細については、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットの *ReportLevel* パラメーターを参照してください。

- ファイル自体
    
    - With the exception of Excel files, Office files are more quickly scanned than PDF files.
    
    - 保護されていないファイルは、保護されたファイルよりもすばやくスキャンされます。
    
    - 大きいファイルは明らかに小さいファイルよりも時間がかかります。

- さらに、本サービスには以下の規定が適用されます。
    
    - Confirm that the service account that runs the scanner has only the rights documented in the [scanner prerequisites](#prerequisites-for-the-azure-information-protection-scanner) section, and then configure the [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) to disable the low integrity level for the scanner (classic client only).
    
    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのファイルに既定のラベルを適用すると、ファイル内容の検査がスキップされるため、スキャナーの実行速度が速くなります。
    
    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのカスタム条件と既知の機密情報の種類を特定すると、スキャナーの実行速度が遅くなりなります。
    
    - You can decrease the scanner timeouts (classic client only) with [advanced client settings](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner) for better scanning rates and lower memory consumption, but with the acknowledgment that some files might be skipped.

## <a name="list-of-cmdlets-for-the-scanner"></a>スキャナーのコマンドレットの一覧

現在では Azure portal からスキャナーを構成するため、データ リポジトリとスキャンされるファイルの種類のリストを構成する以前のバージョンのコマンドレットは、非推奨になりました。 

残っているコマンドレットには、スキャナーをインストールおよびアップグレードするコマンドレット、スキャナーの構成データベースとプロファイルを変更するコマンドレット、ローカルのレポート レベルを変更するコマンドレット、および切断されたコンピューターの構成設定をインポートするコマンドレットが含まれます。 

The full list of cmdlets for the scanner: 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Export-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs) - unified labeling client only

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>スキャナーのイベント ログ ID と説明

次のセクションを使用して、スキャナーの可能性のあるイベント ID と説明を特定できます。 これらのイベントは、Windows の**アプリケーションとサービス**のイベント ログ、**Azure Information Protection** でスキャナー サービスを実行しているサーバーにログオンします。

> [!NOTE]
> This section applies to the scanner from the classic client only. Currently, the scanner from the unified labeling client doesn't write information to the event log.

-----

情報 **910**

**スキャナーのサイクルが開始しました。**

スキャナー サービスが開始され、指定したデータ リポジトリ内のファイルのスキャンが開始されたときに、このイベントがログに記録されます。

----

情報 **911**

**スキャナーのサイクルが完了しました。**

スキャナーで手動スキャンまたは継続的スケジュールのサイクルが完了すると、このイベントがログに記録されます。

スキャナーを連続ではなく手動で実行するように構成した場合、ファイルをもう一度スキャンするには、スキャナーのプロファイルで **[スケジュール]** を **[手動]** または **[常時]** に設定して、サービスを再起動します。

----

## <a name="next-steps"></a>次のステップ

Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

[Windows Server FCI と Azure Information Protection スキャナーの違い](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)についてご説明します。

また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 For more information about this and other scenarios that use PowerShell, see the following sections from the admin guides:

- For the classic client: [Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)

- For the unified labeling client: [Using PowerShell with the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-powershell.md)
