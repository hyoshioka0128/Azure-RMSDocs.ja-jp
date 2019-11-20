---
title: Azure Information Protection の中央レポート機能
description: 中央レポート機能を使用して、Azure Information Protection ラベルの導入を追跡し、機密情報を含むファイルを特定する方法
author: cabailey
ms.author: cabailey
ms.date: 11/19/2019
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: fbd1d4b2b25f9b681d0d25fac63038104bd4bb27
ms.sourcegitcommit: 13085ecbbd89193e949bd6cb49c448341911a972
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74189210"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure Information Protection の中央レポート機能

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> 現在のところ、この機能はプレビュー段階で、変更される可能性があります。

Use Azure Information Protection analytics for central reporting to help you track the adoption of your labels that classify and protect your organization's data. さらに

- ラベル付けされた保護の対象となるドキュメントと組織全体の電子メールを監視します。

- 組織内の機密情報が含まれているドキュメントを識別します。

- ラベル付きのドキュメントと電子メールに対するユーザーのアクセスを監視し、ドキュメントの分類の変更を追跡します。

- 保護されていないと組織をリスクにさらす可能性がある機密情報が含まれるドキュメントを識別し、次の推奨事項に従ってリスクを軽減します。

- Identify when protected documents are accessed by internal or external users from Windows computers, and whether access was granted or denied.

The data that you see is aggregated from your Azure Information Protection clients and scanners, from Microsoft Cloud App Security, from Windows 10 computers using Microsoft Defender Advanced Threat Protection, and from [protection usage logs](log-analyze-usage.md).

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
    
    - What labeling actions were performed by a specific application, such File Explorer and right-click, PowerShell, the scanner, or Microsoft Cloud App Security
    
    - Which protected documents were accessed successfully by users or denied access to users, even if those users don't have the Azure Information Protection client installed or are outside your organization

    - 報告されたファイルをドリルダウンして、追加情報の**アクティビティの詳細**を表示する

- **データ検出**レポートからは、次のことが確認できます。

    - What files are on your scanned data repositories, Windows 10 computers, or computers running the Azure Information Protection clients
    
    - ラベル付けされ、保護されているファイルと、ラベルごとのファイルの場所
    
    - 既知のカテゴリ (財務データや個人情報など) の機密情報が含まれるファイルと、これらのカテゴリごとのファイルの場所

- **推奨事項**レポートから次のことが確認できます。
    
    - 既知の種類の機密情報が含まれていて保護されていないファイルを識別します。 推奨事項に従えば、ご利用のラベルのいずれかによって自動ラベル付けまたは推奨ラベル付けを適用するための対応する条件をすぐに構成することができます。
        
        If you follow the recommendation: The next time the files are opened by a user or scanned by the Azure Information Protection scanner, the files can be automatically classified and protected.
    
    - 識別された機密情報が含まれているファイルが存在していて、Azure Information Protection によってスキャンされていないデータ リポジトリを特定します。 推奨事項に従えば、識別されたデータ ストアをご利用のスキャナーのプロファイルのいずれかにすぐに追加できます。
        
        If you follow the recommendation: On the next scanner cycle, the files can be automatically classified and protected.

レポートでは [Azure Monitor](/azure/log-analytics/log-analytics-overview) を使用して、ご自身の組織が所有している Log Analytics ワークスペースにデータを格納します。 クエリ言語に習熟している場合は、クエリを変更して、新しいレポートや Power BI ダッシュボードを作成できます。 You might find the following tutorial helpful to understand the query language: [Get started with Azure Monitor log queries](/azure/azure-monitor/log-query/get-started-queries).

詳細については、次のブログ記事を参照してください。 
- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) (Microsoft Information Protection を使用して、すべてのデータに対してデータ検出、レポート作成、および分析を行う)

- [Discover and protect sensitive data through Azure Information Protection and Microsoft Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>収集され Microsoft に送信される情報

これらのレポートを生成するため、エンドポイントでは次の種類の情報が Microsoft に送信されます。

- ラベル操作。 ラベルの設定、ラベルの変更、保護の追加または削除、自動ラベルと推奨ラベルなど。

- ラベル操作の前後のラベル名。

- 組織のテナント ID。

- ユーザー ID (電子メール アドレスまたは UPN)。

- ユーザーのデバイスの名前。

- ドキュメントの場合: ラベル付けされているドキュメントのファイル パスとファイル名。

- For emails: The email subject and email sender  for emails that are labeled. 

- コンテンツ内で検出された機密情報の種類 ([定義済み](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)およびカスタム)。

- Azure Information Protection クライアントのバージョン。

- クライアント オペレーティング システムのバージョン。

この情報は、ご自身の組織が所有している Azure Log Analytics ワークスペースに格納され、Azure Information Protection とは別に、このワークスペースへのアクセス権を持つユーザーが表示できます。 詳細については、「[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)」セクションをご覧ください。 ワークスペースへのアクセスの管理の詳細については、Azure ドキュメントの [Azure アクセス許可を使用した Log Analytics ワークスペースへのアクセスの管理](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)に関するセクションをご覧ください。

To prevent Azure Information Protection clients (classic) from sending this data, set the [policy setting](configure-policy-settings.md) of **Send audit data to Azure Information Protection analytics** to **Off**:

- ほとんどのユーザーがこのデータを送信し、ユーザーのサブセットが監査データを送信できない場合: 
    - Set **Send audit data to Azure Information Protection analytics** to **Off** in a scoped policy for the subset of users. この構成は、運用環境のシナリオに一般的なものです。

- ユーザーのサブセットだけが監査データを送信する場合: 
    - Set **Send audit data to Azure Information Protection analytics** to **Off** in the global policy, and **On** in a scoped policy for the subset of users. この構成は、テストのシナリオに一般的なものです。

To prevent Azure Information Protection unified clients from sending this data, configure a label policy [advanced setting](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics).

#### <a name="content-matches-for-deeper-analysis"></a>詳細な分析のためのコンテンツ一致

Azure Information Protection lets you collect and store the actual data that's identified as being a sensitive information type (predefined or custom). たとえば、これには検出されたクレジット カード番号だけでなく、社会保障番号、パスポート番号、銀行口座番号も含まれる場合があります。 The content matches are displayed when you select an entry from **Activity logs**, and view the **Activity Details**. 

By default, Azure Information Protection clients don't send content matches. To change this behavior so that content matches are sent:

- For the classic client, select a checkbox as part of the [configuration](#configure-a-log-analytics-workspace-for-the-reports) for Azure Information Protection analytics. The checkbox is named **Enable deeper analytics into your sensitive data**.
    
    If you want most users who are using this client to send content matches but a subset of users cannot send content matches, select the checkbox and then configure an [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) in a scoped policy for the subset of users.

- For the unified labeling client, configure an [advanced setting](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) in a label policy.

## <a name="prerequisites"></a>必要条件
Azure Information Protection レポートを表示し、独自のレポートを作成するには、次の要件を満たしていることを確認してください。

|要件|説明を見る|
|---------------|--------------------|
|Log Analytics を含む Azure サブスクリプションで、Azure Information Protection と同じテナント用のサブスクリプション|「[Azure Monitor の価格](https://azure.microsoft.com/pricing/details/log-analytics)」ページをご覧ください。<br /><br />Azure サブスクリプションをお持ちでない場合、または現在 Azure Log Analytics をご使用でない場合、価格ページには無料試用版へのリンクが含まれます。|
|For reporting information from labeling clients: <br /><br />- Azure Information Protection clients|Both the unified labeling client and the classic client are supported. <br /><br />If not already installed, you can download and install these clients from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|For reporting information from cloud-based data stores: <br /><br />- Microsoft Cloud App Security |To display information from Microsoft Cloud App Security, configure [Azure Information Protection integration](https://docs.microsoft.com/cloud-app-security/azip-integration).|
|For reporting information from on-premises data stores: <br /><br />- Azure Information Protection scanner |スキャナーのインストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。 |
|For reporting information from Windows 10 computers:  <br /><br />- Minimum build of 1809 with Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)|You must enable the Azure Information Protection integration feature from Microsoft Defender Security Center. For more information, see [Information protection in Windows overview](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure Information Protection 分析に必要なアクセス許可

Azure Information Protection 分析に固有の機能として、ご自身の Azure Log Analytics ワークスペースを構成した後、セキュリティ閲覧者の Azure AD 管理者ロールを、Azure portal で Azure Information Protection の管理をサポートしている他の Azure AD ロールの代替として使用することができます。

この機能は Azure 監視を使うため、Azure のロールベースのアクセス制御 (RBAC) でワークスペースへのアクセスを制御することもできます。 したがって、Azure Information Protection 分析を管理するためには、Azure ロールと Azure AD の管理者ロールが必要です。 Azure ロールを初めてご使用になる場合は、「[Azure RBAC ロールと Azure AD 管理者ロールの違い](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)」が役に立つ場合があります。

詳細:

1. One of the following [Azure AD administrator roles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) to access the Azure Information Protection analytics pane:
    
    - Log Analytics ワークスペースを作成する、またはカスタム クエリを作成するには:
    
        - **Azure Information Protection administrator**
        - **セキュリティ管理者**
        - **コンプライアンス管理者**
        - **Compliance data administrator**
        - **グローバル管理者**
    
    - After the workspace has been created, you can then use the following roles with fewer permissions to view the data collected:
    
        - **セキュリティ閲覧者**
        - **Global reader**
    
    > [!NOTE] 
    > You cannot use the Azure Information Protection administrator role or the Global reader role if your tenant is on the [unified labeling platform](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

2. さらに、自分の Azure Log Analytics ワークスペースにアクセスするには、次の [Azure Log Analytics ロール](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)または標準の [Azure ロール](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles)のいずれかが必要です。
    
    - ワークスペースを作成する、またはカスタム クエリを作成するには、次のいずれか:
    
        - **Log Analytics 共同作成者**
        - **共同作成者**
        - **所有者**
    
    - ワークスペースが作成された後は、アクセス許可がさらに少ない次のロールのいずれかを使用して、収集されたデータを表示できます。
    
        - **Log Analytics 閲覧者**
        - **閲覧者**

#### <a name="minimum-roles-to-view-the-reports"></a>レポートを表示するための最低限のロール

Azure Information Protection 分析のためにワークスペースを構成した後、Azure Information Protection 分析レポートを表示するために必要な最低限のロールは、次の両方です。

- Azure AD administrator role: **Security reader**
- Azure role: **Log Analytics Reader**

ただし、多くの組織での標準的なロールの割り当ては、Azure AD の**セキュリティ閲覧者**ロールと、Azure の**閲覧者**ロールです。

### <a name="storage-requirements-and-data-retention"></a>Storage requirements and data retention

The amount of data collected and stored in your Azure Information Protection workspace will vary significantly for each tenant, depending on factors such as how many Azure Information Protection clients and other supported endpoints you have, whether you're collecting endpoint discovery data, you've deployed scanners, the number of protected documents that are accessed, and so on.

However, as a starting point, you might find the following estimates useful:

- For audit data generated by Azure Information Protection clients only: 2 GB per 10,000 active users per month.

- For audit data generated by Azure Information Protection clients, scanners, and Microsoft Defender ATP: 20 GB per 10,000 active users per month.

If you use mandatory labeling or you've configured a default label for most users, your rates are likely to be significantly higher.

Azure Monitor Logs has a **Usage and estimated costs** feature to help you estimate and review the amount of data stored, and you can also control the data retention period for your Log Analytics workspace. For more information, see [Manage usage and costs with Azure Monitor Logs](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>レポート用に Log Analytics ワークスペースを構成する

1. まだそれを実行していない場合、新しいブラウザー ウィンドウを開き、[Azure Information Protection 分析に必要なアクセス許可](#permissions-required-for-azure-information-protection-analytics)を備えたアカウントを使って [Azure portal にサインインします](https://portal.azure.com)。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.
    
2. **[管理]** メニュー オプションを探し、 **[Configure analytics (Preview)]\(分析の構成 (プレビュー)\)** を選択します。

3. On the **Azure Information Protection log analytics** pane, you see a list of any Log Analytics workspaces that are owned by your tenant. 以下のいずれかを実行します。
    
    - To create a new Log Analytics workspace: Select **Create new workspace**, and on the **Log analytics workspace** pane, supply the requested information.
    
    - 既存の Log Analytics ワークスペースを使用するには、一覧からワークスペースを選択します。
    
    Log Analytics ワークスペースの作成に関する情報については、「[Azure portal で Log Analytics ワークスペースを作成する](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)」を参照してください。

4. If you have Azure Information Protection clients (classic), select the checkbox **Enable deeper analytics into your sensitive data** if you want to store the actual data that's identified as being a sensitive information type. For more information about this setting, see the [Content matches for deeper analysis](#content-matches-for-deeper-analysis) section on this page.

5. **[OK]** を選択します。

You're now ready to view the reports.

## <a name="how-to-view-the-reports"></a>レポートの表示方法

From the Azure Information Protection pane, locate the **Dashboards** menu options, and select one of the following options:

- **使用状況レポート (プレビュー)** : ラベルがどのように使用されているかを確認するには、このレポートを使用します。

- **アクティビティ ログ (プレビュー)** : ユーザーからの、およびデバイスとファイル パス上でのラベル付けアクションを確認するには、このレポートを使用します。 In addition, for protected documents, you can see access attempts (successful or denied) for users both inside and outside your organization, even if they don't have the Azure Information Protection client installed
    
    このレポートには **[列]** オプションが備わっています。これを使うと、既定の表示よりも多くのアクティビティ情報を表示できます。 ファイルを選択して**アクティビティの詳細**を表示することで、ファイルの詳細を確認することもできます。

- **Data discovery (Preview)** : Use this report to see information about labeled files found by scanners and supported endpoints.
    
    Tip: From the information collected, you might find users accessing files that contain sensitive information from location that you didn't know about or aren't currently scanning:
    
    - 場所がオンプレミスの場合は、Azure Information Protection スキャナーの追加のデータ リポジトリとして、その場所を追加することを検討します。
    - 場所がクラウド上の場合は、Microsoft Cloud App Security を使用してそれらを管理することを検討します。 
    
- **Recommendations (Preview)** : Use this report to identify files that have sensitive information and mitigate your risk by following the recommendations.
    
    項目を選択すると、 **[データの表示]** オプションによって、推奨事項をトリガーした監査アクティビティが表示されます。


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>レポートを変更し、カスタム クエリを作成する方法

Select the query icon in the dashboard to open a **Log Search** pane: 

![Azure Information Protection のレポートをカスタマイズする [Log Analytics] アイコン](./media/log-analytics-icon.png)


Azure Information Protection のログに記録されたデータは、テーブル **InformationProtectionLogs_CL** に格納されます。

独自のクエリを作成する場合は、**InformationProtectionEvents** 関数として実装されているフレンドリ スキーマ名を使用します。 これらの関数は、カスタム クエリ用にサポートされている属性から派生し (一部の属性は内部使用のみ)、基になる属性が機能強化や新機能に対応するために変更された場合でも、それらの名前が変更されることはありません。

### <a name="friendly-schema-reference-for-event-functions"></a>イベント関数のフレンドリ スキーマ リファレンス

次の表を使用して、Azure Information Protection 分析のカスタム クエリで使用できるイベント関数のフレンドリ名を識別してください。

|列名|[説明]|
|-----------|-----------|
|［時間］|Event time: UTC in format YYYY-MM-DDTHH:MM:SS|
|User|User: Format UPN or DOMAIN\USER|
|ItemPath|Full item path or email subject|
|ItemName|File name or email subject |
|認証方法|Label assigned method: Manual, Automatic, Recommended, Default, or Mandatory|
|作業内容|Audit activity: DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, Discover, Access, RemoveCustomProtection, ChangeCustomProtection, or NewCustomProtection |
|LabelName|Label name (not localized)|
|LabelNameBefore |Label name before change (not localized) |
|ProtectionType|Protection type [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|ProtectionBefore|Protection type before change [JSON] |
|MachineName |FQDN when available; otherwise host name|
|DeviceRisk|Device risk score from WDATP when available|
|プラットフォーム|Device platform (Win, OSX, Android, iOS) |
|ApplicationName|Application friendly name|
|AIPVersion|Version of the Azure Information Protection client that performed the audit action |
|TenantId|Azure AD テナント ID |
|AzureApplicationId|Azure AD registered application ID (GUID)|
|ProcessName|Process that hosts MIP SDK|
|LabelId|Label GUID or null|
|IsProtected|Whether protected: Yes/No |
|ProtectionOwner |Rights Management owner in UPN format|
|LabelIdBefore|Label GUID or null before change|
|InformationTypesAbove55|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 55 or above |
|InformationTypesAbove65|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 65 or above |
|InformationTypesAbove75|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 75 or above |
|InformationTypesAbove85|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 85 or above |
|InformationTypesAbove95|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 95 or above|
|DiscoveredInformationTypes |JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data and their matched content (if enabled) where an empty array means no information types found, and null means no information available |
|ProtectedBefore|Whether the content was protected before change: Yes/No |
|ProtectionOwnerBefore|Rights Management owner before change |
|UserJustification|Justification when downgrading or removing label|
|LastModifiedBy|User in UPN format who last modified the file. Available for Office and SharePoint Online only|
|LastModifiedDate|UTC in format YYYY-MM-DDTHH:MM:SS: Available for Office & SharePoint Online only |


#### <a name="examples-using-informationprotectionevents"></a>InformationProtectionEvents の使用例

次の例で、カスタム クエリを作成するフレンドリ スキーマを使用する方法を確認してください。

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>Example 1: Return all users who sent audit data in the last 31 days 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>Example 2: Return the number of labels that were downgraded per day in the last 31 days 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>Example 3: Return the number of labels that were downgraded from Confidential by user, in the last 31 days 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

この例では、アクション前のラベルの名前に **Confidential** (社外秘) が含まれ、アクション後の名前に **Confidential** が含まれていない場合のみ、ダウングレードされたラベルとしてカウントされます。 


## <a name="next-steps"></a>次のステップ
After reviewing the information in the reports, if you are using the Azure Information Protection client, you might decide to make changes to your Azure Information Protection policy. 手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。

Microsoft 365 のサブスクリプションがある場合は、Microsoft 365 コンプライアンス センターと Microsoft 365 セキュリティ センターでラベルの使用状況を表示することもできます。 詳しくは、「[ラベル分析によるラベル使用状況の表示](/microsoft-365/compliance/label-analytics)」をご覧ください。
