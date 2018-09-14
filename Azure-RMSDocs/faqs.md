---
title: Azure Information Protection に関してよく寄せられる質問
description: Azure Information Protection とそのデータ保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問の一部
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4d991a96dd82bdc27aed036fd05119ba3f7ca1f2
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2018
ms.locfileid: "44151675"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure Information Protection に関してよく寄せられる質問

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection、または Azure Rights Management サービス (Azure RMS) に関して質問がございますか。 ここで回答を探してみてください。

これらの FAQ ページは定期的に更新されます。新しい情報は [Azure Information Protection 技術ブログ](https://aka.ms/AIPblog)上の月次のドキュメント更新発表に一覧表示されます。

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure Information Protection と Azure Rights Management の違いは何ですか。

Azure Information Protection では、組織の文書や電子メールを分類、ラベル付け、保護できます。 保護テクノロジでは、Azure Information Protection のコンポーネントになった、Azure Rights Management サービスが利用されます。

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>Azure Information Protection の ID 管理の役割とは何ですか。

Azure Information Protection で保護されたコンテンツにアクセスするには、有効なユーザー名とパスワードが必要です。 Azure Information Protection でデータを保護するしくみについての詳細は、「[データのセキュリティ保護における Azure Information Protection の役割](/enterprise-mobility-security/solutions/azure-information-protection-securing-data)」をご覧ください。 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。
「[Azure Information Protection の価格](https://azure.microsoft.com/en-us/pricing/details/information-protection)」ページのサブスクリプション情報と機能一覧を参照してください。 

Azure Rights Management データ保護を含む Office 365 サブスクリプションをお持ちの場合は、[Azure Information Protection ライセンス データシート](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)をダウンロードしてください。このデータシートにはライセンスに関してよく寄せられる質問もいくつか含まれています。

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Azure Information Protection client は分類とラベル付けを含むサブスクリプション用のみでしょうか。

いいえ。 ご覧いただきました Azure Information Protection クライアントのプレゼンテーションとデモの大部分は、分類とラベル付けのサポート方法を示していますが、データを保護するAzure Rights Management サービスのみを含むサブスクリプションと共に使用することもできます。

Windows 用の Azure Information Protection クライアントがインストールされているが Azure Information Protection ポリシーがない場合、クライアントは自動的に[保護のみモード](./rms-client/client-protection-only-mode.md)で動作します。 このモードでは、ユーザーは Rights Management テンプレートとカスタム アクセス許可に簡単に適用できます。 分類とラベル付けを含むサブスクリプションを後で購入した場合、Azure Information Protection ポリシーをダウンロードする際に、クライアントは自動的に標準モードへと切り替わります。

Windows 用の Rights Management 共有アプリケーションを現在使用している場合、このアプリケーションを Azure Information Protection クライアントに変えることをお勧めします。 共有アプリケーションのサポートは 2019 年 1 月 31 日に終了します。 移行に関するヘルプは、[RMS 共有アプリケーションを使用して実行するタスク](./rms-client/upgrade-client-app.md)をご覧ください。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Azure Information Protection を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?

Office 365 テナントまたは Azure AD テナントのグローバル管理者は、Azure Information Protection のすべての管理タスクを実行できます。 ただし、管理アクセス許可を他のユーザーに割り当てる場合は、次のオプションがあります。

- **Information Protection 管理者**: この Azure Active Directory 管理者ロールでは、管理者が Azure Information Protection のさまざまな設定を構成できますが、他のサービスは構成できません。 この役割を持つ管理者は、Azure Rights Management 保護サービスのアクティブ化と非アクティブ化、保護設定とラベルの構成、Azure Information Protection ポリシーの構成を行うことができます。 さらに、この役割を持つ管理者は、[Azure Information Protection クライアント](./rms-client/client-admin-guide-powershell.md)と [AADRM モジュール](administer-powershell.md)からのすべての PowerShell コマンドレットを実行できます。 
    
    ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。

- **セキュリティ管理者**: この Azure Active Directory 管理者ロールでは、管理者が、他の Azure サービスの一部を構成するだけでなく、Azure Portal で Azure Information Protection のさまざまな設定を構成することができます。 この役割を持つ管理者は、[AADRM モジュールからどの PowerShell コマンドレット](administer-powershell.md)も実行することはできません。
    
    ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。 この役割のユーザーが持つその他のアクセス許可を確認するには、Azure Active Directory ドキュメントの「[使用可能なロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles)」セクションを参照してください。

- Azure Rights Management の**グローバル管理者**および**コネクタ管理者**: これらの Azure Rights Management の管理者ロールの場合、グローバル管理者は、ユーザーをその他のクラウド サービスのグローバル管理者にすることなく、[AADRM モジュールからすべての PowerShell コマンドレット](administer-powershell.md)を実行するアクセス許可をユーザーに付与し、コネクタ管理者は Rights Management (RMS) コネクタのみを実行するアクセス許可を付与します。 これらの管理者ロールはどちらも、管理コンソールへのアクセス許可を付与することはありません。また、ドキュメント追跡サイトで管理者モードを使用することはありません。

    これらのいずれかの管理者ロールを割り当てるには、AADRM PowerShell コマンドレット ([Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator)) を使用します。

注意事項:

- [オンボーディング コントロール](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成してある場合は、RMS コネクタを除き、Azure Information Protection を管理する機能に影響はありません。 たとえば、コンテンツを保護する機能を "IT department" グループに制限するようにオンボーディング コントロールが構成されている場合、RMS コネクタのインストールと構成に使用するアカウントは、そのグループのメンバーである必要があります。 

- 管理者ロールが割り当てられているユーザーは、Azure Information Protection によって保護されたドキュメントやメールから保護を自動的に削除することはできません。 スーパー ユーザーを割り当てられたユーザーだけが、スーパー ユーザー機能が有効になっているときにのみ、この操作を行うことができます。 ただし、Azure Information Protection への管理アクセス許可を割り当てたすべてのユーザーが、各自のアカウントなど、ユーザーにスーパー ユーザーを割り当てることができます。 また、スーパー ユーザー機能を有効にすることもできます。 これらのアクションは、管理者ログに記録されます。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](configure-super-users.md)」のセキュリティのベスト プラクティスに関するセクションを参照してください。 


## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection はオンプレミスおよびハイブリッドのシナリオをサポートしますか?

はい。 Azure Information Protection はクラウドベースのソリューションですが、クラウドだけでなく、オンプレミスに保存されているドキュメントや電子メールの分類、ラベル付け、および保護が可能です。

Exchange Server、SharePoint Server、および Windows ファイル サーバーがある場合は、これらのオンプレミス サーバーで Azure Rights Management サービスを使用して電子メールやドキュメントを保護できるように、[Rights Management コネクタ](deploy-rms-connector.md)をデプロイすることができます。 また、Active Directory ドメイン コントローラーを Azure AD と同期し、連携することで、たとえば [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)を使用して、よりシームレスな認証方法をユーザーに提供できます。

必要に応じて、Azure Rights Management サービスで XrML 証明書の生成と管理が自動的に行われるので、オンプレミスの PKI は使用されません。 Azure Rights Management での証明書の使用方法については、記事「[Azure RMS の機能の詳細](./how-does-it-work.md)」の「[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」セクションを参照してください。

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Azure Information Protection ではどのようなデータの種類を分類し、保護できますか?

Azure Information Protection では、メール メッセージやドキュメントがオンプレミスまたはクラウドのどちらに配置されていても、それらを分類し、管理することができます。 これらのドキュメントには、Word ドキュメント、Excel スプレッドシート、PowerPoint プレゼンテーション、PDF ドキュメント、テキストベースのファイル、および画像ファイルが含まれます。 サポートされるドキュメントの種類の一覧については、管理者ガイドの[サポートされているファイルの種類](./rms-client/client-admin-guide-file-types.md)の一覧を参照してください。

Azure Information Protection では、データベース ファイル、予定表アイテム、PowerBI レポート、Yammer の投稿、Sway コンテンツ、および OneNote ノートブックなど、構造化されたデータを分類または保護することはできません。

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>条件付きアクセスに利用できるクラウド アプリとして Azure Information Protection が一覧に記載されています。これはどのように動作しますか。

はい。公共プレビュー サービスとして、Azure Information Protection に Azure AD 条件付きアクセスを構成できるようになりました。

Azure Information Protection で保護されているドキュメントをユーザーが開くとき、標準的な条件付きアクセス コントロールに基づき、管理者は自分のテナントでユーザーをブロックするか、アクセス許可を与えることができるようになりました。 最も一般的に要求される条件の 1 つが多要素認証 (MFA) を要求することです。 もう 1 つは、デバイスが [Intune ポリシーに準拠する](/intune/conditional-access-intune-common-ways-use)必要があるということです (たとえば、モバイル デバイスがパスワード要件やオペレーティング システムの最小バージョンを満たすようにする)。また、コンピューターはドメインに参加する必要があります。

チュートリアル形式の例が必要であれば、ブログ投稿の「[Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/)」 (Azure Information Protection の条件付きアクセス ポリシー) を参照してください。

追加情報:

- Windows コンピューターの場合: 現行プレビュー リリースの場合、[ユーザー環境が初期化](./how-does-it-work.md#initializing-the-user-environment) (このプロセスはブートストラップとも呼ばれています) されたときに Azure Information Protection の条件付きアクセス ポリシーが評価され、その後、30 日おきに評価されます。

- 条件付きアクセス ポリシーの評価頻度を微調整することもできます。 この微調整は、トークンの有効期間を構成することで実行できます。 詳細については、「[Azure Active Directory における構成可能なトークンの有効期間](/azure/active-directory/active-directory-configurable-token-lifetimes)」を参照してください。

- 条件付きアクセス ポリシーには管理者アカウントを追加しないことをお勧めします。管理者アカウントでは、Azure Portal の [Azure Information Protection] ブレードにアクセスできません。

- 多くのクラウド アプリで条件付きアクセスを使用する場合、選択対象の一覧に **Microsoft Azure Information Protection** が表示されないことがあります。 その場合、一覧の上にある検索ボックスを使用します。 「Microsoft Azure Information Protection」と入力し、利用可能アプリを絞り込みます。 サポートされているサブスクリプションがある場合、選択対象として **Microsoft Azure Information Protection** が表示されます。 

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Azure Information Protection のラベルと Office 365 のラベルにはどのような違いがありますか。

Azure Information Protection のラベルでは、ドキュメントおよび電子メールがオンプレミスのものであるかクラウド内のものであるかに関係なく、ドキュメントと電子メールに対して一貫性のある分類および保護ポリシーを適用できます。 この分類と保護は、コンテンツの格納場所または移動方法とは関係ありません。 [Office 365 Security & Compliance のラベル](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30)では、ドキュメントおよび電子メールのコンテンツが Office 365 サービス内に置かれている場合に、それらを分類して監査および保持することができます。 

今日、これらのラベルは別々に適用および管理されていますが、Microsoft では、Azure Information Protection、Office 365、Microsoft Cloud App Security、Windows 情報保護などの複数のサービスに対応する包括的で統一されたラベル戦略に向けて作業を進めています。 "Microsoft Information Protection"(MIP) と呼ばれるこの戦略については、聞いたことがあるかもしれません。 これと同じラベル スキーマおよびストアを、ソフトウェア ベンダーも使用できるようになります。 詳細については、ブログ投稿「[Consistent labeling and protection policies coming to Office 365 and Azure Information Protection](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Consistent-labeling-and-protection-policies-coming-to-Office-365/ba-p/161553)」(一貫性のあるラベルと保護ポリシーを Office 365 と Azure Information Protection に導入) を参照してください。

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Windows Server FCI と Azure Information Protection スキャナーの違い

しばらくの間、[Rights Management コネクタ](deploy-rms-connector.md) (Office ドキュメントのみ) や [PowerShell スクリプト](./rms-client/configure-fci.md) (すべてのファイルの種類) を使用して、ドキュメントを分類し、保護するには、Windows Server ファイル分類インフラストラクチャを使用することができました。 

[Azure Information Protection スキャナー](deploy-aip-scanner.md)を使用できるようになりました。 スキャナーは Azure Information Protection クライアントと Azure Information Protection ポリシーを使用して、ドキュメント (すべてのファイルの種類) にラベルを付けるため、これらのドキュメントは分類され、必要に応じて保護されます。

この 2 つのトポロジの主な違いを次に示します。

|Windows Server FCI|Azure Information Protection スキャナー|
|--------------------------------|-------------------------------------|
|サポートされるデータ ストア: <br /><br />- Windows Server のローカル フォルダー|サポートされるデータ ストア: <br /><br />- Windows Server のローカル フォルダー<br /><br />- Windows ファイル共有とネットワーク接続ストレージ<br /><br />- SharePoint Server 2016 と SharePoint Server 2013。 SharePoint Server 2010 は、[このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様、および前のバージョンのスキャナーを使用しているお客様にもサポートされます。|
|操作モード: <br /><br />- リアルタイム|操作モード: <br /><br />- 体系的にデータ ストアをクロールします。このサイクルは 1 回のみまたは繰り返し実行できます|
|ファイルの種類ごとのサポート: <br /><br />- すべてのファイルの種類が既定で保護されます <br /><br />- レジストリを編集することで、特定のファイルの種類を保護から除外できます|ファイルの種類ごとのサポート: <br /><br />- Office のファイルの種類が既定で保護されます <br /><br />- レジストリを編集することで、特定のファイルの種類を保護に含めることができます|

現在、ローカル フォルダーまたはネットワーク共有で保護されるファイルに対して、[Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)の設定に違いがあります。 既定では、どちらのソリューションでも、Rights Management の所有者は、ファイルを保護するアカウントに設定されますが、この設定をオーバーライドすることができます。

- Windows Server FCI の場合: すべてのファイルに対して単一アカウントとなるように Rights Management 所有者を設定したり、各ファイルの Rights Management 所有者を動的に設定したりすることができます。 Rights Management 所有者を動的に設定するには、**-OwnerMail [ソース ファイルの所有者の電子メール]** パラメーターと値を使用します。 この構成では、ファイルの所有者プロパティのユーザー アカウント名を使用して、Active Directory からユーザーのメール アドレスを取得します。

- Azure Information Protection スキャナーの場合: 指定のデータ ストアのすべてのファイルに対して単一アカウントとなるように Rights Management 所有者を設定できますが、各ファイルの Rights Management 所有者を動的に設定することはできません。 アカウントを設定するには、[データ リポジトリ プロファイル](/powershell/module/azureinformationprotection/Set-AIPScannerRepository?view=azureipps#optional-parameters)に **-DefaultOwner** パラメーターを指定します。

スキャナーで SharePoint サイトおよびライブラリのファイルを保護する場合、Rights Management 所有者は SharePoint 作成者の値を使用して、ファイルごとに動的に設定されます。

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>新しいリリースが Azure Information Protection ですぐに利用できるようになると聞きました。いつリリースされますか?

技術文書には今後のリリースに関する情報は含まれません。 この種の情報およびリリースの通知については、[Enterprise Mobility and Security のブログ](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services)を参照し、Twitter の [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) から最新の情報を入手してください。 Office のリリースに興味がある場合は、[Office ブログ](https://blogs.office.com/)も確認してください。

## <a name="is-azure-information-protection-suitable-for-my-country"></a>自分の国に Azure Information Protection は適していますか?

国によって、さまざまな要件と規制があります。 組織のこの質問に対する回答は、[国ごとの適合性](./compliance.md#suitability-for-different-countries)に関する記事が役立ちます。

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Azure Information Protection は GDPR にどのように役立ちますか?

一般データ保護規則 (GDPR) に準拠するために Azure Information Protection がどのように役立つかを確認するには、ブログ投稿「[Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr)」(Microsoft 365 が GDPR で役立つ情報保護戦略を提供) のお知らせとビデオをご覧ください。

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>法律、法令遵守、SLA など、Azure Information Protection に関するサポート情報はどこで入手できますか。
「[Azure Information Protection のコンプライアンスとサポート情報](./compliance.md)」を参照してください。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Azure Information Protection の問題を報告またはフィードバックを送信するにはどうすればよいですか。

テクニカル サポートの場合は、標準のサポート チャネルを使用するか、[Microsoft サポートに問い合わせ](information-support.md#to-contact-microsoft-support)てください。

改善や新機能の提案などのフィードバックについては、Office アプリケーションの **[ホーム]** タブの **[保護]** グループで **[保護]** をクリックし、**[ヘルプとフィードバック]** をクリックします。 **[Microsoft Azure Information Protection]** ダイアログ ボックスで、**[フィードバックの送信]** をクリックします。 そうすると、Information Protection チームに送信される電子メール メッセージが開きます。

[Azure Information Protection の Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>質問がここに含まれていない場合は、どうすればよいですか

最初に、分類、ラベル付け、データ保護に関する次の FAQ を確認してください。 Azure Rights Management サービス (Azure RMS) は、Azure Information Protection のデータ保護テクノロジを提供します。 Azure RMS は分類およびラベル付けと併用するか、単体で使用できます。 

- [分類とラベル付けに関してよく寄せられる質問](faqs-infoprotect.md)

- [データ保護に関してよく寄せられる質問](faqs-rms.md)

回答が得られない場合、「[Azure Information Protection の情報とサポート](information-support.md)」に一覧表示されているリンクとリソースを使用します。

さらに、エンドユーザー向けの FAQ が用意されています。

- [iOS 用と Android 用の Azure Information Protection の FAQ](./rms-client/mobile-app-faq.md)

- [Mac コンピューターと Windows Phone 用 RMS 共有アプリの FAQ](https://technet.microsoft.com/dn451248)

- [Windows 用 Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn467883)



