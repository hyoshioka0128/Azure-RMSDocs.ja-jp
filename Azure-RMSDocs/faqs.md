---
title: Azure Information Protection に関してよく寄せられる質問
description: Some frequently asked questions about Azure Information Protection and its protection service, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: f4583260708267575f35d4c67d6cd2afc5add68d
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474339"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure Information Protection に関してよく寄せられる質問

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection、または Azure Rights Management サービス (Azure RMS) に関して質問がございますか。 ここで回答を探してみてください。

これらの FAQ ページは定期的に更新されます。新しい情報は [Azure Information Protection 技術ブログ](https://aka.ms/AIPblog)上の月次のドキュメント更新発表に一覧表示されます。

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Azure Information Protection と Microsoft Information Protection の違いは何ですか。

Azure Information Protection とは異なり、Microsoft Information Protection は購入できるサブスクリプションや製品ではありません。 そうではなく、これは組織の機密情報を保護するのに役立つ製品および統合された機能のフレームワークです。

- このフレームワークに含まれる個々の製品には、Azure Information Protection、Office 365 Information Protection (たとえば Office 365 DLP)、Windows Information Protection、Microsoft Cloud App Security などがあります。 

- このフレームワークに含まれる統合された機能としては、統合ラベルの管理、Office アプリに組み込みのエンド ユーザーのラベル付けエクスペリエンス、Windows で統合ラベルを使用したりデータに保護を適用したりする機能、Microsoft Information Protection SDK、ラベル付けされた PDF と保護された PDF を表示する Adobe Acrobat Reader の新機能などがあります。

詳細については、「[Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)」(機密データを保護するために使用できる情報保護機能の発表) をご覧ください。

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Azure Information Protection のラベルと Office 365 のラベルにはどのような違いがありますか。

当初は、Office 365 には[保有期間ラベル](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30)のみがあり、ドキュメントおよび電子メールのコンテンツが Office 365 サービス内にある場合に、それらを分類して監査および保持することができました。 これに対して、Azure Information Protection のラベルでは、ドキュメントおよび電子メールがオンプレミスのものであるかクラウド内のものであるかに関係なく、ドキュメントと電子メールに対して一貫性のある分類および保護ポリシーを適用できます。

Announced at Microsoft Ignite 2018 in Orlando, you now have an option to create and configure [sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) in addition to retention labels in one of the admin centers: The Office 365 Security & Compliance Center, the Microsoft 365 security center, or the Microsoft 365 compliance center. You can migrate your existing Azure Information Protection labels to the new unified labeling store, to be used as sensitivity labels with Office apps. 

統合ラベル付けの管理と各ラベルのサポート方法について詳しくは、ブログ記事「[Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)」 (機密データの保護に役立つ情報保護機能の可用性の発表) をご覧ください。

For more information about migrating your existing labels, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>How can I determine if my tenant is on the unified labeling platform?

When your tenant is on the unified labeling platform, sensitivity labels can be used by [clients and services that support unified labeling](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling). If you obtained your subscription for Azure Information Protection in June 2019 or later, your tenant is automatically on the unified labeling platform and no further action is needed. Your tenant might also be on this platform because somebody migrated your Azure Information Protection labels.

To check the status, in the Azure portal, go to **Azure Information Protection** > **Manage** > **Unified labeling**, and view the status of **Unified labeling**:

- If you see **Activated**, your tenant is on the unified labeling platform.

- If you see **Not activated**, your tenant is not on the unified labeling platform. For migration instructions, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>What's the difference between the Azure Information Protection client and the Azure Information Protection unified labeling client?

The **Azure Information Protection client (classic)** has been available since Azure Information Protection was first announced as a new service for classifying and protecting files and emails. This client downloads labels and policy settings from Azure, and you configure the Azure Information Protection policy from the Azure portal. For more information, see [Overview of the Azure Information Protection policy](overview-policy.md). 

The **Azure Information Protection unified labeling client** is a more recent addition, to support the unified labeling store that multiple applications and services support. This client downloads sensitivity labels and policy settings from the following admin centers: The Office 365 Security & Compliance Center, the Microsoft 365 security center, and the Microsoft 365 compliance center. For more information, see [Overview of sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels).

If you're not sure which client to use, see [Choose which Azure Information Protection client to use](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

### <a name="identify-which-client-you-have-installed"></a>Identify which client you have installed

Both clients, when they are installed, display **Azure Information Protection**. To help you identify which client you have installed, use the **Help and feedback** option to open the **Microsoft Azure Information Protection** dialog box:

- エクスプローラーから単一ファイル、複数ファイル、またはフォルダーを右クリックで選択し、 **[分類して保護する]** 、 **[ヘルプとフィードバック]** の順に選択します。

- From an Office application: From the **Protect** button (the classic client) or **Sensitivity** button (unified labeling client), select **Help and Feedback**.

Use the **Version** number displayed to identify the client:

- A version **1**, for example, **1.53.10.0**, identifies the Azure Information Protection client (classic).

- A version **2**, for example, **2.2.14.0**, identifies the Azure Information Protection unified labeling client.

## <a name="when-is-the-right-time-to-migrate-my-labels"></a>When is the right time to migrate my labels?

Now that the option to migrate labels in the Azure portal is in general availability, we recommend you activate the migration so that you can use your labels as sensitivity labels with [clients and services that support unified labeling](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

For more information and instructions, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>ラベルを移行した後に使用する管理ポータルはどれですか。

Azure portal でラベルを移行した場合:

- If you have [unified labeling clients and services](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling), go to one of the admin centers (Office 365 Security & Compliance Center, Microsoft 365 security center, or Microsoft 365 compliance center) to publish these labels, and to configure their policy settings. 転送されるラベル変更には、いずれかの管理センターを使用します。 統合ラベル付けのクライアントは、これらの管理センターからラベルとポリシー設定をダウンロードします。

- If you have the [Azure Information Protection client (classic)](./rms-client/aip-client.md), continue to use the Azure portal to edit your labels and policy settings. The classic client continues to download labels and policy settings from Azure.

- If you have both [unified labeling clients](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) and [classic clients](./rms-client/aip-client.md), you can use the admin centers or the Azure portal to make label changes. However, for the classic clients to pick up the label changes that you make in the admin centers, you must return to the Azure portal: Use the **Publish** option from the **Azure Information Protection - Unified labeling** pane in the Azure portal. 

[中央レポート機能](reports-aip.md)と[スキャナー](deploy-aip-scanner.md)には、引き続き Azure portal を使用します。

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure Information Protection と Azure Rights Management の違いは何ですか。

Azure Information Protection では、組織の文書や電子メールを分類、ラベル付け、保護できます。 保護テクノロジでは、Azure Information Protection のコンポーネントになった、Azure Rights Management サービスが利用されます。

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>What's the role of identity management for Azure Information Protection?

Azure Information Protection で保護されたコンテンツにアクセスするには、有効なユーザー名とパスワードが必要です。 Azure Information Protection でデータを保護するしくみについての詳細は、「[データのセキュリティ保護における Azure Information Protection の役割](/enterprise-mobility-security/solutions/azure-information-protection-securing-data)」をご覧ください。 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。

「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)」ページのサブスクリプション情報と機能一覧を参照してください。

Azure Rights Management データ保護を含む Office 365 サブスクリプションをお持ちの場合は、[Azure Information Protection ライセンス データシート](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)をダウンロードしてください。

ライセンスについてまだご質問がありますか。 [ライセンスについてよく寄せられる質問](https://azure.microsoft.com/pricing/details/information-protection#faq)のセクションで回答されているかどうかを確認してください。

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Azure Information Protection client は分類とラベル付けを含むサブスクリプション用のみでしょうか。

いいえ。 The Azure Information Protection client (classic) can also be used with subscriptions that include just the Azure Rights Management service to protect data.

When the classic client is installed and it doesn't have an Azure Information Protection policy, this client automatically operates in [protection-only mode](./rms-client/client-protection-only-mode.md). このモードでは、ユーザーは Rights Management テンプレートとカスタム アクセス許可に簡単に適用できます。 分類とラベル付けを含むサブスクリプションを後で購入した場合、Azure Information Protection ポリシーをダウンロードする際に、クライアントは自動的に標準モードへと切り替わります。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Azure Information Protection を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?

Office 365 テナントまたは Azure AD テナントのグローバル管理者は、Azure Information Protection のすべての管理タスクを実行できます。 ただし、管理アクセス許可を他のユーザーに割り当てる場合は、次のオプションがあります。

- **Azure Information Protection administrator**: This Azure Active Directory administrator role lets an administrator configure Azure Information Protection but not other services. この役割を持つ管理者は、Azure Rights Management 保護サービスのアクティブ化と非アクティブ化、保護設定とラベルの構成、Azure Information Protection ポリシーの構成を行うことができます。 In addition, an administrator with this role can run all the PowerShell cmdlets for the [Azure Information Protection client](./rms-client/client-admin-guide-powershell.md) and from the [AIPService module](administer-powershell.md). However, this role doesn't support tracking and revoking documents for users.
    
    > [!NOTE]
    > This role is not supported in the Azure portal if your tenant is on the [unified labeling platform](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).
    
    ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。

- **Compliance administrator** or **Compliance data administrator**: These Azure Active Directory administrator roles let an administrator configure Azure Information Protection, which includes activate and deactivate the Azure Rights Management protection service, configure protection settings and labels, and configure the Azure Information Protection policy. In addition, an administrator with either of these roles can run all the PowerShell cmdlets for the [Azure Information Protection client](./rms-client/client-admin-guide-powershell.md) and from the [AIPService module](administer-powershell.md). However, these roles don't support tracking and revoking documents for users.
    
    To assign a user to one of these administrative roles, see [Assign a user to administrator roles in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). To see what other permissions a user with these roles have, see the [Available roles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) section from the Azure Active Directory documentation.

- **Security reader** or **Global reader**: For [Azure Information Protection analytics](reports-aip.md) only. この Azure Active Directory の管理者ロールを持っている管理者は、ご自身のラベルの使用方法を確認したり、ラベル付きのドキュメントやメールに対するユーザー アクセスや、各分類への変更を監視したり、保護する必要がある機密情報を含んでいるドキュメントを識別したりできます。 Because this feature uses Azure Monitor, you must also have a supporting [RBAC role](reports-aip.md#permissions-required-for-azure-information-protection-analytics).
    
    > [!NOTE]
    > The Security reader and Global reader roles are not supported if your tenant is on the [unified labeling platform](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

- **Security administrator**: This Azure Active Directory administrator role lets an administrator configure Azure Information Protection in the Azure portal, in addition to configuring some aspects of other Azure services. An administrator with this role cannot run any of the [PowerShell cmdlets from the AIPService module](administer-powershell.md), or track and revoke documents for users.
    
    ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。 この役割のユーザーが持つその他のアクセス許可を確認するには、Azure Active Directory ドキュメントの「[使用可能なロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles)」セクションを参照してください。

- Azure Rights Management **Global Administrator** and **Connector Administrator**: For these Azure Rights Management administrator roles, the first grants users permissions to run all [PowerShell cmdlets from the AIPService module](administer-powershell.md) without making them a global administrator for other cloud services, and the second role grants permissions to run only the Rights Management (RMS) connector. Neither of these administrative roles grant permissions to management consoles or tracking and revoking documents for users.
    
    To assign either of these administrative roles, use the AIPService PowerShell cmdlet, [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator).

注意事項:

- Microsoft accounts are not supported for delegated administration of Azure Information Protection, even if these accounts are assigned to one of the administrative roles listed. 

- [オンボーディング コントロール](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成してある場合は、RMS コネクタを除き、Azure Information Protection を管理する機能に影響はありません。 たとえば、コンテンツを保護する機能を "IT department" グループに制限するようにオンボーディング コントロールが構成されている場合、RMS コネクタのインストールと構成に使用するアカウントは、そのグループのメンバーである必要があります。 

- 管理者ロールが割り当てられているユーザーは、Azure Information Protection によって保護されたドキュメントやメールから保護を自動的に削除することはできません。 スーパー ユーザーを割り当てられたユーザーだけが、スーパー ユーザー機能が有効になっているときにのみ、この操作を行うことができます。 ただし、Azure Information Protection への管理アクセス許可を割り当てたすべてのユーザーが、各自のアカウントなど、ユーザーにスーパー ユーザーを割り当てることができます。 また、スーパー ユーザー機能を有効にすることもできます。 これらのアクションは、管理者ログに記録されます。 For more information, see the security best practices section in [Configuring super users for Azure Information Protection and discovery services or data recovery](configure-super-users.md). 

- If you are migrating your Azure Information Protection labels to the unified labeling store, be sure to read the following section from the label migration documentation: [Administrative roles that support the unified labeling platform](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection はオンプレミスおよびハイブリッドのシナリオをサポートしますか?

○ Azure Information Protection はクラウドベースのソリューションですが、クラウドだけでなく、オンプレミスに保存されているドキュメントや電子メールの分類、ラベル付け、および保護が可能です。

Exchange Server、SharePoint Server、および Windows ファイル サーバーがある場合は、これらのオンプレミス サーバーで Azure Rights Management サービスを使用して電子メールやドキュメントを保護できるように、[Rights Management コネクタ](deploy-rms-connector.md)をデプロイすることができます。 また、Active Directory ドメイン コントローラーを Azure AD と同期し、連携することで、たとえば [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect) を使用して、よりシームレスな認証方法をユーザーに提供できます。

必要に応じて、Azure Rights Management サービスで XrML 証明書の生成と管理が自動的に行われるので、オンプレミスの PKI は使用されません。 Azure Rights Management での証明書の使用方法については、記事「[Azure RMS の機能の詳細](./how-does-it-work.md)」の「[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」セクションを参照してください。

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Azure Information Protection ではどのようなデータの種類を分類し、保護できますか?

Azure Information Protection では、メール メッセージやドキュメントがオンプレミスまたはクラウドのどちらに配置されていても、それらを分類し、管理することができます。 これらのドキュメントには、Word ドキュメント、Excel スプレッドシート、PowerPoint プレゼンテーション、PDF ドキュメント、テキストベースのファイル、および画像ファイルが含まれます。 サポートされるドキュメントの種類の一覧については、管理者ガイドの[サポートされているファイルの種類](./rms-client/clientv2-admin-guide-file-types.md)の一覧を参照してください。

Azure Information Protection cannot classify and protect structured data such as database files, calendar items, Yammer posts, Sway content, and OneNote notebooks.

**Newly announced in preview**: Power BI now supports classification by using sensitivity labels and can apply protection from those labels to data that is exported to the following file formats: .pdf, .xls, and .ppt. For more information, see [Data protection in Power BI (preview)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview).

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>条件付きアクセスに利用できるクラウド アプリとして Azure Information Protection が一覧に記載されています。これはどのように動作しますか。

はい。プレビュー オファリングとして、Azure Information Protection に Azure AD 条件付きアクセスを構成できるようになりました。

Azure Information Protection で保護されているドキュメントをユーザーが開くとき、標準的な条件付きアクセス コントロールに基づき、管理者は自分のテナントでユーザーをブロックするか、アクセス許可を与えることができるようになりました。 最も一般的に要求される条件の 1 つが多要素認証 (MFA) を要求することです。 もう 1 つは、デバイスが [Intune ポリシーに準拠する](/intune/conditional-access-intune-common-ways-use)必要があるということです (たとえば、モバイル デバイスがパスワード要件やオペレーティング システムの最小バージョンを満たすようにする)。また、コンピューターはドメインに参加する必要があります。

チュートリアル形式の例が必要であれば、ブログ投稿の「[Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/)」 (Azure Information Protection の条件付きアクセス ポリシー) を参照してください。

追加情報:

- Windows コンピューターの場合: 現行プレビュー リリースの場合、[ユーザー環境が初期化](./how-does-it-work.md#initializing-the-user-environment) (このプロセスはブートストラップとも呼ばれています) されたときに Azure Information Protection の条件付きアクセス ポリシーが評価され、その後、30 日おきに評価されます。

- 条件付きアクセス ポリシーの評価頻度を微調整することもできます。 この微調整は、トークンの有効期間を構成することで実行できます。 詳細については、「[Azure Active Directory における構成可能なトークンの有効期間](/azure/active-directory/active-directory-configurable-token-lifetimes)」を参照してください。

- We recommend that you do not add administrator accounts to your conditional access policies because these accounts will not be able to access the Azure Information Protection pane in the Azure portal.

- 他の組織とのコラボレーション (B2B) のための条件付きアクセス ポリシーで MFA を使用する場合は、[Azure AD B2B コラボレーション](/azure/active-directory/b2b/what-is-b2b)を使用して、他の組織と共有するユーザーのためのゲスト アカウントを作成する必要があります。

- 2018 年 12 月の Azure AD プレビュー リリースでは、ユーザーが保護されたドキュメントを初めて開く前に、ユーザーに使用条件への同意を求めることができるようになりました。 For more information, see the following blog post announcement: [Updates to Azure AD Terms of Use functionality within conditional access](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822)

- 多くのクラウド アプリで条件付きアクセスを使用する場合、選択対象の一覧に **Microsoft Azure Information Protection** が表示されないことがあります。 その場合、一覧の上にある検索ボックスを使用します。 「Microsoft Azure Information Protection」と入力し、利用可能アプリを絞り込みます。 サポートされているサブスクリプションがある場合、選択対象として **Microsoft Azure Information Protection** が表示されます。 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Azure Information Protection が Microsoft Graph Security のセキュリティ プロバイダーとして記載されています。これはどのように動作しますか? また、どのようなアラートを受信できますか?

はい。公共プレビュー サービスとして、**Azure Information Protection の異常なデータ アクセス**に対するアラートを受信できるようになりました。 Azure Information Protection によって保護されているデータに対する異常なアクセスの試行があると、このアラートがトリガーされます。 たとえば、異常に大量のデータへのアクセス、不自然な時間帯でのアクセス、または不明な場所からのアクセスなどです。

このようなアラートは、データ関連の高度な攻撃や、環境内部の脅威を検出するのに役立ちます。 これらのアラートでは、保護されたデータにアクセスするユーザーの動作をプロファイルするために機械学習が使用されます。 

Azure Information Protection のアラートにアクセスするには、[Microsoft Graph Security API を使用します](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/security-api-overview)。または、Azure Monitor を使用して、Splunk や IBM Qradar などの SIEM ソリューションに[アラートをストリームする](https://developer.microsoft.com/graph/docs/concepts/security_siemintegration)ことができます。

Microsoft Graph Security API について詳しくは、「[Microsoft Graph Security API の概要](https://developer.microsoft.com/graph/docs/concepts/security-concept-overview)」をご覧ください。

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Windows Server FCI と Azure Information Protection スキャナーの違い

[Rights Management コネクタ](deploy-rms-connector.md) (Office ドキュメントのみ) や [PowerShell スクリプト](./rms-client/configure-fci.md) (すべてのファイルの種類) を使用してドキュメントを分類して保護するために、これまでは Windows Server ファイル分類インフラストラクチャが選択されてきました。 

これからは、[Azure Information Protection スキャナー](deploy-aip-scanner.md)の使用をお勧めします。 スキャナーは Azure Information Protection クライアントと Azure Information Protection ポリシーを使用して、ドキュメント (すべてのファイルの種類) にラベルを付けるため、これらのドキュメントは分類され、必要に応じて保護されます。

この 2 つのトポロジの主な違いを次に示します。

|Windows Server FCI|Azure Information Protection スキャナー|
|--------------------------------|-------------------------------------|
|サポートされるデータ ストア: <br /><br />- Windows Server のローカル フォルダー|サポートされるデータ ストア: <br /><br />- Windows Server のローカル フォルダー<br /><br />- Windows ファイル共有とネットワーク接続ストレージ<br /><br />- SharePoint Server 2016 と SharePoint Server 2013。 [このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様向けに SharePoint Server 2010 もサポートされています。|
|操作モード: <br /><br />- リアルタイム|操作モード: <br /><br />- 体系的にデータ ストアをクロールします。このサイクルは 1 回のみまたは繰り返し実行できます|
|ファイルの種類ごとのサポート: <br /><br />- すべてのファイルの種類が既定で保護されます <br /><br />- レジストリを編集することで、特定のファイルの種類を保護から除外できます|ファイルの種類ごとのサポート: <br /><br />- Office ファイルの種類と PDF ドキュメントは既定で保護されます <br /><br />- レジストリを編集することで、保護に含めるファイルの種類を追加できます|

There is a difference in setting the [Rights Management owner](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) for files that are protected on a local folder or network share. 既定では、どちらのソリューションでも、Rights Management の所有者は、ファイルを保護するアカウントに設定されますが、この設定をオーバーライドすることができます。

- Windows Server FCI の場合: すべてのファイルに対して単一アカウントとなるように Rights Management 所有者を設定したり、各ファイルの Rights Management 所有者を動的に設定したりすることができます。 Rights Management 所有者を動的に設定するには、 **-OwnerMail [ソース ファイルの所有者の電子メール]** パラメーターと値を使用します。 この構成では、ファイルの所有者プロパティのユーザー アカウント名を使用して、Active Directory からユーザーのメール アドレスを取得します。

- For the Azure Information Protection scanner: For newly protected files, you can set the Rights Management owner to be a single account for all files on a specified data store, but you cannot dynamically set the Rights Management owner for each file. 以前から保護されていたファイルについては、Rights Management 所有者は変更されません。 新しく保護されるファイルに対してアカウントを設定するには、スキャナー プロファイルで **-Default owner** 設定を指定します。 

スキャナーで SharePoint サイトおよびライブラリのファイルを保護する場合、Rights Management 所有者は SharePoint エディターの値を使用して、ファイルごとに動的に設定されます。

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>新しいリリースが Azure Information Protection ですぐに利用できるようになると聞きました。いつリリースされますか?

技術文書には今後のリリースに関する情報は含まれません。 For this type of information, use the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent), check the [Enterprise Mobility + Security Blog](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>自分の国に Azure Information Protection は適していますか?

国によって、さまざまな要件と規制があります。 組織のこの質問に対する回答は、[国ごとの適合性](./compliance.md#suitability-for-different-countries)に関する記事が役立ちます。

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Azure Information Protection は GDPR にどのように役立ちますか?

一般データ保護規則 (GDPR) に準拠するために Azure Information Protection がどのように役立つかを確認するには、ブログ投稿「[Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr)」(Microsoft 365 が GDPR で役立つ情報保護戦略を提供) のお知らせとビデオをご覧ください。

## <a name="where-can-i-find-supporting-information-for-azureinformation-protectionsuch-as-legal-compliance-and-slas"></a>法律、法令遵守、SLA など、Azure Information Protection に関するサポート情報はどこで入手できますか。
「[Azure Information Protection のコンプライアンスとサポート情報](./compliance.md)」を参照してください。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Azure Information Protection の問題を報告またはフィードバックを送信するにはどうすればよいですか。

テクニカル サポートの場合は、標準のサポート チャネルを使用するか、[Microsoft サポートに問い合わせ](information-support.md#to-contact-microsoft-support)てください。

[Azure Information Protection の Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>質問がここに含まれていない場合は、どうすればよいですか

最初に、分類、ラベル付け、データ保護に関する次の FAQ を確認してください。 Azure Rights Management サービス (Azure RMS) は、Azure Information Protection のデータ保護テクノロジを提供します。 Azure RMS は分類およびラベル付けと併用するか、単体で使用できます。 

- [分類とラベル付けに関してよく寄せられる質問](faqs-infoprotect.md)

- [データ保護に関してよく寄せられる質問](faqs-rms.md)

回答が得られない場合、「[Azure Information Protection の情報とサポート](information-support.md)」に一覧表示されているリンクとリソースを使用します。

さらに、エンドユーザー向けの FAQ が用意されています。

- [iOS 用と Android 用の Azure Information Protection の FAQ](./rms-client/mobile-app-faq.md)

- [Mac コンピューター用 RMS 共有アプリの FAQ](https://technet.microsoft.com/dn451248)

