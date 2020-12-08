---
title: アプリケーションでの Azure Information Protection の RMS データ保護のサポート
description: Azure Rights Management (Azure RMS) サービスがネイティブでサポートされるアプリケーションとソリューションを特定します。 Azure RMS によって、Azure Information Protection (AIP) のデータ保護が提供されます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f25b020a72a48e79b24840a597aefd4cc9e594af
ms.sourcegitcommit: 13dac930fabafeb05d71d7ae8acf5c0a78c12397
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96849706"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするアプリケーション

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

このページに一覧表示されているアプリケーションとソフトウェアにより、Azure Information Protection のデータ保護を提供する Azure Rights Management (Azure RMS) サービスがネイティブでサポートされます。

これらのアプリケーションとソリューションは、"RMS 対応" と呼ばれ、Rights Management および[使用制限](configure-usage-rights.md)が Rights Management API を使用して密接に統合されています。

> [!NOTE]
> 別途明記されていない限り、サポートされる機能は Azure RMS と AD RMS の両方に適用されます。 
>
> iOS、Android、macOS、および Windows Phone 8.1 での AD RMS のサポートには、[Active Directory Rights Management サービス モバイル デバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))も必要です。
> 

## <a name="windows-rms-enlightened-applications"></a>Windows RMS 対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - [Microsoft 365 アプリ](#microsoft-365-app-support) <br />- Office 2010 <br />- Office 2013<br />- Office 2016 <br />- Office 2019 <br />- [Office for the web (保護されたドキュメントの表示)](#viewing-protected-documents-in-office-for-the-web)<br />- [Web ブラウザー](#web-browser-support)        |
|[**電子メール**](#viewing-protected-content-in-email-clients)      |   - Outlook 2010<br />- Outlook 2013<br />- Outlook 2016 <br />- Outlook 2019 <br />- Microsoft 365 Apps for Enterprise の Outlook<br />- [Web ブラウザー](#web-browser-support)<br />- [Windows メール](#email-clients-using-exchange-activesync-irm)|
|[**他のファイルの種類**](#supported-text-and-image-file-types)    |  - Microsoft 365 アプリ、Office 2019、および Office 2016 の Visio: **.vsdm、** **.vsdx、** **.vssm**、 **.vstm**、 **.vssx**、 **.vstx** <br />- Windows 用 Azure Information Protection クライアント: テキスト、画像、**pfile** <br />- AutoCAD 用 SealPath RMS プラグイン: **.dwg**       |
| | |

## <a name="macos-rms-enlightened-applications"></a>macOS RMS 対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    |  - Microsoft 365 アプリ、バージョン 16.40 以降 <br />- Office 2019 for Mac、バージョン 16.40 以降<br />- Office 2016 for Mac、バージョン 16.16.27 以降<br />- [Office for the web](#viewing-protected-documents-in-office-for-the-web)<br />- [Web ブラウザー](#web-browser-support)    |
|[**電子メール**](#viewing-protected-content-in-email-clients)   |   - Outlook 2019 for Mac、バージョン 16.40 以降<br />- Outlook 2016 for Mac、バージョン 16.16.27 以降<br />- [Web ブラウザー](#web-browser-support)     |
|[**他のファイルの種類**](#supported-text-and-image-file-types)    | RMS 共有アプリ (保護されているテキスト、イメージ、一般的に保護されているファイルの表示)   |
| | |

## <a name="android-rms-enlightened-applications"></a>Android RMS 対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    |- GigaTrust App for Android<br />- [Office for the web](#viewing-protected-documents-in-office-for-the-web)<br />- Office Mobile (秘密度ラベルを使用しない場合は、保護されたドキュメントの表示と編集に限定) <br />- [Web ブラウザー](#web-browser-support)      |
|[**電子メール**](#viewing-protected-content-in-email-clients)     | - [9Folders](#email-clients-using-exchange-activesync-irm)<br />- Azure Information Protection アプリ (保護された電子メールの表示)<br />- BlackBerry Work <br />- [GigaTrust App for Android](#email-clients-using-exchange-activesync-irm) <br />- Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook for Android](#email-clients-using-exchange-activesync-irm)<br />- [Samsung 電子メール (S3 以降)](#email-clients-using-exchange-activesync-irm)<br />- TITUS Classification for Mobile <br /><br />- [Web ブラウザー](#web-browser-support)       |
|[**他のファイルの種類**](#supported-text-and-image-file-types)    |  Azure Information Protection アプリ (保護されたテキストとイメージの表示)  |
| | |


## <a name="ios-rms-enlightened-applications"></a>iOS RMS 対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    |  - GigaTrust<br />- Office Mobile <br />- [Office for the web](#viewing-protected-documents-in-office-for-the-web)<br />- TITUS Docs<br />- [Web ブラウザー](#web-browser-support)    |
|[**電子メール**](#viewing-protected-content-in-email-clients)     |   - Azure Information Protection アプリ (保護された電子メールの表示)<br />- BlackBerry Work<br />- Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [iPad および iPhone 用 Outlook](#email-clients-using-exchange-activesync-irm)<br />- TITUS Mail <br />- [Web ブラウザー](#web-browser-support)     |
|[**他のファイルの種類**](#supported-text-and-image-file-types)     | - Azure Information Protection アプリ (保護されたテキストとイメージの表示)<br />- TITUS Docs: **Pfile**  |
| | |

## <a name="windows-10-mobile-rms-enlightened-applications"></a>Windows 10 Mobile RMS 対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - Office Mobile アプリ (Azure RMS を使用して保護されたドキュメントの表示) <br />- [Web ブラウザー](#web-browser-support)    |
|[**電子メール**](#viewing-protected-content-in-email-clients)    |  - Citrix WorxMail <br />- Outlook メール (保護された電子メールの表示) <br />- [Web ブラウザー](#web-browser-support)     |
|[**他のファイルの種類**](#supported-text-and-image-file-types)    | サポートされていません   |
| | |

## <a name="blackberry-10-rms-enlightened-applications"></a>Blackberry 10 RMS 対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - [Web ブラウザー](#web-browser-support)    |
|[**電子メール**](#viewing-protected-content-in-email-clients)   | - [Blackberry 電子メール](#email-clients-using-exchange-activesync-irm) <br />- [Web ブラウザー](#web-browser-support)      |
|[**他のファイルの種類**](#supported-text-and-image-file-types)    | サポートされていません   |
| | |


## <a name="additional-details-about-rms-enlightened-applications"></a>RMS 対応アプリケーションに関する追加の詳細情報

上の表に一覧表示されている RMS 対応アプリケーションの詳細については、以下を参照してください。

- [電子メール クライアントでの保護されたコンテンツの表示](#viewing-protected-content-in-email-clients)
- [サポートされているテキスト ファイルと画像ファイルの種類](#supported-text-and-image-file-types)
- [Microsoft 365 アプリのサポート](#microsoft-365-app-support)
- [Office for the web での保護されたドキュメントの表示](#viewing-protected-documents-in-office-for-the-web)
- [Web ブラウザーのサポート](#web-browser-support)
- [Exchange ActiveSync Information Rights Management (IRM) を使用する電子メール クライアント](#email-clients-using-exchange-activesync-irm)

### <a name="viewing-protected-content-in-email-clients"></a>電子メール クライアントでの保護されたコンテンツの表示

電子メール クライアントによってメッセージが保護される場合、そのメッセージに添付されており、現在保護されていない Office ファイルはすべて、電子メール メッセージと共に保護されます。 このような場合、電子メール メッセージと添付ファイルの両方を電子メール クライアントで表示できるのは、許可された受信者のみとなります。

しかし、添付ファイルのみが保護されており、電子メール メッセージ自体は保護されていない場合、許可された受信者であっても、電子メール クライアントで添付ファイルをプレビューすることはできません。

> [!TIP]
> 電子メールの保護をサポートしていない電子メール クライアントの場合は、[Exchange Online メール フロー ルールを使用してこの保護を適用する](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)ことを検討してください。

### <a name="supported-text-and-image-file-types"></a>サポートされているテキスト ファイルと画像ファイルの種類

Office ファイルや電子メール メッセージ以外のファイルの種類には、テキストおよび画像ファイルの種類が含まれ、 **.txt、** **.xml、** **.jpg、** 、 **.jpeg** などの拡張子が付いています。 

これらのファイルは、Rights Management によってネイティブで保護された後に、そのファイル名拡張子が変更され、読み取り専用になります。 

ネイティブで保護できないファイルは、Rights Management によって一般的に保護された後に、 **.pfile** というファイル名拡張子が付けられます。

詳細については、「[サポートされるファイルの種類](./rms-client/client-admin-guide-file-types.md)」を参照してください。

### <a name="microsoft-365-app-support"></a>Microsoft 365 アプリのサポート

含まれるもの: 
- Office アプリ。[更新チャネルによる Microsoft 365 アプリにサポートされている表](/officeupdates/update-history-microsoft365-apps-by-date)に記載されているバージョンについては、ユーザーに Azure Rights Management (Azure Information Protection for Office 365 ともいう) のライセンスが割り当てられている場合は、Microsoft 365 Apps for Business または Microsoft 365 Business Premium の Office アプリの最小バージョン 1805、ビルド 9330.2078
- Microsoft 365 Apps for enterprise

### <a name="viewing-protected-documents-in-office-for-the-web"></a>Office for the web での保護されたドキュメントの表示

Microsoft SharePoint および OneDrive でのみサポートされており、ドキュメントは保護されているライブラリにアップロードされる前に保護が解除されます。

### <a name="web-browser-support"></a>Web ブラウザー サポート

- [Microsoft 365 メッセージ暗号化と新機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)を使用して [Office 添付ファイル](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)が保護されている場合、**Word、Excel、および PowerPoint** ファイルで Web ブラウザーがサポートされます。

- **電子メール** の場合、Web ブラウザーは次のシナリオでのみサポートされます。

    - 送信者と受信者の両方が同じ組織に属する場合
    - 送信者または受信者が Exchange Online を使用している場合
    - 送信者がハイブリッド構成でオンプレミスの Exchange を使用している場合 

### <a name="email-clients-using-exchange-activesync-irm"></a>Exchange ActiveSync IRM を使用する電子メール クライアント

次の電子メール クライアントによって Exchange ActiveSync IRM が使用されます。これは、Exchange 管理者が有効にする必要があります。

- Windows メール
- 9Folders
- GigaTrust App for Android
- NitroDesk
- Outlook for Android
- Samsung Email (S3 以降)
- iPad および iPhone 用 Outlook
- Blackberry 電子メール

ユーザーは保護された電子メール メッセージを表示、返信、全員に返信することができますが、新しい電子メール メッセージを保護することはできません。
 
Exchange ActiveSync IRM が有効になっていないために、電子メール アプリケーションがメッセージをレンダリングできない場合は、送信者がハイブリッド構成で Exchange Online またはオンプレミス Exchange を使用していれば、受信者は Web ブラウザーで電子メールを表示できます。 

## <a name="azure-rms-support-for-office"></a>Azure RMS による Office のサポート

Azure RMS は、Word、Excel、PowerPoint、および Outlook のアプリケーションと緊密に統合されています。多くの場合、この機能は Information Rights Management (IRM) と呼ばれます。 

- [Information Rights Management (IRM) 用の Windows コンピューター](#windows-computers-for-information-rights-management-irm)
- [Information Rights Management (IRM) 用の Mac コンピューター](#mac-computers-for-information-rights-management-irm)

関連項目: [Office アプリケーション サービスの説明](/office365/servicedescriptions/office-applications-service-description/office-applications-service-description)

### <a name="windows-computers-for-information-rights-management-irm"></a>Information Rights Management (IRM) 用の Windows コンピューター

次の Office クライアント スイートは、Windows コンピューター上にあるファイルや電子メールの Azure Rights Management サービスを使用した保護をサポートします。

- **Office アプリ**。[更新チャネルによる Microsoft 365 アプリにサポートされている表](/officeupdates/update-history-microsoft365-apps-by-date)に記載されているバージョンについては、ユーザーに Azure Rights Management (Azure Information Protection for Office 365 ともいう) のライセンスが割り当てられている場合は、Microsoft 365 Apps for Business または Microsoft 365 Business Premium の Office アプリの最小バージョン 1805、ビルド 9330.2078

- **Microsoft 365 Apps for Enterprise**

    これらのエディションの Office は、Azure Information Protection のデータ保護を含むほぼすべてのサブスクリプションに含まれています。 サブスクリプション情報を調べ、Microsoft 365 Apps for Enterprise ProPlus が含まれているかどうかを確認してください。 この情報は、[Azure Information Protection データシート](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)にもあります。

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013**

- **Office Professional Plus 2010 Service Pack 2**

Office のすべてのエディション (Office 2007 を除く) で、保護されたコンテンツの使用がサポートされます。

#### <a name="azure-rights-management-service-with-office-professional-plus-2010-and-service-pack-2-or-office-professional-2010-with-service-pack-2"></a>Office Professional Plus 2010 Service Pack 2 または Office Professional 2010 Service Pack 2 を使用する Azure Rights Management サービス

Office Professional Plus 2010 Service Pack 2 または Office Professional 2010 Service Pack 2 で Azure Rights Management サービスを使用する場合は、Windows 用 AIP クライアントも必要です。

また、この構成は次のようになります。

- Windows 10 でサポートされていません。
- フェデレーションされるユーザー アカウントのフォーム ベース認証はサポートされていません。 これらのアカウントで、Windows 統合認証を使用する必要があります。
- AIP クライアントで選択されたカスタム アクセス許可を使用して、テンプレート保護をオーバーライドする機能はサポートされていません。 このシナリオでは、カスタムのアクセス許可を適用する前に、元の保護を取り除く必要があります。

### <a name="mac-computers-for-information-rights-management-irm"></a>Information Rights Management (IRM) 用の Mac コンピューター

次の Office クライアント スイートは、macOS 上にあるファイルや電子メールの Azure RMS を使用した保護をサポートします。

- Microsoft 365 Apps for enterprise
- Office Standard 2019 for Mac
- Office Standard 2016 for Mac

Office for Mac 2019 および Office for Mac 2016 のすべてのエディションで、保護されたコンテンツの使用がサポートされます。

> [!TIP]
> Office for Mac を使用してドキュメントの保護を開始するには、次の FAQ が役に立ちます: [ドキュメントを保護および追跡するように Mac コンピューターを設定するにはどうすればよいのですか?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)
> 
## <a name="azure-information-protection-apps-for-ios-and-android"></a>iOS 用と Android 用の Azure Information Protection

iOS および Android 用の Azure Information Protection アプリにより、これらのモバイル デバイス上に保護された電子メールを開くことができる電子メール アプリがない場合に、権利で保護された電子メール メッセージ ( **.rpmsg** ファイル) 用のビューアーが提供されます。 このアプリでは、権利で保護された PDF ファイル、画像、テキスト ファイルも開くことができます。

iOS デバイスや Android デバイスを Microsoft Intune で登録している場合、ユーザーは Intune ポータル サイトからアプリをインストールでき、管理者は Intune の[アプリ保護ポリシー](/intune/apps/app-protection-policies)を使用してアプリを管理できます。

アプリの使用方法について詳しくは、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](./rms-client/mobile-app-faq.md)」をご覧ください。

## <a name="the-azure-information-protection-client-for-windows"></a>Windows 用 Azure Information Protection クライアント

Azure Information Protection (AIP) クライアントには 2 つのバージョンが含まれており、バージョンごとに管理者およびユーザー ガイドがあります。

- **統合ラベル付けクライアント**:
    - [管理者ガイド](./rms-client/clientv2-admin-guide.md)
    - [ユーザー ガイド](./rms-client/clientv2-user-guide.md)

- **クラシック クライアント**:
    - [管理者ガイド](./rms-client/client-admin-guide.md)
    - [ユーザー ガイド](./rms-client/client-user-guide.md)

[Microsoft Azure Information Protection のページ](https://go.microsoft.com/fwlink/?LinkId=303970)から関連アプリをダウンロードします。

> [!NOTE]
> これら 2 つのバージョンの違いがよくわかりませんか? 関連する [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) を参照してください。
> 
## <a name="rights-management-sharing-app"></a>Rights Management 共有アプリ

Mac コンピューターの場合、Rights Management 共有アプリにより、保護された PDF ファイル **(.ppdf)** 、保護されたテキスト イメージ、および一般的に保護されたファイル用のビューアーが提供されます。 イメージ ファイルも保護できますが、他のファイルを保護することはできません。 これらのコンピューターで Office ファイルを保護するには、Office for Mac または Microsoft 365 Apps for Enterprise を使用します。 

詳細については、[モバイル プラットフォーム用 Microsoft Rights Management 共有アプリケーションの FAQ](/previous-versions/msdn10/dn451248(v=msdn.10)) に関するページを参照してください

[Microsoft Azure Information Protection のページ](https://go.microsoft.com/fwlink/?LinkId=303970)から、Mac コンピューター用の Rights Management 共有アプリをダウンロードします。

## <a name="other-applications-that-support-azure-information-protection"></a>Azure Information Protection をサポートするその他のアプリケーション

上に一覧表示されているアプリケーションだけでなく、Azure Rights Management サービスの API をサポートするアプリケーションはすべて、Azure Information Protection と統合することができます。 

例として、社内で作成された基幹業務アプリケーションや、RSM SDK を使用して作成されたソフトウェア ベンダーのアプリケーションが挙げられます。

詳細については、「[Azure Information Protection 開発者ガイド](./develop/developers-guide.md)」を参照してください。

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Azure RMS でサポートされていないアプリケーション

Azure RMS で現在サポートされていないアプリケーションには次のようなものがあります。

- Microsoft OneDrive for SharePoint Server 2013
- XPS ビューアー
- Windows 7 Service Pack 1 より前のバージョンの Windows で実行されているアプリケーション


## <a name="next-steps"></a>次のステップ

次の用語も参照:

- 「[Azure Information Protection の要件](requirements.md)」で確認してください。
- [アプリケーションによる Azure Rights Management サービスのサポート](./applications-support.md)。
- [Azure Rights Management 用にアプリケーションを構成する](configure-applications.md)。

Azure Rights Management サービスと Azure Information Protection をサポートするソリューションの最新情報については、ブログ記事「[Microsoft Ignite 2019 – Microsoft Information Protection ソリューションのパートナー エコシステム ショーケース](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024)」を参照してください。