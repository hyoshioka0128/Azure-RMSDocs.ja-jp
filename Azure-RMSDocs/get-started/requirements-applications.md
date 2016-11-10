---
title: "アプリケーションでのデータ保護のサポート | Azure Information Protection"
description: "Azure Information Protection から Azure Rights Management サービスをネイティブにサポートするために、RMS API を使用するアプリケーションを特定します。"
author: cabailey
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a036da617d88a65903cfea9df30d5f851bda6e36
ms.openlocfilehash: 80874b7e15fef7f4e7685774b31410149301c124


---


# <a name="applications-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするアプリケーション

>*適用対象: Azure Information Protection、Office 365*


次の表を使用して、Azure Information Protection のデータ保護を提供する、Azure Rights Management サービス (Azure RMS) をネイティブでサポートするアプリケーションを特定します。 

これらのアプリケーションでは、Rights Management サポートは、使用制限をサポートするために Rights Management API を使用して密接に統合されています。 このようなアプリケーションは RMS 対応とも呼ばれます。

別途明記されていない限り、サポートされる機能は Azure RMS と AD RMS の両方に適用されます。 また、iOS、Android、OS X、Windows Phone 8.1 で AD RMS をサポートするには、[Active Directory Rights Management サービス モバイル デバイス拡張機能](https://technet.microsoft.com/library/dn673574.aspx)が必要です。

表の列に関する情報

-   **保護された PDF**: このファイルの拡張子は .ppdf です。RMS 共有アプリケーションを使用して Office ファイルや PDF ファイルを電子メールで共有すると、自動的に作成されます。 RMS 共有アプリケーションと iOS 用および Android 用の Azure Information Protection アプリには、保護された PDF ファイル用のリーダーが含まれています。 以前に Azure RMS または AD RMS を使用して保護された PDF ファイルを作成していた場合は、Windows、iOS、および Android デバイス上で Foxit Reader および Nitro Pro を使用して、引き続きこれらのファイルを読み取ることができます。

-   **電子メール:** 表示されている電子メール クライアントは、電子メール メッセージを保護できるので、添付されているファイルも自動的に保護されます。 このシナリオでは、クライアントのプレビュー機能で、許可された受信者に対して保護されたコンテンツ (メッセージと添付ファイル) を表示できます。 ただし、電子メール メッセージが保護さておらず、添付ファイルが保護されている場合、クライアントのプレビュー機能では、許可された受信者に対する場合も保護された添付ファイルを表示できません。

-   **他のファイルの種類**: テキスト ファイルと画像ファイルには、.txt、.xml、.jpg、.jpeg などのファイル名拡張子が付いているファイルがあります。 これらのファイルでは、Rights Management によりネイティブで保護された後に、ファイル名拡張子が変更され、読み取り専用になります。 ネイティブで保護できないファイルでは、Rights Management によって一般的に保護された後に、ファイル名拡張子が .pfile になります。 詳細については、「[Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)」を参照してください。


|**デバイス オペレーティング システム**|Word、Excel、PowerPoint|保護された PDF|電子メール|他のファイルの種類|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office モバイル アプリ (Azure RMS のみ) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />RMS 共有アプリ|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows メール [[4]](#footnote-4)|Windows 用 RMS 共有アプリケーション: テキスト、イメージ、pfile<br /><br />Siemens JT2Go: JT ファイル (Windows 10 のみ)|
|**iOS**|iPad および iPhone 用 Office [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS Docs|Azure Information Protection アプリ [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />TITUS Docs|Azure Information Protection アプリ [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for iOS [[4]](#footnote-4)<br /><br />OWA for iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Azure Information Protection アプリ [[1]](#footnote-1): テキスト、画像<br /><br />TITUS Docs: Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (Azure RMS のみ) [[1]](#footnote-1)|Azure Information Protection アプリ [[1]](#footnote-1)<br /><br />GigaTrust App for Android<br /><br />Foxit Reader<br /><br />RMS 共有アプリ [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Azure Information Protection アプリ [[1]](#footnote-1)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for Android [[4]](#footnote-4)<br /><br />OWA for Android [[3]](#footnote-3) と [[7]](#footnote-7)<br /><br />Samsung Email (S3 以降) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Azure Information Protection アプリ [[1]](#footnote-1): テキスト、画像|
|**OS X**|Office 2011 (AD RMS のみ)<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />RMS 共有アプリ [[1]](#footnote-1)|Outlook 2011 (AD RMS のみ)<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共有アプリ [[1]](#footnote-1): テキスト、イメージ、pfile|
|**Windows 10 Mobile**|Office モバイル アプリ (Azure RMS のみ)[[1]](#footnote-1)|サポートされていません|Citrix WorxMail [[6]](#footnote-6)<br /><br />Outlook メール|サポートされていません|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|サポートされていません|Outlook 2013 RT<br /><br />Windows 用メール アプリケーション<br /><br />Windows メール [[4]](#footnote-4)|Siemens JT2Go: JT ファイル|
|**Windows Phone 8.1**|Office Mobile (AD RMS のみ)|RMS 共有アプリ [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|RMS 共有アプリ [[1]](#footnote-1): テキスト、イメージ、pfile|
|**Blackberry 10**|サポートされていません|サポートされていません|Blackberry の電子メール [[4]](#footnote-4)|サポートされていません|


##### <a name="footnote-1"></a>脚注 1:
保護されたコンテンツの表示をサポートします。

##### <a name="footnote-2"></a>脚注 2: 
保護されていないドキュメントが SharePoint Online と OneDrive for Business の保護ライブラリにアップロードされたときの、保護されたドキュメントの表示をサポートします。 

##### <a name="footnote-3"></a>脚注 3:
受信者が保護された電子メールを受信したが、メール サーバーとして Exchange を使用していない場合、または送信者が別の組織に属している場合、このコンテンツは Outlook のような機能が豊富なメール クライアントでしか開くことができません。 このコンテンツは Outlook Web Access から開くことはできません。

##### <a name="footnote-4"></a>脚注 4:
Exchange ActiveSync IRM を使用します。Exchange の管理者が有効にする必要があります。 ユーザーは保護された電子メール メッセージを表示、返信、全員に返信することができますが、新しい電子メール メッセージを自身で保護することはできません。

受信者が保護された電子メールを受信したが、メール サーバーとして Exchange を使用していない場合、または送信者が別の組織に属している場合、このコンテンツは Outlook のような機能が豊富なメール クライアントでしか開くことができません。 このコンテンツは、Outlook Web Access から開くことも、Exchange Active Sync IRM を使用してモバイル メール クライアントから開くこともできません。

##### <a name="footnote-5"></a>脚注 5:
保護されたドキュメントの表示と編集をサポートします。 詳細については、Office ブログの投稿「[Azure Rights Management support comes to Office for iPad and iPhone (Azure Rights Management による iPad および iPone 用 Office 向けのサポート)](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)」を参照してください。

##### <a name="footnote-6"></a>脚注 6:
詳細については、「[Citrix product documentation for WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html)」 (Citrix の WorxMail 向け製品文書) を参照してください。

##### <a name="footnote-7"></a>脚注 7:
詳細については、Office ブログの投稿「[OWA for Android now available on select devices (一部のデバイスで OWA for Android が利用可能になりました)](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)」を参照してください。

## <a name="more-information-about-azure-rms-support-for-office"></a>Azure RMS による Office のサポートの詳細

Azure RMS は、Word、Excel、PowerPoint、および Outlook のアプリケーションと緊密に統合されています。多くの場合、この機能は Information Rights Management (IRM) と呼ばれます。 次の Office クライアント エディションは、Azure RMS を使用したファイルや電子メールの保護をサポートします。

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

Office のすべてのエディション (Office 2007 を除く) で、保護されたコンテンツの使用がサポートされます。

Azure RMS と Office Professional Plus 2010 または Office Professional 2010:

- Windows 用 Rights Management 共有アプリケーションが必要です

- Windows 10 ではサポートされていません

## <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Azure Information Protection アプリに関する詳細

iOS 用および Android 用の Azure Information Protection アプリは、これらのデバイスの RMS 共有アプリに置き換わります。 同様の機能を提供し、さらに SharePoint Online 上の権利で保護された電子メール メッセージおよび権利で保護された PDF ファイルをサポートします。

使用している iOS デバイスや Android デバイスが Microsoft Intune で登録された場合、ポリシーで管理されているアプリを使用して、このアプリをデプロイおよび管理できます。 詳細については、Intune のドキュメントの「[Configure and deploy mobile application management policies in the Microsoft Intune console (Microsoft Intune コンソールでモバイル アプリケーション管理ポリシーを構成およびデプロイする)](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)」を参照してください。 この Intune ドキュメントの手順 2 では、ポリシーで管理されているアプリを発行するためにこの手順を使用します。

詳細については、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](../rms-client/mobile-app-faq.md)」をご覧ください。


## <a name="more-information-about-the-rights-management-sharing-application"></a>Rights Management 共有アプリケーションの詳細

Windows 用 Rights Management 共有アプリケーションの詳細については、以下のリソースを参照してください。

-   [Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)

-   [Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)

モバイル プラットフォーム用 Rights Management 共有アプリケーションの詳細については、以下のリソースを参照してください。

-   [Microsoft Rights Management のページ](http://go.microsoft.com/fwlink/?LinkId=303970)にあるリンクを使用して関連アプリをダウンロードする

-   [モバイル プラットフォーム用 Microsoft Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn451248)

> [!NOTE]
> iOS 用および Android 用の RMS 共有アプリケーションは、Azure Information Protection アプリに置き換わっています。

## <a name="more-information-about-other-applications-that-support-azure-rms"></a>Azure RMS をサポートしている他のアプリケーションの詳細

テーブル内のアプリケーションだけでなく、RMS API をサポートするアプリケーションはどれでも Azure RMS と統合できます。次のようなアプリケーションがこれに該当します。

- RMS SDK を使用して社内で作成した基幹業務アプリケーション

- RMS SDK を使用してソフトウェア ベンダーが作成したアプリケーション

SDK の詳細については、「[Microsoft Rights Management SDK](../develop/developers-guide.md)」を参照してください。

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Azure RMS でサポートされていないアプリケーション

Azure RMS では、現在のところ以下のアプリケーションはサポートされません。

-   Microsoft Office for Mac 2011:

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS ビューアー
 
また、RMS 共有アプリケーションには次の制限事項があります。

-   Windows コンピューターの場合: Windows 7 Service Pack 1 以降が必要です



## <a name="next-steps"></a>次のステップ
その他の要件を確認するには、「[Azure Information Protection の要件](requirements-azure-rms.md)」をご覧ください。

これらの最も一般的に使用されるアプリケーションが Azure RMS をサポートする方法の詳細については、「[アプリケーションによる Azure Rights Management サービスのサポート](../understand-explore/applications-support.md)」をご覧ください。

Azure RMS で最も一般的に使用されるアプリケーションを構成する方法の詳細については、「[Azure Rights Management 用にアプリケーションを構成する](../deploy-use/configure-applications.md)」を参照してください。


<!--HONumber=Nov16_HO1-->


