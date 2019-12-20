---
title: iOS 用と Android 用の Azure Information Protection アプリに関する FAQ
description: iOS 用および Android 用の Azure Information Protection アプリの使用に役立つよく寄せられる質問
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: user
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a8f6871f322765abf07087ce3c7bd629bfc9748f
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74160825"
---
# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ

*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

このページでは、iOS 用および Android 用の Azure Information Protection アプリの使用に役立つよく寄せられる質問への回答を示します。

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>Azure Information Protection アプリを使ってできる操作

お使いの電子メール アプリが Rights Management データ保護をネイティブにサポートしていない場合、このアプリを使うと、権利が保護された電子メール メッセージ (.rpmsg ファイル) を表示できます。 このアプリでは、権利で保護された PDF ドキュメントや、権利で保護された画像およびテキスト ファイルを表示させることもできます。 

このアプリはビューアーであるため、これを使って保護されたメール メッセージを新規作成したり、それらに返信したり、保護されたファイルを作成または編集したりすることはできません。 さらに、表示するファイルの添付ファイルをアプリで開くことはできません。 たとえば、保護された PDF ドキュメントや、権利で保護されたメール メッセージの添付ファイルです。

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>SharePoint の保護されているライブラリと OneDrive for Business にある PDF ファイルを開くことはできますか。

はい。SharePoint と OneDrive for Business によって、他のユーザーがお客様と共有している保護された PDF ファイルを開くことができます。 リンクをタップし、このアプリを選択してファイルを自分用に開きます。 

このアプリで、SharePoint と OneDrive for Business の外部で保護されている PDF ファイル (保護されている PDF ファイルと .ppdf ファイル) を開くこともできます。

## <a name="can-my-mobile-device-run-the-azure-information-protection-app"></a>モバイル デバイスで Azure Information Protection アプリを実行するには

Azure Information Protection アプリには、 **iOS 11**または**Android 6.0**の最小バージョンが必要です。

これらのバージョン以降を搭載している場合は、モバイル デバイスにアプリをインストールして実行できます。

- モバイル デバイスが Microsoft Intune で管理されている場合は、ポータル サイトから Azure Information Protection アプリをインストールできます。

- モバイル デバイスが Microsoft Intune で管理されていない、または Azure Information Protection アプリをポータル サイトで入手できない場合は、iTunes ストアや Google Play ストアから直接インストールするか、[Azure Information Protection のダウンロード ページ](https://portal.azurerms.com/#/download)の **[モバイル デバイス]** セクションから iOS または Android のアイコンをクリックしてアプリをインストールすることができます。 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>ビューアー アプリを開始するにはどうすればよいですか。

アプリをインストールした後、その時点では何もする必要はありません。 表示対象の保護された電子メールまたはファイルを取得するまで待機し、 **[AIP Viewer]** を選択して開きます。 職場または学校アカウントでサインインするか、証明書を選択するように求められます。 これらの資格情報が認証されると、コンテンツを読み取ることができます。

ただし、待機しない場合は、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリの開始](mobile-app-get-started.md)」の手順に従って、表示対象の保護された電子メールまたはファイルを自分自身に送信できます 

## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>このアプリにサインインするにはどのような資格情報を使用する必要がありますか?

組織が既にオンプレミスの AD RMS (モバイルデバイス拡張機能を使用) している場合、または Azure Information Protection を使用している場合は、職場の資格情報を使用してサインインします。 

ファイルの保護に個人の電子メール アドレスが使用されている場合は、無料の [Microsoft アカウント](https://signup.live.com)の資格情報を使用してサインインします。

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>Hotmail または Gmail アカウントなど、個人の電子メール アドレスで無料アカウントにサインアップできますか?

はい、Microsoft アカウントを申請する際には、Hotmail や Gmail などの電子メール アドレスのほか、所有しているその他の電子メール アドレスを指定できます。 

ただし、このビューアーではこのアカウントを使って保護されたファイルを開くことができますが、認証に Microsoft アカウントが使用されている場合、アプリケーションによっては、保護されたコンテンツを開けない場合もあります。 [詳細情報](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="which-file-extensions-can-i-open-with-this-app"></a>このアプリで開くことができるファイル拡張子

.rpmsg、.pdf、.ppdf、.pjpg、.pjpeg、.ptiff、.ppng、.ptxt、.pxml などのテキストと画像ファイル形式を開くことができます。

テキストと画像ファイルの拡張子一覧については、管理者ガイドの「[分類と保護がサポートされているファイルの種類](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)」に記載されている最初の表を参照してください。

##  <a name="how-do-i-provide-feedback-about-this-app"></a>このアプリに関するフィードバックを提供する方法

アプリで、 **[設定]**  >  **[フィードバックの送信]** に移動します。


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>自分の質問が回答されていません。どうすればよいですか。

[Yammer サイト](https://www.yammer.com/AskIPTeam)に質問を投稿してください。
