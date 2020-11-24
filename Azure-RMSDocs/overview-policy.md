---
title: Azure Information Protection ポリシーの概要
description: Azure Information Protection クライアントにダウンロードされる Azure Information Protection ポリシーのラベルと設定について説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a0b456d8e436de77ae54f2b6a9b543d82acd1b12
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "95570078"
---
# <a name="overview-of-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーの概要

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> Azure Information Protection ポリシーは Azure Information Protection クライアント (クラシック) に適用され、Azure Information Protection の統合されたラベル付けクライアントには適用されません。 これらのクライアントの違いがわからない場合は、 こちらの [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) を参照してください。
> 
> 機密ラベルに関する情報を探している場合は、Microsoft 365 の準拠に関するドキュメントを参照してください。 たとえば、「[機密ラベルについて](/microsoft-365/compliance/sensitivity-labels)」です。

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

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーをカスタマイズする方法や、ユーザーに対して結果の動作を表示する方法の例については、次のチュートリアルをご覧ください。

- [Edit the Azure Information Protection policy and create a new label (Azure Information Protection ポリシーを編集して新しいラベルを作成する)](infoprotect-quick-start-tutorial.md)

- [連携させる Azure Information Protection のポリシー設定を構成する](infoprotect-settings-tutorial.md)