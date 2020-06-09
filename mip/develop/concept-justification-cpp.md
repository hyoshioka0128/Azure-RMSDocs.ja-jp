---
title: 概念-MIP SDK のアクションの理由 (C++)
description: この記事は、理由を必要とするラベルをダウングレードまたは削除する方法のシナリオを理解するのに役立ちます。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: v-anikep
ms.openlocfilehash: 1b0926114dd4d494593bd0d2340fee35edfe5fe6
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548243"
---
# <a name="action-justification-in-mip-sdk-c"></a>MIP SDK のアクションの理由 (C++)

## <a name="overview"></a>概要

セキュリティとコンプライアンスセンターのラベルポリシーを使用すると、管理者はラベルの削除またはダウングレードに関する**根拠**を求めることができます。 ダウングレードは、既存のラベルの代わりに、より低い感度の値を持つラベルを適用するように定義されています。

前に説明したように、File API は、サービスからラベルを読み取り、定義されたファイルの種類にラベルを適用し、それらのファイルの種類からラベルを読み取るための使いやすいインターフェイスを提供します。 また、ラベルをから削除したり、サポートされている filetype のラベルを変更したりするためのファイル操作もサポートしています。 ファイルラベルへの変更は、の機能によってサポートされています。これにより、保護されて `mip::FileHandler` `SetLabel()` いないファイルまたは以前に保護されたファイルに新しいラベルを設定したり、 `mip::FileHandler` 以前に `DeleteLabel()` 保護されたファイルからラベルを削除したりする機能が提供されます。

機密ラベルによっては、ユーザーがラベルを削除したりラベルを制限の緩い値に変更したりして感度をダウングレードしようとしたときに、セキュリティ管理者がより厳密なポリシーを適用することが必要になる場合があります。 管理者は、チェックボックスをオンにして、[セキュリティとコンプライアンスセンター](https://sip.compliance.microsoft.com/)のラベルポリシー構成を使用してこれを構成できます。

![アクションの理由が必要です](./media/justify-action.png)

ファイルに既存のラベルがあり、秘密度レベルのダウングレードが発生した場合にラベルポリシーで理由が必要な場合は、関数によってが `SetLabel()` / `DeleteLabel()` スローされ `mip::JustificationRequiredError` ます。 このようなシナリオでは、API にユーザーの理由を記録する機能が用意されています。 SDK のコンシューマーは、ダウングレードの理由について入力を提供するために、アプリケーションインターフェイスをユーザーに提供する必要があります。 理由が記録されると、アプリケーションはプロパティを `isDowngradeJustified` `mip::LabelingOptions` 設定するだけでなく、のプロパティを設定でき `Justification` ます。

## <a name="next-steps"></a>次の手順

- [アクションの理由に関するレビュークイックスタート (C++)](quick-file-justify-actions-cpp.md)
- [アクションの理由に関するレビュークイックスタート (C#)](quick-file-justify-actions-csharp.md)