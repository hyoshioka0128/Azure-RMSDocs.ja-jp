---
title: "Azure Information Protection に関してよく寄せられる質問"
description: "Azure Information Protection とそのデータ保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問の一部"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/06/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 23c2b24a830b6d1ab7e0712fc1d1d70056f5d736
ms.sourcegitcommit: d32d1f5afa5ee9501615a6ecc4af8a4cd4901eae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2018
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure Information Protection に関してよく寄せられる質問

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection、または Azure Rights Management サービス (Azure RMS) に関して質問がございますか。 ここで回答を探してみてください。

これらの FAQ ページは定期的に更新されます。新しい情報は [Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services&content-type=updates)上の月次のドキュメント更新発表に一覧表示されます。

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure Information Protection と Azure Rights Management の違いは何ですか。

Azure Information Protection では、組織の文書や電子メールを分類、ラベル付け、保護できます。 保護テクノロジでは、Azure Information Protection のコンポーネントになった、Azure Rights Management サービスが利用されます。

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>Azure Information Protection の ID 管理の役割とは何ですか。

Azure Information Protection で保護されたコンテンツにアクセスするには、有効なユーザー名とパスワードが必要です。 Azure Information Protection でデータを保護するしくみについての詳細は、「[データのセキュリティ保護における Azure Information Protection の役割](/enterprise-mobility-security/solutions/azure-information-protection-securing-data)」をご覧ください。 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。
Azure Information Protection サイトの[サブスクリプション情報](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)と[機能一覧](https://www.microsoft.com/cloud-platform/azure-information-protection-features)を参照してください。 

Rights Management を含む Office 365 サブスクリプションをお持ちの場合は、**機能**ページから [Azure Information Protection ライセンス データシート](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)をダウンロードしてください。

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Azure Information Protection client は分類とラベル付けを含むサブスクリプション用のみでしょうか。

いいえ。 ご覧いただきました Azure Information Protection クライアントのプレゼンテーションとデモの大部分は、分類とラベル付けのサポート方法を示していますが、データを保護するAzure Rights Management サービスのみを含むサブスクリプションと共に使用することもできます。

Windows 用の Azure Information Protection クライアントがインストールされているが Azure Information Protection ポリシーがない場合、クライアントは自動的に[保護のみモード](../rms-client/client-protection-only-mode.md)で動作します。 このモードでは、ユーザーは Rights Management テンプレートとカスタム アクセス許可に簡単に適用できます。 分類とラベル付けを含むサブスクリプションを後で購入した場合、Azure Information Protection ポリシーをダウンロードする際に、クライアントは自動的に標準モードへと切り替わります。

Windows 用の Rights Management 共有アプリケーションを現在使用している場合、このアプリケーションを Azure Information Protection クライアントに変えることをお勧めします。 共有アプリケーションのサポートは 2019 年 1 月 31 日に終了します。 移行に関するヘルプは、[RMS 共有アプリケーションを使用して実行するタスク](../rms-client/upgrade-client-app.md)をご覧ください。

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection はオンプレミスおよびハイブリッドのシナリオをサポートしますか?

はい。 Azure Information Protection はクラウドベースのソリューションですが、クラウドだけでなく、オンプレミスに保存されているドキュメントや電子メールの分類、ラベル付け、および保護が可能です。

Exchange Server、SharePoint Server、および Windows ファイル サーバーがある場合は、これらのオンプレミス サーバーで Azure Rights Management サービスを使用して電子メールやドキュメントを保護できるように、[Rights Management コネクタ](../deploy-use/deploy-rms-connector.md)をデプロイすることができます。 また、Active Directory ドメイン コントローラーを Azure AD と同期し、連携することで、たとえば [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)を使用して、よりシームレスな認証方法をユーザーに提供できます。

必要に応じて、Azure Rights Management サービスで XrML 証明書の生成と管理が自動的に行われるので、オンプレミスの PKI は使用されません。 Azure Rights Management での証明書の使用方法については、記事「[Azure RMS の機能の詳細](../understand-explore/how-does-it-work.md)」の「[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」セクションを参照してください。

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>条件付きアクセスに利用できるクラウド アプリとして Azure Information Protection が一覧に記載されています。これはどのように動作しますか。

はい。公共プレビュー サービスとして、Azure Information Protection に Azure AD 条件付きアクセスを構成できるようになりました。

Azure Information Protection で保護されているドキュメントをユーザーが開くとき、標準的な条件付きアクセス コントロールに基づき、管理者は自分のテナントでユーザーをブロックするか、アクセス許可を与えることができるようになりました。 最も一般的に要求される条件の 1 つが多要素認証 (MFA) を要求することです。 もう 1 つは、デバイスが [Intune ポリシーに準拠する](/intune/conditional-access-intune-common-ways-use)必要があるということです (たとえば、モバイル デバイスがパスワード要件やオペレーティング システムの最小バージョンを満たすようにする)。また、コンピューターはドメインに参加する必要があります。

チュートリアル形式の例が必要であれば、ブログ投稿の「[Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/)」 (Azure Information Protection の条件付きアクセス ポリシー) を参照してください。

追加情報:

- Windows コンピューターの場合: 現行プレビュー リリースの場合、[ユーザー環境が初期化](../understand-explore/how-does-it-work.md#initializing-the-user-environment) (このプロセスはブートストラップとも呼ばれています) されたときに Azure Information Protection の条件付きアクセス ポリシーが評価され、その後、30 日おきに評価されます。

- 条件付きアクセス ポリシーの評価頻度を微調整することもできます。 この微調整は、トークンの有効期間を構成することで実行できます。 詳細については、「[Azure Active Directory における構成可能なトークンの有効期間](/azure/active-directory/active-directory-configurable-token-lifetimes)」を参照してください。

- 条件付きアクセス ポリシーには管理者アカウントを追加しないことをお勧めします。管理者アカウントでは、Azure Portal の [Azure Information Protection] ブレードにアクセスできません。

- 大量のクラウド アプリで条件付きアクセスを使用する場合、選択対象の一覧に **Microsoft Azure Information Protection** が表示されないことがあります。 その場合、一覧の上にある検索ボックスを使用します。 「Microsoft Azure Information Protection」と入力し、利用可能アプリを絞り込みます。 サポートされているサブスクリプションがある場合、選択対象として **Microsoft Azure Information Protection** が表示されます。 

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Azure Information Protection のラベルと Office 365 のラベルにはどのような違いがありますか。

Azure Information Protection のラベルでは、ドキュメントおよび電子メールがオンプレミスのものであるかクラウド内のものであるかに関係なく、ドキュメントと電子メールに対して一貫性のある分類および保護ポリシーを適用できます。 この分類と保護は、コンテンツの格納場所または移動方法とは関係ありません。 [Office 365 Security & Compliance のラベル](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30)では、ドキュメントおよび電子メールのコンテンツが Office 365 サービス内に置かれている場合に、それらを分類して監査および保持することができます。 

今日、これらのラベルは別々に適用および管理されていますが、Microsoft では、Azure Information Protection、Office 365、Microsoft Cloud App Security、Windows 情報保護などの複数のサービスに対応する包括的で統一されたラベル戦略に向けて作業を進めています。 これと同じラベル スキーマおよびストアを、ソフトウェア ベンダーも使用できるようになります。 詳細については、Microsoft Ignite 2017 セッション「[Microsoft の情報保護機能を使用してデータのライフサイクル全体を保護する](https://myignite.microsoft.com/videos/55397)」を参照してください。

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Windows Server FCI と Azure Information Protection スキャナーの違い

しばらくの間、[Rights Management コネクタ](../deploy-use/deploy-rms-connector.md) (Office ドキュメントのみ) や [PowerShell スクリプト](../rms-client/configure-fci.md) (すべてのファイルの種類) を使用して、ドキュメントを分類し、保護するには、Windows Server ファイル分類インフラストラクチャを使用することができました。 

現在、プレビューの段階である [Azure Information Protection スキャナー](../deploy-use/deploy-aip-scanner.md)を使用できるようになりました。 スキャナーは Azure Information Protection クライアントと Azure Information Protection ポリシーを使用して、ドキュメント (すべてのファイルの種類) にラベルを付けるため、これらのドキュメントは分類され、必要に応じて保護されます。

この 2 つのトポロジの主な違いを次に示します。

|Windows Server FCI|Azure Information Protection スキャナー|
|--------------------------------|-------------------------------------|
|サポートされるデータ ストア: <br /><br />- Windows Server のローカル フォルダー|サポートされるデータ ストア: <br /><br />- Windows Server のローカル フォルダー<br /><br />- Windows ファイル共有とネットワーク接続ストレージ<br /><br />- SharePoint Server 2016 と SharePoint Server 2013|
|操作モード: <br /><br />- リアルタイム|操作モード: <br /><br />- 体系的にデータ ストアをクロールします。このサイクルは 1 回のみまたは繰り返し実行できます|

現在、ローカル フォルダーまたはネットワーク共有で保護されるファイルに対して、[Rights Management 所有者](../deploy-use/configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)の設定に違いがあります。 既定では、どちらのソリューションでも、Rights Management の所有者は、ファイルを保護するアカウントに設定されますが、この設定を上書きすることができます。

- Windows Server FCI の場合: すべてのファイルに対して単一アカウントとなるように Rights Management 所有者を設定したり、各ファイルの Rights Management 所有者を動的に設定したりすることができます。 Rights Management 所有者を動的に設定するには、**-OwnerMail [ソース ファイルの所有者の電子メール]** パラメーターと値を使用します。 この構成では、ファイルの所有者プロパティのユーザー アカウント名を使用して、Active Directory からユーザーのメール アドレスを取得します。

- Azure Information Protection スキャナーの場合: 指定のデータ ストアのすべてのファイルに対して単一アカウントとなるように Rights Management 所有者を設定できますが、各ファイルの Rights Management 所有者を動的に設定することはできません。 アカウントを設定するには、[データ リポジトリ プロファイル](/powershell/module/azureinformationprotection/Set-AIPScannerRepository?view=azureipps#optional-parameters)に **-DefaultOwner** パラメーターを指定します。

スキャナーで SharePoint サイトおよびライブラリのファイルを保護する場合、Rights Management 所有者は SharePoint 作成者の値を使用して、ファイルごとに動的に設定されます。

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>新しいリリースが Azure Information Protection ですぐに利用できるようになると聞きました。いつリリースされますか?

技術文書には今後のリリースに関する情報は含まれません。 この種の情報およびリリースの通知については、[Enterprise Mobility and Security のブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services)を参照し、Twitter の [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) から最新の情報を入手してください。 Office のリリースに興味がある場合は、[Office ブログ](https://blogs.office.com/)も確認してください。

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>法律、法令遵守、SLA など、Azure Information Protection に関するサポート情報はどこで入手できますか。

「[Azure Information Protection のコンプライアンスとサポート情報](../understand-explore/compliance.md)」を参照してください。

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

- [iOS 用と Android 用の Azure Information Protection の FAQ](../rms-client/mobile-app-faq.md)

- [Mac コンピューターと Windows Phone 用 RMS 共有アプリの FAQ](https://technet.microsoft.com/dn451248)

- [Windows 用 Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn467883)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

