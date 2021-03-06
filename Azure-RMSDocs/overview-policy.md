---
title: Azure Information Protection ポリシーの概要
description: ラベルと、Azure Information Protection クライアントにダウンロードされる Azure Information Protection ポリシーの設定を理解します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 2e18f90b343dec10f1649ccfcf13e19931d53378
ms.sourcegitcommit: 2fe9333c3e6c98e7dd9003c5f4cd7c1e7a48b297
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64880159"
---
# <a name="overview-of-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーの概要

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection ポリシーには、構成可能な次の要素があります。
    
- 含めるラベル。管理者とユーザーは、ラベルを使用してドキュメントや電子メールを分類できます (また、必要に応じて保護できます)。

- ユーザーの Office アプリケーションで、Information Protection バーに表示されるタイトルとツールヒント。

- ドキュメントと電子メールを分類するための開始点となる既定のラベルを設定するオプション。

- ユーザーがドキュメントの保存と電子メールの送信を行ったときに分類を実行するオプション。

- ユーザーが元のレベルよりも低い秘密度レベルのラベルを選択したときに、理由を示すことをユーザーに要求するオプション。

- 添付ファイルに基づいて、電子メール メッセージに自動的にラベルを付けるオプション。

- Office アプリケーションで Information Protection バーが表示されるかどうかを制御するオプション。

- Outlook に [Do Not Forward]\(転送不可\) ボタンを表示するかどうかを制御するオプション。

- ユーザーがドキュメントに独自のアクセス許可を指定できるようにするオプション。

- ユーザーにカスタム ヘルプ リンクを提供するオプション。

Azure Information Protection には[既定ポリシー](configure-policy-default.md)があり、5 つの主要なラベルが含まれています。 これらのうちの 2 つのラベルには、必要なときにサブカテゴリを提供するためのサブラベルが含まれています。 

サブラベルのラベルを構成するときに、ユーザーはメインのラベルを選択することはできませんが、サブラベルをいずれか 1 つ選択する必要があります。 このシナリオでは、メインのラベルは名前と色の表示コンテナーとしてのみサポートされます。

Azure Information Protection ラベルは、最下位の分類である個人データから、最上位の分類である非常に機密性の高い社外秘データまで、組織が通常作成して保存するあらゆるデータで使用できます。 

これらの既定のラベルは、そのまま使用する、カスタマイズする、または削除することができ、新しいラベルを作成することもできます。 詳しい手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーをカスタマイズする方法や、ユーザーに対して結果の動作を表示する方法の例については、次のチュートリアルをご覧ください。

- [Edit the Azure Information Protection policy and create a new label (Azure Information Protection ポリシーを編集して新しいラベルを作成する)](infoprotect-quick-start-tutorial.md)

- [Configure Azure Information Protection policy settings that work together (連携させる Azure Information Protection のポリシー設定を構成する)](infoprotect-settings-tutorial.md)
