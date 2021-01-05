---
title: ラベル付けと保護-Microsoft Information Protection SDK
description: Microsoft Information Protection ソフトウェア開発キットの運用
author: msmbaldwin
ms.author: mbaldwin
ms.date: 08/20/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 2e18b9ae65a4915807fdcb8fc37dd18396270fee
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865012"
---
# <a name="labeling-and-pre-existing-protection-in-microsoft-information-protection-sdk"></a>Microsoft Information Protection SDK でのラベル付けと既存の保護

Microsoft Information Protection はラベル付けと分類サービスをサポートしています。 ユーザーとアプリケーションは、次のものをサポートされるファイルに適用できます。

- ラベルの適用によってのみ分類

- ラベルの適用による分類と保護

- 保護のみ

この記事では、既存の保護が適用されているファイルにラベルを適用するために SDK がどのように処理を行うかについて説明します。 ドキュメントがラベルの適用によって既に保護されている場合、またはそれ以外の場合、SDK は次のようなシナリオで新しいラベルの適用を処理します。

## <a name="label-based-protection-when-label-metadata-has-been-stripped"></a>ラベルのメタデータが削除されたときのラベルベースの保護

ファイルにラベルが適用されていて、そのラベルが適用されている場合は、SDK がそのファイル保護を特定のラベルに解決できる必要があります。 ファイルに対して "編集" アクセス許可を持つユーザーが、誤って、または悪意のあるラベルメタデータを削除しても、保護は維持されます。 次に SDK がファイルと対話するときに、保護データを確認し、保護テンプレートを元のラベルに解決して、ラベルを再適用します。 これは、ラベルメタデータが改ざんされた場合に備えて、情報保護のために SDK に組み込まれている安全性メカニズムです。

## <a name="custom-protection-and-label-applications"></a>カスタム保護とアプリケーションのラベル付け

ファイルに何らかの形式の保護が適用されている場合、RMS テンプレートを使用してファイルにラベルを適用しようとすると、SDK はまず元の保護をラベルに解決できる必要があります。 これを行うことができない場合、SDK は、新しい保護の感度レベルが元の保護の感度よりも制限されているか制限されているかを評価できないため、SDK は新しいラベルをファイルに適用しません。

## <a name="user-defined-permissions"></a>ユーザー定義のアクセス許可

ファイルにラベルが適用されていて、そのラベルにユーザー定義保護が適用されている場合、保護はファイルに適用されますが、SDK で RMS テンプレートと同じように解決することはできません。 この場合、ユーザーが新しいラベルをファイルに適用しようとすると、SDK は上記と同様のアクションを処理し、ファイルに新しいラベルを適用しません。
