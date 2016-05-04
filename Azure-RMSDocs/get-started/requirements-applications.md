---
# required metadata

title: Azure RMS の要件&#58; アプリケーション | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Azure RMS の要件: アプリケーション

次のテーブルを使用して、Azure RMS をネイティブにサポートするアプリケーションを特定します。RMS API を使用することで RMS はこれらのアプリケーションと緊密に統合され、使用制限がサポートされます。 このようなアプリケーションは RMS 対応とも呼ばれます。

別途明記されていない限り、サポートされる機能は Azure RMS と AD RMS の両方に適用されます。 また、iOS、Android、OS X、Windows Phone 8.1 で AD RMS をサポートするには、[Active Directory Rights Management サービス モバイル デバイス拡張機能](https://technet.microsoft.com/library/dn673574.aspx)が必要です。

表の列に関する情報

-   **保護された PDF**: このファイルの拡張子は .ppdf です。RMS 共有アプリケーションを使用して Office ファイルや PDF ファイルを電子メールで共有すると、自動的に作成されます。 RMS 共有アプリケーションには、保護された PDF ファイル用のリーダーが含まれています。 以前に Azure RMS または AD RMS を使用して保護された PDF ファイルを作成していた場合は、Windows、iOS、および Android デバイス上で Foxit Reader および Nitro Pro を使用して、引き続きこれらのファイルを読み取ることができます。

-   **電子メール:** 表示されている電子メール クライアントは、電子メール メッセージを保護できるので、添付されているファイルも自動的に保護されます。 このシナリオでは、クライアントのプレビュー機能で、許可された受信者に対して保護されたコンテンツ (メッセージと添付ファイル) を表示できます。 ただし、電子メール メッセージが保護さておらず、添付ファイルが保護されている場合、クライアントのプレビュー機能では、許可された受信者に対する場合も保護された添付ファイルを表示できません。

-   **他のファイルの種類**: テキスト ファイルと画像ファイルには、.txt、.xml、.jpg、.jpeg などのファイル名拡張子が付いているファイルがあります。 これらのファイルでは、RMS によりネイティブで保護された後に、ファイル名拡張子が変更され、読み取り専用になります。 ネイティブで保護できないファイルでは、RMS によって一般的に保護された後に、ファイル名拡張子が .pfile になります。 詳細については、「[Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)」を参照してください。


|**デバイス オペレーティング システム**|Word、Excel、PowerPoint|保護された PDF|電子メール|他のファイルの種類|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office モバイル アプリ (Azure RMS のみ) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />RMS 共有アプリ|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows メール [[4]](#footnote-4)|Windows 用 RMS 共有アプリケーション: テキスト、イメージ、pfile<br /><br />Siemens JT2Go: JT ファイル (Windows 10 のみ)|
|**iOS**|iPad および iPhone 用 Office [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS Docs|Foxit Reader<br /><br />RMS 共有アプリ [[1]](#footnote-1)<br /><br />TITUS Docs|Citrix WorxMail<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />iPad および iPhone 用 Outlook [[4]](#footnote-4)<br /><br />OWA for iOS [[3]](#footnote-3)<br /><br />TITUS Mail|RMS 共有アプリ [[1]](#footnote-1): テキスト、イメージ、pfile<br /><br />TITUS Docs: Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)|GigaTrust App for Android<br /><br />Foxit Reader<br /><br />RMS 共有アプリ [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />OWA for Android [[3]](#footnote-3) および [[6]](#footnote-6)<br /><br />Samsung Email (S3 以降) [[6]](#footnote-6)<br /><br />TITUS Classification for Mobile|RMS 共有アプリ [[1]](#footnote-1): テキスト、イメージ、pfile|
|**OS X**|Office 2011 (AD RMS のみ)<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />RMS 共有アプリ [[1]](#footnote-1)|Outlook 2011 (AD RMS のみ)<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共有アプリ [[1]](#footnote-1): テキスト、イメージ、pfile|
|**[Windows] 10 Mobile**|Office モバイル アプリ (Azure RMS のみ)[[1]](#footnote-1)|サポートされていません|Citrix WorxMail<br /><br />Outlook メール|サポートされていません|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|サポートされていません|Outlook 2013 RT<br /><br />Windows 用メール アプリケーション<br /><br />Windows メール [[4]](#footnote-4)|Siemens JT2Go: JT ファイル|
|**Windows Phone 8。1**|Office Mobile (AD RMS のみ)|RMS 共有アプリ [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|RMS 共有アプリ [[1]](#footnote-1): テキスト、イメージ、pfile|
|**Blackberry 10**|サポートされていません|サポートされていません|Blackberry の電子メール [[4]](#footnote-4)|サポートされていません|


###### 脚注 1:
保護されたコンテンツの表示をサポートします。

###### 脚注 2: 
SharePoint Online、OneDrive for Business、Outlook Web Access での保護されたコンテンツの表示をサポートします。

###### 脚注 3:
受信者が Exchange On-Premises にメールボックスを所有していて、保護された電子メールを受信した場合、このコンテンツは、Outlook などの機能の豊富な電子メール クライアントでのみ開くことができます。  このコンテンツは Outlook Web Access から開くことはできません。

###### 脚注 4:
Exchange ActiveSync IRM を使用します。Exchange の管理者が有効にする必要があります。 ユーザーは保護された電子メール メッセージを表示、返信、全員に返信することができますが、新しい電子メール メッセージを自身で保護することはできません。

受信者が Exchange On-premises にメールボックスを所有していて、Exchange を使用している別の組織から保護された電子メールを受信した場合、このコンテンツは、Outlook などの機能豊富な電子メール クライアントでのみ開くことができます。  このコンテンツは、Exchange Active Sync IRM を使用するデバイスから開くことはできません。

###### 脚注 5:
保護されたドキュメントの表示と編集をサポートします。 詳細については、Office ブログの投稿「[Azure Rights Management support comes to Office for iPad and iPhone (Azure Rights Management による iPad および iPone 用 Office 向けのサポート)](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)」を参照してください。

###### 脚注 6:
詳細については、Office ブログの投稿「[OWA for Android now available on select devices (一部のデバイスで OWA for Android が利用可能になりました)](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)」を参照してください。

## Azure RMS による Office のサポートの詳細

Office のすべてのエディション (Office 2007 を除く) で、保護されたコンテンツの使用がサポートされます。

Azure RMS と Office Professional Plus 2010 または Office Professional 2010:

- Windows 用 Rights Management 共有アプリケーションが必要です

- Windows 10 ではサポートされていません


## Rights Management 共有アプリケーションの詳細

Windows 用 Rights Management 共有アプリケーションの詳細については、以下のリソースを参照してください。

-   [Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)

-   [Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)

モバイル プラットフォーム用 Rights Management 共有アプリケーションの詳細については、以下のリソースを参照してください。

-   [Microsoft Rights Management のページ](http://go.microsoft.com/fwlink/?LinkId=303970)にあるリンクを使用して関連アプリをダウンロードする

-   Microsoft Intune を使用している場合は、ポリシー管理型アプリを使用して、アプリをデプロイおよび管理できます。 

    -   Intune で登録されている iOS および Android デバイスについては、「[Microsoft Intune でモバイル アプリケーション管理ポリシーを使用してデータを保護する](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)」をご覧ください。

    -   Intune で登録されていない Android デバイスについては、「[Microsoft Intune でのモバイル アプリ管理ポリシーの作成および展開](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune)」をご覧ください。

-   [モバイル プラットフォーム用 Microsoft Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn451248)



## Azure RMS をサポートしている他のアプリケーションの詳細

テーブル内のアプリケーションだけでなく、RMS API をサポートするアプリケーションはどれでも Azure RMS と統合できます。次のようなアプリケーションがこれに該当します。

- RMS SDK を使用して社内で作成した基幹業務アプリケーション

- RMS SDK を使用してソフトウェア ベンダーが作成したアプリケーション

SDK の詳細については、「[Microsoft Rights Management SDK](../develop/developers-guide.md)」を参照してください。

## Azure RMS でサポートされていないアプリケーション

Azure RMS では、現在のところ以下のアプリケーションはサポートされません。

-   Microsoft Office for Mac 2011:

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS ビューアー
 
また、RMS 共有アプリケーションには次の制限事項があります。

-   Windows コンピューターの場合: Windows 7 Service Pack 1 以降が必要です



## 次のステップ
その他の要件を確認するには、「[Azure Rights Management の要件](requirements-azure-rms.md)」を参照してください。

これらの最も一般的に使用されるアプリケーションが Azure RMS をサポートする方法の詳細については、「[アプリケーションで Azure Rights Management をサポートする方法](../understand-explore/applications-support.md)」を参照してください。

Azure RMS で最も一般的に使用されるアプリケーション を構成する方法の詳細については、「[Azure Rights Management 用にアプリケーションを構成する](../deploy-use/configure-applications.md)」を参照してください。

<!--HONumber=Apr16_HO4-->


