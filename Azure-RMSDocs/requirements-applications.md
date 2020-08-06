---
title: Azure Information Protection の RMS データ保護のアプリケーションサポート
description: Azure Rights Management (Azure RMS) サービスのネイティブサポートがあるアプリケーションとソリューションを特定します。 Azure RMS は Azure Information Protection (AIP) のデータ保護を提供します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 37cb3b1f3c3eb60459cabe813f0cb00fb69b7d5b
ms.sourcegitcommit: dec5df81b569283a72f0a983d3f53b82cbbc562c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87802166"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするアプリケーション

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

このページに記載されているアプリケーションとソリューションは、Azure Rights Management (Azure RMS) サービスをネイティブでサポートしており、Azure Information Protection のデータ保護を提供します。

これらのアプリケーションとソリューションは "RMS-enlighted と呼ばれ、Rights Management と[使用制限](configure-usage-rights.md)が Rights Management api を使用して密接に統合されています。

> [!NOTE]
> 別途明記されていない限り、サポートされる機能は Azure RMS と AD RMS の両方に適用されます。 
>
> IOS、Android、macOS、および Windows Phone 8.1 で AD RMS サポートには、 [Active Directory Rights Management サービスのモバイルデバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))も必要です。
> 

## <a name="windows-rms-enlightened-applications"></a>Windows RMS-対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - [Office 365 アプリ](#office-365-app-support) <br />- Office 2010 <br />-Office 2013<br />- Office 2016 <br />-Office 2019 <br />- [Web 用 Office (保護されたドキュメントの表示)](#viewing-protected-documents-in-office-for-the-web)<br />- [Web ブラウザー](#web-browser-support)        |
|[**電子メール**](#viewing-protected-content-in-email-clients)      |   -Outlook 2010<br />-Outlook 2013<br />-Outlook 2016 <br />-Outlook 2019 <br />-Office 365 ProPlus の Outlook<br />- [Web ブラウザー](#web-browser-support)<br />- [Windows メール](#email-clients-using-exchange-activesync-irm)|
|[**他のファイルの種類**](#supported-text-and-image-file-types)    |  -Office 365 アプリからの Visio、Office 2019、Office 2016: **vsdm、** **.vsdx、** **vssm**、 **vstm**、 **vssx**、 **.vstx** <br />-Azure Information Protection client for Windows: Text、images、 **pfile** <br />-SealPath RMS プラグイン (AutoCAD): **.dwg**       |
| | |

## <a name="macos-rms-enlightened-applications"></a>macOS RMS-対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    |  -Office 365 アプリ<br />-Mac 用 Office 2019<br />-Mac 用 Office 2016<br />- [Web 用 Office](#viewing-protected-documents-in-office-for-the-web)<br />- [Web ブラウザー](#web-browser-support)    |
|[**電子メール**](#viewing-protected-content-in-email-clients)   |   -Mac 用 Outlook 2019<br />-Mac 用 Outlook 2016<br />- [Web ブラウザー](#web-browser-support)     |
|[**他のファイルの種類**](#supported-text-and-image-file-types)    | RMS 共有アプリ (保護されているテキスト、イメージ、一般的に保護されているファイルの表示)   |
| | |

## <a name="android-rms-enlightened-applications"></a>Android RMS-対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    |-Android 用の GigaTrust アプリ<br />- [Web 用 Office](#viewing-protected-documents-in-office-for-the-web)<br />-Office Mobile (機密ラベルを使用しない場合は、保護されたドキュメントの表示と編集に限定) <br />- [Web ブラウザー](#web-browser-support)      |
|[**電子メール**](#viewing-protected-content-in-email-clients)     | - [9Folders](#email-clients-using-exchange-activesync-irm)<br />-Azure Information Protection アプリ (保護された電子メールの表示)<br />-BlackBerry の作業 <br />- [Android 用 GigaTrust アプリ](#email-clients-using-exchange-activesync-irm) <br />-Citrix のアカウント <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Android 用 Outlook](#email-clients-using-exchange-activesync-irm)<br />- [Samsung Email (S3 以降)](#email-clients-using-exchange-activesync-irm)<br />-Mobile の TITUS 分類 <br /><br />- [Web ブラウザー](#web-browser-support)       |
|[**他のファイルの種類**](#supported-text-and-image-file-types)    |  Azure Information Protection アプリ (保護されたテキストとイメージの表示)  |
| | |


## <a name="ios-rms-enlightened-applications"></a>iOS RMS-対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    |  -GigaTrust<br />-Office Mobile <br />- [Web 用 Office](#viewing-protected-documents-in-office-for-the-web)<br />-TITUS Docs<br />- [Web ブラウザー](#web-browser-support)    |
|[**電子メール**](#viewing-protected-content-in-email-clients)     |   -Azure Information Protection アプリ (保護された電子メールの表示)<br />-BlackBerry の作業<br />-Citrix のアカウント <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [IPad および iPhone 用 Outlook](#email-clients-using-exchange-activesync-irm)<br />-TITUS Mail <br />- [Web ブラウザー](#web-browser-support)     |
|[**他のファイルの種類**](#supported-text-and-image-file-types)     | -Azure Information Protection アプリ (保護するテキストとイメージの表示)<br />-TITUS Docs: **Pfile**  |
| | |

## <a name="windows-10-mobile-rms-enlightened-applications"></a>Windows 10 mobile RMS-対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    | -Office モバイルアプリ (Azure RMS を使用した保護されたドキュメントの表示) <br />- [Web ブラウザー](#web-browser-support)    |
|[**電子メール**](#viewing-protected-content-in-email-clients)    |  -Citrix のアカウント <br />-Outlook メール (保護された電子メールの表示) <br />- [Web ブラウザー](#web-browser-support)     |
|[**他のファイルの種類**](#supported-text-and-image-file-types)    | サポートされていません   |
| | |

## <a name="blackberry-10-rms-enlightened-applications"></a>Blackberry 10 RMS 対応アプリケーション

|Type  |サポートされているアプリケーション   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - [Web ブラウザー](#web-browser-support)    |
|[**電子メール**](#viewing-protected-content-in-email-clients)   | - [Blackberry の電子メール](#email-clients-using-exchange-activesync-irm) <br />- [Web ブラウザー](#web-browser-support)      |
|[**他のファイルの種類**](#supported-text-and-image-file-types)    | サポートされていません   |
| | |


## <a name="additional-details-about-rms-enlightened-applications"></a>RMS 対応アプリケーションに関する追加の詳細情報

上記の表に示す RMS 対応アプリケーションの詳細については、以下を参照してください。

- [電子メールクライアントでの保護されたコンテンツの表示](#viewing-protected-content-in-email-clients)
- [サポートされているテキストファイルとイメージファイルの種類](#supported-text-and-image-file-types)
- [Office 365 アプリのサポート](#office-365-app-support)
- [Office での web 用の保護されたドキュメントの表示](#viewing-protected-documents-in-office-for-the-web)
- [Web ブラウザーのサポート](#web-browser-support)
- [Exchange ActiveSync Information Rights Management (IRM) を使用してクライアントに電子メールを送信する](#email-clients-using-exchange-activesync-irm)

### <a name="viewing-protected-content-in-email-clients"></a>電子メールクライアントでの保護されたコンテンツの表示

電子メールクライアントがメッセージを保護する場合、メッセージに添付され、現在保護されていない Office ファイルは、電子メールメッセージと共に保護されます。 このような場合は、電子メールメッセージと添付ファイルの両方を、承認された受信者のみが電子メールクライアントで表示できます。

ただし、添付ファイルだけが保護されていても、電子メールメッセージ自体は保護されていない場合は、承認された受信者であっても、電子メールクライアントが添付ファイルをプレビューすることはできません。

> [!TIP]
> 電子メールの保護をサポートしていない電子メール クライアントの場合は、[Exchange Online メール フロー ルールを使用してこの保護を適用する](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)ことを検討してください。

### <a name="supported-text-and-image-file-types"></a>サポートされているテキストファイルとイメージファイルの種類

Office ファイルや電子メールメッセージ以外のファイルの種類には、テキストファイルとイメージファイルの種類、 **.txt、** **.xml、** **.jpg、** .jpeg などの拡張子が付いてい**ます**。 

これらのファイルは、Rights Management によってネイティブに保護された後、読み取り専用になると、ファイル名拡張子を変更します。 

ネイティブに保護できないファイルは、Rights Management によって一般的に保護された後、 **pfile**ファイル名拡張子を持ちます。

詳細については、[サポートされているファイルの種類](./rms-client/client-admin-guide-file-types.md)を参照してください。

### <a name="office-365-app-support"></a>Office 365 アプリのサポート

含まれるもの: 
- Office アプリの最小バージョン1805。 Office 365 Business または Microsoft 365 Business から9330.2078 をビルドします。 ユーザーに Azure Rights Management のライセンスが割り当てられている場合にのみサポートされます (Office 365 の Azure Information Protection とも呼ばれます)。
- Office 365 ProPlus アプリ。

### <a name="viewing-protected-documents-in-office-for-the-web"></a>Office での web 用の保護されたドキュメントの表示

Microsoft SharePoint と OneDrive でのみサポートされます。ドキュメントは保護されたライブラリにアップロードされる前に保護されません。

### <a name="web-browser-support"></a>Web ブラウザー サポート

- Office [365 Message Encryption と新機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)を使用して[office の添付](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)ファイルが保護されている場合、 **Word、Excel、および PowerPoint**の各ファイルに対して Web ブラウザーがサポートされます。

- **電子メール**の場合、web ブラウザーは次のシナリオでのみサポートされます。

    - 送信者と受信者の両方が同じ組織に属している場合
    - 送信者または受信者が Exchange Online を使用している場合
    - 送信者がハイブリッド構成で Exchange on-premises を使用している場合 

### <a name="email-clients-using-exchange-activesync-irm"></a>Exchange ActiveSync IRM を使用してクライアントを電子メールで送信する

次の電子メールクライアントは Exchange ActiveSync IRM を使用しますが、Exchange 管理者が有効にする必要があります。

- Windows メール
- 9Folders
- GigaTrust App for Android
- NitroDesk
- Outlook for Android
- Samsung Email (S3 以降)
- iPad および iPhone 用 Outlook
- Blackberry の電子メール

ユーザーは、保護された電子メールメッセージの表示、返信、および返信を行うことができますが、新しい電子メールメッセージを保護することはできません。
 
Exchange ActiveSync IRM が有効になっていないために、電子メール アプリケーションがメッセージをレンダリングできない場合は、送信者がハイブリッド構成で Exchange Online またはオンプレミス Exchange を使用していれば、受信者は Web ブラウザーで電子メールを表示できます。 

## <a name="azure-rms-support-for-office"></a>Office の Azure RMS サポート

Azure RMS は、Word、Excel、PowerPoint、および Outlook のアプリケーションと緊密に統合されています。多くの場合、この機能は Information Rights Management (IRM) と呼ばれます。 

- [Information Rights Management (IRM) 用の Windows コンピューター](#windows-computers-for-information-rights-management-irm)
- [Information Rights Management (IRM) 用の Mac コンピューター](#mac-computers-for-information-rights-management-irm)

関連項目: [Office アプリケーション サービスの説明](https://technet.microsoft.com/library/office-applications-service-description.aspx)

### <a name="windows-computers-for-information-rights-management-irm"></a>Information Rights Management (IRM) 用の Windows コンピューター

次の Office クライアント スイートは、Windows コンピューター上にあるファイルや電子メールの Azure Rights Management サービスを使用した保護をサポートします。

- Office アプリの最小バージョン1805、ユーザーに Azure Rights Management のライセンスが割り当てられている場合 (office 365 の場合は Azure Information Protection とも呼ばれます) に **、office 365 Business または Microsoft 365 Business から9330.2078 をビルド**します。

- **Office 365 ProPlus**

    Office のこれらのエディションは、Azure Information Protection のデータ保護を含むほぼすべての Office 365 サブスクリプションに含まれています。 Office 365 ProPlus が含まれているかどうかについては、サブスクリプション情報を確認してください。 この情報は、[Azure Information Protection データシート](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)にもあります。

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013**

- **Office Professional Plus 2010 Service Pack 2**

Office のすべてのエディション (Office 2007 を除く) で、保護されたコンテンツの使用がサポートされます。

#### <a name="azure-rights-management-service-with-office-professional-plus-2010-and-service-pack-2-or-office-professional-2010-with-service-pack-2"></a>Office Professional Plus 2010 および Service Pack 2 または Office Professional 2010 Service Pack 2 を使用した Azure Rights Management サービス

Office Professional Plus 2010 および Service Pack 2 または Office Professional 2010 (Service Pack 2) で Azure Rights Management サービスを使用する場合は、AIP client for Windows も必要です。

また、この構成は次のようになります。

- は、Windows 10 ではサポートされていません。
- フェデレーションされるユーザー アカウントのフォーム ベース認証はサポートされていません。 これらのアカウントでは、Windows 統合認証を使用する必要があります。
- では、AIP クライアントで選択したカスタムアクセス許可を使用して、テンプレート保護をオーバーライドする機能はサポートされていません。 このシナリオでは、カスタムのアクセス許可を適用する前に、元の保護を取り除く必要があります。

### <a name="mac-computers-for-information-rights-management-irm"></a>Information Rights Management (IRM) 用の Mac コンピューター

次の Office クライアント スイートは、macOS 上にあるファイルや電子メールの Azure RMS を使用した保護をサポートします。

- Office 365 ProPlus
- Office Standard 2019 for Mac
- Office Standard 2016 for Mac

Office for Mac 2019 および Office for Mac 2016 のすべてのエディションで、保護されたコンテンツの使用がサポートされます。

> [!TIP]
> Office for Mac を使用してドキュメントの保護を開始するには、次の FAQ が役に立つことがあります。[操作方法ドキュメントを保護および追跡するように Mac コンピューターを構成](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)するには
> 
## <a name="azure-information-protection-apps-for-ios-and-android"></a>iOS 用と Android 用の Azure Information Protection

IOS および Android 用の Azure Information Protection アプリでは、保護された電子メールを開くことができる電子メールアプリがこれらのモバイルデバイスにない場合に、権利で保護された電子メールメッセージ **(つまり、rpq msg**ファイル) 用のビューアーを提供します。 このアプリでは、権利で保護された PDF ファイル、画像、テキスト ファイルも開くことができます。

iOS デバイスや Android デバイスを Microsoft Intune で登録している場合、ユーザーは Intune ポータル サイトからアプリをインストールでき、管理者は Intune の[アプリ保護ポリシー](/intune/app-protection-policies)を使用してアプリを管理できます。

アプリの使用方法について詳しくは、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](./rms-client/mobile-app-faq.md)」をご覧ください。

## <a name="the-azure-information-protection-client-for-windows"></a>Windows 用の Azure Information Protection クライアント

Azure Information Protection (AIP) クライアントには、各バージョンの管理者ガイドとユーザーガイドを含む2つのバージョンが含まれています。

- 統一された**ラベル付けクライアント**:
    - [管理者ガイド](./rms-client/clientv2-admin-guide.md)
    - [ユーザー ガイド](./rms-client/clientv2-user-guide.md)

- **従来のクライアント**:
    - [管理者ガイド](./rms-client/client-admin-guide.md)
    - [ユーザー ガイド](./rms-client/client-user-guide.md)

[Microsoft Azure Information Protection のページ](https://go.microsoft.com/fwlink/?LinkId=303970)から関連するアプリをダウンロードします。

> [!NOTE]
> これら2つのバージョンの違いについては、 関連する[FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)を参照してください。
> 
## <a name="rights-management-sharing-app"></a>Rights Management 共有アプリ

Mac コンピューターの場合、Rights Management 共有アプリには、保護された PDF ファイル **(ppdf)、** 保護されたテキストイメージ、および一般的に保護されたファイルのビューアーが用意されています。 イメージ ファイルも保護できますが、他のファイルを保護することはできません。 これらのコンピューターで Office ファイルを保護するには、Office for Mac または Office 365 ProPlus を使用します。 

詳細については、「[モバイルプラットフォーム用の Microsoft Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn451248) 」を参照してください。

[Microsoft Azure Information Protection ページ](https://go.microsoft.com/fwlink/?LinkId=303970)から、Mac コンピューター用の Rights Management 共有アプリをダウンロードします。

## <a name="other-applications-that-support-azure-information-protection"></a>Azure Information Protection をサポートするその他のアプリケーション

上記のアプリケーションに加えて、Azure Rights Management サービス用の Api をサポートするすべてのアプリケーションを Azure Information Protection と統合できます。 

例としては、社内で作成された基幹業務アプリケーションや、RSM Sdk を使用して作成されたソフトウェアベンダーのアプリケーションが挙げられます。

詳細については、「[Azure Information Protection 開発者ガイド](./develop/developers-guide.md)」を参照してください。

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Azure RMS でサポートされていないアプリケーション

現在 Azure RMS でサポートされていないアプリケーションには次のものがあります。

- Microsoft OneDrive for SharePoint Server 2013
- XPS ビューアー
- Windows 7 Service Pack 1 より前のバージョンで実行されているアプリケーション


## <a name="next-steps"></a>次のステップ

関連項目:

- [Azure Information Protection の要件](requirements.md)。
- [アプリケーションが Azure Rights Management サービスをサポートする方法](./applications-support.md)。
- [Azure Rights Management 用のアプリケーションを構成して](configure-applications.md)います。

Azure Rights Management サービスと Azure Information Protection をサポートするソリューションの最新情報については、ブログの投稿「 [Microsoft Ignite 2019 – microsoft Information Protection Solutions Partner エコシステムショーケース](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024)」を参照してください。
