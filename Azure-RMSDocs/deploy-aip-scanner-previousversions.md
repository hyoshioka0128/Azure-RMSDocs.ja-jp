---
title: Azure Information Protection スキャナーを展開する-以前のバージョン
description: 現在の一般公開バージョンより古いバージョンの Azure Information Protection スキャナーの配置手順。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 43ff7296f3b35cf63347fef678d3c0d173a5e39c
ms.sourcegitcommit: 2cb5fa2a8758c916da8265ae53dfb35112c41861
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88953016"
---
# <a name="deploying-previous-versions-of-the-azure-information-protection-scanner"></a>以前のバージョンの Azure Information Protection スキャナーの展開

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

> [!NOTE]
> この記事は、バージョン **1.48.204.0** より前の Azure Information Protection スキャナーのバージョンであり、まだサポートされています。 以前のバージョンを現在のバージョンにアップグレードするには、「 [Azure Information Protection スキャナーをアップグレード](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)する」を参照してください。
>
> Azure portal からの構成を含む、現在のバージョンのスキャナーのデプロイ手順については、「 [ファイルを自動的に分類して保護するための Azure Information Protection スキャナーの展開](deploy-aip-scanner.md)」を参照してください。

この情報を使用して、Azure Information Protection スキャナーについて説明し、正常にインストール、構成、および実行する方法について説明します。

このスキャナーは、Windows Server でサービスとして実行され、次のデータ ストア上のファイルを検出、分類、および保護することができます。

- サーバー メッセージ ブロック (SMB) プロトコルを使用するネットワーク共有の UNC パス。

- Sharepoint server 2019 のドキュメントライブラリとフォルダーは、SharePoint Server 2013 を介して使用できます。 [SharePoint 2010 の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)をご利用のお客様向けに、このバージョンの SharePoint もサポートされています。

クラウド リポジトリ上のファイルをスキャンおよびラベル付けするには、スキャナーの代わりに [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) を使用します。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの概要

自動分類を適用するラベルに [Azure Information Protection ポリシー](configure-policy.md)を構成している場合、このスキャナーで検出されたファイルにラベルを付けることができます。 ラベルは分類を適用し、必要に応じて、保護を適用または保護を解除します。

![Azure Information Protection スキャナーのアーキテクチャの概要](./media/infoprotect-scanner.png)

スキャナーは、コンピューターにインストールされている IFilters を使うことで、Windows によってインデックス化できるすべてのファイルを検証できます。 そして、ファイルでラベル付けが必要かどうかを判断するため、スキャナーで Office 365 に組み込まれたデータ損失防止 (DLP) の機密情報の種類とパターン検出、または Office 365 の正規表現パターンが使われます。 スキャナーは Azure Information Protection クライアントを使用するため、同じ[ファイルの種類](./rms-client/client-admin-guide-file-types.md)を分類および保護できます。

スキャナーを実行できるのは検索モードでのみです。この場合、レポートを使用して、ファイルがラベル付けされた場合に何が発生するかをチェックします。 またはスキャナーを実行して、自動的にラベルを適用できます。 機密情報の種類を含んだファイルを検出するためにスキャナーを実行することもできます (自動分類を適用する条件用にラベルを構成する必要はありません)。

スキャナーは検出せず、リアルタイムでラベル付けしないことに注意してください。 スキャナーは指定したデータ ストア上のファイルを体系的にクロールします。この実行サイクルは、1 回限りまたは繰り返しに設定することができます。

スキャンするファイルの種類を指定したり、スキャン対象から除外することができます。 スキャナーによって検査されるファイルを制限するには、**Set-AIPScannerScannedFileTypes** を使用してファイルの種類のリストを定義します。

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの前提条件

Azure Information Protection スキャナーをインストールする前に、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|スキャナー サービスを実行する Windows Server コンピューター:<br /><br />- 4 コア プロセッサ<br /><br />- 8 GB の RAM<br /><br />- 一時ファイルのための空き容量 10 GB (平均)|Windows Server 2019、Windows Server 2016、または Windows Server 2012 R2。 <br /><br />**注**: 非運用環境でテストまたは評価を行う場合は、 [Azure Information Protection クライアントでサポート](requirements.md#client-devices)されている Windows クライアントオペレーティングシステムを使用できます。<br /><br />このコンピューターは、スキャンするデータ ストアへの高速で信頼性の高いネットワーク接続がある物理コンピューターまたは仮想コンピューターにすることができます。<br /><br /> スキャナーは、スキャンする各ファイル用に、コアごとに 4 つの一時ファイルを作成するために、十分なディスク領域を必要とします。 推奨される 10 GB のディスク領域を使用すると、4 コア プロセッサで、それぞれのサイズが 625 MB であるファイルを 16 個スキャンできます。 <br /><br />組織のポリシーのためにインターネット接続ができない場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations) 」セクションを参照してください。 それ以外の場合は、このコンピューターがインターネットに接続されていることを確認し、HTTPS 経由で次の Url を使用できるようにします (ポート 443)。<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|スキャナー サービスを実行するサービス アカウント |Windows Server コンピューター上でのスキャナー サービスの実行に加えて、この Windows アカウントは Azure AD で認証され、Azure Information Protection ポリシーをダウンロードします。 このアカウントは Active Directory アカウントであり、かつ Azure AD と同期している必要があります。 組織のポリシーによってこのアカウントを同期できない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />このサービス アカウントには次の要件があります。<br /><br />- **[Log on locally]\(ローカル ログオン\)** ユーザー権限の割り当て。 この権限は、スキャナーのインストールと構成に必要ですが、操作には必要ありません。 この権限をサービス アカウントに付与する必要がありますが、スキャナーがファイルを検出、分類、保護できることを確認したら、この権限を削除することができます。 組織のポリシーによって、短時間でもこの権限を付与することができない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />- **[サービスとしてログオン]** ユーザー権限の割り当て。 この権限は、スキャナーのインストール中にサービス アカウントに自動的に付与され、スキャナーのインストール、構成、操作に必要です。 <br /><br />-データリポジトリに対するアクセス許可: オンプレミスの SharePoint のデータリポジトリの場合、サイトの [**ページの追加とカスタマイズ**] が選択されている場合は、[**編集**] アクセス許可を常に付与します。または、[**デザイン**] アクセス許可を付与します。 その他のデータリポジトリの場合は、ファイルをスキャンして、Azure Information Protection ポリシーの条件を満たすファイルに分類と保護を適用する **読み取り** と **書き込み** のアクセス許可を付与します。 これらの他のデータリポジトリに対してのみ検出モードでスキャナーを実行するには、 **読み取り** アクセス許可で十分です。<br /><br />- 再保護または保護を解除するラベル: スキャナーが保護されたファイルに常にアクセスできるようにするには、このアカウントを Azure Rights Management サービスの[スーパー ユーザー](configure-super-users.md)にして、スーパー ユーザー機能が有効になっていることを確認します。 保護を適用するためのアカウント要件の詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」を参照してください。 さらに、段階的な展開の[オンボーディング制御](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を実装している場合は、このアカウントが構成したオンボーディング制御に含まれていることを確認してください。|
|スキャナーの構成を格納する SQL Server:<br /><br />- ローカルまたはリモート インスタンス<br /><br />- [大文字と小文字を区別しない照合順序](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15) <br /><br />- スキャナーをインストールする sysadmin ロール|次のエディションでは、SQL Server 2012 が最小バージョンとなります。<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />スキャナーの複数のインスタンスをインストールする場合は、スキャナー インスタンスごとに独自の SQL Server インスタンスが必要です。<br /><br />Sysadmin ロールを持つアカウントでスキャナーをインストールすると、インストールのプロセスで AzInfoProtectionScanner データベースが自動的に作成され、スキャナーを実行するサービス アカウントに対して必要な db_owner ロールが付与されます。 Sysadmin ロールが付与されない場合や、組織のポリシーがデータベースを手動で作成し構成することを要求している場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」をご覧ください。<br /><br />構成データベースのサイズはデプロイごとに異なりますが、スキャンしたい 1,000,000 ファイルごとに 500 MB を割り当てることをお勧めします。 |
|Azure Information Protection クライアント (クラシック) が Windows Server コンピューターにインストールされている|スキャナーに対する完全なクライアントをインストールする必要があります。 PowerShell モジュールだけで、クライアントをインストールしないでください。<br /><br />クライアントのインストール手順については、[管理者ガイド](./rms-client/client-admin-guide.md)を参照してください。 スキャナーを以前にインストールしていて、今回新しいバージョンにアップグレードする必要がある場合は、[「Azure Information Protection スキャナーのアップグレード](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)」をご覧ください。|
|自動分類と、必要に応じて保護を適用する構成済みのラベル|条件用にラベルを構成し、保護を適用する方法について詳しくは、次をご覧ください。<br /> - [自動および推奨分類の条件を構成する方法](configure-policy-classification.md)<br /> - [Rights Management 保護のラベルを構成する方法](configure-policy-protection.md) <br /><br />**ヒント**: [チュートリアル](infoprotect-quick-start-tutorial.md) の指示に従って、準備された Word 文書でクレジットカード番号を検索するラベルを使用してスキャナーをテストできます。 ただし、**[このラベルの適用方法を選択]** が **[推奨]** ではなく **[自動]** に設定されるように、ラベルの構成を変更する必要があります。 その後、(適用される場合は) ドキュメントからラベルを削除して、スキャナー用のデータ リポジトリにファイルをコピーします。 <br /><br /> 自動分類を適用するラベルを構成していない場合でもスキャナーを実行できますが、このシナリオについては、これらの手順では説明されていません。 [詳細情報](#using-the-scanner-with-alternative-configurations)|
|スキャンする SharePoint ドキュメントライブラリおよびフォルダーの場合:<br /><br />-SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|スキャナーでは SharePoint の他のバージョンはサポートされていません。<br /><br />[バージョン管理](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning)を使用すると、スキャナーは最後に発行されたバージョンを検査してラベルを付けます。 スキャナーがファイルと [コンテンツの承認](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) を必要とする場合は、そのラベルの付いたファイルをユーザーが使用できるように承認する必要があります。 <br /><br />大規模な SharePoint ファームの場合は、スキャナーがすべてのファイルにアクセスするために、リスト ビューのしきい値 (既定では 5,000) を増やす必要があるかどうかを確認します。 詳細については、SharePoint のドキュメント「 [sharepoint での大規模なリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。|
|スキャンされる Office ドキュメントの場合:<br /><br />- Word、Excel、PowerPoint の 97-2003 ファイル形式および Office Open XML 形式|これらのファイル形式についてスキャナーでサポートされるファイルの種類について詳しくは、「[Azure Information Protection クライアントでサポートされるファイルの種類](./rms-client/client-admin-guide-file-types.md)」をご覧ください|
|長いパスの場合:<br /><br />- 最大 260 文字 (スキャナーが Windows 2016 にインストールされていて、コンピューターが長いパスをサポートするように構成されているのでない場合)|Windows 10 および windows Server 2016 は、次の[グループポリシー設定](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)を使用して、260文字を超えるパスの長さをサポートしています:**ローカルコンピューターポリシー**  >  **コンピューターの構成**  >  **管理用テンプレート**  >  **すべての設定**で  >  **Win32 の長いパスを有効にする**<br /><br /> 長いファイルのパスのサポートについて詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

組織のポリシーによる禁止のためにテーブルの要件をすべて満たすことができない場合は、代替案として次のセクションをご覧ください。

要件がすべて満たされる場合は、[インストールのセクション](#install-the-scanner)に直接移動してください。

### <a name="deploying-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーのデプロイ

テーブルに一覧表示されている前提条件は、スキャナーの既定の要件であり、推奨されます。何故なら、これらはスキャナーをデプロイするための最も簡単な構成であるためです。 これらは、スキャナーの機能を確認するための最初のテスト用に適しています。 ただし、運用環境では、次の制限の 1 つ以上に該当するために組織のポリシーによって既定の要件が禁止される場合があります。

- サーバーはインターネット接続を許可されていません

- Sysadmin が付与されていないため、データベースを手動で作成および構成する必要がある

- サービスアカウント **にローカルログオン** 権限を付与することはできません

- サービスアカウントを Azure Active Directory に同期することはできませんが、サーバーがインターネットに接続しています

スキャナーをこれらの制限に対応させることは可能ですが、追加構成が必要です。

#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>制限: スキャナーサーバーはインターネットに接続できません

[切断されたコンピューター](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)向けの手順に従ってください。

この構成では、スキャナーは、組織のクラウドベース キーを使用することによる保護 (または保護の削除) を適用できません。 代わりに、スキャナーは、分類にのみ適用されるラベルの使用か、[HYOK](configure-adrms-restrictions.md) を使用する保護に制限されます。

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

スキャナーをインストールするために一時的に Sysadmin ロールが付与される場合、スキャナーのインストールが完了したらこのロールを削除できます。 この構成を使用すると、データベースが自動的に作成され、スキャナー用のサービス アカウントに必要なアクセス許可が自動的に付与されます。 ただし、スキャナーを構成するユーザー アカウントには、AzInfoProtectionScanner データベースの db_owner ロールが必要です。このロールをユーザー アカウントに手動で付与する必要があります。

Sysadmin ロールが一時的に付与されていない場合は、スキャナーをインストールする前に、Sysadmin 権限を持つユーザーに、AzInfoProtectionScanner という名前のデータベースを手動で作成するように依頼する必要があります。 この構成では、次のロールを割り当てる必要があります。

|Account|データベースレベルのロール|
|--------------------------------|---------------------|
|スキャナーのサービス アカウント|db_owner|
|スキャナーのインストール用のユーザー アカウント|db_owner|
|スキャナーの構成用のユーザー アカウント |db_owner|

通常、スキャナーのインストールと構成には同じユーザー アカウントを使用します。 別々のアカウントを使用する場合は、両方に AzInfoProtectionScanner データベースの db_owner ロールが必要です。

このデータベースに対してユーザーを作成し db_owner 権限を付与するには、Sysadmin に次の SQL スクリプトを2回実行するように依頼します。 スキャナーを実行するサービスアカウントと、スキャナーをインストールして管理するための2回目の時間。 スクリプトを実行する前に、 *domain\user* を、サービスアカウントまたはユーザーアカウントのドメイン名とユーザーアカウント名に置き換えます。

```sql
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
USE AzInfoProtectionScanner IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
```

補足:

- スキャナーを実行するサーバーのローカル管理者である必要があります。
- スキャナーを実行するサービスアカウントには、次のレジストリキーに対するフルコントロールのアクセス許可が付与されている必要があります。

    - HKEY_LOCAL_MACHINE \SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\MSIPC\Server

これらのアクセス許可を構成した後、スキャナーをインストールするときにエラーが表示される場合は、エラーを無視して、スキャナーサービスを手動で開始することができます。

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>制限: スキャナーのサービス アカウントに**ローカル ログオン**権限を付与できない

組織のポリシーで、サービス アカウントに対する**ローカル ログオン**権限の付与が禁止されているが、**バッチ ジョブとしてログオン**権限が許可されている場合は、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」の手順に従います。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>制限: スキャナーサービスアカウントを Azure Active Directory に同期することはできませんが、サーバーがインターネットに接続しています

スキャナーのサービスを実行するために 1 つのアカウントを持ち、Azure Active Directory を認証するために別のアカウントを使用することができます。

- スキャナーのサービス アカウントのためには、ローカルの Windows アカウントか Active Directory アカウントを使用できます。

- Azure Active Directory アカウントの場合は、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」の手順に従ってください。

## <a name="install-the-scanner"></a>スキャナーのインストール

1. スキャナーを実行する Windows Server コンピューターにサインインします。 ローカル管理者権限と SQL Server マスター データベースに書き込むためのアクセス許可を持つアカウントを使用します。

2. **[管理者として実行]** オプションを使用して Windows PowerShell セッションを開きます。

3. Azure Information Protection スキャナー用のデータベースを作成する SQL Server インスタンスを指定して、 **Install-AIPScanner** コマンドレットを実行します。

    ```ps
    Install-AIPScanner -SqlServerInstance <name>
    ```

    次に例を示します。

    - 既定のインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1`

    - 名前付きインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`

    - SQL Server Express の場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`

    プロンプトが表示されたら、スキャナーサービスアカウントの資格情報 ( \<domain\user name> ) とパスワードを入力します。

4. **管理ツール**サービスを使用して、サービスがインストールされていることを確認し  >  **Services**ます。

    インストールされているサービスの名前は **Azure Information Protection スキャナー**で、作成したスキャナー サービス アカウントを使用して実行するように構成されます。

スキャナーをインストールしたら、スキャナーを無人で実行できるように、スキャナー サービス アカウントを認証するための Azure AD トークンを取得する必要があります。

## <a name="get-an-azure-ad-token-for-the-scanner"></a>スキャナー用の Azure AD トークンを取得する

Azure AD トークンを使用することで、Azure Information Protection サービスに対してスキャナー サービス アカウントを認証できます。

1. 同じ Windows Server コンピューター、またはデスクトップから、Azure Portal にサインインして、認証のためのアクセス トークンを指定するために必要な 2 つの Azure AD アプリケーションを作成します。 初めて対話型サインインをした後は、このトークンにより非対話的にスキャナーを実行できます。

    これらのアプリケーションを作成するには、管理者ガイドの「[非対話形式でファイルに Azure Information Protection のラベル付けをする方法](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」の指示に従います。

2. スキャナーのサービス アカウントにインストール用に**ローカルでログオン**する権限が付与されている場合、Windows Server コンピューターから、このアカウントを使用してサインインし、PowerShell セッションを開始します。 前の手順でコピーした値を指定して **Set-AIPAuthentication** を実行します。

    ```ps
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    求められたら、Azure AD のサービス アカウントの資格情報のパスワードを指定し、**[同意する]** をクリックします。

    スキャナーのサービス アカウントにインストールのための**ローカルでログオン**の権限が付与されない場合、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」の手順に従います。

これでスキャナーに Azure AD を認証するためのトークンが取得されました。トークンの有効期間は、Azure AD での **Web アプリ/API** の構成に従って、1 年間、2 年間、または無期限のいずれかになります。 トークンが期限切れになったら、手順 1 と 2 を繰り返す必要があります。

これでスキャンするデータ ストアを指定する準備ができました。

## <a name="specify-data-stores-for-the-scanner"></a>スキャナーのデータ ストアの指定

**Add-AIPScannerRepository** コマンドレットを使用して、Azure Information Protection スキャナーでスキャンするデータ ストアを指定します。 SharePoint ドキュメントライブラリおよびフォルダーの UNC パスと SharePoint サーバーの Url を指定できます。

Sharepoint でサポートされているバージョン: SharePoint Server 2019、SharePoint Server 2016、および SharePoint Server 2013。 [このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様向けに SharePoint Server 2010 もサポートされています。

1. 同じ Windows Server コンピューターから、PowerShell セッションで次のコマンドを実行して、最初のデータ ストアを追加します。

    ```ps
    Add-AIPScannerRepository -Path <path>
    ```

    たとえば、`Add-AIPScannerRepository -Path \\NAS\Documents` のように指定します。

    その他の例については、このコマンドレットの PowerShell ヘルプコマンドを使用して `Get-Help Add-AIPScannerRepository -examples` ください。

2. スキャンするすべてのデータ ストアに対し、このコマンドを繰り返します。 追加したデータ ストアを削除する必要がある場合は、**Remove-AIPScannerRepository** コマンドレットを使用します。

3. **Get-AIPScannerRepository** コマンドレットを実行して、すべてのデータ ストアが正しく指定されていることを確認します。
    
    ```ps
    Get-AIPScannerRepository
    ```

スキャナーの既定の構成を使用して、最初のスキャンを検索モードで実行できます。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>探索サイクルの実行とスキャナーのレポートの表示

1. PowerShell セッションで、次のコマンドを入力してスキャナーを起動します。

    ```ps
    Start-AIPScan
    ```

    または、Azure portal からスキャナーを起動することができます。 [ **Azure Information Protection-ノード** ] ウィンドウでスキャナーノードを選択し、[ **今すぐスキャン** ] オプションを選択します。

    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)

2. 次のコマンドを実行し、スキャナーがサイクルを完了するまで待機します。

    ```ps
    Get-AIPScannerStatus
    ```

    または、[**状態**] 列を確認して、Azure portal の [ **Azure Information Protection ノード**] ウィンドウから状態を表示することもできます。

    表示が **[スキャン中]** ではなく **[アイドル]** になっている状態を探します。

    スキャナーが指定したデータ ストア内のすべてのファイルをクロールすると、スキャナー サービスの動作が続いていてもスキャナーは停止します。

    ローカル Windows イベント ログの **[アプリケーションとサービス]** の **[Azure Information Protection]** を確認します。 このログでは、スキャナーがスキャンを完了した時刻も、結果の概要と共に報告されます。 情報イベント ID **911** を探します。

3. %*localappdata*%\Microsoft\MSIP\Scanner\Reports に格納されているレポートを確認します。 .txt の概要ファイルには、スキャンにかかった時間、スキャンされたファイルの数、情報の種類と一致したファイルの数が含まれています。 .csv ファイルには各ファイルに関する詳細情報が記載されています。 このフォルダーには、スキャンのサイクルごとに最大 60 のレポートが格納され、必要なディスク領域を最小限に抑えるために最新のもの以外のすべてのレポートが圧縮されます。

    > [!NOTE]
    > **Set-AIPScannerConfiguration** と共に *ReportLevel* パラメーターを使って、ログ記録のレベルを変更することができます。ただし、レポート フォルダーの場所または名前を変更することはできません。 別のボリュームまたはパーティションにレポートを保存したい場合は、フォルダーに対するディレクトリのジャンクションの使用を検討してください。
    >
    > たとえば、[Mklink](/windows-server/administration/windows-commands/mklink) コマンドを使います。`mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`

    既定の設定では、自動分類用に構成した条件を満たすファイルのみが詳細レポートに含まれます。 これらのレポートでラベルが適用されていない場合は、ラベルの構成に推奨される分類ではなく自動分類が含まれていることを確認します。

    > [!TIP]
    > スキャナーでは 5 分ごとにこの情報が Azure Information Protection に送信されます。このため、Azure portal から結果をほぼリアルタイムで確認することができます。 詳細については、[Azure Information Protection のレポート作成](reports-aip.md)に関するページを参照してください。

    結果が期待どおりにならない場合は、Azure Information Protection ポリシーに指定した条件を微調整する必要がある場合があります。 その場合は、構成を変更して分類、および必要に応じて保護を適用する準備ができるまで、手順 1 から 3 を繰り返します。

Azure portal には、最後のスキャンに関する情報のみが表示されます。 前のスキャンの結果を確認する必要がある場合は、スキャナー コンピューターの %*localappdata*%\Microsoft\MSIP\Scanner\Reports フォルダーに格納されているレポートに戻ります。

スキャナーが検出したファイルに自動的にラベル付けする準備ができたら、次の手順に進みます。

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>スキャナーを構成して分類と保護を適用する

既定の設定では、スキャナーは、レポートのみモードで 1 回だけ実行されます。 これらの設定を変更するには、次のように **設定**します。

1. Windows Server コンピューターの PowerShell セッションで、次のコマンドを実行します。

    ```ps
    Set-AIPScannerConfiguration -Enforce On -Schedule Always
    ```

    変更する可能性があるその他の構成があります。 たとえば、ファイル属性を変更するかどうか、およびレポートに記録する項目などがあります。 さらに、Azure Information Protection ポリシーに分類レベルを下げる、または保護を解除する理由メッセージを必要とする設定が含まれている場合、このコマンドレットを使用してそのメッセージを指定します。 各構成設定の詳細については、次の PowerShell ヘルプコマンドを使用してください。 `Get-Help Set-AIPScannerConfiguration -detailed`

2. 現在の時刻をメモしておき、次のコマンドを実行してもう一度スキャナーを開始します。
    
    ```ps
    Start-AIPScan
    ```

    または、Azure portal からスキャナーを起動することができます。 [ **Azure Information Protection-ノード** ] ウィンドウでスキャナーノードを選択し、[ **今すぐスキャン** ] オプションを選択します。

    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)

3. 情報の種類が **911** で、タイム スタンプが前の手順でスキャンを開始した時刻よりも後のイベント ログを再び監視します。

    次に、レポートをチェックして、ラベル付けされたファイル、各ファイルに適用された分類、それらに保護が適用されたかどうかについての詳細を確認します。 または、Azure portal を使用してより簡単にこの情報を確認します。

スケジュールを継続的に実行するように構成したため、スキャナーはすべてのファイルの作業を完了すると、新しいファイルや変更されたファイルをすべて検出するために新しいサイクルを開始します。

## <a name="how-files-are-scanned"></a>ファイルをスキャンする方法

スキャナーでは、ファイルをスキャンするとき、次のプロセスが実行されます。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. スキャンのためにファイルが含まれるか除外されるかを決定します。

スキャナーでは、実行可能ファイルやシステム ファイルなど、[分類と保護から除外されている](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)ファイルは自動的にスキップされます。

スキャンする (またはスキャン対象から除外する) ファイルの種類のリストを定義することで、この動作を変更できます。 このリストを指定し、データ リポジトリを指定しなかった場合、そのリストは、独自のリストが指定されていないすべてのデータ リポジトリに適用されます。 このリストを指定するには、**Set-AIPScannerScannedFileType** を使用します。

ファイルの種類のリストを指定した後、新しいファイルの種類をリストに追加するには、**Add-AIPScannerScannedFileTypes** を使用します。リストからファイルの種類を削除するには、**Remove-AIPScannerScannedFileTypes** を使用します。

### <a name="2-inspect-and-label-files"></a>2. ファイルを検査してラベルを付ける

その後、スキャナーでは、フィルターを使用して、サポートされているファイルの種類がスキャンされます。 これらの同じフィルターが、オペレーティング システムによって Windows Search とインデックス作成にも使用されます。 構成を何も追加しなくても、Word、Excel、PowerPoint、PDF ドキュメント、テキスト ファイルに対して使用されるファイルの種類のスキャンに、Windows IFilter が使用されます。

既定でサポートされているファイルの種類の完全な一覧、および .zip ファイルと .tiff ファイルを含む既存のフィルターの構成方法に関する追加情報については、「[検査に対してサポートされているファイルの種類](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)」をご覧ください。

検査が済むと、ユーザーがラベルに対して指定した条件を使用して、これらのファイルの種類にラベルを付けることができます。 または、検出モードを使用している場合は、ユーザーがラベルに対して指定した条件、またはすべての既知の機密情報の種類を含むように、これらのファイルを報告できます。

ただし、以下の状況では、スキャナーでファイルにラベルを付けることはできません。

- ラベルで分類は適用されるが、保護は適用されず、ファイルの種類で ["分類のみ" がサポート](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)されていない場合。

- ラベルで分類と保護が適用されるが、スキャナーでファイルの種類が保護されていない場合。

    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 他のファイルの種類は、次のセクションで説明するように、[レジストリを編集](#editing-the-registry-for-the-scanner)すると保護できます。

たとえば、.txt ファイルの種類では "分類のみ" がサポートされていないため、ファイル名拡張子が .txt であるファイルを検査した後は、分類用にだけ構成されていて保護用には構成されていないラベルを、スキャナーで適用することはできません。 ラベルが分類用と保護用に構成されていて、レジストリが .txt ファイルの種類用に編集されている場合は、スキャナーでファイルにラベルを付けることができます。

> [!TIP]
> このプロセス中にスキャナーが停止し、リポジトリ内の大量のファイルのスキャンが完了しない場合:
>
> - ファイルをホストしているオペレーティング システムに対し、動的ポートの数を増やす必要がある場合があります。 SharePoint 用にサーバーのセキュリティが強化されている場合、スキャナーが許可されているネットワーク接続の数を超えて、そのために停止する原因の 1 つになる可能性があります。
>  
>     スキャナーの停止の原因であるかどうかを確認するには、%*localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog (複数のログがある場合は zip 形式) のスキャナーに対して次のエラーメッセージが記録されているかどうかを確認してください。 **リモートサーバーに接続できません。 >。ソケット例外: 各ソケットアドレス (---プロトコル/ネットワークアドレス/ポート) の使用は通常、許可されている IP: ポートです**
>  
>     現在のポート範囲を表示し、範囲を拡大する方法について詳しくは、「[ネットワーク パフォーマンスを向上させるために変更可能な設定](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)」をご覧ください。
>
> - 大規模な SharePoint ファームの場合、リスト ビューのしきい値 (既定では 5,000) を増やす必要がある場合があります。 詳細については、SharePoint のドキュメント「 [sharepoint での大きなリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。

### <a name="3-label-files-that-cant-be-inspected"></a>3. 検査できないファイルにラベルを付ける

検査できないファイルの種類に対し、スキャナーでは Azure Information Protection ポリシーの既定のラベル、またはユーザーがスキャナー用に構成した既定のラベルが適用されます。

前のステップと同じように、以下の状況では、スキャナーでファイルにラベルを付けることはできません。

- ラベルで分類は適用されるが、保護は適用されず、ファイルの種類で ["分類のみ" がサポート](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)されていない場合。

- ラベルで分類と保護が適用されるが、スキャナーでファイルの種類が保護されていない場合。

    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 他のファイルの種類は、次に説明するように、[レジストリを編集](#editing-the-registry-for-the-scanner)すると保護できます。

### <a name="editing-the-registry-for-the-scanner"></a>スキャナーのレジストリの編集

Office ファイルと PDF 以外のファイルの種類を保護するためにスキャナーの既定の動作を変更するには、レジストリを手動で編集し、保護する他のファイルの種類と、保護の種類 (ネイティブまたは汎用) を指定する必要があります。 詳しくは、開発者ガイダンスの「[ファイル API の構成](develop/file-api-configuration.md)」をご覧ください。 この開発者向けドキュメントでは、汎用的な保護は "PFile" と呼ばれています。 さらに、スキャナーの場合:

- スキャナーには独自の既定の動作があります。既定では、Office ファイル形式と PDF ドキュメントのみが保護されます。 レジストリを変更しない場合、その他のファイル形式は、スキャナーによってラベル付けまたは保護されません。

- すべてのファイルがネイティブ保護または汎用保護で自動的に保護される Azure Information Protection クライアントと同じ既定の保護動作が必要な場合は、 `*` ワイルドカードをレジストリキーとして、 `Encryption` 値 (REG_SZ)、および値データとして指定します `Default` 。

レジストリを編集するときには、各ファイル名拡張子のキーと共に、**MSIPC** キーと **FileProtection** キーが存在しない場合には手動で作成します。

たとえば、Office ファイルと PDF だけでなく、TIFF イメージも保護するスキャナーの場合、レジストリの編集後は、次の図のようになります。 イメージ ファイルなので、TIFF ファイルではネイティブ保護がサポートされ、結果としてファイル名拡張子は .ptiff になります。

![保護を適用するためのスキャナーのレジストリの編集](./media/editregistry-scanner.png)

同様に、ネイティブ保護はサポートされていても、レジストリで指定する必要があるテキスト ファイルとイメージ ファイルの種類の一覧については、管理者ガイドの「[分類と保護がサポートされているファイルの種類](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)」をご覧ください。

ネイティブ保護がサポートされていないファイルの場合は、新しいキーとしてファイル名拡張子を指定し、汎用的な保護のために **PFile** を指定します。 結果として、保護されるファイルのファイル名拡張子は .pfile になります。

## <a name="when-files-are-rescanned"></a>ファイルが再スキャンされる場合

最初のスキャン サイクルではスキャナーは構成されているデータ ストアのすべてのファイルを検査し、後続のスキャンでは、新しいファイルまたは変更されたファイルのみが検査されます。

*Reset*パラメーターを指定して**Start-aipscan**を実行することで、すべてのファイルを再検査するようスキャナーに強制できます。 スキャナーは手動スケジュール用に構成されている必要があります。そのためには、 *schedule*パラメーターを**Set-Aipscanの構成**で**手動**に設定する必要があります。

または、Azure portal の [ **Azure Information Protection ノード** ] ウィンドウで、すべてのファイルを再度検査するようスキャナーに強制することもできます。 一覧からスキャナーを選択し、**[Rescan all files]\(すべてのファイルを再スキャン\)** オプションを選択します。

![Azure Information Protection スキャナーの再スキャンを開始する](./media/scanner-rescan-files.png)

すべてのファイルの再検査はレポートにすべてのファイルを含める必要がある場合に役立ち、この構成は通常、検索モードでスキャナーが実行されるときに使用されます。 フル スキャンが完了すると、後続のスキャンで新しいファイルまたは変更されたファイルのみがスキャンされるように、スキャンの種類が自動的に [増分] に変更されます。

さらに、新しいまたは変更された条件を含む Azure Information Protection ポリシーをスキャナーがダウンロードした場合も、すべてのファイルが検査されます。 スキャナーは、1 時間ごと、およびサービスの開始時にそのポリシーが 1 時間前よりも古い場合にポリシーを更新します。  

> [!TIP]
> テスト期間など、この 1 時間の間隔よりも早くポリシーを更新する必要がある場合は、**%LocalAppData%\Microsoft\MSIP\Policy.msip** と **%LocalAppData%\Microsoft\MSIP\Scanner** の両方からポリシー ファイル **Policy.msip** を手動で削除します。 その後、Azure Information Scanner サービスを再起動します。
>
> ポリシーの保護設定を変更した場合、保護設定を保存してから 15 分待機した後に、サービスを再起動してください。

スキャナーで自動条件が構成されていないポリシーをダウンロードした場合、スキャナー フォルダーのポリシー ファイルのコピーは更新されません。 このシナリオでは、ラベルが自動条件に対して正しく構成された新たにダウンロードしたポリシー ファイルを使用できるようにするには、その前に **%LocalAppData%\Microsoft\MSIP\Policy.msip** と **%LocalAppData%\Microsoft\MSIP\Scanner** からポリシー ファイル **Policy.msip** を削除する必要があります。

## <a name="using-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーの使用

特定の条件用にラベルを構成する必要がない、次の 2 つの代替シナリオが Azure Information Protection スキャナーでサポートされています。

- データ リポジトリ内のすべてのファイルに既定のラベルを適用する。

    この構成では、**Set-AIPScannerRepository** コマンドレットを使用し、*MatchPolicy*パラメーターを **Off** に設定します。

    ファイルの内容は検査されず、データ リポジトリ内のすべてのファイルが、データ リポジトリ用に指定した既定のラベル (*SetDefaultLabel* パラメーター) に従ってラベル付けされます。これが指定されていない場合は、スキャナー アカウントのポリシー設定として指定された既定のラベルが適用されます。

- すべてのカスタム条件と、既知の機密情報の種類を特定する。

    この構成では、**Set-AIPScannerConfiguration** コマンドレットを使用し、 *DiscoverInformationTypes* パラメーターを **All** に設定します。

    スキャナーでは、Azure Information Protection ポリシー内のラベルに対して指定したカスタム条件と、Azure Information Protection ポリシー内のラベルに指定できる情報の種類のリストが使用されます。

    次のクイックスタートでは、この構成を使用しています。ただし、現在のバージョンのスキャナーの場合は、「 [クイックスタート: 使用している機密情報を検索](quickstart-findsensitiveinfo.md)する」を参照してください。

## <a name="optimizing-the-performance-of-the-scanner"></a>スキャナーのパフォーマンスの最適化

スキャナーのパフォーマンスを最適化するには、次のガイダンスを使用します。 ただし、スキャナーのパフォーマンスではなく、スキャナーコンピューターの応答性が優先される場合は、 [高度なクライアント設定](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner) を使用して、スキャナーが使用するスレッドの数を制限することができます。

スキャナーのパフォーマンスを最大化するには

- **スキャナー コンピューターとスキャンされたデータ ストア間のネットワーク接続を高速かつ信頼性の高い接続にする**

    たとえば、同じ LAN 内か、スキャンされたデータ ストアと同じネットワーク セグメント内 (推奨) にスキャナー コンピューターを配置します。

    ネットワーク接続の品質は、スキャナーがスキャナー サービスを実行しているコンピューターにファイルのコンテンツを転送してファイルを検査するため、スキャナーのパフォーマンスに影響します。 このデータを移動する必要があるネットワークのホップ数を減らす (削除する) と、ネットワークの負荷も軽減されます。

- **スキャナー コンピューターに利用可能なプロセッサ リソースがあることを確認する**

    ファイル コンテンツが構成した条件に一致するかの検査、およびファイルの暗号化と複合化は、プロセッサ負荷の高いアクションです。 プロセッサ リソースの不足がスキャナー パフォーマンスを低下させるかどうかを識別するには、指定したデータ ストアの標準のスキャン サイクルを監視します。


スキャナーのパフォーマンスに影響するその他の要因

- スキャンするファイルを含むデータ ストアの現在の負荷と応答時間

- スキャナーが検索モードまたは強制モードのどちらで実行されているか

    通常、検索モードでは、強制モードよりもスキャン速度が速くなります。これは、発見には単一ファイルの読み取りアクションが必要なのに対して、強制モードでは読み取り/書き込みアクションが必要なためです。

- Azure Information Protection の条件を変更する

    スキャナーがすべてのファイルを検査する必要があるときの最初のスキャン サイクルでは、既定では、新規および変更されたファイルのみを検査する後続のスキャン サイクルよりも明らかに長く時間がかかります。 ただし、Azure Information Protection ポリシーの条件を変更した場合、[上記のセクション](#when-files-are-rescanned)に示されているように、すべてのファイルがもう一度スキャンされます。

- カスタム条件に対する正規表現式の構築

    メモリの大量消費とタイムアウト (1 ファイルあたり 15 分) のリスクを回避するには、ご利用の正規表現式を確認して効率的なパターン マッチングが行われているかを確認してください。 次に例を示します。

    - [最長の量指定子](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)を開始します

    - `(expression)` ではなく、`(?:expression)` などの非キャプチャ グループを使用します

- 選択したログ レベル

    スキャナー レポートに対して **[デバッグ]**、**[情報]**、**[エラー]**、**[オフ]** から選択できます。 **[オフ]** を選択すると、最適なパフォーマンスになります。**[デバッグ]** は大幅にスキャナーのスピードを低下させるので、トラブルシューティング時にのみ使用してください。 詳細については、を実行して、Set Aipscanの構成コマンドレットの *Reportlevel* パラメーターを参照してください `Get-Help Set-AIPScannerConfiguration -detailed` 。

- ファイル自体

    - Excel ファイルを除き、Office ファイルは PDF ファイルよりもすばやくスキャンされます。

    - 保護されていないファイルは、保護されたファイルよりもすばやくスキャンされます。

    - 大きいファイルは明らかに小さいファイルよりも時間がかかります。

- 補足:

    - スキャナーを実行するサービスアカウントに、「 [スキャナーの前提条件](#prerequisites-for-the-azure-information-protection-scanner) 」セクションに記載されている権限のみがあることを確認し、 [詳細なクライアント設定](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) を構成して、スキャナーの低整合性レベルを無効にします。

    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのファイルに既定のラベルを適用すると、ファイル内容の検査がスキップされるため、スキャナーの実行速度が速くなります。

    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのカスタム条件と既知の機密情報の種類を特定すると、スキャナーの実行速度が遅くなりなります。

    - [高度なクライアント設定](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner)でスキャナーのタイムアウトを小さくすると、スキャン速度が向上し、メモリ消費が減少しますが、一部のファイルがスキップされる可能性があります。

## <a name="list-of-cmdlets-for-the-scanner"></a>スキャナーのコマンドレットの一覧

スキャナーの他のコマンドレットを使用して、サービス アカウントとスキャナーのデータベースを変更したり、スキャナーの現在の設定を取得したり、スキャナー サービスをアンインストールしたりすることができます。 スキャナーは、次のコマンドレットを使用します。

- Add-AIPScannerScannedFileTypes

- Add-AIPScannerRepository

- Get-AIPScannerConfiguration

- Get-AIPScannerRepository

- Get-AIPScannerStatus

- Install-AIPScanner

- Remove-AIPScannerRepository

- Remove-AIPScannerScannedFileTypes

- Set-AIPScanner

- Set-AIPScannerConfiguration

- Set-AIPScannerScannedFileTypes

- Set-AIPScannerRepository

- Start-AIPScan

- Uninstall-AIPScanner

- Update-AIPScanner

> [!NOTE]
> 現在のバージョンのスキャナーでは、これらのコマンドレットの多くが非推奨となりました。スキャナーのコマンドレットのオンラインヘルプには、この変更が反映されています。 スキャナーのバージョン1.48.204.0 より前のコマンドレットヘルプについては、PowerShell セッションで組み込みコマンドを使用して `Get-Help <cmdlet name>` ください。

## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>スキャナーのイベント ログ ID と説明

次のセクションを使用して、スキャナーの可能性のあるイベント ID と説明を特定できます。 これらのイベントは、Windows の**アプリケーションとサービス**のイベント ログ、**Azure Information Protection** でスキャナー サービスを実行しているサーバーにログオンします。

-----

情報 **910**

**スキャナーのサイクルが開始しました。**

スキャナー サービスが開始され、指定したデータ リポジトリ内のファイルのスキャンが開始されたときに、このイベントがログに記録されます。

----

情報 **911**

**スキャナーのサイクルが完了しました。**

スキャナーで手動スキャンまたは継続的スケジュールのサイクルが完了すると、このイベントがログに記録されます。

継続的ではなく手動で実行するようにスキャナーが構成されていた場合、新しいスキャンを実行するには、**Start-AIPScan** コマンドレットを使用します。 スケジュールを変更するには、**Set-AIPScannerConfiguration** コマンドレットと *[スケジュール]* パラメーターを使用します。

----

## <a name="next-steps"></a>次のステップ

Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

[Windows Server FCI と Azure Information Protection スキャナーの違いは何ですか](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)。

また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 これに関する詳細および PowerShell を使用するその他のシナリオについては、「[Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md)」をご覧ください。
