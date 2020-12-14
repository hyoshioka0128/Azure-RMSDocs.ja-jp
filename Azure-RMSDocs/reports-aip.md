---
title: Azure Information Protection の中央レポート機能
description: 中央レポート機能を使用して、Azure Information Protection ラベルの導入を追跡し、機密情報を含むファイルを特定する方法
author: batamig
ms.author: bagol
ms.date: 11/09/2020
manager: rkarlin
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 25ea3c8e008334ec50f81f0c5fcef15690132ef6
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386272"
---
# <a name="central-reporting-for-azure-information-protection-public-preview"></a>Azure Information Protection の中央レポート (パブリックプレビュー)

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection analytics for central reporting を使用すると、組織のデータを分類して保護するラベルの導入を追跡するのに役立ちます。 さらに:

- ラベル付けされた保護の対象となるドキュメントと組織全体の電子メールを監視します。

- 組織内の機密情報が含まれているドキュメントを識別します。

- ラベル付きのドキュメントと電子メールに対するユーザーのアクセスを監視し、ドキュメントの分類の変更を追跡します。

- 保護されていないと組織をリスクにさらす可能性がある機密情報が含まれるドキュメントを識別し、次の推奨事項に従ってリスクを軽減します。

- Windows コンピューターからの内部ユーザーまたは外部ユーザーが保護されたドキュメントにアクセスするタイミングと、アクセスが許可または拒否されたかどうかを特定します。

表示されるデータは、Azure Information Protection のクライアントとスキャナー、Microsoft Cloud App Security、Microsoft Defender Advanced Threat Protection を使用した Windows 10 コンピューター、および保護の [使用状況ログ](log-analyze-usage.md)から集計されます。 [AIP ビューアー](rms-client/clientv2-view-use-files.md)では監査ログが送信されないことに注意してください。

Central reporting の Azure Information Protection analytics は現在プレビュー段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 


## <a name="aip-reporting-data"></a>AIP レポートデータ

たとえば、中央レポートの Azure Information Protection analytics には、次のデータが表示されます。

|レポート  |表示されるサンプルデータ |
|---------|---------|
|**利用状況レポート**     |  次のいずれかを表示する期間を選択します。 <br /><br />     -適用されているラベル <br /><br />-ラベル付けされているドキュメントと電子メールの数 <br /><br />-保護されているドキュメントと電子メールの数 <br /><br />-ドキュメントと電子メールにラベルを付けているユーザー数とデバイス数 <br /><br />ラベル付けに使用されているアプリケーション     |
|**アクティビティ ログ**     | 次のいずれかを表示する期間を選択します。 <br /><br />      -スキャナーによって以前に検出されたファイルは、スキャンされたリポジトリから削除されました <br /> <br /> -特定のユーザーによって実行されたラベル付けアクション <br /><br /> -特定のデバイスで実行されたラベル付けアクション<br /> <br />    -特定のラベル付きドキュメントにアクセスしたユーザー<br /> <br />-特定のファイルパスに対して実行されたラベル付けアクション<br /> <br />-ファイルエクスプローラー、右クリック、PowerShell、スキャナー、また Microsoft Cloud App Security はなど、特定のアプリケーションによってラベル付けされたアクションが実行されました。 <br /> <br />-ユーザーが正常にアクセスした、またはユーザーへのアクセスが拒否された、ユーザーに Azure Information Protection クライアントがインストールされていない、または組織外にある保護されたドキュメント <br /> <br />-報告されたファイルにドリルダウンし、追加情報の **アクティビティの詳細** を表示します      |
|**データ検出レポート**     |      -スキャンされたデータリポジトリ、Windows 10 コンピューター、または Azure Information Protection クライアントを実行しているコンピューターにあるファイル <br /><br />-ラベルが付けられ、保護されているファイルとラベル別のファイルの場所 <br /><br />-財務データや個人情報などの既知のカテゴリの機密情報が含まれているファイル、およびこれらのカテゴリによるファイルの場所       |
|**推奨事項レポート**     | -既知の機密情報の種類を含む保護されていないファイルを特定します。 推奨事項に従えば、ご利用のラベルのいずれかによって自動ラベル付けまたは推奨ラベル付けを適用するための対応する条件をすぐに構成することができます。 次 **<br /> の推奨事項に従うと**、次にユーザーがファイルを開いたとき、または Azure Information Protection スキャナーでスキャンしたときに、ファイルを自動的に分類して保護することができます。 <br /><br /> -特定の機密情報が含まれているが、Azure Information Protection によってスキャンされていないファイルを持つデータリポジトリ。 推奨事項に従えば、識別されたデータ ストアをご利用のスキャナーのプロファイルのいずれかにすぐに追加できます。 <br />   次のスキャナーサイクルで **推奨事項に従う** と、ファイルを自動的に分類して保護することができます。        |
 
レポートでは [Azure Monitor](/azure/log-analytics/log-analytics-overview) を使用して、ご自身の組織が所有している Log Analytics ワークスペースにデータを格納します。 クエリ言語に習熟している場合は、クエリを変更して、新しいレポートや Power BI ダッシュボードを作成できます。 クエリ言語の概要については、「 [Azure Monitor のログクエリの使用](/azure/azure-monitor/log-query/get-started-queries)」を参照してください。

詳細については、次のブログ記事を参照してください。 
- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) (Microsoft Information Protection を使用して、すべてのデータに対してデータ検出、レポート作成、および分析を行う)

- [Azure Information Protection と Microsoft Defender ATP を使用して機密データを検出して保護する](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>収集され Microsoft に送信される情報

これらのレポートを生成するため、エンドポイントでは次の種類の情報が Microsoft に送信されます。

- ラベル操作。 ラベルの設定、ラベルの変更、保護の追加または削除、自動ラベルと推奨ラベルなど。

- ラベル操作の前後のラベル名。

- 組織のテナント ID。

- ユーザー ID (電子メール アドレスまたは UPN)。

- ユーザーのデバイスの名前。

- ユーザーのデバイスの IP アドレス。 

- **Outlook** や **msip. app** など、関連するプロセス名。

- **Outlook** や **エクスプローラー** など、ラベル付けを実行したアプリケーションの名前

- ドキュメントの場合: ラベル付けされているドキュメントのファイル パスとファイル名。

- 電子メールの場合: ラベルが付けられている電子メールの件名と電子メールの送信者。 

- コンテンツ内で検出された機密情報の種類 ([定義済み](/office365/securitycompliance/what-the-sensitive-information-types-look-for)およびカスタム)。

- Azure Information Protection クライアントのバージョン。

- クライアント オペレーティング システムのバージョン。

この情報は、ご自身の組織が所有している Azure Log Analytics ワークスペースに格納され、Azure Information Protection とは別に、このワークスペースへのアクセス権を持つユーザーが表示できます。 

詳細については、次のリンクを参照してください。

- [Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)
- [Azure のアクセス許可を使用して Log Analytics ワークスペースへのアクセスを管理する](/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)
- [監査ログの参照の Azure Information Protection](audit-logs.md)

#### <a name="prevent-the-aip-clients-from-sending-auditing-data"></a>AIP クライアントが監査データを送信できないようにする

**統合ラベル付けクライアント** 

Azure Information Protection 統合されたラベル付けクライアントが監査データを送信できないようにするには、ラベルポリシーの [詳細設定](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics)を構成します。

**従来のクライアント**

Azure Information Protection のクラシッククライアントがこのデータを送信しないようにするには、[**監査データを Azure Information Protection analytics に送信** する] の [ポリシー設定](configure-policy-settings.md)を [**オフ**] に設定します。

|要件  |Instructions  |
|---------|---------|
|**データを送信できないユーザーのサブセットを使用して、ほとんどのユーザーがデータを送信できるように構成するには**     |  ユーザーのサブセットのスコープ **ポリシーで [** **監査データを Azure Information Protection analytics に送信** する。 <br><br> この構成は、運用環境のシナリオに一般的なものです。     |
|**データを送信するユーザーのサブセットのみを構成するには**     |  グローバルポリシーで [**監査データを Azure Information Protection analytics に送信** する] を [オフ] に、ユーザーのサブセットに対してスコープポリシーを **[** **オフ**] に設定します。 <br><br>この構成は、テストのシナリオに一般的なものです。       |
| | |

#### <a name="content-matches-for-deeper-analysis"></a>詳細な分析のためのコンテンツ一致

Azure Information Protection を使用すると、機密情報の種類 (定義済みまたはカスタム) として識別された実際のデータを収集して保存することができます。 たとえば、これには検出されたクレジット カード番号だけでなく、社会保障番号、パスポート番号、銀行口座番号も含まれる場合があります。 コンテンツの一致は、 **アクティビティログ** からエントリを選択すると表示され、 **アクティビティの詳細** を表示します。 

既定では Azure Information Protection クライアントはコンテンツの一致を送信しません。 コンテンツの一致が送信されるようにこの動作を変更するには:

|クライアント  |Instructions  |
|---------|---------|
|**統合ラベル付けクライアント**      |  ラベルポリシーの [詳細設定](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) を構成します。       |
|**従来のクライアント**      |   Azure Information Protection analytics の [構成](#configure-a-log-analytics-workspace-for-the-reports) の一部としてチェックボックスをオンにします。 このチェックボックスを **オンにすると、機微なデータに対してより深い分析を行う** ことができます。 <br><br> このクライアントを使用しているほとんどのユーザーがコンテンツの一致を送信できないが、一部のユーザーがコンテンツの一致を送信できないようにする場合は、チェックボックスをオンにして、ユーザーのサブセットのスコープポリシーの [ [詳細なクライアント設定](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) ] を構成します。     |
|     |         |


## <a name="prerequisites"></a>前提条件
Azure Information Protection レポートを表示し、独自のレポートを作成するには、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|Log Analytics を含む Azure サブスクリプションで、Azure Information Protection と同じテナント用のサブスクリプション|「[Azure Monitor の価格](https://azure.microsoft.com/pricing/details/log-analytics)」ページをご覧ください。<br /><br />Azure サブスクリプションをお持ちでない場合、または現在 Azure Log Analytics をご使用でない場合、価格ページには無料試用版へのリンクが含まれます。|
|クライアントにラベルを付けるためのレポート情報の場合: <br /><br />-Azure Information Protection クライアント|統一されたラベル付けクライアントと従来のクライアントの両方がサポートされています。 <br /><br />まだインストールされていない場合は、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)から、統合されたラベル付けクライアントをダウンロードしてインストールすることができます。 AIP クラシック クライアントをデプロイするには、サポート チケットを作成してダウンロード アクセスを取得します。|
|クラウドベースのデータストアからの情報を報告する場合: <br /><br />-Microsoft Cloud App Security |Microsoft Cloud App Security から情報を表示するには [Azure Information Protection 統合](/cloud-app-security/azip-integration)を構成します。|
|オンプレミスのデータストアからのレポート情報の場合: <br /><br />-Azure Information Protection スキャナー |スキャナーのインストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。 |
|Windows 10 コンピューターからの情報を報告する場合:  <br /><br />-Microsoft Defender Advanced Threat Protection を使用した1809の最小ビルド (Microsoft Defender ATP)|Azure Information Protection 統合機能を Microsoft Defender Security Center から有効にする必要があります。 詳細については、「 [Windows の情報保護の概要](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview)」を参照してください。|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure Information Protection 分析に必要なアクセス許可

Azure Information Protection 分析に固有の機能として、ご自身の Azure Log Analytics ワークスペースを構成した後、セキュリティ閲覧者の Azure AD 管理者ロールを、Azure portal で Azure Information Protection の管理をサポートしている他の Azure AD ロールの代替として使用することができます。 この追加のロールは、テナントが統一された [ラベル付けプラットフォーム](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)にない場合にのみサポートされます。

Azure Information Protection analytics では Azure 監視が使用されるため、Azure 用のロールベースのアクセス制御 (RBAC) によっても、ワークスペースへのアクセスが制御されます。 したがって、Azure Information Protection 分析を管理するためには、Azure ロールと Azure AD の管理者ロールが必要です。 Azure ロールを初めてご使用になる場合は、「[Azure RBAC ロールと Azure AD 管理者ロールの違い](/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)」が役に立つ場合があります。

詳細については、次を参照してください。

- [必要な Azure AD 管理者ロール](#required-azure-ad-administrator-roles)
- [必要な Azure Log Analytics ロール](#required-azure-log-analytics-roles)
- [レポートを表示するための最低限のロール](#minimum-roles-to-view-the-reports)

#### <a name="required-azure-ad-administrator-roles"></a>必要な Azure AD 管理者ロール

Azure Information Protection analytics] ウィンドウにアクセスするには、次のいずれかの [Azure AD 管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) が必要です。

- Log Analytics ワークスペースを作成する、またはカスタム クエリを作成するには:
    
    - **Azure Information Protection 管理者**
    - **セキュリティ管理者**
    - **コンプライアンス管理者**
    - **コンプライアンス データ管理者**
    - **グローバル管理者**
    
- ワークスペースが作成された後、次のロールを使用して、収集されるデータを表示するアクセス許可を減らすことができます。
    
    - **セキュリティ閲覧者**
    - **グローバルリーダー**

#### <a name="required-azure-log-analytics-roles"></a>必要な Azure Log Analytics ロール

Azure Log Analytics ワークスペースにアクセスするには、次のいずれかの [azure Log Analytics ロール](/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions) または標準の [azure ロール](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles) が必要です。
    
- ワークスペースを作成する、またはカスタム クエリを作成するには、次のいずれか:
    
    - **Log Analytics Contributor**
    - **Contributor**
    - **所有者**
    
- ワークスペースが作成された後は、アクセス許可がさらに少ない次のロールのいずれかを使用して、収集されたデータを表示できます。
    
    - **Log Analytics Reader**
    - **Reader**

#### <a name="minimum-roles-to-view-the-reports"></a>レポートを表示するための最低限のロール

Azure Information Protection 分析のためにワークスペースを構成した後、Azure Information Protection 分析レポートを表示するために必要な最低限のロールは、次の両方です。

- Azure AD 管理者ロール:**セキュリティ閲覧** 者
- Azure ロール: **Log Analytics リーダー**

ただし、多くの組織での標準的なロールの割り当ては、Azure AD の **セキュリティ閲覧者** ロールと、Azure の **閲覧者** ロールです。

### <a name="storage-requirements-and-data-retention"></a>ストレージ要件とデータ保有期間

Azure Information Protection ワークスペースに収集されて格納されるデータの量は、テナントごとに大きく異なります。たとえば、Azure Information Protection クライアントやその他のサポートされているエンドポイントの数など、エンドポイント探索データを収集する場合、スキャナーを展開した場合、アクセスされる保護されたドキュメントの数などの要因によって異なります。

ただし、出発点として、次のような見積もりが役に立つ場合があります。

- Azure Information Protection クライアントによって生成された監査データの場合のみ: 1 か月あたり1万のアクティブユーザーあたり 2 GB。

- Azure Information Protection クライアント、スキャナー、Microsoft Defender ATP によって生成される監査データの場合: 1 か月あたり1万のアクティブユーザーあたり 20 GB。

必須のラベル付けを使用した場合、またはほとんどのユーザーに既定のラベルを構成した場合、料金は大幅に高くなる可能性があります。

Azure Monitor ログには、格納されているデータの量の見積もりと確認に役立つ **使用量と推定コスト** の機能があります。また、Log Analytics ワークスペースのデータ保有期間を制御することもできます。 詳細については、「 [Azure Monitor ログを使用した使用状況とコストの管理](/azure/azure-monitor/platform/manage-cost-storage)」を参照してください。

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>レポート用に Log Analytics ワークスペースを構成する

1. まだそれを実行していない場合、新しいブラウザー ウィンドウを開き、[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)を備えたアカウントを使って [Azure portal にサインインします](https://portal.azure.com)。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。
    
1. [ **管理** ] メニューオプションを探し、[ **analytics の構成 (プレビュー)**] を選択します。

1. [ **Log analytics の Azure Information Protection** ] ウィンドウに、テナントが所有している Log Analytics ワークスペースの一覧が表示されます。 次のいずれかの操作を行います。
    
    - **新しい Log Analytics ワークスペースを作成するに** は、[ **新しいワークスペースの作成**] を選択し、[ **Log Analytics ワークスペース** ] ウィンドウで、要求された情報を入力します。
    
    - **既存の Log Analytics ワークスペースを使用するに** は、一覧からワークスペースを選択します。
    
    Log Analytics ワークスペースの作成に関する情報については、「[Azure portal で Log Analytics ワークスペースを作成する](/azure/log-analytics/log-analytics-quick-create-workspace)」を参照してください。

1. **AIP クラシッククライアントのみ**: 機密性の高い情報の種類として識別された実際のデータを保存する場合は、[ **機微なデータへの分析をさらに有効に** する] チェックボックスをオンにします。 

    この設定の詳細については、このページの「詳細な [分析のためのコンテンツの一致](#content-matches-for-deeper-analysis) 」を参照してください。

1. **[OK]** を選択します。

これで、レポートを表示する準備ができました。

## <a name="how-to-view-the-reports"></a>レポートの表示方法

Azure Information Protection ウィンドウで、[ **ダッシュボード** ] メニューオプションを見つけて、次のいずれかのオプションを選択します。

|レポート  |説明  |
|---------|---------|
|**使用状況レポート (プレビュー)**     |  ラベルがどのように使用されているかを確認するには、このレポートを使用します。       |
|**アクティビティログ (プレビュー)**     |  ユーザーからの、およびデバイスとファイル パス上でのラベル付けアクションを確認するには、このレポートを使用します。 さらに、保護されたドキュメントについては、Azure Information Protection クライアントがインストールされていない場合でも、組織の内部と外部の両方でユーザーのアクセス試行 (成功または拒否) を確認できます。 <br><br>  このレポートには **[列]** オプションが備わっています。これを使うと、既定の表示よりも多くのアクティビティ情報を表示できます。 ファイルを選択して **アクティビティの詳細** を表示することで、ファイルの詳細を確認することもできます。     |
|**データ検出 (プレビュー)**     |    スキャナーとサポートされているエンドポイントによって検出されたラベル付きファイルに関する情報を表示するには、このレポートを使用します。  <br><br>**ヒント**: 収集された情報から、機密情報が含まれているファイルにアクセスするユーザーが、知らない場所や現在スキャンしていない場所からアクセスしている可能性があります。 <br><br>-場所がオンプレミスの場合は、Azure Information Protection スキャナーの追加データリポジトリとして場所を追加することを検討してください。 <br>  -場所がクラウド内にある場合は、Microsoft Cloud App Security を使用して管理することを検討してください。    |
|**推奨事項 (プレビュー)**     | このレポートを使用すると、推奨事項に従って機密情報が含まれているファイルを識別し、リスクを軽減することができます。  <br><br> 項目を選択すると、**[データの表示]** オプションによって、推奨事項をトリガーした監査アクティビティが表示されます。     |
|     |         |


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>レポートを変更し、カスタム クエリを作成する方法

ダッシュボードのクエリアイコンを選択して、 **ログ検索** ウィンドウを開きます。 

![Azure Information Protection のレポートをカスタマイズする [Log Analytics] アイコン](./media/log-analytics-icon.png)


Azure Information Protection のログに記録されたデータは、テーブル **InformationProtectionLogs_CL** に格納されます。

独自のクエリを作成する場合は、**InformationProtectionEvents** 関数として実装されているフレンドリ スキーマ名を使用します。 これらの関数は、カスタム クエリ用にサポートされている属性から派生し (一部の属性は内部使用のみ)、基になる属性が機能強化や新機能に対応するために変更された場合でも、それらの名前が変更されることはありません。

### <a name="friendly-schema-reference-for-event-functions"></a>イベント関数のフレンドリ スキーマ リファレンス

次の表を使用して、Azure Information Protection 分析のカスタム クエリで使用できるイベント関数のフレンドリ名を識別してください。

|列名|説明|
|-----------|-----------|
|**Time**|イベント時間: YYYY-MM-YYYY-MM-DDTHH: MM: SS 形式の UTC|
|**User**|User: UPN または DOMAIN\USER の形式を設定します。|
|**ItemPath**|アイテムの完全なパスまたは電子メールの件名|
|**ItemName**|ファイル名または電子メールの件名 |
|**方法**|ラベルの割り当て方法: 手動、自動、推奨、既定、または必須|
|**アクティビティ**|監査アクティビティ: DowngradeLabel、UpgradeLabel、RemoveLabel、NewLabel、Discover、Access、RemoveCustomProtection、ChangeCustomProtection、NewCustomProtection、または FileRemoved |
|**ResultStatus**|アクションの結果の状態:<br /><br /> 成功または失敗 (AIP スキャナーのみによって報告)|
|**ErrorMessage_s**|ResultStatus = Failed の場合、エラーメッセージの詳細が含まれます。 AIP スキャナーのみによって報告されました|
|**LabelName**|ラベル名 (ローカライズされていない)|
|**LabelNameBefore** |変更前のラベル名 (ローカライズされていない) |
|**ProtectionType**|保護の種類 [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|**保護の開始**|変更前の保護の種類 [JSON] |
|**MachineName** |FQDN (使用可能な場合)。それ以外のホスト名|
|**DeviceRisk**|WDATP からのデバイスのリスクスコア (利用可能な場合)|
|**プラットフォーム**|デバイスプラットフォーム (Win、OSX、Android、iOS) |
|**ApplicationName**|アプリケーションのフレンドリ名|
|**AIPVersion**|監査アクションを実行した Azure Information Protection クライアントのバージョン |
|**TenantId**|Azure AD テナント ID |
|**AzureApplicationId**|Azure AD 登録されたアプリケーション ID (GUID)|
|**ProcessName**|MIP SDK をホストするプロセス|
|**LabelId**|GUID または null のラベル|
|**IsProtected**|保護されているかどうか: はい/いいえ |
|**ProtectionOwner** |UPN 形式の Rights Management 所有者|
|**Labの前に**|GUID または null を変更する前に null を付ける|
|**InformationTypesAbove55**|信頼レベル55以上のデータで見つかった [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列 |
|**InformationTypesAbove65**|信頼レベル65以上のデータで見つかった [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列 |
|**InformationTypesAbove75**|信頼レベル75以上のデータで見つかった [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列 |
|**InformationTypesAbove85**|信頼レベル85以上のデータで見つかった [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列 |
|**InformationTypesAbove95**|信頼レベル95以上のデータで見つかった [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列|
|**DiscoveredInformationTypes** |[SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for)の JSON 配列が、データと一致するコンテンツ (有効な場合) で見つかりました。空の配列は、情報の種類が見つからないことを意味し、null は使用できる情報がないことを意味します。 |
|**ProtectedBefore**|変更前にコンテンツが保護されていたかどうか: はい/いいえ |
|**ProtectionOwnerBefore**|変更前に所有者を Rights Management |
|**UserJustification**|ラベルをダウングレードまたは削除するときの理由|
|**LastModifiedBy**|ファイルを最後に変更したユーザー (UPN 形式)。 Office および SharePoint のみで使用可能|
|**LastModifiedDate**|形式の UTC-YYYY-MM-DDTHH: MM: SS: Office および SharePoint のみで使用可能 |

#### <a name="examples-using-informationprotectionevents"></a>InformationProtectionEvents の使用例

次の例で、カスタム クエリを作成するフレンドリ スキーマを使用する方法を確認してください。

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>例 1: 過去31日間に監査データを送信したすべてのユーザーを返す 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>例 2: 過去31日間の1日あたりにダウングレードされたラベルの数を返す 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>例 3: 過去31日以内にユーザーによって機密情報からダウングレードされたラベルの数を返す 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

この例では、アクション前のラベルの名前に **Confidential** (社外秘) が含まれ、アクション後の名前に **Confidential** が含まれていない場合のみ、ダウングレードされたラベルとしてカウントされます。 


## <a name="next-steps"></a>次のステップ
レポートの情報を確認した後、Azure Information Protection クライアントを使用している場合は、ラベル付けポリシーに変更を加えることができます。 

- **統一** されたラベル付けクライアント: Microsoft 365 security center、Microsoft 365 コンプライアンスセンター、Microsoft 365 Security & コンプライアンスセンターなど、ラベル付けポリシーをラベル管理センターで変更します。 詳細については、[Microsoft 365 のドキュメント](/microsoft-365/compliance/sensitivity-labels)を参照してください。

- **クラシッククライアント**: Azure portal でポリシーに変更を加えます。 詳細については、「 [Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。

Microsoft 365 のサブスクリプションがある場合は、Microsoft 365 コンプライアンス センターと Microsoft 365 セキュリティ センターでラベルの使用状況を表示することもできます。 詳しくは、「[ラベル分析によるラベル使用状況の表示](/microsoft-365/compliance/label-analytics)」をご覧ください。

