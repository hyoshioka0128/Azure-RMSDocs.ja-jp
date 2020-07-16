---
title: 概念-MIP SDK のアクションの理由
description: この記事では、理由を必要とするラベルをダウングレードまたは削除する方法のシナリオについて説明します。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: v-anikep
ms.openlocfilehash: c783722a7cded0242ae12386854b3c8fca325a9e
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86405205"
---
# <a name="action-justification-in-mip-sdk"></a>MIP SDK のアクションの理由

## <a name="overview"></a>概要

セキュリティとコンプライアンスセンターのラベルポリシーを使用すると、管理者はラベルの削除またはダウングレードに関する**根拠**を求めることができます。 ダウングレードは、既存のラベルの代わりに、より低い感度の値を持つラベルを適用するように定義されています。

前に説明したように、File API は、サービスからラベルを読み取り、定義されたファイルの種類にラベルを適用し、それらのファイルの種類からラベルを読み取るための使いやすいインターフェイスを提供します。 サポートされている filetype のラベルを削除したり変更したりするためのファイル操作もサポートしています。 ファイルラベルへの変更は、の機能によってサポートされています。これにより、保護されて `mip::FileHandler` `SetLabel()` いないファイルまたは以前に保護されたファイルに新しいラベルを設定したり、 `mip::FileHandler` 以前に `DeleteLabel()` 保護されたファイルからラベルを削除したりする機能が提供されます。

機密ラベルによっては、ユーザーがラベルを削除したりラベルを制限の緩い値に変更したりして感度をダウングレードしようとしたときに、セキュリティ管理者がより厳密なポリシーを適用することが必要になる場合があります。 管理者は、チェックボックスをオンにして、[セキュリティとコンプライアンスセンター](https://sip.compliance.microsoft.com/)のラベルポリシー構成を使用してこれを構成できます。

![アクションの理由が必要です](./media/justify-action.png)

ファイルに既存のラベルがあり、ラベルのダウングレードが発生した場合にラベルポリシーで理由が必要な場合は、関数によってが `SetLabel()` / `DeleteLabel()` スローされ `mip::JustificationRequiredError` ます。 アプリケーションはこの例外をキャッチしてから、ダウングレードの理由について入力を提供するために、アプリケーションインターフェイスをユーザーに提供する必要があります。 理由が記録されると、アプリケーションはプロパティを `isDowngradeJustified` `mip::LabelingOptions` 設定するだけでなく、のプロパティを設定でき `Justification` ます。

## <a name="next-steps"></a>次の手順

- [アクションの理由に関するレビュークイックスタート (C++)](quick-file-justify-actions-cpp.md)
- [アクションの理由に関するレビュークイックスタート (C#)](quick-file-justify-actions-csharp.md)