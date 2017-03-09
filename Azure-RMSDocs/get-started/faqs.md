---
title: "Azure Information Protection に関してよく寄せられる質問"
description: "Azure Information Protection とそのデータ保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問の一部"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/24/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 37ce3f1596878e28962119faef22bc1c61a067f8
ms.openlocfilehash: 0bb42f7ec5f2c1768c9eaaa7890b8b46853abd99
ms.lasthandoff: 02/25/2017


---

# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure Information Protection に関してよく寄せられる質問

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection、または Azure Rights Management サービス (Azure RMS) に関して質問がございますか。 ここで回答を探してみてください。

これらの FAQ ページは定期的に更新されます。新しい情報は [Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services)上の月次のドキュメント更新発表に一覧表示されます。

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure Information Protection と Azure Rights Management の違いは何ですか。

Azure Information Protection では、組織の文書や電子メールを分類、ラベル付け、保護できます。 保護テクノロジでは、Azure Information Protection のコンポーネントになった、Azure Rights Management サービスが利用されます。

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。
Azure Information Protection サイトの[サブスクリプション情報](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)と[機能一覧](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)を参照してください。 

Rights Management を含む Office 365 サブスクリプションをお持ちの場合は、**機能**ページから [Azure Information Protection ライセンス データシート](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)をダウンロードしてください。

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection はオンプレミスおよびハイブリッドのシナリオをサポートしますか?

はい。 Azure Information Protection はクラウドベースのソリューションですが、クラウドだけでなく、オンプレミスに保存されているドキュメントや電子メールの分類、ラベル付け、および保護が可能です。

Exchange Server、SharePoint Server、および Windows ファイル サーバーがある場合は、これらのオンプレミス サーバーで Azure Rights Management サービスを使用して電子メールやドキュメントを保護できるように、[Rights Management コネクタ](../deploy-use/deploy-rms-connector.md)をデプロイすることができます。 また、Active Directory ドメイン コントローラーを Azure AD と同期し、連携することで、たとえば [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)を使用して、よりシームレスな認証方法をユーザーに提供できます。

必要に応じて、Azure Rights Management サービスで XrML 証明書の生成と管理が自動的に行われるので、オンプレミスの PKI は使用されません。 Azure Rights Management での証明書の使用方法については、記事「[Azure RMS の機能の詳細](../understand-explore/how-does-it-work.md)」の「[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」セクションを参照してください。

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>新しいリリースが Azure Information Protection ですぐに利用できるようになると聞きました。いつリリースされますか?

技術文書には今後のリリースに関する情報は含まれません。 この種の情報およびリリースの通知については、[Enterprise Mobility and Security のブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services)を参照し、Twitter の [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) から最新の情報を入手してください。 Office のリリースに興味がある場合は、[Office ブログ](https://blogs.office.com/)も確認してください。

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>法律、法令遵守、SLA など、Azure Information Protection に関するサポート情報はどこで入手できますか。

「[Azure Information Protection のコンプライアンスとサポート情報](../understand-explore/compliance.md)」を参照してください。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Azure Information Protection の問題を報告またはフィードバックを送信するにはどうすればよいですか。

テクニカル サポートの場合は、標準のサポート チャネルを使用するか、[Microsoft サポートに問い合わせ](information-support.md#to-contact-microsoft-support)てください。

改善や新機能の提案などのフィードバックについては、Office アプリケーションの **[ホーム]** タブの **[保護]** グループで **[保護]** をクリックし、**[ヘルプとフィードバック]** をクリックします。 **[Microsoft Azure Information Protection]** ダイアログ ボックスで、**[フィードバックの送信]** をクリックします。 これにより、Information Protection チームに電子メールが送信され、PC のログ ファイルが自動的に添付されます。 

[Azure Information Protection の Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>質問がここに含まれていない場合は、どうすればよいですか

最初に、分類、ラベル付け、またはデータ保護に関してよく寄せられる質問を確認してください。 Azure Rights Management サービス (Azure RMS) は、Azure Information Protection のデータ保護テクノロジを提供します。Azure RMS は分類やラベル付けと併用できます (併用しないことも選択できます)。 

- [分類とラベル付けに関してよく寄せられる質問](faqs-infoprotect.md)

- [データ保護に関してよく寄せられる質問](faqs-rms.md)

回答が得られない場合、「[Azure Information Protection の情報とサポート](information-support.md)」に一覧表示されているリンクとリソースを使用します。

さらに、FAQ がエンドユーザー向けに用意されています。

- [iOS 用と Android 用の Azure Information Protection の FAQ](../rms-client/mobile-app-faq.md)

- [Mac コンピューターと Windows Phone 用 RMS 共有アプリの FAQ](https://technet.microsoft.com/dn451248)

- [Windows 用 Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn467883)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


