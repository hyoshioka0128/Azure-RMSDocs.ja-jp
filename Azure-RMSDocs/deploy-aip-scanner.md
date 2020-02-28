---
title: Azure Information Protection スキャナーを展開する-AIP
description: 現在のバージョンの Azure Information Protection スキャナーをインストール、構成、および実行して、データストア上のファイルを検出、分類、および保護する方法について説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 02/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cc2c9a134c222ad9ec8463e94dc5b355ade20d91
ms.sourcegitcommit: 275d31ef762c702b6c63025cbba0a45ca9528ce5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "77778655"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*


> [!NOTE]
> この記事は、Azure Information Protection クライアント (クラシック) を使用した Azure Information Protection スキャナーの現在の一般公開バージョンと、Azure の現在の一般公開バージョンのスキャナーのプレビュー版を対象としています。Information Protection 統合されたラベル付けクライアント。
> 
> 以前にスキャナーをインストールし、アップグレードする場合は、次のアップグレード手順を実行し、このページの手順を使用して、スキャナーをインストールする手順を省略します。
> - クラシッククライアントの場合: [Azure Information Protection スキャナーのアップグレード](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> - 統一されたラベル付けクライアントの場合: [Azure Information Protection スキャナーのアップグレード](./rms-client/clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> 
> 1\.48.204.0 よりも前のバージョンのスキャナーを使用していて、アップグレードする準備ができていない場合は、「[ファイルを自動的に分類して保護するために以前のバージョンの Azure Information Protection スキャナーを展開する](deploy-aip-scanner-previousversions.md)」を参照してください。


この情報を使用して、Azure Information Protection スキャナーについて説明し、正常にインストール、構成、および実行する方法について説明します。

このスキャナーは、Windows Server でサービスとして実行され、次のデータ ストア上のファイルを検出、分類、および保護することができます。

- スキャナーを実行する Windows Server コンピューター上のローカル フォルダー。

- サーバー メッセージ ブロック (SMB) プロトコルを使用するネットワーク共有の UNC パス。

- Sharepoint server 2019 のドキュメントライブラリとフォルダーは、SharePoint Server 2013 を介して使用できます。 [このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様向けに SharePoint 2010 もサポートされています。

クラウド リポジトリ上のファイルをスキャンおよびラベル付けするには、スキャナーの代わりに [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) を使用します。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの概要

自動分類を適用するラベルを構成すると、このスキャナーが検出するファイルにラベルを付けることができます。 ラベルは分類を適用し、必要に応じて、保護を適用または保護を解除します。

![Azure Information Protection スキャナーのアーキテクチャの概要](./media/infoprotect-scanner.png)

スキャナーは、コンピューターにインストールされている IFilters を使うことで、Windows によってインデックス化できるすべてのファイルを検証できます。 そして、ファイルでラベル付けが必要かどうかを判断するため、スキャナーで Office 365 に組み込まれたデータ損失防止 (DLP) の機密情報の種類とパターン検出、または Office 365 の正規表現パターンが使われます。 スキャナーは Azure Information Protection クライアント (従来のクライアントまたは統一されたラベル付けクライアント) を使用するため、スキャナーは同じファイルの種類を分類して保護することができます。

- クラシッククライアント: [Azure Information Protection クライアントによってサポートされるファイルの種類](./rms-client/client-admin-guide-file-types.md)

- 統一されたラベル付けクライアント: [Azure Information Protection 統合されたラベル付けクライアントでサポートされるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md)

スキャナーを実行できるのは検索モードでのみです。この場合、レポートを使用して、ファイルがラベル付けされた場合に何が発生するかをチェックします。 またはスキャナーを実行して、自動的にラベルを適用できます。 機密情報の種類を含んだファイルを検出するためにスキャナーを実行することもできます (自動分類を適用する条件用にラベルを構成する必要はありません)。

スキャナーは検出せず、リアルタイムでラベル付けしないことに注意してください。 スキャナーは指定したデータ ストア上のファイルを体系的にクロールします。この実行サイクルは、1 回限りまたは繰り返しに設定することができます。

スキャナーの構成の一部としてファイルの種類の一覧を定義することで、スキャンするファイルの種類、またはスキャンから除外するファイルの種類を指定できます。


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの前提条件
Azure Information Protection スキャナーをインストールする前に、次の要件を満たしていることを確認してください。

|要件|説明|
|---------------|--------------------|
|スキャナー サービスを実行する Windows Server コンピューター:<br /><br />- 4 コア プロセッサ<br /><br />- 8 GB の RAM<br /><br />- 一時ファイルのための空き容量 10 GB (平均)|Windows Server 2019、Windows Server 2016、または Windows Server 2012 R2。 <br /><br />注: 非運用環境でテストまたは評価を行う場合、[Azure Information Protection クライアントでサポートされている](requirements.md#client-devices) Windows クライアント オペレーティング システムを使用できます。<br /><br />このコンピューターは、スキャンするデータ ストアへの高速で信頼性の高いネットワーク接続がある物理コンピューターまたは仮想コンピューターにすることができます。<br /><br /> スキャナーは、スキャンする各ファイル用に、コアごとに 4 つの一時ファイルを作成するために、十分なディスク領域を必要とします。 推奨される 10 GB のディスク領域を使用すると、4 コア プロセッサで、それぞれのサイズが 625 MB であるファイルを 16 個スキャンできます。 <br /><br /> 組織のポリシーのためにインターネット接続ができない場合は、「[代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」セクションを参照してください。 それ以外の場合は、このコンピューターがインターネットに接続されていることを確認し、HTTPS 経由で次の Url を使用できるようにします (ポート 443)。<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com <br /> \*。 protection.outlook.com (統合ラベル付けクライアントのスキャナーのみ)|
|スキャナー サービスを実行するサービス アカウント|Windows Server コンピューター上でのスキャナー サービスの実行に加えて、この Windows アカウントは Azure AD で認証され、Azure Information Protection ポリシーをダウンロードします。 このアカウントは Active Directory アカウントであり、かつ Azure AD と同期している必要があります。 組織のポリシーによってこのアカウントを同期できない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />このサービス アカウントには次の要件があります。<br /><br />-  **[Log on locally]\(ローカル ログオン\)** ユーザー権限の割り当て。 この権限は、スキャナーのインストールと構成に必要ですが、操作には必要ありません。 この権限をサービス アカウントに付与する必要がありますが、スキャナーがファイルを検出、分類、保護できることを確認したら、この権限を削除することができます。 組織のポリシーによって、短時間でもこの権限を付与することができない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />-  **[サービスとしてログオン]** ユーザー権限の割り当て。 この権限は、スキャナーのインストール中にサービス アカウントに自動的に付与され、スキャナーのインストール、構成、操作に必要です。 <br /><br />- データ リポジトリへのアクセス許可: <br /><br /> ファイル共有またはローカルファイル: ファイルをスキャンして、Azure Information Protection ポリシーの条件を満たすファイルに分類と保護を適用するには、**読み取り**と**書き込み**、および**変更**のアクセス許可を付与する必要があります。 <br /><br /> SharePoint: ファイルをスキャンして、Azure Information Protection ポリシーの条件を満たすファイルに分類と保護を適用するには、**フルコントロール**アクセス許可を付与する必要があります。 <br /><br /> スキャナーを検索モードでのみ実行するには、**読み取り**アクセス許可で十分です。<br /><br />-保護を再保護または削除するラベルの場合: スキャナーが常に保護されたファイルにアクセスできるようにするには、このアカウントを Azure Information Protection の[スーパーユーザー](configure-super-users.md)にして、スーパーユーザー機能が有効になっていることを確認します。 さらに、段階的な展開の[オンボーディング制御](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を実装している場合は、このアカウントが構成したオンボーディング制御に含まれていることを確認してください。|
|スキャナーの構成を格納する SQL Server:<br /><br />- ローカルまたはリモート インスタンス<br /><br />- [大文字と小文字を区別しない照合順序](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15) <br /><br />- スキャナーをインストールする sysadmin ロール|次のエディションでは、SQL Server 2012 が最小バージョンとなります。<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Azure Information Protection スキャナーでは、スキャナーのカスタム プロファイル名を指定するときに同じ SQL Server インスタンス上の複数の構成データベースがサポートされます。 統一されたラベル付けクライアントのプレビューバージョンのスキャナーを使用すると、複数のスキャナーで同じ構成データベースを共有できます。<br /><br />Sysadmin ロールを持つアカウントでスキャナーをインストールすると、インストールのプロセスでスキャナーの構成データベースが自動的に作成され、スキャナーを実行するサービス アカウントに対して必要な db_owner ロールが付与されます。 Sysadmin ロールが付与されない場合や、組織のポリシーがデータベースを手動で作成し構成することを要求している場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」をご覧ください。<br /><br /> 容量のガイダンスについては、「 [SQL Server のストレージ要件と容量計画](#storage-requirements-and-capacity-planning-for-sql-server)」を参照してください。|
|次のいずれかの Azure Information Protection クライアントが Windows Server コンピューターにインストールされている <br /><br /> -クラシッククライアント <br /><br /> -統一されたラベル付けクライアント ([現在の一般公開バージョンのみ](./rms-client/unifiedlabelingclient-version-release-history.md#version-25330)) |スキャナーに対する完全なクライアントをインストールする必要があります。 PowerShell モジュールだけで、クライアントをインストールしないでください。<br /><br />インストールおよびアップグレードの手順については、次のとおりです。 <br /> [クラシッククライアント](./rms-client/client-admin-guide.md)を - する<br /> - 統合された[ラベル付けクライアント](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner) |
|自動分類と、必要に応じて保護を適用する構成済みのラベル|クラシッククライアントで条件のラベルを構成し、保護を適用する手順については、次を参照してください。<br /> - [自動および推奨分類の条件を構成する方法](configure-policy-classification.md)<br /> - [Rights Management による保護でラベルを構成する方法](configure-policy-protection.md) <br /><br />ヒント:[チュートリアル](infoprotect-quick-start-tutorial.md)の指示に従って、準備された Word 文書でクレジットカード番号を検索するラベルを使用してスキャナーをテストできます。 ただし、オプション **[このラベルの適用方法を選択]** が **[推奨]** ではなく **[自動]** に設定されるように、ラベルの構成を変更する必要があります。 その後、(適用される場合は) ドキュメントからラベルを削除して、スキャナー用のデータ リポジトリにファイルをコピーします。 簡単なテストの場合、これにはスキャナー コンピューター上のローカル フォルダーを使用できます。<br /><br /> ラベルを自動ラベル付けするようにラベルを構成し、保護を適用するための統一されたラベル付けクライアントの手順については、以下を参照してください。<br /> [コンテンツに機密ラベルを自動的に適用](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)- には<br /> [秘密度ラベルの暗号化を使用してコンテンツへのアクセスを制限 - には](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)<br /><br /> 自動分類を適用するラベルを構成していない場合でもスキャナーを実行できますが、このシナリオについては、これらの手順では説明されていません。 [詳細情報](#using-the-scanner-with-alternative-configurations)|
|スキャンする SharePoint ドキュメントライブラリおよびフォルダーの場合:<br /><br />-SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|スキャナーでは SharePoint の他のバージョンはサポートされていません。<br /><br />[バージョン管理](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning)を使用すると、スキャナーは最後に発行されたバージョンを検査してラベルを付けます。 スキャナーがファイルと[コンテンツの承認](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval)を必要とする場合は、そのラベルの付いたファイルをユーザーが使用できるように承認する必要があります。 <br /><br />大規模な SharePoint ファームの場合は、スキャナーがすべてのファイルにアクセスするために、リスト ビューのしきい値 (既定では 5,000) を増やす必要があるかどうかを確認します。 詳細については、SharePoint のドキュメント「 [sharepoint での大規模なリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。|
|スキャンされる Office ドキュメントの場合:<br /><br />- Word、Excel、PowerPoint の 97-2003 ファイル形式および Office Open XML 形式|これらのファイル形式でスキャナーがサポートするファイルの種類の詳細については、次の情報を参照してください。 <br />-Classic クライアント: [Azure Information Protection クライアントによってサポートされるファイルの種類](./rms-client/client-admin-guide-file-types.md)<br />-統一されたラベル付けクライアント: [Azure Information Protection 統合されたラベル付けクライアントでサポートされるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md)|
|長いパスの場合:<br /><br />- 最大 260 文字 (スキャナーが Windows 2016 にインストールされていて、コンピューターが長いパスをサポートするように構成されているのでない場合)|Windows 10 および Windows Server 2016 では、次の[グループポリシー設定](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)を使用して、260文字を超えるパスの長さをサポートしています:**ローカルコンピューターポリシー** > **コンピューターの構成** > **管理用テンプレート** > **すべての設定** > **Win32 の長いパスを有効にする**<br /><br /> 長いファイルのパスのサポートについて詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。|
|使用状況の統計|[Allowtelemetry](https://docs.microsoft.com/azure/information-protection/rms-client/client-admin-guide-install#to-install-the-azure-information-protection-client-by-using-the-executable-installer)パラメーターを0に設定して、microsoft に使用状況の統計情報を送信するオプションを無効にしてください。または、スキャナーのインストールプロセス中に、[**使用状況の統計情報を microsoft に送信して Azure Information Protection を改善**する] オプションが選択されていないことを確認してください。| 

組織のポリシーによって禁止されているためにテーブル内のすべての要件を満たすことができない場合は、「[代替構成](#deploying-the-scanner-with-alternative-configurations)」セクションを参照してください。

スキャナーを運用環境に展開する場合、または複数のスキャナーのパフォーマンスをテストする場合は、次のセクションの SQL Server の容量計画のガイダンスを参照してください。

ただし、スキャナーのデプロイを開始する準備ができたら、 [「スキャナーの構成」セクション](#configure-the-scanner-in-the-azure-portal)に進んでください。

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>SQL Server のストレージ要件と容量計画

スキャナーの構成データベースに必要なディスク領域と、SQL Server を実行しているコンピューターの仕様は環境によって異なる場合があるため、独自のテストを行うことをお勧めします。 ただし、次のガイダンスを出発点として使用できます。

詳細については、「[スキャナーのパフォーマンスの最適化](#optimizing-the-performance-of-the-scanner)」を参照してください。

##### <a name="scanner-from-the-classic-client"></a>クラシッククライアントからのスキャナー:

- **ディスクサイズ**: 構成データベースのサイズは、展開ごとに異なりますが、スキャンする100万ファイルごとに 500 MB を割り当てることをお勧めします。

- **各スキャナーの場合**: 4 コアプロセッサ。8 GB の RAM が推奨されます (最小 4 GB)。

##### <a name="scanner-from-the-unified-labeling-client"></a>統一されたラベル付けクライアントからのスキャナー:

- **ディスクサイズ**: スキャナー構成データベースのサイズは、展開ごとに異なりますが、`100 KB + <file count> *(1000 + 4*<average file name length>)`については、次の式を参考にしてください。 
    
    たとえば、ファイル名の長さが平均250バイトの100万ファイルをスキャンするには、2 GB のディスク領域を割り当てます。

- **複数のスキャナーの場合、最大 10**: 4 コアプロセッサ8 GB の RAM を推奨します。

- **10 を超える複数のスキャナーの場合 (最大 40)** : 8 コアプロセス。16 GB の RAM を推奨します。

### <a name="deploying-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーのデプロイ

テーブルに一覧表示されている前提条件は、スキャナーの既定の要件であり、推奨されます。何故なら、これらはスキャナーをデプロイするための最も簡単な構成であるためです。 これらは、スキャナーの機能を確認するための最初のテスト用に適しています。 ただし、運用環境では、次の制限の 1 つ以上に該当するために組織のポリシーによって既定の要件が禁止される場合があります。

- サーバーはインターネット接続を許可されていません

- Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

- サービス アカウントに**ローカル ログオン**権限を付与できない

- サービスアカウントを Azure Active Directory に同期することはできませんが、サーバーがインターネットに接続しています

スキャナーをこれらの制限に対応させることは可能ですが、追加構成が必要です。


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>制限: スキャナーサーバーはインターネットに接続できません

切断されたコンピューターをサポートするには、管理者ガイドの指示に従います。

- クラシッククライアントの場合: 切断された[コンピューターのサポート](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)
    
    この構成では、クラシッククライアントのスキャナーは、組織のクラウドベースのキーを使用して保護を適用したり、保護を削除したり、保護されたファイルを検査したりすることはできません。 代わりに、分類のみを適用するラベルを使用するか、 [HYOK](configure-adrms-restrictions.md)を使用する保護を適用するようにスキャナーを制限します。

- 統一されたラベル付けクライアントの場合: 統合ラベル付けクライアントは、オンライン接続を使用せずに保護を適用できません。 
    
    統一されたラベル付けクライアントのスキャナーは、 [import-Aipscanの configuration](https://docs.microsoft.com/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration?view=azureipps)コマンドレットを使用してインポートされたポリシーに基づいてラベルを適用できます。

次に、次の操作を行います。

1. スキャナーのプロファイルを作成して、Azure portal でスキャナーを構成します。 この手順に関してサポートが必要な場合は、「[Azure portal でスキャナーを構成する](#configure-the-scanner-in-the-azure-portal)」をご覧ください。

2. **[Azure Information Protection-プロファイル]** ウィンドウから **[エクスポート]** オプションを使用して、スキャナープロファイルをエクスポートします。

3. 最後に、PowerShell セッションで、[Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) を実行し、エクスポートされた設定を含んでいるファイルを指定します。

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

スキャナーをインストールするために一時的に Sysadmin ロールが付与される場合、スキャナーのインストールが完了したらこのロールを削除できます。 この構成を使用すると、データベースが自動的に作成され、スキャナー用のサービス アカウントに必要なアクセス許可が自動的に付与されます。 ただし、スキャナーを構成するユーザー アカウントには、スキャナー構成データベースの db_owner ロールが必要です。このロールをユーザー アカウントに手動で付与する必要があります。

Sysadmin ロールが一時的に付与されていない場合は、スキャナーをインストールする前に、データベースを手動で作成するための Sysadmin 権限をユーザーに要求する必要があります。 この構成では、次のロールを割り当てる必要があります。
    
|アカウント|データベースレベルのロール|
|--------------------------------|---------------------|
|スキャナーのサービス アカウント|db_owner|
|スキャナーのインストール用のユーザー アカウント|db_owner|
|スキャナーの構成用のユーザー アカウント |db_owner|

通常、スキャナーのインストールと構成には同じユーザー アカウントを使用します。 ただし、別々のアカウントを使用する場合は、両方にスキャナー構成データベースの db_owner ロールが必要です。

- クラシック クライアントの場合:

    スキャナーに独自のプロファイル名を指定しない場合、構成データベースの名前は computer_name > (クラシッククライアントのみ) **AIPScanner_\<** になります。 次の手順に進み、ユーザーを作成し、データベースに対する db_owner 権限を付与します。 

- 統合ラベル付けクライアントの場合:
    
    独自のプロファイル名を指定した場合、構成データベースには**AIPScannerUL_ < profile_name >** (統合ラベル付けクライアント) という名前が付けられます。
    
    次のスクリプトを使用してデータベースを設定します。 

    存在しない場合 (select * from master. sys. server_principals where sid = SUSER_SID ("domain\user")) BEGIN declare @T nvarchar (500) Set @T = ' CREATE LOGIN ' + quotename (' domain\user ') + ' FROM WINDOWS ' exec (@T) END 

このデータベースに対してユーザーを作成し db_owner 権限を付与するには、Sysadmin に次の操作を依頼します。

1. スキャナー用の DB を作成します。 <br>
    **CREATE database AIPScannerUL_ [profilename]** **ALTER Database AIPScannerUL_ [PROFILENAME] の信頼を設定**
    - この手順は省略可能ですが、必要に応じてより簡単にトラブルシューティングを行うことができます。

2. インストールコマンドを実行するユーザーに権限を付与します。これは、スキャナー管理コマンドの実行に使用されます。

SQL スクリプト:

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END

3. スキャナーサービスアカウントに権限を付与する:

SQL スクリプト:

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    
補足:

- スキャナーを実行するサーバーのローカル管理者である必要があります。
- スキャナーを実行するサービスアカウントには、次のレジストリキーに対するフルコントロールのアクセス許可が付与されている必要があります。
    
    - HKEY_LOCAL_MACHINE \SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\MSIPC\Server

これらのアクセス許可を構成した後、スキャナーをインストールするときにエラーが表示される場合は、エラーを無視して、スキャナーサービスを手動で開始することができます。


#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>制限: スキャナーのサービス アカウントに**ローカル ログオン**権限を付与できない

組織のポリシーによって、サービスアカウントに**ローカルでログオン**する権限が禁止されていても、**バッチジョブとしてログオン**する権限が許可されている場合は、次の手順に従います。

- クラシッククライアントの場合: クライアントの管理者ガイドの「 [Set-AIPAuthentication」の「Token パラメーターを指定して使用する](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」を参照してください。

- 統一されたラベル付けクライアントの場合: クライアントの管理者ガイドの「 [Azure Information Protection のために非対話形式でファイルにラベルを付ける方法](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」で説明されているように、Set-AIPAuthentication で*OnBehalfOf*パラメーターを使用します。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>制限: スキャナーサービスアカウントを Azure Active Directory に同期することはできませんが、サーバーがインターネットに接続しています

スキャナーのサービスを実行するために 1 つのアカウントを持ち、Azure Active Directory を認証するために別のアカウントを使用することができます。

- スキャナーのサービス アカウントのためには、ローカルの Windows アカウントか Active Directory アカウントを使用できます。

- Azure Active Directory アカウントについては、次の手順を使用します。
    - クラシッククライアントの場合: クライアントの管理者ガイドの「 [Set-AIPAuthentication」の「Token パラメーターを指定して使用する](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」を参照してください。
    - 統一されたラベル付けクライアントの場合: クライアントの管理者ガイドの「 [Azure Information Protection のために非対話形式でファイルにラベルを付ける方法](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」で説明されているように、Set-AIPAuthentication で*OnBehalfOf*パラメーターのローカルアカウントを指定します。


## <a name="configure-the-scanner-in-the-azure-portal"></a>Azure portal でスキャナーを構成する

スキャナーをインストールする前、または以前の一般公開バージョンのスキャナーからアップグレードする前に、Azure portal でスキャナー用のプロファイルを作成します。 スキャナーの設定に関するプロファイルと、スキャンするデータ リポジトリを構成します。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、 **[Azure Information Protection]** を選択します。
    
2. **[スキャナー]** メニュー オプションを見つけて、 **[プロファイル]** を選択します。

3. **[Azure Information Protection] - [プロファイル]** ペインで、 **[追加]** を選択します。
    
    ![Azure Information Protection スキャナーのプロファイルを追加する](./media/scanner-add-profile.png)

4. **[新しいプロファイルを追加する]** ペインで、その構成設定とスキャンするデータ リポジトリを識別するために使うスキャナーの名前を指定します。 たとえば、スキャナーの対象となるデータ リポジトリの地理的な場所を識別するために、**Europe** を指定する場合があります。 後でスキャナーをインストールまたはアップグレードするときに、同じプロファイル名を指定する必要があります。
    
    スキャナーのプロファイル名を識別するために、必要に応じて管理目的の説明を指定します。

5. この初期構成では、次の設定を構成してから、 **[保存]** を選択しますが、ウィンドウは閉じないでください。
    
    **[プロファイルの設定]** セクションの場合:
    - **スケジュール**:**既定のままにし**ておきます。
    - **検出される情報の種類**:**ポリシーのみ**に変更
    - **リポジトリを構成**する: プロファイルを最初に保存する必要があるため、現時点では構成しないでください。
    
    **[ポリシーの適用]** セクションの場合:
    - **強制**: **[オフ]** を選択します。
    - **コンテンツに基づいてファイルにラベルを付ける**: の既定値のまま**に**します。
    - **既定のラベル**: 既定の**ポリシー**の既定値のままにします。
    - **ファイルのラベル**を変更する: 既定値を**オフ**のままにします。
    
    **[ファイル設定の構成]** セクションでは、次の手順を実行します。
    - [**更新日]、[最終更新日]、[変更者] を保持し**ます。の既定値のまま**に**します。
    - **スキャンするファイルの種類**: **除外**するファイルの種類を既定のままにする。
    - **既定の所有者**: 既定の**スキャナーアカウント**を保持します

6. これでプロファイルの作成と保存が完了したので、 **[リポジトリの構成]** オプションに戻って、スキャンするデータ ストアを指定する準備が整いました。 SharePoint オンプレミスのドキュメントライブラリおよびフォルダーに対して、ローカルフォルダー、UNC パス、および SharePoint サーバーの Url を指定できます。 
    
    Sharepoint では、sharepoint server 2019、SharePoint Server 2016、および SharePoint Server 2013 がサポートされています。 また、SharePoint Server 2010 も、[このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)を受けている場合はサポートされます。
    
    最初のデータストアを追加するには、 **[新しいプロファイルの追加]** ウィンドウの **[リポジトリの構成]** を選択し、 **[リポジトリ]** ペインを開きます。
    
    ![Azure Information Protection スキャナーのデータ リポジトリを構成する](./media/scanner-repositories-bar.png)

7. **[リポジトリ]** ペインで、 **[追加]** を選択します。
    
    ![Azure Information Protection スキャナーのデータ リポジトリを追加する](./media/scanner-repository-add.png)

8. **[リポジトリ]** ウィンドウで、データリポジトリのパスを指定します。 
    
    ワイルドカードはサポートされていません。また、WebDav の場所はサポートされていません。
    
    次に例を示します。
    
    - ローカル パスの場合: `C:\Folder`
    
    - ネットワーク共有の場合: `C:\Folder\Filename`
    
    - UNC パスの場合: `\\Server\Folder`
    
    - SharePoint ライブラリの場合: `http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > "共有ドキュメント" の SharePoint パスを追加する場合:
    >
     >- 共有ドキュメントのすべてのドキュメントとすべてのフォルダーをスキャンしたい場合は、パスに **Shared Documents** を指定します。 例: `http://sp2013/Shared Documents`
     >
     >- 共有ドキュメント下のサブフォルダーのすべてのドキュメントとすべてのフォルダーをスキャンしたい場合は、パスに **Documents** を指定します。 例: `http://sp2013/Documents/Sales Reports`
    
    このウィンドウのその他の設定については、この初期構成では変更せず、**プロファイルの既定値**のままにしておきます。 これは、データ リポジトリがスキャナーのプロファイルから設定を継承することを意味します。 
    
    **[保存]** を選択します。

9. 別のデータ リポジトリを追加する場合は、手順 7 と 8 を繰り返します。

10. これで、 **[リポジトリ]** ウィンドウとプロファイルウィンドウを閉じることができます。 **[Azure Information Protection-プロファイル]** ウィンドウに戻り、 **[スケジュール]** 列に **[手動]** が表示され、 **[適用]** 列が空白になっていることを確認します。

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

Azure AD トークンを使用すると、スキャナーは Azure Information Protection サービスに対して認証を行うことができます。

1. Azure portal に戻り、認証用のアクセストークンを指定するために必要な2つの Azure AD アプリケーション (1 つの Azure AD アプリケーション) を作成します。 このトークンを使用すると、スキャナーを非対話形式で実行できます。
    
    これらのアプリケーションを作成するには、関連するクライアントの管理者ガイドの指示に従います。
    
    - Classic クライアントの場合: [Azure Information Protection のために非対話形式でファイルにラベルを付ける方法](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)
    
    - 統一されたラベル付けクライアントの場合: [Azure Information Protection のために非対話形式でファイルにラベルを付ける方法](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

2. スキャナーのサービス アカウントにインストール用に**ローカルでログオン**する権限が付与されている場合、Windows Server コンピューターから、このアカウントを使用してサインインし、PowerShell セッションを開始します。 前の手順でコピーした値を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行します。
    
    **クラシッククライアントの場合:**
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    求められたら、Azure AD のサービス アカウントの資格情報のパスワードを指定し、 **[同意する]** をクリックします。

        
    スキャナーサービスアカウントにインストールの**ローカルログオン**権限が付与されていない場合は、そのクライアントの管理者ガイドの「 [Set-Aipauthentication」の Token パラメーターを指定](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)して使用します。


    **従来のクライアントの例:**

    ```
    Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip
    Acquired application access token on behalf of the user
    ```
       
    **統一されたラベル付けクライアントの場合:**
    
    ```
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
    
    スキャナーサービスアカウントにインストール用の**ローカルログオン**権限が付与されていない場合は、「クライアントの管理者ガイドの「 [Azure Information Protection のために非対話形式でファイルにラベルを付ける方法](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」の説明に従って、 *OnBehalfOf*パラメーターを Set-aipauthentication と共に使用します。

    **統一されたラベル付けクライアントの例:**

    ```
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
    Acquired application access token on behalf of CONTOSO\scanner.
    ```

スキャナーには Azure AD に対して認証するためのトークンが用意されています。これは、 **Web アプリ/API** (クラシッククライアント) の構成または Azure AD でのクライアントシークレット (統合ラベル付けクライアント) の構成に従って、1年間、2年間、または期限切れになります。 トークンが期限切れになったら、手順 1 と 2 を繰り返す必要があります。

これで、最初のスキャンを検索モードで実行する準備ができました。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>探索サイクルの実行とスキャナーのレポートの表示

1. Azure portal の **[Azure Information Protection プロファイル]** ウィンドウで、スキャナーのプロファイルを選択し、 **[今すぐスキャン]** オプションを選択します。
    
    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)
    
    または、PowerShell セッションで、次のコマンドを実行します。
    
        Start-AIPScan

2. スキャナーのサイクルが完了するまで待ちます。 スキャナーが指定したデータ ストア内のすべてのファイルをクロールし終わると、スキャナー サービスの動作が続いていてもスキャナーは停止します。
    
    - **Azure Information Protection プロファイル** ウィンドウで、最新の情報に**更新** オプションを使用して、**最後のスキャン結果** 列の値と **最後のスキャン (終了時刻)** 列の値が表示されるまで待ちます。
    
    - PowerShell を使用すると、`Get-AIPScannerStatus` を実行して状態の変化を監視できます。
    
    - クラシッククライアントからのスキャナーのみ: ローカルの Windows**アプリケーションとサービス**のイベントログ、 **Azure Information Protection**を確認します。 このログでは、スキャナーがスキャンを完了した時刻も、結果の概要と共に報告されます。 情報イベント ID **911** を探します。

3. %*localappdata*%\Microsoft\MSIP\Scanner\Reports に格納されているレポートを確認します。 .txt の概要ファイルには、スキャンにかかった時間、スキャンされたファイルの数、情報の種類と一致したファイルの数が含まれています。 .csv ファイルには各ファイルに関する詳細情報が記載されています。 このフォルダーには、スキャンのサイクルごとに最大 60 のレポートが格納され、必要なディスク領域を最小限に抑えるために最新のもの以外のすべてのレポートが圧縮されます。
    
    > [!NOTE]
    > *Set-AIPScannerConfiguration* と共に [ReportLevel](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) パラメーターを使って、ログ記録のレベルを変更することができます。ただし、レポート フォルダーの場所または名前を変更することはできません。 別のボリュームまたはパーティションにレポートを保存したい場合は、フォルダーに対するディレクトリのジャンクションの使用を検討してください。
    >
    > たとえば、[Mklink](/windows-server/administration/windows-commands/mklink) コマンドを使います。`mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    **[検出する情報の種類]** に対して **[ポリシーのみ]** を設定しているため、自動分類用に設定した条件を満たすファイルのみが詳細レポートに含まれます。 ラベルが適用されていない場合は、ラベルの構成に推奨される分類ではなく自動分類が含まれていることを確認します。
    
    > [!TIP]
    > スキャナーでは 5 分ごとにこの情報が Azure Information Protection に送信されます。このため、Azure portal から結果をほぼリアルタイムで確認することができます。 詳細については、[Azure Information Protection のレポート作成](reports-aip.md)に関するページを参照してください。 
        
    期待どおりの結果が得られない場合は、ラベルに指定した条件の再構成が必要になることがあります。 その場合は、構成を変更して分類、および必要に応じて保護を適用する準備ができるまで、手順 1 から 3 を繰り返します。 

Azure portal には、最後のスキャンに関する情報のみが表示されます。 前のスキャンの結果を確認する必要がある場合は、スキャナー コンピューターの %*localappdata*%\Microsoft\MSIP\Scanner\Reports フォルダーに格納されているレポートに戻ります。

スキャナーが検出したファイルに自動的にラベル付けする準備ができたら、次の手順に進みます。 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>スキャナーを構成して分類と保護を適用する

これらの手順に従っている場合、スキャナーは、レポートのみモードで 1 回だけ実行されます。 これらの設定を変更するには、スキャナーのプロファイルを編集します。

1. **[Azure Information Protection-プロファイル]** ウィンドウに戻り、スキャナープロファイルを選択して編集します。

2. [**プロファイル名**の \<>] ウィンドウで、次の2つの設定を変更し、 **[保存]** を選択します。
    
   - **[プロファイルの設定]** セクション: [**スケジュール**を**常**に変更する]
   - **[ポリシーの適用]** セクションから: **[適用]** 先 を **[オン**] に変更します。
    
     変更する可能性があるその他の構成があります。 たとえば、ファイル属性を変更するかどうか、またはスキャナーでファイルのラベルを書き換えられるかどうかなどです。 情報のポップアップ ヘルプを使って、各構成設定について詳しく学習してください。

3. 現在の時刻をメモし、 **[Azure Information Protection プロファイル]** ウィンドウからもう一度スキャナーを起動します。
    
    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)
    
    または、PowerShell セッションで次のコマンドを実行できます。
    
        Start-AIPScan

4. クラシッククライアントからのスキャナーのみ: 前の手順でスキャンを開始したときより後のタイムスタンプを使用して、イベントログの情報の種類**911**をもう一度監視します。
    
    次に、レポートをチェックして、ラベル付けされたファイル、各ファイルに適用された分類、それらに保護が適用されたかどうかについての詳細を確認します。 または、Azure portal を使用してより簡単にこの情報を確認します。

スケジュールを継続的に実行するように構成したため、スキャナーはすべてのファイルの作業を完了すると、新しいファイルや変更されたファイルをすべて検出するために新しいサイクルを自動的に開始します。

## <a name="stop-a-scan"></a>スキャンを停止する 

以前に開始したスキャンを完了する前に停止するには、インターフェイスから **[スキャンの停止]** オプションを使用します。
 
![Azure Information Protection スキャナーのスキャンを停止する](./media/scanner-stop-scan.png)
    
または、PowerShell セッションで次のコマンドを実行できます。
    
        Stop-AIPScan 

## <a name="how-files-are-scanned"></a>ファイルをスキャンする方法

スキャナーでは、ファイルをスキャンするとき、次のプロセスが実行されます。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. スキャンのためにファイルが含まれるか除外されるかを決定します。 
実行可能ファイルやシステムファイルなど、分類と保護から除外されたファイルは、スキャナーによって自動的にスキップされます。 詳細については、次の管理者ガイドを参照してください。

- クラシッククライアントの場合:[分類と保護から除外されるファイルの種類](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- 統一されたラベル付けクライアントの場合:[分類と保護から除外されるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

スキャンする (またはスキャン対象から除外する) ファイルの種類のリストを定義することで、この動作を変更できます。 スキャナーに対してこのリストを指定し、既定ですべてのデータ リポジトリに適用させることができます。また、データ リポジトリごとに 1 つのリストを指定することができます。 このリストを指定するには、スキャナーのプロファイルの **[スキャンするファイルの種類]** 設定を使います。

![Azure Information Protection スキャナー用にスキャンするファイルの種類を構成する](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2. ファイルを検査してラベルを付ける

その後、スキャナーでは、フィルターを使用して、サポートされているファイルの種類がスキャンされます。 これらの同じフィルターが、オペレーティング システムによって Windows Search とインデックス作成にも使用されます。 構成を何も追加しなくても、Word、Excel、PowerPoint、PDF ドキュメント、テキスト ファイルに対して使用されるファイルの種類のスキャンに、Windows IFilter が使用されます。

既定でサポートされているファイルの種類の完全な一覧と、.zip ファイルと tiff ファイルを含む既存のフィルターを構成する方法の詳細については、次の管理者ガイドを参照してください。

- クラシッククライアントの場合:[検査がサポートされているファイルの種類](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)
- 統一されたラベル付けクライアントの場合:[検査でサポートされるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection)

検査が済むと、ユーザーがラベルに対して指定した条件を使用して、これらのファイルの種類にラベルを付けることができます。 または、検出モードを使用している場合は、ユーザーがラベルに対して指定した条件、またはすべての既知の機密情報の種類を含むように、これらのファイルを報告できます。 

ただし、以下の状況では、スキャナーでファイルにラベルを付けることはできません。

- ラベルが分類を適用し、保護されていない場合、およびファイルの種類では、[従来のクライアント](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)または統合された[ラベル付けクライアント](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only)による分類のみがサポートされません。

- ラベルで分類と保護が適用されるが、スキャナーでファイルの種類が保護されていない場合。
    
    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 次のセクションで説明するように、[保護するファイルの種類を変更](#change-which-file-types-to-protect)するときに、その他のファイルの種類を保護することができます。

たとえば、.txt ファイルの種類では "分類のみ" がサポートされていないため、ファイル名拡張子が .txt であるファイルを検査した後は、分類用にだけ構成されていて保護用には構成されていないラベルを、スキャナーで適用することはできません。 ラベルが分類および保護用に構成されていて、拡張子 .txt が付いている場合は、スキャナーによってファイルにラベルを付けることができます。 

> [!TIP]
> このプロセス中にスキャナーが停止し、リポジトリ内の大量のファイルのスキャンが完了しない場合:
> 
> - ファイルをホストしているオペレーティング システムに対し、動的ポートの数を増やす必要がある場合があります。 SharePoint 用にサーバーのセキュリティが強化されている場合、スキャナーが許可されているネットワーク接続の数を超えて、そのために停止する原因の 1 つになる可能性があります。
>     
>     スキャナーの停止の原因であるかどうかを確認するには、%*localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog (複数のログがある場合は zip 形式) のスキャナーに対して次のエラーメッセージが記録されているかどうかを確認してください。**リモートサーバーに接続できません。 >。ソケット例外: 各ソケットアドレス (---プロトコル/ネットワークアドレス/ポート) の使用は通常、許可されている IP: ポートです**
>    
>     現在のポート範囲を表示し、範囲を拡大する方法について詳しくは、「[ネットワーク パフォーマンスを向上させるために変更可能な設定](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)」をご覧ください。
> 
> - 大規模な SharePoint ファームの場合、リスト ビューのしきい値 (既定では 5,000) を増やす必要がある場合があります。 詳細については、SharePoint のドキュメント「 [sharepoint での大きなリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。

### <a name="3-label-files-that-cant-be-inspected"></a>3. 検査できないファイルにラベルを付ける
検査できないファイルの種類に対し、スキャナーでは Azure Information Protection ポリシーの既定のラベル、またはユーザーがスキャナー用に構成した既定のラベルが適用されます。

前のステップと同じように、以下の状況では、スキャナーでファイルにラベルを付けることはできません。

- ラベルが分類を適用し、保護されていない場合、およびファイルの種類では、[従来のクライアント](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)または統合された[ラベル付けクライアント](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only)による分類のみがサポートされません。

- ラベルで分類と保護が適用されるが、スキャナーでファイルの種類が保護されていない場合。
    
    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 次に説明するように、保護するファイルの種類を変更するときに、その他のファイルの種類を保護できます。

## <a name="change-which-file-types-to-protect"></a>保護するファイルの種類を変更する

既定では、スキャナーは Office ファイルの種類と PDF ファイルのみを保護します。 この動作は、たとえばスキャナーがすべてのファイルの種類を保護するように変更できます。これは、クライアントと同じ保護動作です。 また、スキャナーは、Office のファイルの種類と PDF ファイルに加えて、指定した追加のファイルの種類を保護します。 

構成手順については、次のセクションを参照してください。

### <a name="scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected"></a>クラシッククライアントからのスキャナー: レジストリを使用して、保護するファイルの種類を変更します。

このセクションは、クラシッククライアントからのスキャナーにのみ適用されます。

Office ファイルや Pdf 以外のファイルの種類を保護するための既定のスキャナー動作を変更するには、レジストリを編集し、保護するファイルの種類と保護の種類 (ネイティブまたは汎用) を指定する必要があります。 詳しくは、開発者ガイダンスの「[ファイル API の構成](develop/file-api-configuration.md)」をご覧ください。 この開発者向けドキュメントでは、汎用的な保護は "PFile" と呼ばれています。 さらに、スキャナーの場合:

- スキャナーには独自の既定の動作があります。既定では、Office ファイル形式と PDF ドキュメントのみが保護されます。 レジストリを変更しない場合、その他のファイル形式は、スキャナーによってラベル付けまたは保護されません。

- すべてのファイルがネイティブ保護または汎用保護で自動的に保護される Azure Information Protection クライアントと同じ既定の保護動作が必要な場合は、`*` ワイルドカードをレジストリキーとして指定し、値 (REG_SZ) として `Encryption` し、値データとして `Default` します。

レジストリを編集するときには、各ファイル名拡張子のキーと共に、**MSIPC** キーと **FileProtection** キーが存在しない場合には手動で作成します。

たとえば、Office ファイルと PDF だけでなく、TIFF イメージも保護するスキャナーの場合、レジストリの編集後は、次の図のようになります。 イメージ ファイルなので、TIFF ファイルではネイティブ保護がサポートされ、結果としてファイル名拡張子は .ptiff になります。

![保護を適用するためのスキャナーのレジストリの編集](./media/editregistry-scanner.png)

ネイティブ保護をサポートしていても、レジストリで指定する必要がある、テキストおよびイメージファイルの種類の一覧については、「[分類と保護のサポートされているファイルの種類](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)」を参照してください。

ネイティブ保護がサポートされていないファイルの場合は、新しいキーとしてファイル名拡張子を指定し、汎用的な保護のために **PFile** を指定します。 結果として、保護されるファイルのファイル名拡張子は .pfile になります。

### <a name="scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected"></a>統合されたラベル付けクライアントからのスキャナー: PowerShell を使用して、保護するファイルの種類を変更します。

このセクションは、統合されたラベル付けクライアントからのスキャナーにのみ適用されます。

スキャナーのラベルをダウンロードするユーザーアカウントに適用されるラベルポリシーについては、 **PFileSupportedExtensions**という名前の PowerShell の詳細設定を指定します。 

> [!NOTE]
> インターネットにアクセスできるスキャナーの場合、このユーザーアカウントは、 *DelegatedUser*パラメーターに指定するアカウントで、Set-AIPAuthentication コマンドを使用します。

例 1: すべてのファイルの種類を保護するためのスキャナーの PowerShell コマンド: ラベルポリシーの名前は "Scanner" です。

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

例 2: スキャナーの PowerShell コマンドを使用して、Office ファイルと PDF ファイルに加えて .xml ファイルと tiff ファイルを保護します。ここで、ラベルポリシーには "Scanner" という名前を付けます。

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}

詳細な手順については、管理者ガイドの「[保護するファイルの種類を変更](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)する」を参照してください。


## <a name="when-files-are-rescanned"></a>ファイルが再スキャンされる場合

最初のスキャン サイクルではスキャナーは構成されているデータ ストアのすべてのファイルを検査し、後続のスキャンでは、新しいファイルまたは変更されたファイルのみが検査されます。 

Azure portal の **[Azure Information Protection-プロファイル]** ウィンドウから、すべてのファイルを再度検査するようスキャナーに強制できます。 一覧からスキャナープロファイルを選択し、 **[すべてのファイルを再スキャン]** オプションを選択します。

![Azure Information Protection スキャナーの再スキャンを開始する](./media/scanner-rescan-files2.png)

すべてのファイルの再検査はレポートにすべてのファイルを含める必要がある場合に役立ち、この構成は通常、検索モードでスキャナーが実行されるときに使用されます。 フル スキャンが完了すると、後続のスキャンで新しいファイルまたは変更されたファイルのみがスキャンされるように、スキャンの種類が自動的に [増分] に変更されます。

また、クラシッククライアントのスキャナーが、新しい条件または変更された条件を持つ Azure Information Protection ポリシーをダウンロードしたときに、すべてのファイルが検査されます。また、統合されたラベル付けクライアントのスキャナーは、自動およびラベルを付けることをお勧めします。 

スキャナーは、次のトリガーに従ってポリシーを更新します。

- クラシッククライアントからのスキャナー: 1 時間ごと、およびサービスが開始され、ポリシーが1時間を経過した場合。 

- 統一されたラベル付けクライアントからのスキャナー: 4 時間ごと。 

> [!TIP]
> テスト期間中など、既定の間隔よりも早くポリシーを更新する必要がある場合は、次のようにします。 
>
> - クラシッククライアントからのスキャナー: ポリシーファイル **%LocalAppData%\Microsoft\MSIP\Policy.msip**からポリシーファイルを手動で削除し**ます。**
>
> - 統一されたラベル付けクライアントからのスキャナー: **%LocalAppData%\Microsoft\MSIP\mip\\<*processname*>/Mip**から手動でコンテンツを削除します。
>
その後、Azure Information Scanner サービスを再起動します。 ラベルの保護設定を変更した場合は、保護設定を保存してから15分待ってから、サービスを再起動してください。


## <a name="editing-in-bulk-for-the-data-repository-settings"></a>データ リポジトリ設定の一括編集

スキャナーのプロファイルに追加したデータ リポジトリに対して、 **[エクスポート]** と **[インポート]** オプションを使って簡単に設定を変更することができます。 たとえば、ご自分の SharePoint データ リポジトリに対して、スキャンから除外する新しいファイルの種類を追加したいことがあります。

Azure portal 内の各データリポジトリを編集するのではなく、 **[リポジトリ]** ペインの **[エクスポート]** オプションを使用します。

![スキャナーのデータ リポジトリの設定をエクスポートする](./media/export-scanner-repositories.png)

ファイルを手動で編集して変更を加え、同じウィンドウで **[インポート]** オプションを使用します。

## <a name="using-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーの使用

Azure Information Protection スキャナーでは、どのような状況でもラベルを構成する必要がないという3つの代替シナリオがサポートされています。 

- データ リポジトリ内のすべてのファイルに既定のラベルを適用する。
    
    この構成では、 **[コンテンツに基づくラベルファイル**] を **[オフ]** に設定します。 次に、 **[既定のラベル]** を **[カスタム]** に設定し、使用するラベルを選択します。
    
    ファイルの内容は検査されず、データリポジトリ内のラベルのないすべてのファイルには、データリポジトリまたはスキャナープロファイルに指定した既定のラベルに従ってラベルが付けられます。 
    
    統合されたラベル付けクライアントのスキャナーでは、既定のラベルが既にラベル付けされている場合でも、すべてのファイルに既定のラベルを適用する場合は、[**既定のラベル**を適用する] を選択することもできます。
    

- データリポジトリ内のすべてのファイルから既存のラベルを削除します。
    
    この構成では、統一されたラベル付けクライアントからのスキャナーにのみ適用できます。既存のラベルを削除することもできます。このラベルに適用されている場合は、保護が含まれます。 ラベルとは独立して適用された保護が保持されます。 リポジトリ内のファイルからすべてのラベルを削除する必要がある場合は、この構成を使用します。
    
    次の設定を構成します。
    - **コンテンツに基づいてファイルにラベルを付ける**:**オフ**
    - **既定のラベル**:**なし**
    - **ファイル**のラベルの再設定: **[** **既定のラベルを強制**する] チェックボックスがオンになっている

- すべてのカスタム条件と、既知の機密情報の種類を特定する。
    
    この構成では、 **[検出する情報の種類]** を **[すべて]** に設定します。
    
    クラシッククライアントからのスキャナーの場合: スキャナーは、Azure Information Protection ポリシーでラベルに指定したカスタム条件、および Azure 情報のラベルに指定できる情報の種類の一覧を使用します。保護ポリシー。 
    
    統一されたラベル付けクライアントのスキャナーの場合: スキャナーは、指定したカスタムの機密情報の種類、およびラベル付け管理センターで選択できる組み込みの機密情報の種類の一覧を使用します。
    
    この設定は、気付かない可能性がある機密情報を発見するのに役立ちますが、スキャナーのスキャン速度が犠牲になります。
    
    スキャナーの次のクイックスタートでは、この構成を使用します。[クイックスタート: 使用している機密情報を検索](quickstart-findsensitiveinfo.md)します。

## <a name="optimizing-the-performance-of-the-scanner"></a>スキャナーのパフォーマンスの最適化

スキャナーのパフォーマンスを最適化するには、次のガイダンスを使用します。 ただし、スキャナーのパフォーマンスではなく、スキャナーコンピューターの応答性が優先される場合は、高度なクライアント設定を使用して、スキャナーが使用するスレッドの数を制限することができます。

- クラシッククライアントからのスキャナー:[スキャナーによって使用されるスレッドの数を制限](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)する

- 統合ラベル付けクライアントからのスキャナー:[スキャナーで使用するスレッドの数を制限](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)する

スキャナーのパフォーマンスを最大化するには

- **スキャナー コンピューターとスキャンされたデータ ストア間のネットワーク接続を高速かつ信頼性の高い接続にする**
    
    たとえば、同じ LAN 内か、スキャンされたデータ ストアと同じネットワーク セグメント内 (推奨) にスキャナー コンピューターを配置します。
    
    ネットワーク接続の品質は、スキャナーがスキャナー サービスを実行しているコンピューターにファイルのコンテンツを転送してファイルを検査するため、スキャナーのパフォーマンスに影響します。 このデータを移動する必要があるネットワークのホップ数を減らす (削除する) と、ネットワークの負荷も軽減されます。 

- **スキャナー コンピューターに利用可能なプロセッサ リソースがあることを確認する**
    
    ファイルの内容の検査、およびファイルの暗号化と複合化は、プロセッサ負荷の高いアクションです。 プロセッサ リソースの不足がスキャナー パフォーマンスを低下させるかどうかを識別するには、指定したデータ ストアの標準のスキャン サイクルを監視します。
    
- **スキャナー サービスを実行しているコンピューター上のローカル フォルダーをスキャンしない**
    
    Windows Server 上にスキャンするフォルダーがある場合は、別のコンピューター上にスキャナーをインストールし、これらのフォルダーをネットワーク共有として構成してスキャンします。 ファイルをホストする機能とファイルをスキャンする機能の 2 つの機能を分離させると、これらのサービス用のリソースの計算が相互に競合していないことを意味します。

必要に応じて、スキャナーの複数のインスタンスをインストールします。 Azure Information Protection スキャナーでは、スキャナーのカスタム プロファイル名を指定するときに同じ SQL Server インスタンス上の複数の構成データベースがサポートされます。 統一されたラベル付けクライアントのスキャナーでは、複数のスキャナーが同じプロファイルを共有できるため、スキャン時間が短縮されます。

スキャナーのパフォーマンスに影響するその他の要因

- スキャンするファイルを含むデータ ストアの現在の負荷と応答時間

- スキャナーが検索モードまたは強制モードのどちらで実行されているか
    
    通常、検索モードでは、強制モードよりもスキャン速度が速くなります。これは、発見には単一ファイルの読み取りアクションが必要なのに対して、強制モードでは読み取り/書き込みアクションが必要なためです。

- Azure Information Protection ポリシーの条件を変更する (クラシッククライアント) か、ラベルポリシーで自動ラベル付け (クライアントの統合)
    
    スキャナーがすべてのファイルを検査する必要がある場合、最初のスキャン サイクルには、既定では新規および変更されたファイルのみを検査する後続のスキャン サイクルよりも、長い時間がかかります。 ただし、条件または自動ラベル設定を変更すると、[前のセクション](#when-files-are-rescanned)で説明したように、すべてのファイルが再度スキャンされます。

- カスタム条件に対する正規表現式の構築
    
    メモリの大量消費とタイムアウト (1 ファイルあたり 15 分) のリスクを回避するには、ご利用の正規表現式を確認して効率的なパターン マッチングが行われているかを確認してください。 例 :
    
    - [最長の量指定子](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)を開始します
    
    - `(?:expression)` ではなく、`(expression)` などの非キャプチャ グループを使用します

- 選択したログ レベル
    
    スキャナー レポートに対して **[デバッグ]** 、 **[情報]** 、 **[エラー]** 、 **[オフ]** から選択できます。 **[オフ]** を選択すると、最適なパフォーマンスになります。 **[デバッグ]** は大幅にスキャナーのスピードを低下させるので、トラブルシューティング時にのみ使用してください。 詳細については、*Set-AIPScannerConfiguration* コマンドレットの [ReportLevel](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) パラメーターを参照してください。

- ファイル自体
    
    - Excel ファイルを除き、Office ファイルは PDF ファイルよりもすばやくスキャンされます。
    
    - 保護されていないファイルは、保護されたファイルよりもすばやくスキャンされます。
    
    - 大きいファイルは明らかに小さいファイルよりも時間がかかります。

- 補足:
    
    - スキャナーを実行するサービスアカウントに、「[スキャナーの前提条件](#prerequisites-for-the-azure-information-protection-scanner)」セクションに記載されている権限のみがあることを確認し、[詳細なクライアント設定](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner)を構成して、スキャナーの低整合性レベルを無効にします (クラシッククライアントのみ)。
    
    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのファイルに既定のラベルを適用すると、ファイル内容の検査がスキップされるため、スキャナーの実行速度が速くなります。
    
    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのカスタム条件と既知の機密情報の種類を特定すると、スキャナーの実行速度が遅くなりなります。
    
    - スキャンのタイムアウト (クラシッククライアントのみ) を減らすことができます。また、スキャン速度を向上させ、メモリ消費を減らすことができますが、[一部のファイル](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner)はスキップされる可能性があります。

## <a name="list-of-cmdlets-for-the-scanner"></a>スキャナーのコマンドレットの一覧

現在では Azure portal からスキャナーを構成するため、データ リポジトリとスキャンされるファイルの種類のリストを構成する以前のバージョンのコマンドレットは、非推奨になりました。 

残っているコマンドレットには、スキャナーをインストールおよびアップグレードするコマンドレット、スキャナーの構成データベースとプロファイルを変更するコマンドレット、ローカルのレポート レベルを変更するコマンドレット、および切断されたコンピューターの構成設定をインポートするコマンドレットが含まれます。 

スキャナーのコマンドレットの完全な一覧: 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Export-Ai/gs](/powershell/module/azureinformationprotection/Export-AIPLogs) -統一されたラベル付けクライアントのみ

- [インポート-Aipscanの構成](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>スキャナーのイベント ログ ID と説明

次のセクションを使用して、スキャナーの可能性のあるイベント ID と説明を特定できます。 これらのイベントは、Windows の**アプリケーションとサービス**のイベント ログ、**Azure Information Protection** でスキャナー サービスを実行しているサーバーにログオンします。

> [!NOTE]
> このセクションは、クラシッククライアントからのスキャナーにのみ適用されます。 現在、統一されたラベル付けクライアントのスキャナーは、イベントログに情報を書き込むことはありません。

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

## <a name="next-steps"></a>次のステップ:

Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

[Windows Server FCI と Azure Information Protection スキャナーの違い](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)についてご説明します。

また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 PowerShell を使用するその他のシナリオの詳細については、管理者ガイドの次のセクションを参照してください。

- クラシッククライアントの場合: [Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md)

- 統一されたラベル付けクライアントの場合: [Azure Information Protection 統合されたラベル付けクライアントでの PowerShell の使用](./rms-client/clientv2-admin-guide-powershell.md)
