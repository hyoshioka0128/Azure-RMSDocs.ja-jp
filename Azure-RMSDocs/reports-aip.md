---
title: Azure Information Protection の中央レポート機能
description: 中央レポート機能を使用して、Azure Information Protection ラベルの導入を追跡し、機密情報を含むファイルを特定する方法
author: batamig
ms.author: bagol
ms.date: 08/17/2020
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ecc0a78a942dc4e0c6b1dc89b3d2d2ec57c87f6e
ms.sourcegitcommit: 325bb21a2210069f6d838ca7a875d7082c5e02a6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88264380"
---
# <a name="central-reporting-for-azure-information-protection-public-preview"></a>Azure Information Protection の中央レポート (パブリックプレビュー)

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection analytics for central reporting を使用すると、組織のデータを分類して保護するラベルの導入を追跡するのに役立ちます。 さらに:

- ラベル付けされた保護の対象となるドキュメントと組織全体の電子メールを監視します。

- 組織内の機密情報が含まれているドキュメントを識別します。

- ラベル付きのドキュメントと電子メールに対するユーザーのアクセスを監視し、ドキュメントの分類の変更を追跡します。

- 保護されていないと組織をリスクにさらす可能性がある機密情報が含まれるドキュメントを識別し、次の推奨事項に従ってリスクを軽減します。

- Windows コンピューターからの内部ユーザーまたは外部ユーザーが保護されたドキュメントにアクセスするタイミングと、アクセスが許可または拒否されたかどうかを特定します。

表示されるデータは、Azure Information Protection のクライアントとスキャナー、Microsoft Cloud App Security、Microsoft Defender Advanced Threat Protection を使用した Windows 10 コンピューター、および保護の [使用状況ログ](log-analyze-usage.md)から集計されます。

たとえば、次のようなことを確認できます。

- 期間を選択できる**使用状況レポート**からは、次のことが確認できます。
    
    - 適用されているラベル
    
    - ラベル付けされているドキュメントと電子メールの数
    
    - 保護されているドキュメントと電子メールの数
    
    - ドキュメントや電子メールにラベル付けしているユーザーの数とデバイスの数
    
    - ラベル付けに使用されているアプリケーション

- 期間を選択できる**アクティビティ ログ**からは、次のことが確認できます。

    - スキャナーによって以前に検出されたファイルは、スキャンされたリポジトリから削除されました    
    - 特定のユーザーが実行したラベル付けアクション
    
    - 特定のデバイスから実行されたラベル付けアクション
    
    - 特定のラベル付きのドキュメントにアクセスしたユーザー
    
    - 特定のファイル パスに対して実行されたラベル付けアクション
    
    - 特定のアプリケーションで実行されたラベル付けアクション (エクスプローラー、右クリック、PowerShell、スキャナー、Microsoft Cloud App Security
    
    - ユーザーが正常にアクセスした保護されたドキュメント、またはユーザーが Azure Information Protection クライアントをインストールしていないか組織の外部にある場合でも、ユーザーがアクセスを拒否したドキュメント

    - 報告されたファイルをドリルダウンして、追加情報の**アクティビティの詳細**を表示する

- **データ検出**レポートからは、次のことが確認できます。

    - スキャンされたデータリポジトリ、Windows 10 コンピューター、または Azure Information Protection クライアントを実行しているコンピューターにあるファイル
    
    - ラベル付けされ、保護されているファイルと、ラベルごとのファイルの場所
    
    - 既知のカテゴリ (財務データや個人情報など) の機密情報が含まれるファイルと、これらのカテゴリごとのファイルの場所

- **推奨事項**レポートから次のことが確認できます。
    
    - 既知の種類の機密情報が含まれていて保護されていないファイルを識別します。 推奨事項に従えば、ご利用のラベルのいずれかによって自動ラベル付けまたは推奨ラベル付けを適用するための対応する条件をすぐに構成することができます。
        
        次の推奨事項に従うと、次にユーザーがファイルを開いたとき、または Azure Information Protection スキャナーでスキャンしたときに、ファイルを自動的に分類して保護することができます。
    
    - 識別された機密情報が含まれているファイルが存在していて、Azure Information Protection によってスキャンされていないデータ リポジトリを特定します。 推奨事項に従えば、識別されたデータ ストアをご利用のスキャナーのプロファイルのいずれかにすぐに追加できます。
        
        次のスキャナーサイクルで推奨事項に従うと、ファイルを自動的に分類して保護することができます。

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

- ドキュメントの場合: ラベル付けされているドキュメントのファイル パスとファイル名。

- 電子メールの場合: ラベルが付けられている電子メールの件名と電子メールの送信者。 

- コンテンツ内で検出された機密情報の種類 ([定義済み](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)およびカスタム)。

- Azure Information Protection クライアントのバージョン。

- クライアント オペレーティング システムのバージョン。

この情報は、ご自身の組織が所有している Azure Log Analytics ワークスペースに格納され、Azure Information Protection とは別に、このワークスペースへのアクセス権を持つユーザーが表示できます。 

詳細については、次のリンクを参照してください。

- [Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)
- [Azure のアクセス許可を使用して Log Analytics ワークスペースへのアクセスを管理する](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)
- [監査ログの参照の Azure Information Protection](audit-logs.md)

Azure Information Protection クライアント (クラシック) がこのデータを送信できないようにするには、[**監査データを Azure Information Protection analytics に送信する**] の[ポリシー設定](configure-policy-settings.md)を [**オフ**] に設定します。

- ほとんどのユーザーがこのデータを送信し、ユーザーのサブセットが監査データを送信できない場合: 
    - ユーザーのサブセットのスコープ**ポリシーで [** **監査データを Azure Information Protection analytics に送信**する。 この構成は、運用環境のシナリオに一般的なものです。

- ユーザーのサブセットだけが監査データを送信する場合: 
    - グローバルポリシーで [**監査データを Azure Information Protection analytics に送信**する] を [オフ] に、ユーザーのサブセットに対してスコープポリシーを **[** **オフ**] に設定します。 この構成は、テストのシナリオに一般的なものです。

Azure Information Protection 統合クライアントがこのデータを送信できないようにするには、ラベルポリシーの [詳細設定](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics)を構成します。

#### <a name="content-matches-for-deeper-analysis"></a>詳細な分析のためのコンテンツ一致

Azure Information Protection を使用すると、機密情報の種類 (定義済みまたはカスタム) として識別された実際のデータを収集して保存することができます。 たとえば、これには検出されたクレジット カード番号だけでなく、社会保障番号、パスポート番号、銀行口座番号も含まれる場合があります。 コンテンツの一致は、 **アクティビティログ**からエントリを選択すると表示され、 **アクティビティの詳細**を表示します。 

既定では Azure Information Protection クライアントはコンテンツの一致を送信しません。 コンテンツの一致が送信されるようにこの動作を変更するには:

- クラシッククライアントの場合は、Azure Information Protection analytics の [構成](#configure-a-log-analytics-workspace-for-the-reports) の一部としてチェックボックスをオンにします。 このチェックボックスを **オンにすると、機微なデータに対してより深い分析を行う**ことができます。
    
    このクライアントを使用しているほとんどのユーザーがコンテンツの一致を送信できないが、一部のユーザーがコンテンツの一致を送信できないようにする場合は、チェックボックスをオンにして、ユーザーのサブセットのスコープポリシーの [ [詳細なクライアント設定](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) ] を構成します。

- 統一されたラベル付けクライアントの場合は、ラベルポリシーの [詳細設定](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) を構成します。

## <a name="prerequisites"></a>[前提条件]
Azure Information Protection レポートを表示し、独自のレポートを作成するには、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|Log Analytics を含む Azure サブスクリプションで、Azure Information Protection と同じテナント用のサブスクリプション|「[Azure Monitor の価格](https://azure.microsoft.com/pricing/details/log-analytics)」ページをご覧ください。<br /><br />Azure サブスクリプションをお持ちでない場合、または現在 Azure Log Analytics をご使用でない場合、価格ページには無料試用版へのリンクが含まれます。|
|クライアントにラベルを付けるためのレポート情報の場合: <br /><br />-Azure Information Protection クライアント|統一されたラベル付けクライアントと従来のクライアントの両方がサポートされています。 <br /><br />まだインストールされていない場合は、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)から、統合されたラベル付けクライアントをダウンロードしてインストールすることができます。 AIP クラシック クライアントをデプロイするには、サポート チケットを作成してダウンロード アクセスを取得します。|
|クラウドベースのデータストアからの情報を報告する場合: <br /><br />-Microsoft Cloud App Security |Microsoft Cloud App Security から情報を表示するには [Azure Information Protection 統合](https://docs.microsoft.com/cloud-app-security/azip-integration)を構成します。|
|オンプレミスのデータストアからのレポート情報の場合: <br /><br />-Azure Information Protection スキャナー |スキャナーのインストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。 |
|Windows 10 コンピューターからの情報を報告する場合:  <br /><br />-Microsoft Defender Advanced Threat Protection を使用した1809の最小ビルド (Microsoft Defender ATP)|Azure Information Protection 統合機能を Microsoft Defender Security Center から有効にする必要があります。 詳細については、「 [Windows の情報保護の概要](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview)」を参照してください。|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure Information Protection 分析に必要なアクセス許可

Azure Information Protection 分析に固有の機能として、ご自身の Azure Log Analytics ワークスペースを構成した後、セキュリティ閲覧者の Azure AD 管理者ロールを、Azure portal で Azure Information Protection の管理をサポートしている他の Azure AD ロールの代替として使用することができます。 この追加のロールは、テナントが統一された [ラベル付けプラットフォーム](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)にない場合にのみサポートされます。

Azure Information Protection analytics では Azure 監視が使用されるため、Azure 用のロールベースのアクセス制御 (RBAC) によっても、ワークスペースへのアクセスが制御されます。 したがって、Azure Information Protection 分析を管理するためには、Azure ロールと Azure AD の管理者ロールが必要です。 Azure ロールを初めてご使用になる場合は、「[Azure RBAC ロールと Azure AD 管理者ロールの違い](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)」が役に立つ場合があります。

詳細:

1. Azure Information Protection analytics] ウィンドウにアクセスするには、次のいずれかの [Azure AD 管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) を使用します。
    
    - Log Analytics ワークスペースを作成する、またはカスタム クエリを作成するには:
    
        - **Azure Information Protection 管理者**
        - **セキュリティ管理者**
        - **コンプライアンス管理者**
        - **コンプライアンス データ管理者**
        - **グローバル管理者**
    
    - ワークスペースが作成された後、次のロールを使用して、収集されるデータを表示するアクセス許可を減らすことができます。
    
        - **セキュリティ閲覧者**
        - **グローバル閲覧者**

2. さらに、自分の Azure Log Analytics ワークスペースにアクセスするには、次の [Azure Log Analytics ロール](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)または標準の [Azure ロール](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles)のいずれかが必要です。
    
    - ワークスペースを作成する、またはカスタム クエリを作成するには、次のいずれか:
    
        - **Log Analytics Contributor**
        - **Contributor**
        - **所有者**
    
    - ワークスペースが作成された後は、アクセス許可がさらに少ない次のロールのいずれかを使用して、収集されたデータを表示できます。
    
        - **Log Analytics Reader**
        - **Reader**

#### <a name="minimum-roles-to-view-the-reports"></a>レポートを表示するための最低限のロール

Azure Information Protection 分析のためにワークスペースを構成した後、Azure Information Protection 分析レポートを表示するために必要な最低限のロールは、次の両方です。

- Azure AD 管理者ロール:**セキュリティ閲覧**者
- Azure ロール: **Log Analytics リーダー**

ただし、多くの組織での標準的なロールの割り当ては、Azure AD の**セキュリティ閲覧者**ロールと、Azure の**閲覧者**ロールです。

### <a name="storage-requirements-and-data-retention"></a>ストレージ要件とデータ保有期間

Azure Information Protection ワークスペースに収集されて格納されるデータの量は、テナントごとに大きく異なります。たとえば、Azure Information Protection クライアントやその他のサポートされているエンドポイントの数など、エンドポイント探索データを収集する場合、スキャナーを展開した場合、アクセスされる保護されたドキュメントの数などの要因によって異なります。

ただし、出発点として、次のような見積もりが役に立つ場合があります。

- Azure Information Protection クライアントによって生成された監査データの場合のみ: 1 か月あたり1万のアクティブユーザーあたり 2 GB。

- Azure Information Protection クライアント、スキャナー、Microsoft Defender ATP によって生成される監査データの場合: 1 か月あたり1万のアクティブユーザーあたり 20 GB。

必須のラベル付けを使用した場合、またはほとんどのユーザーに既定のラベルを構成した場合、料金は大幅に高くなる可能性があります。

Azure Monitor ログには、格納されているデータの量の見積もりと確認に役立つ **使用量と推定コスト** の機能があります。また、Log Analytics ワークスペースのデータ保有期間を制御することもできます。 詳細については、「 [Azure Monitor ログを使用した使用状況とコストの管理](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)」を参照してください。

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>レポート用に Log Analytics ワークスペースを構成する

1. まだそれを実行していない場合、新しいブラウザー ウィンドウを開き、[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)を備えたアカウントを使って [Azure portal にサインインします](https://portal.azure.com)。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。
    
2. [ **管理** ] メニューオプションを探し、[ **analytics の構成 (プレビュー)**] を選択します。

3. [ **Log analytics の Azure Information Protection** ] ウィンドウに、テナントが所有している Log Analytics ワークスペースの一覧が表示されます。 次のいずれかの操作を行います。
    
    - 新しい Log Analytics ワークスペースを作成するには、[ **新しいワークスペースの作成**] を選択し、[ **Log Analytics ワークスペース** ] ウィンドウで、要求された情報を入力します。
    
    - 既存の Log Analytics ワークスペースを使用するには、一覧からワークスペースを選択します。
    
    Log Analytics ワークスペースの作成に関する情報については、「[Azure portal で Log Analytics ワークスペースを作成する](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)」を参照してください。

4. Azure Information Protection クライアント (クラシック) を使用している場合は、機密情報の種類として識別された実際のデータを保存するには、[ **機微なデータに対してより深い分析を有効に** する] チェックボックスをオンにします。 この設定の詳細については、このページの「詳細な [分析のためのコンテンツの一致](#content-matches-for-deeper-analysis) 」を参照してください。

5. **[OK]** を選択します。

これで、レポートを表示する準備ができました。

## <a name="how-to-view-the-reports"></a>レポートの表示方法

Azure Information Protection ウィンドウで、[ **ダッシュボード** ] メニューオプションを見つけて、次のいずれかのオプションを選択します。

- **使用状況レポート (プレビュー)**: ラベルがどのように使用されているかを確認するには、このレポートを使用します。

- **アクティビティ ログ (プレビュー)**: ユーザーからの、およびデバイスとファイル パス上でのラベル付けアクションを確認するには、このレポートを使用します。 さらに、保護されたドキュメントについては、Azure Information Protection クライアントがインストールされていない場合でも、組織の内部と外部の両方でユーザーのアクセス試行 (成功または拒否) を確認できます。
    
    このレポートには **[列]** オプションが備わっています。これを使うと、既定の表示よりも多くのアクティビティ情報を表示できます。 ファイルを選択して**アクティビティの詳細**を表示することで、ファイルの詳細を確認することもできます。

- **データの検出 (プレビュー)**: スキャナーおよびサポートされているエンドポイントによって検出されたラベル付きファイルに関する情報を表示するには、このレポートを使用します。
    
    ヒント: 収集された情報から、機密情報が含まれているファイルにアクセスするユーザーが、知らない場所や現在スキャンしていない場所からアクセスしている可能性があります。
    
    - 場所がオンプレミスの場合は、Azure Information Protection スキャナーの追加のデータ リポジトリとして、その場所を追加することを検討します。
    - 場所がクラウド上の場合は、Microsoft Cloud App Security を使用してそれらを管理することを検討します。 
    
- **推奨事項 (プレビュー)**: このレポートを使用して、機密情報が含まれているファイルを特定し、推奨事項に従ってリスクを軽減します。
    
    項目を選択すると、**[データの表示]** オプションによって、推奨事項をトリガーした監査アクティビティが表示されます。


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>レポートを変更し、カスタム クエリを作成する方法

ダッシュボードのクエリアイコンを選択して、 **ログ検索** ウィンドウを開きます。 

![Azure Information Protection のレポートをカスタマイズする [Log Analytics] アイコン](./media/log-analytics-icon.png)


Azure Information Protection のログに記録されたデータは、テーブル **InformationProtectionLogs_CL** に格納されます。

独自のクエリを作成する場合は、**InformationProtectionEvents** 関数として実装されているフレンドリ スキーマ名を使用します。 これらの関数は、カスタム クエリ用にサポートされている属性から派生し (一部の属性は内部使用のみ)、基になる属性が機能強化や新機能に対応するために変更された場合でも、それらの名前が変更されることはありません。

### <a name="friendly-schema-reference-for-event-functions"></a>イベント関数のフレンドリ スキーマ リファレンス

次の表を使用して、Azure Information Protection 分析のカスタム クエリで使用できるイベント関数のフレンドリ名を識別してください。

|列名|説明|
|-----------|-----------|
|Time|イベント時間: YYYY-MM-YYYY-MM-DDTHH: MM: SS 形式の UTC|
|ユーザー|User: UPN または DOMAIN\USER の形式を設定します。|
|ItemPath|アイテムの完全なパスまたは電子メールの件名|
|ItemName|ファイル名または電子メールの件名 |
|メソッド|ラベルの割り当て方法: 手動、自動、推奨、既定、または必須|
|アクティビティ|監査アクティビティ: DowngradeLabel、UpgradeLabel、RemoveLabel、NewLabel、Discover、Access、RemoveCustomProtection、ChangeCustomProtection、NewCustomProtection、または FileRemoved |
|ResultStatus|アクションの結果の状態:<br /><br /> 成功または失敗 (AIP スキャナーのみによって報告)|
|ErrorMessage_s|ResultStatus = Failed の場合、エラーメッセージの詳細が含まれます。 AIP スキャナーのみによって報告されました|
|LabelName|ラベル名 (ローカライズされていない)|
|LabelNameBefore |変更前のラベル名 (ローカライズされていない) |
|ProtectionType|保護の種類 [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|保護の開始|変更前の保護の種類 [JSON] |
|MachineName |FQDN (使用可能な場合)。それ以外のホスト名|
|DeviceRisk|WDATP からのデバイスのリスクスコア (利用可能な場合)|
|プラットフォーム|デバイスプラットフォーム (Win、OSX、Android、iOS) |
|ApplicationName|アプリケーションのフレンドリ名|
|AIPVersion|監査アクションを実行した Azure Information Protection クライアントのバージョン |
|TenantId|Azure AD テナント ID |
|AzureApplicationId|Azure AD 登録されたアプリケーション ID (GUID)|
|ProcessName|MIP SDK をホストするプロセス|
|LabelId|GUID または null のラベル|
|IsProtected|保護されているかどうか: はい/いいえ |
|ProtectionOwner |UPN 形式の Rights Management 所有者|
|Labの前に|GUID または null を変更する前に null を付ける|
|InformationTypesAbove55|信頼レベル55以上のデータで見つかった [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列 |
|InformationTypesAbove65|信頼レベル65以上のデータで見つかった [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列 |
|InformationTypesAbove75|信頼レベル75以上のデータで見つかった [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列 |
|InformationTypesAbove85|信頼レベル85以上のデータで見つかった [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列 |
|InformationTypesAbove95|信頼レベル95以上のデータで見つかった [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) の JSON 配列|
|DiscoveredInformationTypes |[SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for)の JSON 配列が、データと一致するコンテンツ (有効な場合) で見つかりました。空の配列は、情報の種類が見つからないことを意味し、null は使用できる情報がないことを意味します。 |
|ProtectedBefore|変更前にコンテンツが保護されていたかどうか: はい/いいえ |
|ProtectionOwnerBefore|変更前に所有者を Rights Management |
|UserJustification|ラベルをダウングレードまたは削除するときの理由|
|LastModifiedBy|ファイルを最後に変更したユーザー (UPN 形式)。 Office および SharePoint のみで使用可能|
|LastModifiedDate|形式の UTC-YYYY-MM-DDTHH: MM: SS: Office および SharePoint のみで使用可能 |


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


## <a name="next-steps"></a>次の手順
レポートの情報を確認した後、Azure Information Protection クライアントを使用している場合は、Azure Information Protection ポリシーに変更を加えることができます。 手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。

Microsoft 365 のサブスクリプションがある場合は、Microsoft 365 コンプライアンス センターと Microsoft 365 セキュリティ センターでラベルの使用状況を表示することもできます。 詳しくは、「[ラベル分析によるラベル使用状況の表示](/microsoft-365/compliance/label-analytics)」をご覧ください。
