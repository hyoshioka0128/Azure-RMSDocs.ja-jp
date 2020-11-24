---
title: 方法&#58; 組み込み権限の使用 | Azure RMS
description: RMS SDK 4.2 の組み込み権限と、その制限に従うことでアプリケーションによって適用される使用制限について説明します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
experimental: true
experiment_id: priyamo-TableVsFlatList-20160805
ms.openlocfilehash: 337cb03e6350bafb96f0672f9225ebe613044ea4
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570222"
---
# <a name="how-to-use-built-in-rights"></a>方法: 組み込み権限の使用

このトピックでは、Microsoft Rights Management SDK 4.2 の組み込み権限と、その制限に従うことでアプリケーションによって適用される使用制限について説明します。 組み込み権限、一般的な権限、編集可能なドキュメントの権限、電子メール権限、オペレーティング システムによる説明とその値を次に示します。

**注** – Linux SDK の場合の詳細については、*rights.h* のソース ファイルを参照してください。

## <a name="common-rights"></a>一般的な権限

**すべて** – すべての一般的な権限のコレクション。
- Android: [CommonRights.All](/previous-versions/windows/desktop/msipcthin2/commonrights-class-java)
- iOS および OS X: [MSCommonRights](/previous-versions/windows/desktop/msipcthin2/mscommonrights-interface-objc) - **すべて** を実装するユーザー所有者および表示
- Windows ストアおよび Windows Phone: [CommonRights.All</strong>](/previous-versions/windows/desktop/msipcthin2/commonrights-all)
- Linux: [CommonRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**所有者** -所有者権限は、保護されたコンテンツに対する完全な制御を許可します。
- Android: [ <strong> commonrights. 所有者](/previous-versions/windows/desktop/msipcthin2/commonrights-class-java)
- iOS および OS X: [MSCommonRights owner](/previous-versions/windows/desktop/msipcthin2/mscommonrights-interface-objc)
- Windows ストアおよび Windows Phone: [CommonRights.Owner](/previous-versions/windows/desktop/msipcthin2/commonrights-owner)
- Linux: [CommonRights::Owner](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**表示** – 保護されたコンテンツを表示する権限。 通常、この権限が付与されると、保護されたコンテンツを開いて表示することができますが、コンテンツを変更、抽出、転送、保存するには、追加の権限が必要です。

- Android: [CommonRights.View](/previous-versions/windows/desktop/msipcthin2/commonrights-class-java)
- iOS および OS X: [MSCommonRights view](/previous-versions/windows/desktop/msipcthin2/mscommonrights-interface-objc)
- Windows ストアおよび Windows Phone: [CommonRights.View](/previous-versions/windows/desktop/msipcthin2/commonrights-view)
- Linux: [CommonRights::View](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>編集可能なドキュメントの権限
**すべて** – 編集可能なすべてのドキュメント権限を含むコレクション。
- Android: [EditableDocumentRights.All](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS および OS X: [MSEditableDocumentRights all](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.All](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-all)
- Linux: [EditableDocumentRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**コメント** – ドキュメントにコメントを作成する権限。
- Android: [EditableDocumentRights.Comment](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS および OS X: [MSEditableDocumentRights comment](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Comment](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights--comment)
- Linux: [EditableDocumentRights::Comment](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**編集** – 保護されたコンテンツを編集し、同じ保護された形式で保存する権限。 通常、この権限が付与されると、保護されたコンテンツを変更し、同じファイルに保存することができます。
- Android: [EditableDocumentRights.Edit](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS および OS X: [MSEditableDocumentRights edit](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Edit](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-edit)
- Linux: [EditableDocumentRights::Edit](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**エクスポート** – 保護された形式からコンテンツを抽出し、AD RMS で保護される別の形式にする権限。 通常、この権限が付与されると、保護されたコンテンツを AD RMS で保護される別の形式で保存することができます (アプリケーションに *[名前を付けて保存]* の機能が実装されている場合など)。

- Android: [EditableDocumentRights.Export](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS および OS X: [MSEditableDocumentRights exportable](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Export](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-export)
- Linux: [EditableDocumentRights::Export](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**抽出** – 保護された形式からコンテンツを抽出し、保護されていない形式にする権限。 通常、この権限が付与されると、保護されたコンテンツから情報をコピーして貼り付けることができます。 アプリケーションに <em>[名前を付けて保存]</em> 機能が実装されている場合、保護されたコンテンツを保護されていない形式やその他の保護された形式に保存できます。 この権限の値は、電子メールの抽出権限と同じです。

- Android: [EditableDocumentRights.Extract](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS および OS X: [MSEditableDocumentRights extract](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Extract](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-extract)
- Linux: [EditableDocumentRights::Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**印刷** – 保護されたコンテンツを印刷する権限。 通常、この権限が付与されると、保護されたコンテンツを印刷できます。 この権限の値は、電子メールの印刷権限と同じです。

- Android: [EditableDocumentRights.Print](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS および OS X: [MSEditableDocumentRights print](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Print](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-print)
- Linux: [EditableDocumentRights::Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>電子メール権限

**すべて** – すべての電子メール権限を含むコレクション。
- Android: [EmailRights.All](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS および OS X: [MSEmailRights all](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows ストアおよび Windows Phone: [EmailRights.All](/previous-versions/windows/desktop/msipcthin2/emailrights-all)
- Linux: [EmailRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**抽出** – 保護された形式からコンテンツを抽出し、保護されていない形式にする権限。 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージから情報をコピーして貼り付けることができます。 アプリケーションに <em>[名前を付けて保存]</em> 機能が実装されている場合、受信者は保護されたコンテンツを保護されていない形式やその他の保護された形式に保存できます。 この権限の値は、編集可能なドキュメントの抽出権限と同じです。

- Android: [EmailRights.Extract](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS および OS X: [MSEmailRights extract](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows ストアおよび Windows Phone: [EmailRights.Extract</strong>](/previous-versions/windows/desktop/msipcthin2/emailrights-extract)
- Linux: [EmailRights::Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**転送** – 保護されたメッセージを転送する権限。 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージを転送できます。
- Android: [<strong>EmailRights.Forward</strong>](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS および OS X: [MSEmailRights forward](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows ストアおよび Windows Phone: [EmailRights.Forward](/previous-versions/windows/desktop/msipcthin2/emailrights-forward)
- Linux: [EmailRights::Forward](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**印刷** – 保護されたコンテンツを印刷する権限。 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージを印刷できます。 この権限の値は、編集可能なドキュメントの印刷権限と同じです。

- Android: [EmailRights.Print](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS および OS X: [MSEmailRights print](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows ストアおよび Windows Phone: [EmailRights.Print](/previous-versions/windows/desktop/msipcthin2/emailrights-print)
- Linux: [EmailRights::Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**返信** – 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージに返信し、返信に元のメッセージのコピーを含めることができます。

- Android: [EmailRights.Reply](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS および OS X: [MSEmailRights reply](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows ストアおよび Windows Phone: [EmailRights.Reply](/previous-versions/windows/desktop/msipcthin2/emailrights-reply)
- Linux: [EmailRights::Reply](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**全員に返信** – 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージの受信者全員に返信し、返信に元のメッセージのコピーを含めることができます。

- Android: [EmailRights.ReplyAll</strong>](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS および OS X: [MSEmailRights replyAll](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows ストアおよび Windows Phone: [EmailRights.ReplyAll](/previous-versions/windows/desktop/msipcthin2/emailrights-replyall)
- Linux: [EmailRights::ReplyAll](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)