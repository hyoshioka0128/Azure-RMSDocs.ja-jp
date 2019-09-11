---
title: Azure Information Protection の中央レポート機能
description: 中央レポート機能を使用して、Azure Information Protection ラベルの導入を追跡し、機密情報を含むファイルを特定する方法
author: cabailey
ms.author: cabailey
ms.date: 09/05/2019
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9108dbe9712b57dd5bef59c5258dccccaf137d86
ms.sourcegitcommit: 91982b08ba8ce734b6d82382db227fcaa2b15e56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872357"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure Information Protection の中央レポート機能

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> 現在のところ、この機能はプレビュー段階で、変更される可能性があります。

Azure Information Protection analytics for central reporting を使用すると、組織のデータを分類して保護するラベルの導入を追跡するのに役立ちます。 さらに:

- ラベル付けされた保護の対象となるドキュメントと組織全体の電子メールを監視します。

- 組織内の機密情報が含まれているドキュメントを識別します。

- ラベル付きのドキュメントと電子メールに対するユーザーのアクセスを監視し、ドキュメントの分類の変更を追跡します。

- 保護されていないと組織をリスクにさらす可能性がある機密情報が含まれるドキュメントを識別し、次の推奨事項に従ってリスクを軽減します。

- 内部または外部のユーザーが保護されたドキュメントにアクセスするタイミングと、アクセスが許可または拒否されたかどうかを識別します。

表示されるデータは、統一された[ラベル付けをサポートするクライアントとサービス](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)、および[保護の使用状況ログ](log-analyze-usage.md)から、Azure Information Protection のクライアントとスキャナーから集計されます。

> [!NOTE]
> 現時点では、Azure Information Protection analytics には、統一されたラベル付けをサポートするクライアントとサービスのカスタム情報の種類は含まれていません。

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
    
    - 特定のアプリケーションで実行されたラベル付けアクション (エクスプローラー、右クリック、PowerShell、スキャナー、Microsoft Cloud App Security
    
    - ユーザーが正常にアクセスした保護されたドキュメント、またはユーザーが Azure Information Protection クライアントをインストールしていないか組織の外部にある場合でも、ユーザーがアクセスを拒否したドキュメント

    - 報告されたファイルをドリルダウンして、追加情報の**アクティビティの詳細**を表示する

- **データ検出**レポートからは、次のことが確認できます。

    - スキャンしたデータリポジトリ、Windows 10 コンピューター、または Azure Information Protection クライアントを実行しているコンピューター、または統一され[たラベル付けをサポートするクライアント](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)を実行しているコンピューターにあるファイル
    
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

- [Azure Information Protection と Microsoft Defender ATP を使用して機密データを検出して保護する](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>収集され Microsoft に送信される情報

これらのレポートを生成するため、エンドポイントでは次の種類の情報が Microsoft に送信されます。

- ラベル操作。 ラベルの設定、ラベルの変更、保護の追加または削除、自動ラベルと推奨ラベルなど。

- ラベル操作の前後のラベル名。

- 組織のテナント ID。

- ユーザー ID (電子メール アドレスまたは UPN)。

- ユーザーのデバイスの名前。

- ドキュメントの場合: ラベル付けされているドキュメントのファイル パスとファイル名。

- 電子メールの場合: ラベル付けされた電子メールの件名と電子メールの送信者。 

- コンテンツ内で検出された[定義済みの機密情報の種類](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)。
    
    カスタム条件で Azure Information Protection ラベルを使用している場合は、カスタム情報の種類の名前も送信されます。 Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、または Microsoft 365 コンプライアンスセンターで作成したカスタム機微な情報の種類は送信されません。

- Azure Information Protection クライアントのバージョン。

- クライアント オペレーティング システムのバージョン。

この情報は、ご自身の組織が所有している Azure Log Analytics ワークスペースに格納され、Azure Information Protection とは別に、このワークスペースへのアクセス権を持つユーザーが表示できます。 詳細については、「[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)」セクションをご覧ください。 ワークスペースへのアクセスの管理の詳細については、Azure ドキュメントの [Azure アクセス許可を使用した Log Analytics ワークスペースへのアクセスの管理](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions)に関するセクションをご覧ください。

Azure Information Protection クライアント (クラシック) がこのデータを送信できないようにするには、 **[監査データを Azure Information Protection analytics に送信する]** の[ポリシー設定](configure-policy-settings.md)を **[オフ]** に設定します。

- ほとんどのユーザーがこのデータを送信し、ユーザーのサブセットが監査データを送信できない場合: 
    - ユーザーのサブセットのスコープ**ポリシーで**  **監査データを Azure Information Protection analytics に送信**する。 この構成は、運用環境のシナリオに一般的なものです。

- ユーザーのサブセットだけが監査データを送信する場合: 
    - グローバルポリシーで [**監査データを Azure Information Protection analytics に送信**する] を [オフ] に、ユーザーのサブセットに対してスコープポリシーを **[** **オフ**] に設定します。 この構成は、テストのシナリオに一般的なものです。

Azure Information Protection 統合クライアントがこのデータを送信できないようにするには、ラベルポリシーの[詳細設定](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics)を構成します。

#### <a name="content-matches-for-deeper-analysis"></a>詳細な分析のためのコンテンツ一致 

Azure Information Protection 用の Azure Log Analytics ワークスペースには、機密情報の種類 (定義済みまたはカスタムの条件) として識別されたデータを収集して格納するためのチェックボックスが含まれています。 たとえば、これには検出されたクレジット カード番号だけでなく、社会保障番号、パスポート番号、銀行口座番号も含まれる場合があります。 この追加データを送信しない場合は、[**機微なデータの分析をさらに有効に**する] チェックボックスをオンにしないでください。 ほとんどのユーザーがこの追加データを送信する必要があり、ユーザーのサブセットがそのデータを送信できないようにするには、チェックボックスをオンにして、次のようにします。

- 従来のクライアントとスキャナーの場合:ユーザーのサブセットに対してスコープポリシーの[詳細なクライアント設定](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)を構成します。

- 統一されたラベル付けクライアントの場合:ユーザーのサブセットのラベルポリシーで[詳細設定](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)を構成します。

収集した後のコンテンツ一致は、アクティビティ ログからファイルにドリル ダウンして **[アクティビティの詳細]** を表示すると、レポートに表示されます。 この情報は、クエリで表示および取得することもできます。

## <a name="prerequisites"></a>必須コンポーネント
Azure Information Protection レポートを表示し、独自のレポートを作成するには、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|Log Analytics を含む Azure サブスクリプションで、Azure Information Protection と同じテナント用のサブスクリプション|「[Azure Monitor の価格](https://azure.microsoft.com/pricing/details/log-analytics)」ページをご覧ください。<br /><br />Azure サブスクリプションをお持ちでない場合、または現在 Azure Log Analytics をご使用でない場合、価格ページには無料試用版へのリンクが含まれます。|
|Azure Information Protection クライアント|統一されたラベル付けクライアントと従来のクライアントの両方がサポートされています。 <br /><br />これらのクライアントのいずれもまだ所有していない場合は、 [Microsoft ダウンロードセンター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードしてインストールできます。|
|Microsoft Cloud App Security |Microsoft Cloud App Security から情報を表示するには[Azure Information Protection 統合](https://docs.microsoft.com/cloud-app-security/azip-integration)を構成します。|
|**検出とリスク** レポートの場合: <br /><br />-オンプレミスのデータストアのデータを表示するには、Azure Information Protection スキャナーのインスタンスを少なくとも1つデプロイします。 <br /><br />-Windows 10 コンピューターからのデータを表示するには、1809の最小ビルドであり、Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を使用していて、Microsoft の Azure Information Protection 統合機能を有効にしている必要があります。Defender Security Center|スキャナーのインストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。 <br /><br />Microsoft Defender Security Center の Azure Information Protection 統合機能を構成して使用する方法の詳細については、「 [Windows の情報保護の概要](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview)」を参照してください。|
|**推奨事項**レポートの場合: <br /><br />-推奨される操作として Azure portal から新しいデータリポジトリを追加するには、で構成されているバージョンの Azure Information Protection スキャナーを使用している必要があり Azure portal |スキャナーを展開するには、「[ファイルを自動的に分類して保護するための Azure Information Protection スキャナーの展開](deploy-aip-scanner.md)」を参照してください。|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure Information Protection 分析に必要なアクセス許可

Azure Information Protection 分析に固有の機能として、ご自身の Azure Log Analytics ワークスペースを構成した後、セキュリティ閲覧者の Azure AD 管理者ロールを、Azure portal で Azure Information Protection の管理をサポートしている他の Azure AD ロールの代替として使用することができます。

この機能は Azure 監視を使うため、Azure のロールベースのアクセス制御 (RBAC) でワークスペースへのアクセスを制御することもできます。 したがって、Azure Information Protection 分析を管理するためには、Azure ロールと Azure AD の管理者ロールが必要です。 Azure ロールを初めてご使用になる場合は、「[Azure RBAC ロールと Azure AD 管理者ロールの違い](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)」が役に立つ場合があります。

詳細:

1. Azure Information Protection 分析ブレードにアクセスするには、次の [Azure AD の管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)のいずれか:
    
    - Log Analytics ワークスペースを作成する、またはカスタム クエリを作成するには:
    
        - **Azure Information Protection 管理者**
        - **セキュリティ管理者**
        - **コンプライアンス管理者**
        - **コンプライアンスデータ管理者**
        - **グローバル管理者**
    
    - ワークスペースが作成された後は、アクセス許可がさらに少ない次のロールを使用して、収集されたデータを表示できます。
    
        - **セキュリティ閲覧者**
    
    > [!NOTE] 
    > テナントが統合ラベルストアに移行されている場合、Azure Information Protection 管理者ロールを使用することはできません。 [詳細情報](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform)

2. さらに、自分の Azure Log Analytics ワークスペースにアクセスするには、次の [Azure Log Analytics ロール](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/manage-access#manage-accounts-and-users)または標準の [Azure ロール](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments)のいずれかが必要です。
    
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

### <a name="storage-requirements-and-data-retention"></a>ストレージ要件とデータ保有期間

Azure Information Protection ワークスペースに収集されて格納されるデータの量は、テナントごとに大きく異なります。 Azure Information Protection クライアントとその他のサポートされているエンドポイントの数などの要因によっては、エンドポイント検出データの収集、スキャナーの展開、アクセスされる保護されたドキュメントの数など。

ただし、出発点として、次のような見積もりが役に立つ場合があります。

- Azure Information Protection クライアントのみによって生成される監査データの場合:1か月あたり1万のアクティブユーザーあたり 2 GB。

- Azure Information Protection クライアント、スキャナー、および Microsoft Defender ATP によって生成される監査データの場合:1か月あたり1万のアクティブユーザーあたり 20 GB。

必須のラベル付けを使用した場合、またはほとんどのユーザーに既定のラベルを構成した場合、料金は大幅に高くなる可能性があります。

Azure Monitor ログには、格納されているデータの量の見積もりと確認に役立つ**使用量と推定コスト**の機能があります。また、Log Analytics ワークスペースのデータ保有期間を制御することもできます。 詳細については、「 [Azure Monitor ログを使用した使用状況とコストの管理](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)」を参照してください。

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>レポート用に Log Analytics ワークスペースを構成する

1. まだそれを実行していない場合、新しいブラウザー ウィンドウを開き、[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)を備えたアカウントを使って [Azure portal にサインインします](https://portal.azure.com)。 次に、 **[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
2. **[管理]** メニュー オプションを探し、 **[Configure analytics (Preview)]\(分析の構成 (プレビュー)\)** を選択します。

3. **[Azure Information Protection ログ分析]** ブレードには、テナントによって所有されているすべての Log Analytics ワークスペースの一覧が表示されます。 次のいずれかの操作を行います。
    
    - 新しい Log Analytics ワークスペースを作成するには: **[新しいワークスペースの作成]** を選択し、 **[Log Analytics ワークスペース]** ブレードで、要求された情報を指定します。
    
    - 既存の Log Analytics ワークスペースを使用するには: 一覧からワークスペースを選択します。

Log Analytics ワークスペースの作成に関する情報については、「[Azure portal で Log Analytics ワークスペースを作成する](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)」を参照してください。

ワークスペースが構成されている場合は、次のいずれかの管理センターで機密ラベルを公開する場合は、次の手順を実行します。Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、Microsoft 365 コンプライアンスセンター:

- Azure portal で、[ **Azure Information Protection** > の**統合ラベル**の**管理** > ] にアクセスし、 **[発行]** を選択します。
    
    ラベル付けセンターでラベルの変更 (作成、変更、削除) を行うたびに、この**発行**オプションを選択します。 

これで、レポートを表示する準備ができました。

## <a name="how-to-view-the-reports"></a>レポートの表示方法

[Azure Information Protection] ブレードから **[ダッシュボード]** メニュー オプションを探し、次のいずれかのオプションを選択します。

- **使用状況レポート (プレビュー)** : ラベルがどのように使用されているかを確認するには、このレポートを使用します。

- **アクティビティ ログ (プレビュー)** : ユーザーからの、およびデバイスとファイル パス上でのラベル付けアクションを確認するには、このレポートを使用します。 さらに、保護されたドキュメントについては、Azure Information Protection クライアントがインストールされていない場合でも、組織の内部と外部の両方でユーザーのアクセス試行 (成功または拒否) を確認できます。
    
    このレポートには **[列]** オプションが備わっています。これを使うと、既定の表示よりも多くのアクティビティ情報を表示できます。 ファイルを選択して**アクティビティの詳細**を表示することで、ファイルの詳細を確認することもできます。

- **データ検出 (プレビュー)** : スキャナーとサポートされているエンドポイントによって検出されたラベル付きファイルに関する情報を表示するには、このレポートを使用します。
    
    ヒント:収集された情報から、認識してなかった場所や現時点ではスキャンされていない場所から機密情報が含まれているファイルにアクセスしているユーザーを発見することがあります。
    
    - 場所がオンプレミスの場合は、Azure Information Protection スキャナーの追加のデータ リポジトリとして、その場所を追加することを検討します。
    - 場所がクラウド上の場合は、Microsoft Cloud App Security を使用してそれらを管理することを検討します。 
    
- **推奨事項 (プレビュー)** : このレポートを使用すると、推奨事項に従って機密情報が含まれているファイルを識別し、リスクを軽減することができます。
    
    項目を選択すると、 **[データの表示]** オプションによって、推奨事項をトリガーした監査アクティビティが表示されます。


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>レポートを変更し、カスタム クエリを作成する方法

ダッシュボードでクエリ アイコンを選択して、 **[ログ検索]** ブレードを開きます。 

![Azure Information Protection のレポートをカスタマイズする [Log Analytics] アイコン](./media/log-analytics-icon.png)


ログに記録された Azure Information Protection のデータは、次のテーブルに格納されます: **InformationProtectionLogs_CL**

独自のクエリを作成する場合は、**InformationProtectionEvents** 関数として実装されているフレンドリ スキーマ名を使用します。 これらの関数は、カスタム クエリ用にサポートされている属性から派生し (一部の属性は内部使用のみ)、基になる属性が機能強化や新機能に対応するために変更された場合でも、それらの名前が変更されることはありません。

### <a name="friendly-schema-reference-for-event-functions"></a>イベント関数のフレンドリ スキーマ リファレンス

次の表を使用して、Azure Information Protection 分析のカスタム クエリで使用できるイベント関数のフレンドリ名を識別してください。

|列名|説明|
|-----------|-----------|
|アクセス権|保護されたドキュメントが正常に開かれました。ファイル名が追跡されている場合は、ファイル名で識別されます。追跡されていない場合は ID です。|
|AccessDenied|保護されたドキュメントが、追跡されている場合はファイル名で識別されるアクセスを拒否されました。追跡されていない場合は ID。|
|Time|イベント時間:形式の UTC (YYYY-MM-YYYY-MM-DDTHH: MM: SS)|
|ユーザー|ユーザー:UPN またはドメイン \ ユーザーの書式設定|
|ItemPath|アイテムの完全なパスまたは電子メールの件名|
|ItemName|ファイル名または電子メールの件名 |
|メソッド|ラベルの割り当て方法:手動、自動、推奨、既定、または必須|
|アクティビティ|監査アクティビティ:DowngradeLabel、UpgradeLabel、RemoveLabel、NewLabel、Discover、Access、RemoveCustomProtection、ChangeCustomProtection、または NewCustomProtection |
|LabelName|ラベル名 (ローカライズされていない)|
|LabelNameBefore |変更前のラベル名 (ローカライズされていない) |
|ProtectionType|保護の種類 [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID":"GUID" <br /> } <br />|
|保護の開始|変更前の保護の種類 [JSON] |
|Informationmatches の一致|[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)の JSON 配列が見つかりませんでした。空の配列は、情報の種類が見つからないことを意味し、null は使用できる情報がないことを意味します。|
|MachineName |FQDN (使用可能な場合)。それ以外のホスト名|
|DeviceRisk|WDATP からのデバイスのリスクスコア (利用可能な場合)|
|プラットフォーム|デバイスプラットフォーム (Win、OSX、Android、iOS) |
|ApplicationName|アプリケーションのフレンドリ名|
|AIPVersion|監査アクションを実行した Azure Information Protection クライアントのバージョン |
|TenantId|Azure AD テナント ID |
|AzureApplicationId|Azure AD 登録されたアプリケーション ID (GUID)|
|ProcessName|MIP SDK をホストするプロセス|
|LabelId|GUID または null のラベル|
|IsProtected|保護されているかどうか:はい/いいえ |
|ProtectionOwner |UPN 形式の Rights Management 所有者|
|Labの前に|GUID または null を変更する前に null を付ける|
|InformationTypesAbove55|信頼レベル55以上のデータで見つかった[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)の JSON 配列 |
|InformationTypesAbove65|信頼レベル65以上のデータで見つかった[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)の JSON 配列 |
|InformationTypesAbove75|信頼レベル75以上のデータで見つかった[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)の JSON 配列 |
|InformationTypesAbove85|信頼レベル85以上のデータで見つかった[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)の JSON 配列 |
|InformationTypesAbove95|信頼レベル95以上のデータで見つかった[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)の JSON 配列|
|DiscoveredInformationTypes |[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)の JSON 配列が、データと一致するコンテンツ (有効な場合) で見つかりました。空の配列は、情報の種類が見つからないことを意味し、null は使用できる情報がないことを意味します。 |
|ProtectedBefore|変更前にコンテンツが保護されていたかどうか。はい/いいえ |
|ProtectionOwnerBefore|変更前に所有者を Rights Management |
|UserJustification|ラベルをダウングレードまたは削除するときの理由|
|LastModifiedBy|ファイルを最後に変更したユーザー (UPN 形式)。 Office および SharePoint Online でのみ利用可能|
|LastModifiedDate|形式の UTC (YYYY-MM-YYYY-MM-DDTHH: MM: SS):Office & SharePoint Online のみで利用可能 |


#### <a name="examples-using-informationprotectionevents"></a>InformationProtectionEvents の使用例

次の例で、カスタム クエリを作成するフレンドリ スキーマを使用する方法を確認してください。

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>例 1: 過去 31 日間の監査データを送信したすべてのユーザーを返す 

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
レポートの情報を確認した後、Azure Information Protection クライアントを使用している場合は、Azure Information Protection ポリシーに変更を加えることができます。 手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。

Microsoft 365 のサブスクリプションがある場合は、Microsoft 365 コンプライアンス センターと Microsoft 365 セキュリティ センターでラベルの使用状況を表示することもできます。 詳しくは、「[ラベル分析によるラベル使用状況の表示](/Office365/SecurityCompliance/label-analytics)」をご覧ください。
