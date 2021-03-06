---
title: アプリケーションでの RMS データ保護のサポート - AIP
description: Azure Information Protection から Azure Rights Management サービスをネイティブにサポートするために、RMS API を使用するアプリケーションを特定します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d2bad5f6d4c1ec9a0e7497569781afa9aed47452
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64768108"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするアプリケーション

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


次の各表を使用して、Azure Information Protection のデータ保護を提供する、Azure Rights Management サービス (Azure RMS) をネイティブでサポートするアプリケーションおよびソリューションを特定します。

これらのアプリケーションおよびソリューションでは、Rights Management サポートは、使用制限をサポートするために Rights Management API を使用して密接に統合されています。 このようなアプリケーションおよびソリューションは、"RMS 対応" とも呼ばれます。

別途明記されていない限り、サポートされる機能は Azure RMS と AD RMS の両方に適用されます。 また、iOS、Android、macOS、Windows Phone 8.1 で AD RMS をサポートするには、[Active Directory Rights Management サービス モバイル デバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))が必要です。

## <a name="rms-enlightened-applications"></a>RMS 対応アプリケーション

次の表に、Microsoft およびソフトウェア ベンダーによる RMS 対応のクライアント アプリケーションを示します。 

保護された PDF ドキュメントの表示の詳細については、「[Microsoft Information Protection の保護された PDF リーダー](./rms-client/protected-pdf-readers.md)」を参照してください。

表の列に関する情報

-   **電子メール**: 表示されている電子メール クライアントは、電子メール メッセージ自体を保護できるため、まだ保護されていない添付の Office ファイルも自動的に保護されます。 このシナリオでは、クライアントのプレビュー機能で、許可された受信者に対して保護されたコンテンツ (メッセージと添付ファイル) を表示できます。 ただし、電子メール メッセージが保護さておらず、添付ファイルが保護されている場合、クライアントのプレビュー機能では、許可された受信者に対する場合も保護された添付ファイルを表示できません。 
    
    ヒント:電子メールの保護をサポートしていない電子メール クライアントの場合は、[Exchange Online メール フロー ルールを使用してこの保護を適用する](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)ことを検討してください。

-   **他のファイルの種類**: テキスト ファイルと画像ファイルには、.txt、.xml、.jpg、.jpeg などのファイル名拡張子が付いているファイルがあります。 これらのファイルでは、Rights Management によりネイティブで保護された後に、ファイル名拡張子が変更され、読み取り専用になります。 ネイティブで保護できないファイルでは、Rights Management によって一般的に保護された後に、ファイル名拡張子が .pfile になります。 詳細については、Azure Information Protection クライアント管理者ガイドの[サポートされるファイルの種類](./rms-client/client-admin-guide-file-types.md)に関する記述を参照してください。


|**デバイス オペレーティング システム**|Word、Excel、PowerPoint|Email|他のファイルの種類|
|---------------------------|-----------------------|-----------------|---------|
|**Windows**|Office 365 アプリ [[1]](#footnote-1)<br /><br />Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office 2019 <br /><br />Office Online (保護されたドキュメントの表示) [[2]](#footnote-2)<br /><br />Web ブラウザー [[3]](#footnote-3)|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Office 2019 <br /><br />Office 365 ProPlus<br /><br />Web ブラウザー [[4]](#footnote-4)<br /><br />Windows メール[[5]](#footnote-5) |Windows 用 Azure Information Protection クライアント: テキスト、イメージ、pfile<br /><br />AutoCAD 用 SealPath RMS プラグイン: .dwg|
|**Android**|GigaTrust<br /><br /> Office Mobile <br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS Docs<br /><br />Web ブラウザー [[3]](#footnote-3)|Azure Information Protection アプリ (保護された電子メールの表示)<br /><br />BlackBerry Work<br /><br />Citrix WorxMail <br /><br />NitroDesk [[5]](#footnote-5)<br /><br />iPad および iPhone 用 Outlook [[5]](#footnote-5)<br /><br />TITUS Mail <br /><br />Web ブラウザー [[4]](#footnote-4)|Azure Information Protection アプリ (保護されたテキストとイメージの表示)<br /><br />TITUS Docs:Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (保護されたドキュメントの表示と編集) <br /><br />Web ブラウザー [[3]](#footnote-3)|9Folders [[5]](#footnote-5)<br /><br />Azure Information Protection アプリ (保護された電子メールの表示)<br /><br />BlackBerry Work <br /><br />GigaTrust App for Android [[5]](#footnote-5)<br /><br />Citrix WorxMail <br /><br />NitroDesk [[5]](#footnote-5)<br /><br />Outlook for Android [[5]](#footnote-5)<br /><br />Samsung Email (S3 以降) [[5]](#footnote-5)<br /><br />TITUS Classification for Mobile <br /><br />Web ブラウザー [[4]](#footnote-4)|Azure Information Protection アプリ (保護されたテキストとイメージの表示)|
|**macOS**|Office 365 アプリ<br /><br />Office 2019 for Mac<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)<br /><br />Web ブラウザー [[3]](#footnote-3)|Outlook 2019 for Mac<br /><br /> Outlook 2016 for Mac<br /><br />Web ブラウザー [[4]](#footnote-4)|RMS 共有アプリ (保護されているテキスト、イメージ、一般的に保護されているファイルの表示)|
|**Windows 10 Mobile**|Office Mobile アプリ (Azure RMS で保護されたドキュメントの表示) <br /><br />Web ブラウザー [[3]](#footnote-3)|Citrix WorxMail <br /><br />Outlook メール (保護されたメールの表示) <br /><br />Web ブラウザー [[4]](#footnote-4)|サポートされていません|
|**Blackberry 10**|Web ブラウザー [[3]](#footnote-3)|Blackberry の電子メール [[5]](#footnote-5) <br /><br />Web ブラウザー [[4]](#footnote-4)|サポートされていません|

###### <a name="footnote-1"></a>脚注 1
主な機能: 
- ユーザーに Azure Rights Management (別名: Azure Information Protection for Office 365) のライセンスが割り当てられている場合は、Office 365 Business または Microsoft 365 Business の最小バージョン 1805、ビルド 9330.2078 の Office アプリ
- Office 365 ProPlus アプリ

###### <a name="footnote-2"></a>脚注 2
SharePoint Online と OneDrive for Business でのみサポートされており、ドキュメントは保護されているライブラリにアップロードする前に保護が解除されます。

###### <a name="footnote-3"></a>脚注 3
[Office 365 Message Encryption とその新機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)で保護された [Office 添付ファイル](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)の場合。

###### <a name="footnote-4"></a>脚注 4
送信者と受信者が同じ組織に属する場合。 あるいは、次の状況のいずれか。
- 送信者または受信者が Exchange Online を利用している。
- 送信者がハイブリッド構成でオンプレミス Exchange を利用している。 

###### <a name="footnote-5"></a>脚注 5:
Exchange ActiveSync IRM を使用します。Exchange の管理者が有効にする必要があります。 ユーザーは保護された電子メール メッセージを表示、返信、全員に返信することができますが、新しい電子メール メッセージを保護することはできません。
 
Exchange ActiveSync IRM が有効になっていないために、電子メール アプリケーションがメッセージをレンダリングできない場合は、送信者がハイブリッド構成で Exchange Online またはオンプレミス Exchange を使用していれば、受信者は Web ブラウザーで電子メールを表示できます。 

### <a name="more-information-about-azure-rms-support-for-office"></a>Azure RMS による Office のサポートの詳細

Azure RMS は、Word、Excel、PowerPoint、および Outlook のアプリケーションと緊密に統合されています。多くの場合、この機能は Information Rights Management (IRM) と呼ばれます。 

関連項目:[Office アプリケーション サービスの説明](https://technet.microsoft.com/library/office-applications-service-description.aspx)

#### <a name="windows-computers-for-information-rights-management-irm"></a>Information Rights Management (IRM) 用の Windows コンピューター

次の Office クライアント スイートは、Windows コンピューター上にあるファイルや電子メールの Azure Rights Management サービスを使用した保護をサポートします。

- ユーザーに Azure Rights Management (別名: Azure Information Protection for Office 365) のライセンスが割り当てられている場合は、Office 365 Business または Microsoft 365 Business の最小バージョン 1805、ビルド 9330.2078 の Office アプリ

- Office 365 ProPlus
    
    Office のこれらのエディションは、Azure Information Protection のデータ保護を含むほぼすべての Office 365 サブスクリプションに含まれています。 Office 365 ProPlus が含まれているかどうかについては、サブスクリプション情報を確認してください。 この情報は、[Azure Information Protection データシート](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)にもあります。

- Office Professional Plus 2019

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010 Service Pack 2

Office のすべてのエディション (Office 2007 を除く) で、保護されたコンテンツの使用がサポートされます。

Office Professional Plus 2010 Service Pack 2 または Office Professional 2010 Service Pack 2 で Azure Rights Management サービスを使用する場合:

- Windows 用 Azure Information Protection クライアントが必要です。

- Windows 10 ではサポートされていません。

- フェデレーションされるユーザー アカウントのフォーム ベース認証はサポートされていません。 これらのアカウントでは、Windows 統合認証を使用する必要があります。

- ユーザーが Azure Information Protection クライアントでカスタムのアクセス許可を選択したとき、テンプレート保護がオーバーライドされることはありません。 このシナリオでは、カスタムのアクセス許可を適用する前に、元の保護を取り除く必要があります。

#### <a name="mac-computers-for-information-rights-management-irm"></a>Information Rights Management (IRM) 用の Mac コンピューター

次の Office クライアント スイートは、macOS 上にあるファイルや電子メールの Azure RMS を使用した保護をサポートします。

- Office 365 ProPlus

- Office Standard 2019 for Mac

- Office Standard 2016 for Mac

Office for Mac 2019 および Office for Mac 2016 のすべてのエディションで、保護されたコンテンツの使用がサポートされます。

ヒント:Office for Mac を使用してドキュメントの保護を開始するには、次の FAQ が役に立ちます: [ドキュメントを保護および追跡するように Mac コンピューターを設定するにはどうすればよいのですか?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Azure Information Protection アプリに関する詳細

iOS 用および Android 用の Azure Information Protection アプリでは、これらのモバイル デバイス上に保護された電子メールを開くことができる電子メール アプリがない場合に、権利で保護された電子メール メッセージ (.rpmsg ファイル) 用のビューアーが提供されます。 このアプリでは、権利で保護された PDF ファイル、画像、テキスト ファイルも開くことができます。

iOS デバイスや Android デバイスを Microsoft Intune で登録している場合、ユーザーは Intune ポータル サイトからアプリをインストールでき、管理者は Intune の[アプリ保護ポリシー](/intune/app-protection-policies)を使用してアプリを管理できます。

アプリの使用方法について詳しくは、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](./rms-client/mobile-app-faq.md)」をご覧ください。


### <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>Windows 用 Azure Information Protection クライアントの詳細

詳細については、次のリソースを参照してください。

- [Azure Information Protection クライアント管理者ガイド](./rms-client/client-admin-guide.md)

- [Azure Information Protection クライアントユーザー ガイド](./rms-client/client-user-guide.md)

- [iOS 用と Android 用の Azure Information Protection の FAQ](./rms-client/mobile-app-faq.md)

[Microsoft Azure Information Protection のページ](https://go.microsoft.com/fwlink/?LinkId=303970)にあるリンクを使用して関連アプリをダウンロードします。

### <a name="more-information-about-the-rights-management-sharing-app"></a>Rights Management 共有アプリの詳細

Mac コンピューターの場合、Rights Management 共有アプリでは、保護された PDF ファイル (.ppdf)、保護されたテキスト イメージ、汎用的に保護されたファイル用のビューアーが提供されます。 イメージ ファイルも保護できますが、他のファイルを保護することはできません。 これらのコンピューターで Office ファイルを保護するには、Office for Mac または Office 365 ProPlus を使用します。 

詳細については、次のリソースを参照してください。

-   [モバイル プラットフォーム用 Microsoft Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn451248)

[Microsoft Azure Information Protection のページ](https://go.microsoft.com/fwlink/?LinkId=303970)にあるリンクを使用して、Mac コンピューター用の Rights Management 共有アプリをダウンロードします。


### <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>Azure Information Protection をサポートしている他のアプリケーションの詳細

表に記載されたアプリケーションだけでなく、Azure Rights Management サービスの API をサポートするアプリケーションはすべて、Azure Information Protection と統合することができます。このようなアプリケーションには次が含まれます。

- RMS SDK を使用して社内で作成した基幹業務アプリケーション。

- RMS SDK を使用してソフトウェア ベンダーが作成したアプリケーション。

詳細については、「[Azure Information Protection 開発者ガイド](./develop/developers-guide.md)」を参照してください。

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Azure RMS でサポートされていないアプリケーション

Azure RMS では、現在のところ以下のアプリケーションはサポートされません。

- Microsoft OneDrive for Business for SharePoint Server 2013

- XPS ビューアー

また、Azure Information Protection クライアントには次の制限があります。

- Windows コンピューター。Windows 7 Service Pack 1 の最小バージョンが必要です。

## <a name="rms-enlightened-solutions"></a>RMS 対応ソリューション

次の表に、ソフトウェア ベンダーによる RMS 対応のソリューションを示します。

御社がソフトウェア ベンダーで、御社のソリューションがこの表に該当するにもかかわらず表示されていない場合は、Azure AD でアプリケーションを登録してください。 詳細については、「[Azure AD でアプリの登録と RMS の有効化を行う方法](./develop/authentication-integration.md)」を参照してください。


|製品|ベンダー|説明|
|-------------------------------|---------------------------|-----------------|
|Absolute|Absolute|データ損失防止 (DLP) を使用したコンテンツの保護。|
|コンテンツ保管ボックス|VMware|保護されたコンテンツの保管、使用、および作成。|
|Controle|TakeControle|ラベル付けおよび保護を使用した eDiscovery。|
|Forcepoint|Forcepoint DLP|組織のデータのセキュリティ ポリシーを適用するエンドポイント データ損失防止 (DLP) ソリューション。|
|Halocore|Secude|SAP 環境からエクスポートされたファイルの保護。|
|MaaS 360|IBM|ドキュメントの使用および保護のための統合。|
|Mobiliya|Mobiliya|EMC Documentum レポジトリのドキュメントのセキュリティ保護。
|Ramessys|Ramessys|Chemcart と Documentum の統合。
|Sealpath|Sealpath Technologies|AutoCAD や Siemens Jt2GO などの CAD デザイン ツールとの統合。
|SecRMM|Sqaudra Technologies |外付けメディアのドキュメント保護。
|Security Sheriff|CryptZone |分類およびアクセス許可に基づいた SharePoint 上のアクセス管理およびドキュメント保護。
|Symantec DLP|Symantec |保護されたファイルの検出と監視。

## <a name="next-steps"></a>次の手順
その他の要件を確認するには、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

これらの最も一般的に使用されるアプリケーションが Azure RMS をサポートする方法の詳細については、「[アプリケーションによる Azure Rights Management サービスのサポート](./applications-support.md)」をご覧ください。

Azure RMS で最も一般的に使用されるアプリケーションを構成する方法の詳細については、「[Azure Rights Management 用にアプリケーションを構成する](configure-applications.md)」を参照してください。

