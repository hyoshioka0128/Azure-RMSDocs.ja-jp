---
title: IOS & Android 用 Azure Information Protection アプリ
description: IOS および Android デバイス用の Azure Information Protection (AIP) アプリの基本について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/07/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 0f849dfefa6af9ffd95dcca0c731ed216f465b11
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86046404"
---
# <a name="what-is-the-azure-information-protection-app-for-ios-or-android"></a>IOS または Android 用の Azure Information Protection アプリとは

*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

IOS および Android 用の Azure Information Protection (AIP) アプリを使用すると、電子メールアプリが rights management データ保護をネイティブでサポートしていない場合に、権利で保護された電子メール**メッセージ (** ) を表示できます。  

AIP アプリを使用すると、権利で保護された PDF ドキュメント (保護された PDF および**ppdf**ファイル)、イメージ、テキストファイルを表示することもできます。

> [!NOTE]
> AIP アプリは閲覧者のみであり、保護された電子メールメッセージに対して新規または返信を作成したり、保護されたファイルを作成または編集したりすることはできません。 アプリでは、保護された PDF ドキュメントや電子メールメッセージの添付ファイルなど、表示するファイルの添付ファイルを開くこともできません。
>

## <a name="aip-mobile-app-requirements"></a>AIP モバイルアプリの要件

IOS および Android 用の AIP mobile apps は、次のシステムで使用できます。

- [サポートされているモバイル OS のバージョン](#supported-mobile-os-versions)
- [サポートされているサインイン資格情報](#supported-sign-in-credentials)
- [サポートされるファイル拡張子](#supported-file-extensions)

### <a name="supported-mobile-os-versions"></a>サポートされているモバイル OS のバージョン

AIP mobile apps には、次の最低限のモバイルオペレーティングシステムのいずれかが必要です。 

- iOS 11 
- Android 6.0 

> [!NOTE]
> AIP mobile apps は Intel Cpu ではサポートされていません。
> 

### <a name="supported-sign-in-credentials"></a>サポートされているサインイン資格情報

次のいずれかを使用して、AIP にサインインします。 

- **職場または学校の資格情報。** 組織が既にモバイルデバイス拡張機能を使用してオンプレミス AD RMS を持っている場合、または Azure Information Protection を使用する場合は、を使用します。
 
- **Microsoft アカウント**。 個人用の電子メールアドレスを使用してファイルを保護していた場合は、 [Microsoft アカウント](https://signup.live.com)でサインインします。 

    - Microsoft アカウントに適用する場合は、独自の Hotmail、Gmail、またはその他の電子メールアドレスを使用できます。
    
> [!NOTE]
> Microsoft アカウントが使用されている場合、保護されたコンテンツを開くことができないアプリケーションもあります。 詳細については、「保護され[たドキュメントを開くためのサポートされるシナリオ](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)」を参照してください。
> 

### <a name="supported-file-extensions"></a>サポートされるファイル拡張子

.rpmsg、.pdf、.ppdf、.pjpg、.pjpeg、.ptiff、.ppng、.ptxt、.pxml などのテキストと画像ファイル形式を開くことができます。

テキストと画像ファイルの拡張子一覧については、管理者ガイドの「[分類と保護がサポートされているファイルの種類](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)」に記載されている最初の表を参照してください。

## <a name="installing-your-aip-mobile-apps-and-viewing-files"></a>AIP mobile アプリのインストールとファイルの表示

モバイルデバイスが Microsoft Intune によって管理されている場合は、ポータルサイトからアプリをダウンロードできます。

それ以外の場合は、次の方法でアプリにアクセスします。

- [ITunes](https://apps.apple.com/app/microsoft-rights-management/id689516635)または[Google Play](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)ストア
- [Azure Information Protection のダウンロードページ](https://portal.azurerms.com/#/download)。 [**モバイルデバイス**] セクションで、 [IOS](https://apps.apple.com/app/microsoft-rights-management/id689516635)または[Android](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)のアイコンを選択します。

インストールが完了したら、保護された電子メールまたはファイルが受信されるまで待ってから、開いたときに**AIP ビューアー**を選択します。

職場または学校のアカウントでサインインするか、証明書を選択するように求められます。 認証が完了すると、電子メールまたはファイルが開き、内容を読むことができるようになります。

> [!TIP]
> この操作をすぐに実行するには、保護された電子メールまたはファイルを表示するように送信します。 
>
> 詳細については、「 [iOS 用および Android 用の Microsoft Azure Information Protection アプリの概要](mobile-app-get-started.md)」を参照してください。
> 

## <a name="next-steps"></a>次のステップ

AIP モバイルアプリに関するフィードバックを提供するには、次のいずれかの方法を使用します。

- [**設定**] [  >  **フィードバックの送信**] に移動
- [Yammer サイト](https://www.yammer.com/AskIPTeam)に質問を投稿する
