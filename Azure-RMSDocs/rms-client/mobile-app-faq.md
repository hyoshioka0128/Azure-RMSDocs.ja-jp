---
title: "iOS 用と Android 用の Azure Information Protection アプリに関する FAQ"
description: 
keywords: "iOS 用および Android 用の Azure Information Protection アプリの使用に役立つよく寄せられる質問"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/05/2017
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5ea28525653966d2de609c118bd18079cff99b2d
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ

*適用対象: Active Directory Rights Management サービス、Azure Information Protection*

このページでは、iOS 用および Android 用の Azure Information Protection アプリの使用に役立つよく寄せられる質問への回答を示します。

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>Azure Information Protection アプリを使ってできる操作

お使いの電子メール アプリが Rights Management データ保護をネイティブにサポートしていない場合、このアプリを使うと、権利が保護された電子メール メッセージ (.rpmsg ファイル) を表示できます。 このアプリでは、権利で保護された PDF ファイル、画像、テキスト ファイルを表示することもできます。 現時点では、このアプリを使用して、保護されたメール メッセージを新規作成したり、メール メッセージに返信したり、保護されたファイルを作成または編集したりすることはできません。

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>SharePoint の保護されているライブラリと OneDrive for Business にある PDF ファイルを開くことはできますか。

はい。SharePoint と OneDrive for Business によって、他のユーザーがお客様と共有している保護された PDF ファイルを開くことができます。 リンクをタップし、このアプリを選択してファイルを自分用に開きます。 

このアプリで、SharePoint と OneDrive for Business の外部で保護されている PDF ファイル (保護されている PDF ファイルと .ppdf ファイル) を開くこともできます。

## <a name="can-my-mobile-device-run-the-azure-information-protection-app"></a>モバイル デバイスで Azure Information Protection アプリを実行するには

Azure Information Protection アプリには、**iOS 8** 以降または **Android 4.4** 以降が必要になります。

これらのバージョン以降を搭載している場合は、モバイル デバイスにアプリをインストールして実行できます。

- モバイル デバイスが Microsoft Intune で管理されている場合は、ポータル サイトから Azure Information Protection アプリをインストールできます。

- モバイル デバイスが Microsoft Intune で管理されていない、または Azure Information Protection アプリをポータル サイトで入手できない場合は、iTunes ストアや Google Play ストアから直接インストールするか、[Azure Information Protection のダウンロード ページ](https://portal.azurerms.com/#/download)の **[モバイル デバイス]** セクションから iOS または Android のアイコンをクリックしてアプリをインストールすることができます。 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>ビューアー アプリを開始するにはどうすればよいですか。

アプリをインストールした後、その時点では何もする必要はありません。 表示対象の保護された電子メールまたはファイルを取得するまで待機し、**[AIP Viewer]** を選択して開きます。 職場または学校アカウントでサインインするか、証明書を選択するように求められます。 これらの資格情報が認証されると、コンテンツを読み取ることができます。

ただし、待機しない場合は、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリの開始](mobile-app-get-started.md)」の手順に従って、表示対象の保護された電子メールまたはファイルを自分自身に送信できます 
## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>このアプリにサインインするにはどのような資格情報を使用する必要がありますか?

組織が既に (モバイル デバイス拡張機能と共に) オンプレミスの AD RMS を所有している、または Azure Rights Management サービスを使用している場合は、自分の資格情報を使用してサインインできます。 それ以外の場合は、[Azure Information Protection ページ](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)を使用して、無料の新しいアカウントにサインアップできます。

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>Hotmail または Gmail アカウントなど、個人の電子メール アドレスで無料アカウントにサインアップできますか?

まだできません。 現在、勤務先の電子メール アドレス (職場または学校のアカウント) でのみサインアップできます。 個人の電子メール アドレスのサポートに取り組んでおり、利用可能になった場合はこのエントリを更新します。

## <a name="which-file-extensions-can-i-open-with-this-app"></a>このアプリで開くことができるファイル拡張子

.rpmsg、.pdf、.ppdf、.pjpg、.ptxt、およびその他のいくつかのテキストと画像ファイル形式を開くことができます。

##  <a name="how-do-i-provide-feedback-about-this-app"></a>このアプリに関するフィードバックを提供する方法

アプリで、**[設定]** > **[フィードバックの送信]** に移動します。


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>自分の質問が回答されていません。どうすればよいですか。

質問を [Yammer サイト](https://www.yammer.com/AskIPTeam) に投稿するか、または [情報保護チームに電子メールを送信](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app)してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]