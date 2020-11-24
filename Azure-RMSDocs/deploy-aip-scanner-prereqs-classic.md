---
title: Azure Information Protection (AIP) classic スキャナーの前提条件
description: Azure Information Protection クラシックスキャナーをインストールして展開するための前提条件を示します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4c466fbbad6314a6b0ea0dddb85d07d359a42467
ms.sourcegitcommit: 72694afc0e74fd51662e40db2844cdb322632428
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "95571014"
---
# <a name="prerequisites-for-installing-and-deploying-the-azure-information-protection-classic-scanner"></a>Azure Information Protection クラシックスキャナーをインストールして展開するための前提条件

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と **ラベル管理** は、**2021 年 3 月 31 日** で **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。 
> 
> 統一されたラベル付けスキャナーを使用している場合は、Azure Information Protection 統合された [ラベル付けスキャナーをインストールおよび展開するための前提条件](deploy-aip-scanner-prereqs.md)を参照してください。

オンプレミスの Azure Information Protection スキャナーをインストールする前に、システムが基本的な [Azure Information Protection 要件](requirements.md)に準拠していること、およびスキャナーに固有の次の要件を満たしていることを確認してください。

- [Windows Server の要件](#windows-server-requirements)
- [サービス アカウントの要件](#service-account-requirements)
- [SQL server の要件](#sql-server-requirements)
- [Azure Information Protection クライアントの要件](#azure-information-protection-client-requirements)
- [構成要件のラベル](#label-configuration-requirements)
- [SharePoint の要件](#sharepoint-requirements)
- [Microsoft Office の要件](#microsoft-office-requirements)
- [ファイルパスの要件](#file-path-requirements)
- [使用状況の統計情報の要件](#usage-statistics-requirements)

組織のポリシーによって禁止されているためにテーブル内のすべての要件を満たすことができない場合は、「 [代替構成](#deploying-the-scanner-with-alternative-configurations) 」セクションを参照してください。

スキャナーを運用環境にデプロイする場合、または複数のスキャナーのパフォーマンスをテストする場合は、「 [SQL Server のための記憶域の要件と容量計画](#storage-requirements-and-capacity-planning-for-sql-server)」を参照してください。

スキャナーのインストールと展開を開始する準備ができたら、 [Azure Information Protection スキャナーの展開を続けて、ファイルを自動的に分類して保護](deploy-aip-scanner-configure-install-classic.md)します。

## <a name="windows-server-requirements"></a>Windows Server の要件

スキャナーを実行するには、次のシステム仕様の Windows Server コンピューターが必要です。

|仕様  |詳細  |
|---------|---------|
|**プロセッサ**     |4コアプロセッサ         |
|**RAM**     |8 GB         |
|**ディスク領域**     |一時ファイルの場合、10 GB の空き領域 (平均)。 </br></br>スキャナーは、スキャンする各ファイル用に、コアごとに 4 つの一時ファイルを作成するために、十分なディスク領域を必要とします。 </br></br>推奨される 10 GB のディスク領域を使用すると、4 コア プロセッサで、それぞれのサイズが 625 MB であるファイルを 16 個スキャンできます。 
|**オペレーティング システム**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**注:** 非運用環境でのテストまたは評価の目的では、 [Azure Information Protection クライアントでサポート](requirements.md#client-devices)されている任意の Windows オペレーティングシステムを使用することもできます。
|**ネットワーク接続**     | スキャナーコンピューターは、スキャンするデータストアへの高速で信頼性の高いネットワーク接続がある物理コンピューターまたは仮想コンピューターにすることができます。 </br></br> 組織のポリシーのためにインターネット接続ができない場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」を参照してください。 </br></br>それ以外の場合は、このコンピューターがインターネットに接続されていることを確認し、HTTPS 経由で次の Url を使用できるようにします (ポート 443)。</br><br />-  \*. aadrm.com <br />-  \*. azurerms.com<br />-  \*. informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*. aria.microsoft.com|
| ||

## <a name="service-account-requirements"></a>サービス アカウントの要件

Windows Server コンピューターでスキャナーサービスを実行するには、サービスアカウントが必要です。また、Azure AD を認証し、Azure Information Protection ポリシーをダウンロードする必要があります。

サービスアカウントは Active Directory アカウントであり、Azure AD に同期されている必要があります。

組織のポリシーのためにこのアカウントを同期できない場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」を参照してください。

このサービス アカウントには次の要件があります。

|要件  |詳細  |
|---------|---------|
|**ローカルログオン** ユーザー権利の割り当て     |スキャナーのインストールと構成に必要ですが、スキャンの実行には必要ありません。  </br></br>スキャナーがファイルを検出、分類、保護できることを確認したら、サービスアカウントからこの権限を削除できます。  </br></br>組織のポリシーにより、この権限を短時間でも付与できない場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」を参照してください。         |
|**[サービスとしてログオン]** ユーザー権限の割り当て。     |  この権限は、スキャナーのインストール中にサービス アカウントに自動的に付与され、スキャナーのインストール、構成、操作に必要です。        |
|**データリポジトリに対するアクセス許可**     |- **ファイル共有またはローカルファイル:** ファイルをスキャンし、構成どおりに分類と保護を適用するための **読み取り**、 **書き込み**、 **変更** のアクセス許可を付与します。  <br /><br />- **SharePoint:** ファイルをスキャンし、構成どおりに分類と保護を適用するための **フルコントロール** アクセス許可を付与します。  <br /><br />- **検出モード:** スキャナーを検出モードでのみ実行するには、 **読み取り** アクセス許可で十分です。         |
|**保護を再保護または削除するラベルの場合**     | スキャナーが常に保護されたファイルにアクセスできるようにするには、このアカウントを Azure Information Protection の [スーパーユーザー](configure-super-users.md) にして、スーパーユーザー機能が有効になっていることを確認します。 </br></br>さらに、段階的展開の [オンボードコントロール](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) を実装している場合は、構成したオンボードコントロールにサービスアカウントが含まれていることを確認してください。|
| ||

## <a name="sql-server-requirements"></a>SQL server の要件

スキャナー構成データを格納するには、次の要件を持つ SQL server を使用します。

- **ローカルまたはリモートのインスタンス。**

    小規模なデプロイを使用している場合を除き、SQL server とスキャナーサービスを異なるコンピューターでホストすることをお勧めします。 また、スキャナーデータベースのみを提供し、他のアプリケーションと共有されない専用の SQL インスタンスを用意することをお勧めします。

    共有サーバーで作業している場合は、スキャナーデータベースが動作するために、推奨される [コア数](#windows-server-requirements) が無料であることを確認してください。

    次のエディションでは、SQL Server 2012 が最小バージョンとなります。

    - SQL Server Enterprise
    - SQL Server Standard
    - SQL Server Express (テスト環境にのみ推奨)

- **スキャナーをインストールする Sysadmin ロールを持つアカウント。**

    これにより、インストールプロセスでスキャナー構成データベースが自動的に作成され、スキャナーを実行するサービスアカウントに必要な **db_owner** ロールが付与されます。 

    Sysadmin ロールが付与されていない場合、または組織のポリシーでデータベースを手動で作成して構成する必要がある場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」を参照してください。

- **容量。** 容量のガイダンスについては、「 [SQL Server のストレージ要件と容量計画](#storage-requirements-and-capacity-planning-for-sql-server)」を参照してください。

- **[大文字と小文字を区別しない照合順序](/sql/relational-databases/collations/collation-and-unicode-support)**

> [!NOTE]
> スキャナーにカスタムクラスター (プロファイル) 名を指定した場合、同じ SQL server 上の複数の構成データベースがサポートされます。
> 

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>SQL Server のストレージ要件と容量計画

スキャナーの構成データベースに必要なディスク領域と、SQL Server を実行しているコンピューターの仕様は環境によって異なる場合があるため、独自のテストを行うことをお勧めします。 次のガイダンスを出発点として使用してください。

詳細については、「 [スキャナーのパフォーマンスの最適化](deploy-aip-scanner-configure-install-classic.md#optimizing-scanner-performance)」を参照してください。

構成データベースのディスクサイズは、展開ごとに異なります。 スキャンする100万ファイルごとに 500 MB を割り当てることをお勧めします。 

スキャナーごとに、次を使用します。

- 4コアプロセッサ
- 8 GB RAM (最小 4 GB)

## <a name="azure-information-protection-client-requirements"></a>Azure Information Protection クライアントの要件

Windows Server コンピューターに Azure Information Protection クライアントがインストールされている必要があります。

詳細については、「 [従来のクライアント管理者ガイド](./rms-client/client-admin-guide.md)」を参照してください。

> [!IMPORTANT]
> スキャナーに対する完全なクライアントをインストールする必要があります。 PowerShell モジュールだけで、クライアントをインストールしないでください。
> 

## <a name="label-configuration-requirements"></a>構成要件のラベル

分類、および必要に応じて保護を自動的に適用するようにラベルを構成する必要があります。

これらのラベルが構成されていない場合は、「 [代替構成を使用したスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」を参照してください。

詳細については次を参照してください:

- [自動および推奨分類の条件を構成する方法](configure-policy-classification.md)
- [Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)

> [!TIP] 
> [チュートリアル](infoprotect-quick-start-tutorial.md)の指示に従って、準備された Word 文書でクレジットカード番号を検索するラベルを使用してスキャナーをテストします。 ただし、 **[このラベルを適用する方法を選択** する] オプションが [**推奨**] ではなく [**自動**] に設定されているように、ラベルの構成を変更する必要があります。また、推奨ラベルは自動 (スキャナーバージョン 2.7. x. x 以降で使用可能)**として扱い** ます。 
>
> その後、(適用される場合は) ドキュメントからラベルを削除して、スキャナー用のデータ リポジトリにファイルをコピーします。 

## <a name="sharepoint-requirements"></a>SharePoint の要件

SharePoint ドキュメントライブラリおよびフォルダーをスキャンするには、SharePoint サーバーが次の要件を満たしていることを確認します。

- **サポートされているバージョン。** サポートされているバージョンは、SharePoint 2019、SharePoint 2016、および SharePoint 2013 です。 スキャナーでは SharePoint の他のバージョンはサポートされていません。

- **版.** [バージョン管理](/sharepoint/governance/versioning-content-approval-and-check-out-planning)を使用すると、スキャナーは最後に発行されたバージョンを検査してラベルを付けます。 スキャナーがファイルと [コンテンツの承認](/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) を必要とする場合は、そのラベルの付いたファイルをユーザーが使用できるように承認する必要があります。  

- **大規模な SharePoint ファーム。** 大規模な SharePoint ファームの場合は、スキャナーがすべてのファイルにアクセスするために、リスト ビューのしきい値 (既定では 5,000) を増やす必要があるかどうかを確認します。 詳細については、「 [SharePoint での大規模なリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。


## <a name="microsoft-office-requirements"></a>Microsoft Office の要件

Office ドキュメントをスキャンするには、ドキュメントは次のいずれかの形式である必要があります。

- Microsoft Office 97-2003 
- Word、Excel、PowerPoint 用の Office Open XML 形式

詳細については、「 [Azure Information Protection クライアントでサポートされるファイルの種類](./rms-client/client-admin-guide-file-types.md)」を参照してください。

## <a name="file-path-requirements"></a>ファイルパスの要件

ファイルをスキャンするには、スキャナーが Windows 2016 にインストールされていて、長いパスをサポートするようにコンピューターが構成されていない限り、ファイルパスの文字数は最大260文字にする必要があります。

Windows 10 および windows Server 2016 は、次の [グループポリシー設定](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)を使用して、260文字を超えるパスの長さをサポートしています:**ローカルコンピューターポリシー**  >  **コンピューターの構成**  >  **管理用テンプレート**  >  **すべての設定** で  >  **Win32 の長いパスを有効にする**

長いファイルのパスのサポートについて詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

## <a name="usage-statistics-requirements"></a>使用状況の統計情報の要件

次のいずれかの方法を使用して使用状況の統計を無効にします。

- [Allowtelemetry](./rms-client/client-admin-guide-install.md#to-install-the-azure-information-protection-client-by-using-the-executable-installer)パラメーターを0に設定しています

- スキャナーのインストールプロセス中に、[ **使用状況の統計を Microsoft に送信して Azure Information Protection を改善** する] オプションが選択されていないことを確認します。


## <a name="deploying-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーのデプロイ

上記の前提条件は、スキャナー展開の既定の要件であり、最も単純なスキャナー構成をサポートしているため推奨されています。

既定の要件は、初期テストに適しているため、スキャナーの機能を確認できます。 

ただし、運用環境では、組織のポリシーによってこれらの既定の要件が禁止されることがあります。 スキャナーは、追加の構成に関する次の制限事項に対応できます。

- [スキャナーサーバーはインターネットに接続できません](#restriction-the-scanner-server-cannot-have-internet-connectivity)

- [制限: スキャナーサービスアカウントを Azure Active Directory に同期することはできませんが、サーバーがインターネットに接続しています](#restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity)

- [制限: スキャナーのサービスアカウントに **ローカルログオン** 権限を付与することはできません](#restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right)

- [制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある](#restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually)

- [制限: ラベルにオートラベルの条件がありません](#restriction-your-labels-do-not-have-auto-labeling-conditions)

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>制限: スキャナーサーバーはインターネットに接続できません

切断されたコンピューターをサポートするには、次の手順を実行します。

1. 分類のみを適用するラベルを構成するか、 [HYOK 保護](configure-adrms-restrictions.md)を使用する保護を適用します。 

    インターネット接続がないと、組織のクラウドベースのキーを使用して保護を適用したり、保護を削除したり、保護されたファイルを検査したりすることはできません。 代わりに、スキャナーは分類のみを適用するラベルを使用するか、HYOK 保護を使用する保護を適用するかに制限されます。
    
    詳細については、「切断された [コンピューターのサポート](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)」を参照してください。

1. スキャナークラスターを作成して、Azure portal でスキャナーを構成します。 この手順に関してサポートが必要な場合は、「[Azure portal でスキャナーを構成する](deploy-aip-scanner-configure-install-classic.md#configure-the-scanner-in-the-azure-portal)」をご覧ください。

2. [**エクスポート**] オプションを使用して、[ **Azure Information Protection コンテンツスキャンジョブ**] ウィンドウからコンテンツジョブをエクスポートします。

3. PowerShell セッションで、 [Import-Aipscanの構成](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) を実行し、エクスポートされた設定を含むファイルを指定します。

### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

スキャナーをインストールするために Sysadmin の役割を *一時的* に付与できる場合は、スキャナーのインストールが完了したらこの役割を削除できます。

組織の要件に応じて、次のいずれかの操作を行います。

- **Sysadmin ロールを一時的に持つことができます。** Sysadmin ロールを一時的に持っている場合は、データベースが自動的に作成され、スキャナーのサービスアカウントに必要なアクセス許可が自動的に付与されます。

    ただし、スキャナーを構成するユーザーアカウントには、スキャナー構成データベースの **db_owner** ロールが必要です。 スキャナーのインストールが完了するまで Sysadmin の役割しかない場合は、 [ユーザーアカウントに db_owner の役割を手動で付与](#create-a-user-and-grant-db_owner-rights-manually)します。

- **Sysadmin ロールをまったく持つことはできません**。 Sysadmin ロールが一時的に付与されていない場合は、スキャナーをインストールする前に、データベースを手動で作成するための Sysadmin 権限をユーザーに要求する必要があります。 

    この構成では、 **db_owner** ロールが次のアカウントに割り当てられている必要があります。 

    - スキャナーのサービス アカウント

    - スキャナーのインストール用のユーザーアカウント

    - スキャナーの構成用のユーザー アカウント
      
    通常、スキャナーのインストールと構成には同じユーザー アカウントを使用します。 異なるアカウントを使用する場合は、どちらもスキャナー構成データベースの db_owner ロールが必要です。 必要に応じて、このユーザーと権限を作成します。 

    スキャナーに独自のクラスター (プロファイル) 名を指定しない場合、構成データベースには **AIPScanner_ \<computer_name>** という名前が付けられます。 </br>引き続き、 [ユーザーの作成と、データベースに対する db_owner 権限の付与](#create-a-user-and-grant-db_owner-rights-manually)を行います。 

追加として:

- スキャナーを実行するサーバーのローカル管理者である必要があります。
- スキャナーを実行するサービスアカウントには、次のレジストリキーに対するフルコントロールのアクセス許可が付与されている必要があります。
    
    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

これらのアクセス許可を構成した後、スキャナーをインストールするときにエラーが表示される場合は、エラーを無視して、スキャナーサービスを手動で開始することができます。

#### <a name="populate-the-database-manually"></a>データベースを手動で設定する

次のスクリプトを使用してデータベースを設定します。 

```sql
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END 
```

#### <a name="create-a-user-and-grant-db_owner-rights-manually"></a>ユーザーを作成し、手動で db_owner 権限を付与する

このデータベースに対してユーザーを作成し db_owner 権限を付与するには、Sysadmin に次の操作を依頼します。

1. スキャナー用の DB を作成します。

    ```sql
    **CREATE DATABASE AIPScannerUL_[clustername]**
    
    **ALTER DATABASE AIPScannerUL_[clustername] SET TRUSTWORTHY ON**
    ```
    
2. インストールコマンドを実行するユーザーに権限を付与し、スキャナー管理コマンドを実行するために使用します。

    SQL スクリプト:
    
    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. スキャナーサービスアカウントに権限を付与します。

    SQL スクリプト:

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>制限: スキャナーのサービス アカウントに **ローカル ログオン** 権限を付与できない

組織のポリシーでサービスアカウントに対する **ローカルログオン** 権限が禁止されているが、 **バッチジョブとしてログオン** する権限が許可されている場合は、 [Set-aipauthentication に Token パラメーターを指定して使用](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)します。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>制限: スキャナーサービスアカウントを Azure Active Directory に同期することはできませんが、サーバーがインターネットに接続しています

スキャナーのサービスを実行するために 1 つのアカウントを持ち、Azure Active Directory を認証するために別のアカウントを使用することができます。

- **スキャナーサービスアカウントの** 場合は、ローカルの Windows アカウントまたは Active Directory アカウントを使用します。

- **Azure Active Directory アカウントの場合は、** [Set-Aipauthentication に Token パラメーターを指定して使用](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)します。

#### <a name="restriction-your-labels-do-not-have-auto-labeling-conditions"></a>制限: ラベルにオートラベルの条件がありません

ラベルに自動ラベルの条件がない場合は、スキャナーを構成するときに、次のいずれかのオプションを使用することを計画します。

|オプション  |説明  |
|---------|---------|
|**すべての情報の種類を検出**     |  [コンテンツスキャンジョブ](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)で、[情報の **種類**] を [検出済み]**に設定します。** </br></br>このオプションは、すべての機密情報の種類についてコンテンツをスキャンするようにコンテンツスキャンジョブを設定します。      |
|**既定のラベルを定義する**     |   [ポリシー](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do)、[コンテンツスキャンジョブ](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)、または[リポジトリ](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository)で既定のラベルを定義します。 </br></br>この場合、スキャナーは、見つかったすべてのファイルに既定のラベルを適用します。       |
| | |

## <a name="next-steps"></a>次のステップ

システムがスキャナーの前提条件に準拠していることを確認したら、 [Azure Information Protection スキャナーの展開を続けて、ファイルを自動的に分類して保護](deploy-aip-scanner-configure-install-classic.md)します。

スキャナーの概要については、「 [ファイルを自動的に分類して保護するための Azure Information Protection スキャナーの展開](deploy-aip-scanner-classic.md)」を参照してください。

**詳細情報:**

Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

[Windows Server FCI と Azure Information Protection スキャナーの違いは何ですか](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)。

また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 PowerShell を使用するその他のシナリオの詳細については、「 [Azure Information Protection クラシッククライアントでの powershell の使用](./rms-client/client-admin-guide-powershell.md)」を参照してください。