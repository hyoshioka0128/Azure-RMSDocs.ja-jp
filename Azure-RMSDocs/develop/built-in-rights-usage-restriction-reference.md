---
title: "方法&#58; 組み込み権限の使用 | Azure RMS"
description: "RMS SDK 4.2 の組み込み権限と、その制限に従うことでアプリケーションによって適用される使用制限について説明します。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experimental: True
experiment_id: priyamo-TableVsFlatList-20160805
ms.openlocfilehash: ecc6e420633c42cc5044e9df0a5d86c604a5b24e
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-use-built-in-rights"></a>方法: 組み込み権限の使用

このトピックでは、Microsoft Rights Management SDK 4.2 の組み込み権限と、その制限に従うことでアプリケーションによって適用される使用制限について説明します。 組み込み権限、一般的な権限、編集可能なドキュメントの権限、電子メール権限、オペレーティング システムによる説明とその値を次に示します。

**注** – Linux SDK の場合の詳細については、*rights.h* のソース ファイルを参照してください。

## <a name="common-rights"></a>一般的な権限

**すべて** – すべての一般的な権限のコレクション。
- Android: [CommonRights.All](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS および OS X: [MSCommonRights](https://msdn.microsoft.com/library/dn758314.aspx) - **すべて**を実装するユーザー所有者および表示
- Windows ストアおよび Windows Phone: [CommonRights.All</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.all.aspx)
- Linux: [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**所有者** - 所有者権限は、保護されたコンテンツに対する完全な制御を許可します。
- Android: [<strong>CommonRights.Owner](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS および OS X: [MSCommonRights owner](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows ストアおよび Windows Phone: [CommonRights.Owner](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.owner.aspx)
- Linux: [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**表示** – 保護されたコンテンツを表示する権限。 通常、この権限が付与されると、保護されたコンテンツを開いて表示することができますが、コンテンツを変更、抽出、転送、保存するには、追加の権限が必要です。

- Android: [CommonRights.View](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS および OS X: [MSCommonRights view](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows ストアおよび Windows Phone: [CommonRights.View](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.view.aspx)
- Linux: [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>編集可能なドキュメントの権限
**すべて** – 編集可能なすべてのドキュメント権限を含むコレクション。
- Android: [EditableDocumentRights.All](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS および OS X: [MSEditableDocumentRights all](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.all.aspx)
- Linux: [EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**コメント** – ドキュメントにコメントを作成する権限。
- Android: [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS および OS X: [MSEditableDocumentRights comment](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.comment.aspx)
- Linux: [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**編集** – 保護されたコンテンツを編集し、同じ保護された形式で保存する権限。 通常、この権限が付与されると、保護されたコンテンツを変更し、同じファイルに保存することができます。
- Android: [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS および OS X: [MSEditableDocumentRights edit](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.edit.aspx)
- Linux: [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**エクスポート** – 保護された形式からコンテンツを抽出し、AD RMS で保護される別の形式にする権限。 通常、この権限が付与されると、保護されたコンテンツを AD RMS で保護される別の形式で保存することができます (アプリケーションに *[名前を付けて保存]* の機能が実装されている場合など)。

- Android: [EditableDocumentRights.Export](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS および OS X: [MSEditableDocumentRights exportable](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Export](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.export.aspx)
- Linux: [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**抽出** – 保護された形式からコンテンツを抽出し、保護されていない形式にする権限。 通常、この権限が付与されると、保護されたコンテンツから情報をコピーして貼り付けることができます。 アプリケーションに <em>[名前を付けて保存]</em> 機能が実装されている場合、保護されたコンテンツを保護されていない形式やその他の保護された形式に保存できます。 この権限の値は、電子メールの抽出権限と同じです。

- Android: [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS および OS X: [MSEditableDocumentRights extract](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.extract.aspx)
- Linux: [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**印刷** – 保護されたコンテンツを印刷する権限。 通常、この権限が付与されると、保護されたコンテンツを印刷できます。 この権限の値は、電子メールの印刷権限と同じです。

- Android: [EditableDocumentRights.Print](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS および OS X: [MSEditableDocumentRights print](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows ストアおよび Windows Phone: [EditableDocumentRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.print.aspx)
- Linux: [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>電子メール権限

**すべて** – すべての電子メール権限を含むコレクション。
- Android: [EmailRights.All](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS および OS X: [MSEmailRights all](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows ストアおよび Windows Phone: [EmailRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.all.aspx)
- Linux: [EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**抽出** – 保護された形式からコンテンツを抽出し、保護されていない形式にする権限。 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージから情報をコピーして貼り付けることができます。 アプリケーションに <em>[名前を付けて保存]</em> 機能が実装されている場合、受信者は保護されたコンテンツを保護されていない形式やその他の保護された形式に保存できます。 この権限の値は、編集可能なドキュメントの抽出権限と同じです。

- Android: [EmailRights.Extract](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS および OS X: [MSEmailRights extract](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows ストアおよび Windows Phone: [EmailRights.Extract</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.extract.aspx)
- Linux: [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**転送** – 保護されたメッセージを転送する権限。 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージを転送できます。
- Android: [<strong>EmailRights.Forward</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS および OS X: [MSEmailRights forward](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows ストアおよび Windows Phone: [EmailRights.Forward](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.forward.aspx)
- Linux: [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**印刷** – 保護されたコンテンツを印刷する権限。 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージを印刷できます。 この権限の値は、編集可能なドキュメントの印刷権限と同じです。

- Android: [EmailRights.Print](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS および OS X: [MSEmailRights print](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows ストアおよび Windows Phone: [EmailRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.print.aspx)
- Linux: [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**返信** – 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージに返信し、返信に元のメッセージのコピーを含めることができます。

- Android: [EmailRights.Reply](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS および OS X: [MSEmailRights reply](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows ストアおよび Windows Phone: [EmailRights.Reply](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.reply.aspx)
- Linux: [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**全員に返信** – 通常、この権限が付与されると、電子メールの受信者は保護されたメッセージの受信者全員に返信し、返信に元のメッセージのコピーを含めることができます。

- Android: [EmailRights.ReplyAll</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS および OS X: [MSEmailRights replyAll](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows ストアおよび Windows Phone: [EmailRights.ReplyAll](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.replyall.aspx)
- Linux: [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]