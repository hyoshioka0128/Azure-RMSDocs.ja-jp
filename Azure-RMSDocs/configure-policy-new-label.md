---
title: Azure Information Protection の新しいラベル - AIP
description: Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: a8daf46770bf6fb7c696eedce5d8aeddb31c8b59
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68788942"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Azure Information Protection の新しいラベルを作成する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、独自のラベルを作成することもできます。

新しいラベルを追加するか、分類のレベルをさらに細かくする必要がある場合は既存のラベルに新しいサブラベルを追加できます。 たとえば、[既定のポリシー](configure-policy-default.md)に含まれる最後のラベルには、サブラベルが含まれています。

ラベルに最初のサブラベルを作成すると、ユーザーは元の親ラベルを選択できなくなります。 ユーザーが同じ設定を適用できるように、必要に応じて新しいサブラベルを作成して親ラベル設定を再作成してください。

Azure Information Protection ポリシーに追加できる新しいラベルを追加するには、次の手順に従います。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ブレードに移動します。
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[分類]**  >  **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ブレードで、次のいずれかのアクションを実行します。
    
    - 新しいラベルを作成するには: **[新しいラベルの追加]** をクリックします。
    
    - 新しいサブラベルを作成するには: サブラベルを作成するラベルを右クリックするかコンテキスト メニュー ( **...** ) をクリックし、 **[サブラベルの追加]** をクリックします。

3. **[ラベル]** または **[サブラベル]** ブレードで、新しいラベルに適用するオプションを選択し、 **[保存]** をクリックします。
    
    表示名を指定する際、一部の文字 (円記号やアンパサンドなど) は使用できません。Azure Information Protection を使用するすべてのサービスとアプリケーションで、これらの文字をサポートできるとは限らないためです。 ブロックされる文字に加えて、 **#** 文字も指定しないでください。    
    
    新しいラベルには自動的に黒色が割り当てられます。 識別のための色を一覧から選択するか、赤、緑、青 (RGB) の色のコンポーネントの 16 進数コードを入力します。 たとえば、 **#DAA520** と入力します。 これらのコードの参照が必要な場合は、MSDN web ドキュメントの「 [ \<色の >](https://developer.mozilla.org/docs/Web/CSS/color_value) 」ページから役に立つテーブルを見つけることができます。画像編集できるさまざまなアプリケーションでもコードを参照できます。 たとえば、Microsoft ペイントでは、パレットからカスタム色を選択できます。RGB 値が自動的に表示されるので、それをコピーできます。

4. 新しいラベルをユーザーが利用できるようにするには: **[分類]**  >  **[ポリシー]** メニュー オプションから、新しいラベルを含むポリシーを選択します。 **[ラベルの追加または削除]** を選択します。 **[ポリシー: ラベルの追加または削除]** ブレードからラベルを選択し、 **[OK]** 、 **[保存]** の順に選択します。
    
    >[!TIP]
    >新しいラベルについては、まず、テストに使用するスコープ ポリシーに追加することを検討してください。 結果に満足したら、このテスト スコープからラベルを削除し、運用環境で使用するポリシーにラベルを追加します。     
    
    ラベルの追加について詳しくは、[ラベルを追加または削除する方法](configure-policy-add-remove-label.md)に関する記事をご覧ください。
    
    変更内容はユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

5. この新しいラベル名と説明をユーザーが他の言語で見られるようにするには: [異なる言語のラベルを構成する方法](configure-policy-languages.md)のページにある手順に従ってください。 

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  


