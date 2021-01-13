---
title: IOS & Android 用モバイルアプリの Azure Information Protection
description: IOS および Android デバイス用の Azure Information Protection (AIP) モバイルアプリの基本について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/24/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 4b936baf799808fadbdaaefc0ae1fd55a6853fb2
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164456"
---
# <a name="what-is-the-azure-information-protection-app-for-ios-or-android"></a>IOS または Android 用の Azure Information Protection アプリとは

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連する内容**:[AIP の統合ラベル付けクライアントとクラシック クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

IOS および Android 用の Azure Information Protection (AIP) モバイルアプリは、保護された電子メールメッセージ、Pdf、画像、テキストファイルを表示できるビューアーアプリです。これらのファイルの種類の通常のアプリで保護がサポートされていない場合に便利です。 

たとえば、保護された電子メールが通常の電子メールモバイルアプリに添付ファイルとして表示される場合は、AIP モバイルアプリを使用してその電子メールを表示できます。

アプリでサポートされている保護機能の詳細については、 [Azure Rights Management データ保護をサポートするアプリケーション](../requirements-applications.md)」を参照してください。 

> [!NOTE]
> AIP mobile apps は *閲覧者のみで* あり、新しい電子メールを作成したり、電子メールに返信したり、保護されたファイルを作成または編集したりすることはできません。 AIP mobile apps では、保護された Pdf または電子メールの添付ファイルを開くこともできません。
> 

## <a name="download-and-install-the-aip-app-for-your-device"></a>デバイス用の AIP アプリをダウンロードしてインストールする

次のいずれかの場所から AIP mobile apps をダウンロードしてインストールします。

**iTunes**:

:::image type="content" source="../media/ios-icon.png" alt-text="iTunes" link="https://apps.apple.com/app/microsoft-rights-management/id689516635" border="false":::  

**Google Play**:

:::image type="content" source="../media/android-icon.png" alt-text="Google Play" link="https://play.google.com/store/apps/details?id=com.microsoft.ipviewer" border="false"::: 

**会社のポータル**:

モバイルデバイスが Microsoft Intune によって管理されている場合は、ポータルサイトから AIP mobile アプリをダウンロードできます。 

詳細については、システム管理者にお問い合わせください。 
## <a name="ios-view-protected-files-on-your-device"></a>iOS: デバイス上の保護されたファイルを表示する

[AIP モバイルアプリをインストール](#download-and-install-the-aip-app-for-your-device)したら、保護された電子メールまたはファイルを開きます。 

1. ファイルを開くアプリを選択するように求めるメッセージが表示されたら、[共有] ボタンをタップしてファイルを共有します。

    [**ファイルを共有**] を選択し、[ **AIP ビューアーにコピー** ] を選択します。

    例:

    :::image type="content" source="../media/ios-share-to-aip-viewer.png" alt-text="IOS の AIP ビューアーに共有する" border="false":::

1. メッセージが表示されたら、サインインするか、証明書を選択します。

    認証が完了すると、電子メールまたはファイルが AIP ビューアーで開かれます。
 
## <a name="android-view-protected-files-on-your-device"></a>Android: 保護されたファイルをデバイスで表示する

[AIP モバイルアプリをインストール](#download-and-install-the-aip-app-for-your-device)したら、保護された電子メールまたはファイルを開きます。 

1. アプリの選択を求めるメッセージが表示されたら、AIP ビューアーを選択します。

    :::image type="content" source="../media/select-aip-viewer.png" alt-text="AIP Viewer モバイルアプリを選択する":::

1. メッセージが表示されたら、サインインするか、証明書を選択します。

    認証が完了すると、電子メールまたはファイルが AIP ビューアーで開かれます。

## <a name="aip-mobile-app-requirements"></a>AIP モバイルアプリの要件

IOS および Android 用の AIP mobile apps では、次のファイルの種類と環境がサポートされています。

|要件  |説明  |
|---------|---------|
|**サポートされている OS のバージョン**     | 最小モバイル OSs には次のものが含まれます。 </br>-iOS 11  </br>-Android 6.0 </br></br>**注**: AIP モバイルアプリは Intel cpu ではサポートされていません。  |
|**サポートされているサインイン資格情報**     | 次のいずれかを使用して、AIP mobile apps にサインインします。 </br></br>**職場または学校の資格情報。** 職場または学校の資格情報でログインしてみてください。 ご不明な点がある場合は、管理者に連絡して、組織がモバイルデバイス拡張機能を使用してオンプレミスで AD RMS ているか、Azure Information Protection を使用しているかを確認してください。 </br></br>**Microsoft アカウント。** 個人用の電子メールアドレスを使用してファイルを保護していた場合は、 [Microsoft アカウント](https://signup.live.com)でサインインします。 Microsoft アカウントに適用する必要がある場合は、独自の Hotmail、Gmail、またはその他の電子メールアドレスを使用できます。 </br></br>**注**: Microsoft アカウントで保護されたコンテンツを開くことができないアプリケーションもあります。 詳細については、「保護され [たドキュメントを開くためのサポートされるシナリオ](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)」を参照してください。|
|**サポートされているファイルの種類**     | サポートされているファイルの種類には、保護された電子メールメッセージ、PDF ファイル、画像、テキストファイルなどがあります。 </br></br>たとえば、次のような拡張子が含まれています: **rpq msg**、 **.pdf**、 **ppdf**、 **pjpg**、 **pjpg**、 **pjpg**、. **ppdf**、 **pjpg**、 **pjpg** </br></br>サポートされているファイルの種類の完全な一覧については、 [AIP クライアント管理者ガイド](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)を参照してください。|
| | |

## <a name="admins-testing-the-aip-mobile-apps"></a>管理者: AIP mobile アプリのテスト

通常、ほとんどのユーザーは AIP モバイルアプリを使用して、通常のモバイルアプリを使用して開くことができない保護された電子メールまたはファイルを開きます。

組織の AIP mobile アプリをテストするシステム管理者である場合、または自分で試してみたい場合は、以下の手順に従ってプロセス全体を説明してください。

1. デバイスから AIP モバイルアプリでサポートされているファイルの種類にアクセスできることを確認します。 

    たとえば、次の権利で保護されたファイルのいずれかを自分で送信します。

    |ファイルの種類  |Instructions  |
    |---------|---------|
    |**電子メール (rpq msg)**     | Windows コンピューターの Outlook などの別のデバイスを使用して、権限で保護された電子メールメッセージを自分宛てに送信し、モバイルデバイスからアクセスできるようにします。  |
    |**PDF**     | 1. Windows コンピューターから、AIP クライアントを使用して [PDF ファイルを保護](clientv2-classify-protect.md) します。 </br>2. 保護された PDF を自分で送信するか、SharePoint で保護されたライブラリにアップロードして、自分の電子メールアドレスに共有します。        |
    |**イメージ (. ptxt、ptxt、または ppng)**     | 1. Windows コンピューターから、AIP クライアントを使用して [テキストまたはイメージファイルを保護](clientv2-classify-protect.md) します。 </br></br>2. 保護されたファイルを自分で送信するか、SharePoint で保護されたライブラリにアップロードして、自分の電子メールアドレスに共有します。   |
| | |

1. 自分宛てに送信した電子メールの添付ファイルまたはリンクを使用して、モバイルデバイス上の保護されたファイルを開きます。

    たとえば、保護された電子メールは、通常の電子メールモバイルアプリに添付ファイルとして表示されます。 

1. 保護された電子メールまたはファイルを開くためのアプリを選択するように求めるメッセージが表示されたら、 **AIP Viewer** アプリを選択します。

1. メッセージが表示されたら、サインインするか、証明書を選択します。 

    認証が完了すると、AIP Viewer アプリに電子メールまたはファイルが表示されます。

> [!NOTE]
> 常に、保護されたコンテンツを開いて AIP アプリを開きます。 メッセージが表示されるまで、または AIP Viewer アプリ内から保護されたファイルを開くために、アプリへのサインインを試行しないでください。
> 

## <a name="next-steps"></a>次のステップ

AIP モバイルアプリに関するフィードバックを提供するには、次のいずれかの方法を使用します。

- [**設定**] [  >  **フィードバックの送信**] に移動
- [Yammer サイト](https://www.yammer.com/AskIPTeam)に質問を投稿する
