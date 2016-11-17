---
title: "Azure Information Protection の要件 - 記事の全文 | Azure Information Protection"
description: "組織の Azure Information Protection をデプロイするための前提条件を特定します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 10cf9371-a61b-495f-9d42-898448806994
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 68b3d74d32b98f44cfdf9cf78b7a9151f16124ce
ms.openlocfilehash: b4afd639439f0549ce38de1e63a1798d30680066


---


# <a name="requirements-for-azure-information-protection"></a>Azure Information Protection の要件

>*適用対象: Azure Information Protection、Office 365*


組織の Azure Information Protection をデプロイする前に、次の前提条件が満たされていることを確認します。 

|要件|詳細情報|
|---------------|--------------------|
|Azure Information Protection のサブスクリプション|Azure Information Protection サイトの[サブスクリプション情報](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)および[機能一覧](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)を見て、使用する Azure Information Protection 機能を含むサブスクリプションを組織が所有していることを確認します。|
|Azure Active Directory|組織には Azure Information Protection のユーザー認証をサポートするための Azure Active Directory (Azure AD) が必要です。 また、オンプレミスのディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。<br /><br />アカウントがフェデレーションされる (たとえば、AD FS を使用する) 場合、Windows 統合認証を使用する必要があります。 Azure Information Protection では、フォーム ベースの認証はサポートされていません。<br /><br />必要なクライアント ソフトウェアと正しく構成された MFA サポート インフラストラクチャがある場合は、Azure Information Protection で多要素認証 (MFA) がサポートされます。<br /><br />詳細については、「[Azure Information Protection の Azure Active Directory の要件](requirements-azure-ad.md)」をご覧ください。|
|クライアント デバイス|ユーザーは Azure Information Protection をサポートするオペレーティング システムを実行するクライアント デバイス (コンピューターまたはモバイル デバイス) を所有している必要があります。<br /><br />次のデバイスでは、Azure Information Protection クライアントをサポートします。これにより、ユーザーは次の Office のドキュメントや電子メールの分類およびラベル付けを行うことができます。<br /><br />- Windows 10 (x86、x64)<br /><br />- Windows 8.1 (x86、x64)<br /><br />- Windows 8 (x86、x64)<br /><br />- Windows 7 Service Pack 1 (x86、x64)<br /><br />Azure Rights Management サービスを使用して、このクライアントがデータを保護する場合は、Azure Rights Management サービスをサポートする同じデバイス (Windows、Mac、iOS、Android) から使用できます。 <br /><br />Azure Rights Management サービスをサポートするデバイスの詳細については、「[Azure Rights Management データ保護をサポートするクライアント デバイス](../get-started/requirements-client-devices.md)」をご覧ください。|
|アプリケーション|Azure Information Protection クライアントは、次の Office スイートの Office アプリケーション **Word**、**Excel**、**PowerPoint**、**Outlook** で作成されたファイルと電子メールのラベル付けと保護をサポートします。<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />Azure Rights Management サービスをサポートするアプリケーションの詳細については、「[Azure Rights Management データ保護をサポートするアプリケーション](requirements-applications.md)」をご覧ください。|
|インターネットと依存クラウド サービスへの接続をサポートするインフラストラクチャ|特定の接続を許可するように構成する必要があるファイアウォールまたは同様の介在するネットワーク デバイスがある場合は、Office 記事「[Office 365 URL および IP アドレス範囲](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」の「[Office 365 ポータルと共有](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)」セクションで **Azure Rights Management (RMS)** に関する情報を参照してください。<br /><br />RSS フィードを購読して最新の情報を入手するには、この Office 記事の手順を使用してください。<br /><br />Office の記事の情報に加えて、Azure Information Protection に固有の要件は以下のとおりです。<br /><br />- **api.informationprotection.azure.com** TCP 443 の HTTPS トラフィックを許可します。<br /><br />- TLS クライアント/サービス間接続を終了しないでください (たとえばパケット レベルの検査を行うために)。 終了すると、Azure RMS との通信を保護するのに RMS クライアントが Microsoft が管理する CA と使用する証明書のピン留めが解除されます。<br /><br />- 認証が必要な Web プロキシを使用している場合には、ユーザーの Active Directory ログオン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。|

オンプレミス サーバーで Azure Information Protection から Azure Rights Management サービスを使用する必要がある場合、次の製品がサポートされます。

-   Exchange Server

-   SharePoint Server

-   ファイル分類インフラストラクチャをサポートする Windows Server ファイル サーバー

このシナリオに関する追加の要件については、「[Azure Rights Management データ保護をサポートするオンプレミス サーバー](requirements-servers.md)」をご覧ください。

> [!IMPORTANT]
> 次のデプロイ シナリオは、Azure Information Protection を使用した AD RMS 保護 ("Hold Your Own Key" または HYOK 構成) を使用している場合を除き、サポートされません。
> 
> -   同一組織での AD RMS および Azure RMS の並列実行 (移行時を除く。詳細については、「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照)。
> 
> [AD RMS から Azure Information Protection への移行](http://technet.microsoft.com/library/Dn858447.aspx)、および [Azure Information Protection から AD RMS への移行](http://msdn.microsoft.com/library/azure/dn629429.aspx)には、サポートされている移行パスがあります。 Azure Information Protection をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Information Protection の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」をご覧ください。

## <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Azure Information Protection の Azure Active Directory の要件

Azure Information Protection を使用するには、Azure AD ディレクトリが必要です。 このディレクトリの組織アカウントを使用して Azure クラシック ポータルにサインインします。ここでは、たとえば、Rights Management テンプレートを構成および管理することができます。

組織の Azure サブスクリプションがまだない場合は、無料試用版にサインアップして取得できます。[Azure の「はじめに」](https://account.windowsazure.com/organization)ページにアクセスし、指示に従ってください。

詳細については、Azure Active Directory ドキュメントの次のリソースを参照してください。

-   [Azure AD ディレクトリとは](/active-directory/active-directory-whatis)

-   [Azure サブスクリプションを Azure Active Directory に関連付ける方法](/active-directory/active-directory-how-subscriptions-associated-directory)

Azure AD ディレクトリをオンプレミス AD フォレストと統合する場合は、「[Integrating your on-premises identities with Azure Active Directory (オンプレミス ID と Azure Active Directory の統合)](/active-directory/active-directory-aadconnect)」を参照してください。

> [!NOTE]
> AD FS または同等な認証プロバイダーを使用してオンプレミスで認証を行うモバイル デバイスまたは Mac コンピューターの場合:
> 
> -   最小サーバー バージョンの **Windows Server 2012 R2** で AD FS を使用するか、OAuth 2.0 プロトコルをサポートするその他の認証プロバイダーを使用する必要があります。

### <a name="multifactor-authentication-mfa-and-azure-information-protection"></a>多要素認証 (MFA) と Azure Information Protection
Azure Information Protection で多要素認証 (MFA) を使用するには、次のうち 1 つ以上が必要です。

-   Office 2013 (最小バージョン):

    -   Office 2013 をお持ちの場合、[2015 年 6 月 9 日付 Office 2013 用更新プログラム (KB3054853)](https://support.microsoft.com/kb/3054853) を必ずインストールしてください。 この更新プログラムの詳細や、Active Directory 認証ライブラリ (ADAL) を使用した最新の認証による Office 2013 へのサインインの詳細については、Office ブログの「[Office 2013 modern authentication public preview announced (Office 2013 最新認証パブリック プレビューの公開)](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)」を参照してください。

-   Windows 用 Rights Management 共有アプリケーション:

    -   最小バージョン 1.0.1908.0 がインストールされている必要があります。バージョンはコントロール パネルの [プログラムと機能] で確認できます。 共有アプリケーションの詳細については、「[Windows 用 Rights Management 共有アプリケーション](../rms-client/sharing-app-windows.md)」を参照してください。

-   モバイル デバイス用や Mac コンピューター用の Rights Management 共有アプリ:

    -   最新バージョンがインストールされていることを確認してください。 MFA では、2015 の年 9 月以降にリリースされた RMS 共有アプリがサポートされます。

確認後、MFA ソリューションを構成します。

-   Microsoft が管理するテナント (Azure Active Directory または Office 365) の場合:

    -   Azure MFA を構成してユーザー向けに MFA を適用します。 手順については、Multi-Factor Authentication ドキュメントの「[Getting started with Azure Multi-Factor Authentication in the cloud (クラウドでの Azure Multi-Factor Authentication の概要)](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)」を参照してください。

        Azure MFA の詳細については、「[What is Azure Multi-Factor Authentication? (Azure Multi-Factor Authentication とは)](/multi-factor-authentication/multi-factor-authentication)」を参照してください。

-   統合テナント (オンプレミスのフェデレーション サーバー) の場合:

    -   使用しているフェデレーション サーバーを Azure Active Directory または Office 365 向けに構成します。 たとえば AD FS を使用している場合は、TechNet の記事「[AD FS の追加の認証方法の構成](https://technet.microsoft.com/library/dn758113.aspx)」をご覧ください。

        このシナリオの詳細については、Office ブログの「[The Works with Office 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)」(Office 365 の機能 – 合理化された ID プログラム) を参照してください。

## <a name="client-devices-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするクライアント デバイス

次のセクションを使用して、Azure Information Protection のデータ保護を提供する、Azure Rights Management サービスをサポートするデバイスを特定します。

### <a name="computers"></a>コンピューター
次のコンピューター オペレーティング システムで Azure Rights Management サービスがサポートされています。

-   **Windows 7** (x86、x64)

-   **Windows 8** (x86、x64)

-   **Windows 8.1** (x86、x64)

-   **Windows 10** (x86、x64)

-   **Mac OS X**: Mac OS X 10.8 (Mountain Lion) 以降

### <a name="mobile-devices"></a>モバイル デバイス
次のモバイル デバイス オペレーティング システムで Azure Rights Management サービスがサポートされています。

-   **Windows Phone**: Windows Phone 8.1

-   **Android 端末およびタブレット**: Android 4.0.3 以降

-   **iPhone および iPad**: iOS 7.0 以降

-   **Windows タブレット**: Windows 10 Mobile および Windows 8.1 RT

## <a name="applications-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするアプリケーション

次の表を使用して、Azure Information Protection のデータ保護を提供する、Azure Rights Management サービス (Azure RMS) をネイティブでサポートするアプリケーションを特定します。 

これらのアプリケーションでは、Rights Management サポートは、使用制限をサポートするために Rights Management API を使用して密接に統合されています。 このようなアプリケーションは RMS 対応とも呼ばれます。

別途明記されていない限り、サポートされる機能は Azure RMS と AD RMS の両方に適用されます。 また、iOS、Android、OS X、Windows Phone 8.1 で AD RMS をサポートするには、[Active Directory Rights Management サービス モバイル デバイス拡張機能](https://technet.microsoft.com/library/dn673574.aspx)が必要です。

表の列に関する情報

-   **保護された PDF**: このファイルの拡張子は .ppdf です。RMS 共有アプリケーションを使用して Office ファイルや PDF ファイルを電子メールで共有すると、自動的に作成されます。 RMS 共有アプリケーションと iOS 用および Android 用の Azure Information Protection アプリには、保護された PDF ファイル用のリーダーが含まれています。 以前に Azure RMS または AD RMS を使用して保護された PDF ファイルを作成していた場合は、Windows、iOS、および Android デバイス上で Foxit Reader および Nitro Pro を使用して、引き続きこれらのファイルを読み取ることができます。

-   **電子メール:** 表示されている電子メール クライアントは、電子メール メッセージを保護できるので、添付されているファイルも自動的に保護されます。 このシナリオでは、クライアントのプレビュー機能で、許可された受信者に対して保護されたコンテンツ (メッセージと添付ファイル) を表示できます。 ただし、電子メール メッセージが保護されておらず、添付ファイルが保護されている場合、クライアントのプレビュー機能では、許可された受信者に対する場合も保護された添付ファイルを表示できません。

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

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Azure Information Protection アプリに関する詳細

iOS 用および Android 用の Azure Information Protection アプリは、これらのデバイスの RMS 共有アプリに置き換わります。 同様の機能を提供し、さらに SharePoint Online 上の権利で保護された電子メール メッセージおよび権利で保護された PDF ファイルをサポートします。

使用している iOS デバイスや Android デバイスが Microsoft Intune で登録された場合、ポリシーで管理されているアプリを使用して、このアプリをデプロイおよび管理できます。 詳細については、Intune のドキュメントの「[Configure and deploy mobile application management policies in the Microsoft Intune console (Microsoft Intune コンソールでモバイル アプリケーション管理ポリシーを構成およびデプロイする)](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)」を参照してください。 この Intune ドキュメントの手順 2 では、ポリシーで管理されているアプリを発行するためにこの手順を使用します。

詳細については、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](../rms-client/mobile-app-faq.md)」をご覧ください。


### <a name="more-information-about-the-rights-management-sharing-application"></a>Rights Management 共有アプリケーションの詳細

Windows 用 Rights Management 共有アプリケーションの詳細については、以下のリソースを参照してください。

-   [Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)

-   [Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)

モバイル プラットフォーム用 Rights Management 共有アプリケーションの詳細については、以下のリソースを参照してください。

-   [Microsoft Rights Management のページ](http://go.microsoft.com/fwlink/?LinkId=303970)にあるリンクを使用して関連アプリをダウンロードする

-   [モバイル プラットフォーム用 Microsoft Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn451248)

> [!NOTE]
> iOS 用および Android 用の RMS 共有アプリケーションは、Azure Information Protection アプリに置き換わっています。

### <a name="more-information-about-other-applications-that-support-azure-rms"></a>Azure RMS をサポートしている他のアプリケーションの詳細

テーブル内のアプリケーションだけでなく、RMS API をサポートするアプリケーションはどれでも Azure RMS と統合できます。次のようなアプリケーションがこれに該当します。

- RMS SDK を使用して社内で作成した基幹業務アプリケーション

- RMS SDK を使用してソフトウェア ベンダーが作成したアプリケーション

SDK の詳細については、「[Microsoft Rights Management SDK](../develop/developers-guide.md)」を参照してください。

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Azure RMS でサポートされていないアプリケーション

Azure RMS では、現在のところ以下のアプリケーションはサポートされません。

-   Microsoft Office for Mac 2011:

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS ビューアー
 
また、RMS 共有アプリケーションには次の制限事項があります。

-   Windows コンピューターの場合: Windows 7 Service Pack 1 以降が必要です

## <a name="onpremises-servers-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするオンプレミス サーバー

Azure Rights Management コネクタを使用すると、次のオンプレミス サーバー製品は Azure Information Protection でサポートされます。 このコネクタは、Office ドキュメントや電子メールを保護するために、Azure Information Protection によって使用される Azure Rights Management サービスとオンプレミス サーバーの間の通信インターフェイス (リレー) として機能します。 

このコネクタを使用するには、Active Directory フォレストと Azure Active Directory とのディレクトリ同期を構成する必要があります。

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Windows Server を実行し、ファイル分類インフラストラクチャ (FCI) を使用するファイル サーバー**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Windows Server 2008 R2 を実行するファイル サーバーには、Rights Management の保護を適用する組み込みのファイル管理タスク アクションがないため、このシナリオには Rights Management コネクタを使用できません。 ただし、Azure RMS を使用してファイルを保護できる実行可能ファイルまたはスクリプトを実行するカスタムのファイル管理タスクを構成する場合、これらのオペレーティング システムでファイル分類インフラストラクチャと Azure RMS を使用できます。 たとえば、[RMS Protection コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)を使用する Windows PowerShell スクリプトなどがあります。
    > 
    > 最新の Windows Server を実行しているサーバーでこれらのコマンドレットを使うこともできます。この場合、すべてのファイル タイプが保護されるという利点があります。 RMS コネクタでは Office ファイルのみ保護されます。 操作手順については、「[Windows Server ファイル分類インフラストラクチャ &#40;FCI&#41; での RMS の保護](../rms-client/configure-fci.md)」を参照してください。

Rights Management コネクタは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 でサポートされています。

これらのオンプレミス サーバーで Rights Management コネクタを構成する方法の詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」をご覧ください。




<!--HONumber=Nov16_HO1-->


