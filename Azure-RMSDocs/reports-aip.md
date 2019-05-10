---
title: Azure Information Protection の中央レポート機能
description: 中央レポート機能を使用して、Azure Information Protection ラベルの導入を追跡し、機密情報を含むファイルを特定する方法
author: cabailey
ms.author: cabailey
ms.date: 05/07/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: d7cc81a41b7515edd0df0e38d5813e0e90b2aa73
ms.sourcegitcommit: 7f769dfa8d4758f13b2c7f83d89fabbb84716290
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2019
ms.locfileid: "65191935"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure Information Protection の中央レポート機能

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> 現在のところ、この機能はプレビュー段階で、変更される可能性があります。

Azure Information Protection 分析の中央レポートを使用して、Azure Information Protection ラベルの導入を追跡できます。 さらに:

- ラベル付けされた保護の対象となるドキュメントと組織全体の電子メールを監視します。

- 組織内の機密情報が含まれているドキュメントを識別します。

- ラベル付きのドキュメントと電子メールに対するユーザーのアクセスを監視し、ドキュメントの分類の変更を追跡します。

- 保護されていないと組織をリスクにさらす可能性がある機密情報が含まれるドキュメントを識別し、次の推奨事項に従ってリスクを軽減します。

表示されるデータは、Azure Information Protection クライアントと Azure Information Protection スキャナーからのデータ、[Windows Defender Advanced Threat Protection (Windows Defender ATP)](/windows/security/threat-protection/windows-defender-atp/overview) を実行中の Windows コンピューターからのデータ、および[統合ラベル付けをサポートしているクライアント](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)からのデータを集計したものです。

たとえば、次のようなことを確認できます。

- 期間を選択できる**使用状況レポート**からは、次のことが確認できます。
    
    - 適用されているラベル
    
    - ラベル付けされているドキュメントと電子メールの数
    
    - 保護されているドキュメントと電子メールの数
    
    - ドキュメントや電子メールにラベル付けしているユーザーの数とデバイスの数
    
    - ラベル付けに使用されているアプリケーション

- 期間を選択できる**アクティビティ ログ**からは、次のことが確認できます。
    
    - 特定のユーザーが実行したラベル付けアクション
    
    - 特定のデバイスから実行されたラベル付けアクション
    
    - 特定のラベル付きのドキュメントにアクセスしたユーザー
    
    - 特定のファイル パスに対して実行されたラベル付けアクション
    
    - 特定のアプリケーション (エクスプローラーと右クリック、または AzureInformationProtection PowerShell モジュールなど) によって実行されたラベル付けアクション
    
    - 報告されたファイルをドリルダウンして、追加情報の**アクティビティの詳細**を表示する

- **データ検出**レポートからは、次のことが確認できます。

    - どのようなファイルは、10 のコンピューター、または Azure Information Protection クライアントを実行しているコンピューターで Windows、スキャンされたデータのリポジトリはまたは[統一されたラベル付けをサポートしているクライアント](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)
    
    - ラベル付けされ、保護されているファイルと、ラベルごとのファイルの場所
    
    - 既知のカテゴリ (財務データや個人情報など) の機密情報が含まれるファイルと、これらのカテゴリごとのファイルの場所

- **推奨事項**レポートから次のことが確認できます。
    
    - 既知の種類の機密情報が含まれていて保護されていないファイルを識別します。 推奨事項に従えば、ご利用のラベルのいずれかによって自動ラベル付けまたは推奨ラベル付けを適用するための対応する条件をすぐに構成することができます。
        
        推奨事項に従う場合: 今度ファイルがユーザーによって開かれるか、または Azure Information Protection スキャナーによってスキャンされる場合、ファイルを自動的に分類して保護することができます。
    
    - 識別された機密情報が含まれているファイルが存在していて、Azure Information Protection によってスキャンされていないデータ リポジトリを特定します。 推奨事項に従えば、識別されたデータ ストアをご利用のスキャナーのプロファイルのいずれかにすぐに追加できます。
        
        推奨事項に従う場合: 次のスキャナー サイクルで、ファイルを自動的に分類し、保護することができます。

レポートでは [Azure Monitor](/azure/log-analytics/log-analytics-overview) を使用して、ご自身の組織が所有している Log Analytics ワークスペースにデータを格納します。 クエリ言語に習熟している場合は、クエリを変更して、新しいレポートや Power BI ダッシュボードを作成できます。 クエリ言語を理解するには、「[Log Analytics のクエリの概要](/azure/azure-monitor/log-query/get-started-queries)」のチュートリアルが役立ちます。

詳細については、次のブログ記事を参照してください。 
- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) (Microsoft Information Protection を使用して、すべてのデータに対してデータ検出、レポート作成、および分析を行う)

- [Discover and protect sensitive data through Azure Information Protection and Windows Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292) (Azure Information Protection および Windows Defender ATP を使用して機密データを発見し、保護する)

### <a name="information-collected-and-sent-to-microsoft"></a>収集され Microsoft に送信される情報

これらのレポートを生成するため、エンドポイントでは次の種類の情報が Microsoft に送信されます。

- ラベル操作。 ラベルの設定、ラベルの変更、保護の追加または削除、自動ラベルと推奨ラベルなど。

- ラベル操作の前後のラベル名。

- 組織のテナント ID。

- ユーザー ID (電子メール アドレスまたは UPN)。

- ユーザーのデバイスの名前。

- ドキュメントの場合: ラベル付けされているドキュメントのファイル パスとファイル名。

- 電子メールの場合: ラベル付けされた電子メールの件名と電子メールの送信者。 

- コンテンツ内で検出された機密情報の種類 ([定義済み](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)およびカスタム)。

- Azure Information Protection クライアントのバージョン。

- クライアント オペレーティング システムのバージョン。

この情報は、ご自身の組織が所有している Azure Log Analytics ワークスペースに格納され、Azure Information Protection とは別に、このワークスペースへのアクセス権を持つユーザーが表示できます。 詳細については、「[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)」セクションをご覧ください。 ワークスペースへのアクセスの管理の詳細については、Azure ドキュメントの [Azure アクセス許可を使用した Log Analytics ワークスペースへのアクセスの管理](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions)に関するセクションをご覧ください。

Azure Information Protection クライアントでこのデータが送信されないようにするには、[ポリシー設定](configure-policy-settings.md)の **[監査データを Azure Information Protection ログ分析に送信します]** を **[オフ]** に設定します。

- ほとんどのユーザーがこのデータを送信し、ユーザーのサブセットが監査データを送信できない場合: 
    - ユーザーのサブセットに対するスコープ付きポリシーで、**[監査データを Azure Information Protection ログ分析に送信します]** を **[オフ]** に設定します。 この構成は、運用環境のシナリオに一般的なものです。

- ユーザーのサブセットだけが監査データを送信する場合: 
    - **[監査データを Azure Information Protection ログ分析に送信します]** を、グローバル ポリシーでは **[オフ]** に設定し、ユーザーのサブセットに対するスコープ付きポリシーでは **[オン]** に設定します。 この構成は、テストのシナリオに一般的なものです。

#### <a name="content-matches-for-deeper-analysis"></a>詳細な分析のためのコンテンツ一致 

Azure Information Protection 用の Azure Log Analytics ワークスペースには、機密情報の種類またはカスタム条件によって識別されるデータも収集および格納するためのチェック ボックスが含まれています。 たとえば、これには検出されたクレジット カード番号だけでなく、社会保障番号、パスポート番号、銀行口座番号も含まれる場合があります。 この追加データを送信したくない場合は、このチェック ボックスをオンにしないでください。 ほとんどのユーザーについてはこの追加データを送信し、ユーザーのサブセットでは送信できない場合は、ユーザーのサブセットに対するスコープ付きポリシーでそのチェック ボックスをオンにして、[高度なクライアント設定](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)を構成します。

収集した後のコンテンツ一致は、アクティビティ ログからファイルにドリル ダウンして **[アクティビティの詳細]** を表示すると、レポートに表示されます。 この情報は、クエリで表示および取得することもできます。

## <a name="prerequisites"></a>前提条件
Azure Information Protection レポートを表示し、独自のレポートを作成するには、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|Log Analytics を含む Azure サブスクリプションで、Azure Information Protection と同じテナント用のサブスクリプション|「[Azure Monitor の価格](https://azure.microsoft.com/pricing/details/log-analytics)」ページをご覧ください。<br /><br />Azure サブスクリプションをお持ちでない場合、または現在 Azure Log Analytics をご使用でない場合、価格ページには無料試用版へのリンクが含まれます。|
|Azure Information Protection クライアントまたは Azure Information Protection の統合されたラベル付けクライアント|これらのクライアントのいずれかをいない場合は、ダウンロードしてインストールしてから、 [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)します。 <br /><br /> サポートする最新バージョンがあるかどうかを確認[機能をすべて](#features-that-require-a-minimum-version-of-the-client)Azure Information Protection の分析のためです。|
|**検出とリスク** レポートの場合: <br /><br />、オンプレミスのデータ ストアからデータを表示するには Azure Information Protection スキャナーの少なくとも 1 つのインスタンスをデプロイしました。 <br /><br />- Windows 10 コンピューターからのデータを表示するには、それがビルド 1809 以降であり、Windows Defender Advanced Threat Protection (Windows Defender ATP) を使っていて、Windows Defender セキュリティ センターから Azure Information Protection の統合機能を有効にしていること|スキャナーのインストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。 <br /><br />Windows Defender セキュリティ センターから Azure Information Protection の統合機能を構成および使用する方法について詳しくは、「[Information protection in Windows overview](/windows/security/threat-protection/windows-defender-atp/information-protection-in-windows-overview)」(Windows での情報保護の概要) をご覧ください。|
|**推奨事項**レポートの場合:  <br /><br />-推奨される操作として、Azure portal から新しいデータ リポジトリを追加する必要がありますを使っている Azure Information Protection スキャナーの最新の一般公開バージョン |スキャナーを展開するを参照してください。[ファイルを分類して保護を自動的に Azure Information Protection スキャナーをデプロイして](deploy-aip-scanner.md)します。|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure Information Protection 分析に必要なアクセス許可

Azure Information Protection 分析に固有の機能として、ご自身の Azure Log Analytics ワークスペースを構成した後、セキュリティ閲覧者の Azure AD 管理者ロールを、Azure portal で Azure Information Protection の管理をサポートしている他の Azure AD ロールの代替として使用することができます。

この機能は Azure 監視を使うため、Azure のロールベースのアクセス制御 (RBAC) でワークスペースへのアクセスを制御することもできます。 したがって、Azure Information Protection 分析を管理するためには、Azure ロールと Azure AD の管理者ロールが必要です。 Azure ロールを初めてご使用になる場合は、「[Azure RBAC ロールと Azure AD 管理者ロールの違い](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)」が役に立つ場合があります。

詳細:

1. Azure Information Protection 分析ブレードにアクセスするには、次の [Azure AD の管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)のいずれか:
    
    - Log Analytics ワークスペースを作成する、またはカスタム クエリを作成するには:
    
        - **Information Protection 管理者**
        - **セキュリティ管理者**
        - **コンプライアンス管理者**
        - **グローバル管理者**
    
    - ワークスペースが作成された後は、アクセス許可がさらに少ない次のロールを使用して、収集されたデータを表示できます。
    
        - **セキュリティ閲覧者**
    
    > [!NOTE] 
    > ご自身のテナントが統合ラベル付けストアに移行されている場合、Information Protection 管理者ロールは使用できません。 [詳細情報](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. さらに、自分の Azure Log Analytics ワークスペースにアクセスするには、次の [Azure Log Analytics ロール](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions)または標準の [Azure ロール](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments)のいずれかが必要です。
    
    - ワークスペースを作成する、またはカスタム クエリを作成するには、次のいずれか:
    
        - **Log Analytics 共同作成者**
        - **共同作成者**
        - **所有者**
    
    - ワークスペースが作成された後は、アクセス許可がさらに少ない次のロールのいずれかを使用して、収集されたデータを表示できます。
    
        - **Log Analytics 閲覧者**
        - **閲覧者**

#### <a name="minimum-roles-to-view-the-reports"></a>レポートを表示するための最低限のロール

Azure Information Protection 分析のためにワークスペースを構成した後、Azure Information Protection 分析レポートを表示するために必要な最低限のロールは、次の両方です。

- Azure AD の管理者ロール:**セキュリティ閲覧者**
- Azure ロール:**Log Analytics 閲覧者**

ただし、多くの組織での標準的なロールの割り当ては、Azure AD の**セキュリティ閲覧者**ロールと、Azure の**閲覧者**ロールです。

### <a name="features-that-require-a-minimum-version-of-the-client"></a>クライアントの最小バージョンを必要とする機能

バージョン履歴情報を使用することができます、 [Azure Information Protection クライアントのラベル付けを統合する](./rms-client/unifiedlabelingclient-version-release-history.md)と[Azure Information Protection クライアント](./rms-client/client-version-release-history.md)を確認するかどうか、クライアントのバージョンレポート サーバーの全体のすべての機能をサポートしています。 クライアントの最小バージョン:

Azure Information Protection の統合されたラベル付けクライアント。

- 監査とエンドポイントの検出のサポート:バージョン 2.0.778.0

Azure Information Protection クライアント:

- 監査のサポート:バージョン 1.41.51.0
- エンドポイントの検出のサポート:バージョン 1.48.204.0

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>レポート用に Log Analytics ワークスペースを構成する

1. まだそれを実行していない場合、新しいブラウザー ウィンドウを開き、[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)を備えたアカウントを使って [Azure portal にサインインします](https://portal.azure.com)。 次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
2. **[管理]** メニュー オプションを探し、**[Configure analytics (Preview)]\(分析の構成 (プレビュー)\)** を選択します。

3. **[Azure Information Protection ログ分析]** ブレードには、テナントによって所有されているすべての Log Analytics ワークスペースの一覧が表示されます。 次のいずれかの操作を行います。
    
    - 新しい Log Analytics ワークスペースを作成するには: **[新しいワークスペースの作成]** を選択し、**[Log Analytics ワークスペース]** ブレードで、要求された情報を指定します。
    
    - 既存の Log Analytics ワークスペースを使用するには: 一覧からワークスペースを選択します。

Log Analytics ワークスペースの作成に関する情報については、「[Azure portal で Log Analytics ワークスペースを作成する](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)」を参照してください。

ワークスペースが構成されている場合は、レポートを表示する準備ができています。

> [!NOTE] 
> 現在、レポートで初めてデータを表示するときに既知の問題があります。 これが発生する場合は、グローバル ポリシーで、[ポリシー設定](configure-policy-settings.md)の **[監査データを Azure Information Protection ログ分析に送信します]** を **[オフ]** に設定して、ポリシーを保存します。 その後、同じ設定を **[オン]** に設定して、ポリシーを保存します。 クライアントが[変更をダウンロード](configure-policy.md#making-changes-to-the-policy)した後、その監査イベントが Log Analytics ワークスペースで表示されるまでに、最大で 30 分かかることがあります。

## <a name="how-to-view-the-reports"></a>レポートの表示方法

[Azure Information Protection] ブレードから **[ダッシュボード]** メニュー オプションを探し、次のいずれかのオプションを選択します。

- **使用状況レポート (プレビュー)**: ラベルがどのように使用されているかを確認するには、このレポートを使用します。

- **アクティビティ ログ (プレビュー)**: ユーザーからの、およびデバイスとファイル パス上でのラベル付けアクションを確認するには、このレポートを使用します。
    
    このレポートには **[列]** オプションが備わっています。これを使うと、既定の表示よりも多くのアクティビティ情報を表示できます。 ファイルを選択して**アクティビティの詳細**を表示することで、ファイルの詳細を確認することもできます。

- **データ検出 (プレビュー)**: スキャナーとサポートされているエンドポイントによって検出されたラベル付きファイルに関する情報を表示するには、このレポートを使用します。
    
    注:エンドポイントの検出はテナントに徐々 にロールアウトします。 サポートされているエンドポイントからこのレポートにデータが表示されるのは、この機能がお客様のテナントにロールアウトされた時点から始まります。
    
    構成することができます、[高度なクライアント設定](./rms-client/client-admin-guide-customizations.md#enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents)の機密情報を含むレポート ファイルに Azure Information Protection クライアント。
    
    ヒント:収集された情報から、認識してなかった場所や現時点ではスキャンされていない場所から機密情報が含まれているファイルにアクセスしているユーザーを発見することがあります。
    
    - 場所がオンプレミスの場合は、Azure Information Protection スキャナーの追加のデータ リポジトリとして、その場所を追加することを検討します。
    - 場所がクラウド上の場合は、Microsoft Cloud App Security を使用してそれらを管理することを検討します。 
    
- **推奨事項 (プレビュー)**: このレポートを使用すると、推奨事項に従って機密情報が含まれているファイルを識別し、リスクを軽減することができます。
    
    項目を選択すると、**[データの表示]** オプションによって、推奨事項をトリガーした監査アクティビティが表示されます。


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>レポートを変更し、カスタム クエリを作成する方法

ダッシュボードでクエリ アイコンを選択して、**[ログ検索]** ブレードを開きます。 

![Azure Information Protection のレポートをカスタマイズする [Log Analytics] アイコン](./media/log-analytics-icon.png)


ログに記録された Azure Information Protection のデータは、次のテーブルに格納されます: **InformationProtectionLogs_CL**

独自のクエリを作成する場合は、**InformationProtectionEvents** 関数として実装されているフレンドリ スキーマ名を使用します。 これらの関数は、カスタム クエリ用にサポートされている属性から派生し (一部の属性は内部使用のみ)、基になる属性が機能強化や新機能に対応するために変更された場合でも、それらの名前が変更されることはありません。

### <a name="friendly-schema-reference-for-event-functions"></a>イベント関数のフレンドリ スキーマ リファレンス

次の表を使用して、Azure Information Protection 分析のカスタム クエリで使用できるイベント関数のフレンドリ名を識別してください。

|列名|説明| |-----_-----|-----------| |Time|イベントの時刻:UTC 形式 YYYY-MM-DDTHH:MM:SS| |User|ユーザー:UPN または DOMAIN\USER 形式| |ItemPath|項目の完全パスまたは電子メールの件名| |ItemName|ファイル名または電子メールの件名 | |Method|ラベルの割り当て方法:Manual、Automatic、Recommended、Default、または Mandatory| |Activity|監査アクティビティ:DowngradeLabel、UpgradeLabel、RemoveLabel、NewLabel、Discover、Access、RemoveCustomProtection、ChangeCustomProtection、または NewCustomProtection | |LabelName|ラベルの名前 (ローカライズされません)| |LabelNameBefore |変更前のラベルの名前 (ローカライズされません) | |ProtectionType|保護の種類 [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID":"GUID" <br /> } <br />| |ProtectionBefore|変更前の保護の種類 [JSON] | |InformationTypesMatches|データで検出された [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) の JSON 配列。空の配列は情報の種類が見つからなかったことを、null は入手可能な情報がないことを意味します| |MachineName |入手できた場合は FQDN; それ以外の場合はホスト名| |DeviceRisk|入手できた場合は WDATP からのデバイスのリスク スコア | |Platform|デバイスのプラットフォーム (Win、OSX、Android、iOS) | |ApplicationName|アプリケーションのフレンドリ名| |AIPVersion|監査アクションを実行した Azure Information Protection クライアントのバージョン | |TenantId|Azure AD のテナント ID | |AzureApplicationId|Azure AD の登録アプリケーション ID (GUID)| |ProcessName|MIP SDK をホストしているプロセス| |LabelId|ラベルの GUID または null| |IsProtected|保護されているかどうか:Yes/No | |ProtectionOwner |Rights Management 所有者 (UPN 形式) | |LabelIdBefore|変更前のラベルの GUID または null| |InformationTypesAbove55|データで検出された信頼レベル 55 以上の [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) の JSON 配列 | |InformationTypesAbove65|データで検出された信頼レベル 65 以上の [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) の JSON 配列 | |InformationTypesAbove75|信頼レベル 75 以上のデータで検出された [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) の JSON 配列 | |InformationTypesAbove85|データで検出された信頼レベル 85 以上の [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) の JSON 配列 | |InformationTypesAbove95|データで検出された信頼レベル 95 以上の [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) の JSON 配列| |DiscoveredInformationTypes |データで検出された [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) の JSON 配列とそれらと一致するコンテンツ (有効な場合)。空の配列は情報の種類が見つからなかったことを、null は入手可能な情報がないことを意味します | |ProtectedBefore|変更前にコンテンツが保護されていたかどうか:Yes/No | |ProtectionOwnerBefore|変更前の Rights Management 所有者 | |UserJustification|ラベルのダウングレードまたは削除の実行時の理由| |LastModifiedBy|ファイルを最後に変更したユーザー (UPN 形式)。 Office と SharePoint Online のみで使用可能| |LastModifiedDate| YYYY-MM-DDTHH:MM:SS: 形式のUTCOffice と SharePoint Online のみで使用可能 |


#### <a name="examples-using-informationprotectionevents"></a>InformationProtectionEvents の使用例

次の例で、カスタム クエリを作成するフレンドリ スキーマを使用する方法を確認してください。

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>例 1 : 過去 31 日間の監査データを送信したすべてのユーザーを返す 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>例 2:過去 31 日間の 1 日あたりのダウン グレードされたラベルの数を返す 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>例 3: 過去 31 日間のユーザーによって社外秘からダウングレードされたラベルの数を返す 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

この例では、アクション前のラベルの名前に **Confidential** (社外秘) が含まれ、アクション後の名前に **Confidential** が含まれていない場合のみ、ダウングレードされたラベルとしてカウントされます。 


## <a name="next-steps"></a>次の手順
レポートの情報を確認した後、Azure Information Protection クライアントを使用している場合ことがあります、Azure Information Protection ポリシーを変更します。 手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。

Microsoft 365 のサブスクリプションがある場合は、Microsoft 365 コンプライアンス センターと Microsoft 365 セキュリティ センターでラベルの使用状況を表示することもできます。 詳しくは、「[ラベル分析によるラベル使用状況の表示](/Office365/SecurityCompliance/label-analytics)」をご覧ください。
