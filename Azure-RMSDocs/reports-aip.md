---
title: Azure Information Protection の中央レポート機能
description: 中央レポート機能を使用して、Azure Information Protection ラベルの導入を追跡し、機密情報を含むファイルを特定する方法
author: cabailey
ms.author: cabailey
ms.date: 02/15/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 54a18f52a3b1cd5656d1d2c3cfbd675062b06c47
ms.sourcegitcommit: 95b7df32ecccdab4b80bc3a9f6433dc1c33dbbc5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2019
ms.locfileid: "56407727"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure Information Protection の中央レポート機能

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> 現在のところ、この機能はプレビュー段階で、変更される可能性があります。

Azure Information Protection 分析を使って、中央レポート機能に Azure Information Protection ラベルの導入を追跡させます。 さらに

- ラベル付きのドキュメントや電子メールへのユーザーのアクセスと、その分類に対する変更を監視します。 

- 保護する必要がある機密情報が含まれているドキュメントを識別します。

現在、表示されるデータは、Azure Information Protection クライアントと Azure Information Protection スキャナー、および [Windows Defender Advanced Threat Protection (Windows Defender ATP)](/windows/security/threat-protection/windows-defender-atp/overview) を実行している Windows コンピューターから集計されたものです。

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

- **データ検出**レポートからは、次のことが確認できます。

    - スキャンされたデータ リポジトリ、または Windows 10 コンピューター上にあるファイル
    
    - ラベル付けされ、保護されているファイルと、ラベルごとのファイルの場所
    
    - 既知のカテゴリ (財務データや個人情報など) の機密情報が含まれるファイルと、これらのカテゴリごとのファイルの場所
    
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

- 電子メールの場合: 電子メールの件名、電子メールの送信者、ラベル付けされた電子メールの受信者。 

- コンテンツ内で検出された機密情報の種類 ([定義済み](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)およびカスタム)。

- Azure Information Protection クライアントのバージョン。

- クライアント オペレーティング システムのバージョン。

この情報は、ご自身の組織が所有している Azure Log Analytics ワークスペースに格納され、このワークスペースへのアクセス権を持つユーザーが表示できます。 ワークスペースに対するアクセスの構成について詳しくは、Azure ドキュメントの「[アカウントとユーザーの管理](/azure/azure-monitor/platform/manage-access#manage-accounts-and-users)」セクションをご覧ください。

> [!NOTE]
> Azure Information Protection の Azure Log Analytics ワークスペースには、ドキュメントのコンテンツの一致に関するチェック ボックスが含まれています。 このチェック ボックスをオンにすると、機密情報の種類またはカスタム条件によって識別された実際のデータも収集されます。 たとえば、これには検出されたクレジット カード番号だけでなく、社会保障番号、パスポート番号、銀行口座番号も含まれる場合があります。 このデータを収集したくない場合は、このチェック ボックスをオンにしないでください。
>
> 現時点では、この情報はレポートに表示されませんが、クエリで表示および取得することはできます。

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Azure Information Protection 分析の前提条件
Azure Information Protection レポートを表示し、独自のレポートを作成するには、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|Log Analytics を含む Azure サブスクリプション|「[Azure Monitor の価格](https://azure.microsoft.com/pricing/details/log-analytics)」ページをご覧ください。<br /><br />Azure サブスクリプションをお持ちでない場合、または現在 Azure Log Analytics をご使用でない場合、価格ページには無料試用版へのリンクが含まれます。|
|Azure Information Protection クライアントの現在の一般公開バージョンまたはプレビュー バージョン|このクライアントをまだインストールしていない場合は、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードしてインストールできます。|
|**検出とリスク** レポートの場合: <br /><br />- オンプレミスのデータ ストアからのデータを表示するには、Azure Information Protection スキャナー (現在の一般公開バージョンまたはプレビュー バージョン) のインスタンスを少なくとも 1 つデプロイしていること <br /><br />- Windows 10 コンピューターからのデータを表示するには、それがビルド 1809 以降であり、Windows Defender Advanced Threat Protection (Windows Defender ATP) を使っていて、Windows Defender セキュリティ センターから Azure Information Protection の統合機能を有効にしていること|スキャナーのインストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。 スキャナーの以前のバージョンからアップグレードする場合は、「[Azure Information Protection スキャナーのアップグレード](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)」を参照してください。<br /><br />Windows Defender セキュリティ センターから Azure Information Protection の統合機能を構成および使用する方法について詳しくは、「[Information protection in Windows overview](/windows/security/threat-protection/windows-defender-atp/information-protection-in-windows-overview)」(Windows での情報保護の概要) をご覧ください。|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure Information Protection 分析に必要なアクセス許可

Azure Information Protection 分析に固有の機能として、セキュリティ閲覧者の Azure AD 管理者ロールを、Azure Information Protection の管理をサポートしている他の Azure AD ロールの代替として使用することができます。

この機能は Azure Log Analytics を使うため、Azure のロールベースのアクセス制御 (RBAC) によってもワークスペースへのアクセスを制御できます。 Azure ロールを初めてご使用になる場合は、「[Azure RBAC ロールと Azure AD 管理者ロールの違い](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)」が役に立つ場合があります。

詳細:

1. Azure portal で Azure Information Protection の分析ブレードにアクセスするには、次の [Azure AD の管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)のいずれかを持っている必要があります。
    
    - **Information Protection 管理者**
    
    - **セキュリティ閲覧者**
  
   - **セキュリティ管理者**
    
    - **グローバル管理者**
    
    > [!NOTE] 
    > テナントが統合ラベル付けストアに移行されている場合、ご自分のアカウントはグローバル管理者であるか、リストされたロールのいずれかに加えて Office 365 セキュリティ/コンプライアンス センターに対するアクセス権を持っている必要があります。 [詳細情報](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. Azure Log Analytics を使うには、次の [Azure Log Analytics ロール](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#managing-access-to-log-analytics-using-azure-permissions)、または標準の [Azure ロール](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments)のいずれかを持っている必要があります:
    
    - Log Analytics ワークスペースを作成する、またはカスタム クエリを作成する場合は、次のいずれか:
    
        - **Log Analytics 共同作成者**
        - Azure ロール:**所有者**または**共同作成者**
    
    - 別の管理者が作成した Log Analytics ワークスペースのデータを表示するには:
    
        - **Log Analytics 閲覧者**
        - Azure ロール:**閲覧者**

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>レポート用に Log Analytics ワークスペースを構成する

1. まだそれを実行していない場合、新しいブラウザー ウィンドウを開き、[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)を備えたアカウントを使って [Azure portal にサインインします](https://portal.azure.com)。 次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
2. **[管理]** メニュー オプションを探し、**[Configure analytics (Preview)]\(分析の構成 (プレビュー)\)** を選択します。

3. **[Azure Information Protection ログ分析]** ブレードには、テナントによって所有されているすべての Log Analytics ワークスペースの一覧が表示されます。 以下のいずれかを実行します。
    
    - 新しい Log Analytics ワークスペースを作成するには: **[新しいワークスペースの作成]** を選択し、**[Log Analytics ワークスペース]** ブレードで、要求された情報を指定します。
    
    - 既存の Log Analytics ワークスペースを使用するには: 一覧からワークスペースを選択します。

Log Analytics ワークスペースの作成に関する情報については、「[Azure portal で Log Analytics ワークスペースを作成する](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)」を参照してください。

ワークスペースが構成されている場合は、レポートを表示する準備ができています。

## <a name="how-to-view-the-reports"></a>レポートの表示方法

[Azure Information Protection] ブレードから **[ダッシュボード]** メニュー オプションを探し、次のいずれかのオプションを選択します。

- **使用状況レポート (プレビュー)**: ラベルがどのように使用されているかを確認するには、このレポートを使用します。 

- **アクティビティ ログ (プレビュー)**: ユーザーからの、およびデバイスとファイル パス上でのラベル付けアクションを確認するには、このレポートを使用します。
    
    このレポートには **[列]** オプションが備わっています。これを使うと、既定の表示よりも多くのアクティビティ情報を表示できます。

- **データ検出 (プレビュー)**: スキャナーまたは Windows Defender ATP によって検出されたファイルに関する情報を表示するには、このレポートを使用します。

> [!NOTE]
> 現在、送信元オペレーティング システムのロケールが英語の場合、パスおよびファイル名に含まれる非 ASCII 文字が疑問符 (**?**) で表示されるという既知の問題があります。

## <a name="how-to-modify-the-reports"></a>レポートを変更する方法

ダッシュボードでクエリ アイコンを選択して、**[ログ検索]** ブレードを開きます。 

![Azure Information Protection のレポートをカスタマイズする [Log Analytics] アイコン](./media/log-analytics-icon.png)


ログに記録された Azure Information Protection のデータは、次のテーブルに格納されます: **InformationProtectionLogs_CL**

## <a name="next-steps"></a>次の手順
レポートの情報を確認した後で、Azure Information Protection ポリシーを変更することがあります。 手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。
