---
title: Azure Information Protection の新しいラベル - AIP
description: Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 6da2f54fbd3b3e22d93438b8b369c2d0fe145521
ms.sourcegitcommit: b66b249ab5681d02ec3b5af0b820eda262d5976a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "78972573"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Azure Information Protection の新しいラベルを作成する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順: [Windows 用の Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、独自のラベルを作成することもできます。

新しいラベルを追加するか、分類のレベルをさらに細かくする必要がある場合は既存のラベルに新しいサブラベルを追加できます。 たとえば、[既定のポリシー](configure-policy-default.md)に含まれる最後のラベルには、サブラベルが含まれています。

ラベルに最初のサブラベルを作成すると、ユーザーは元の親ラベルを選択できなくなります。 ユーザーが同じ設定を適用できるように、必要に応じて新しいサブラベルを作成して親ラベル設定を再作成してください。

Azure Information Protection ポリシーに追加できる新しいラベルを追加するには、次の手順に従います。

## <a name="to-create-a-new-label"></a>新しいラベルを作成するには

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ペインに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、 **[Azure Information Protection]** を選択します。

2. [**分類** > **ラベル**] メニューオプションから: **[Azure Information Protection ラベル]** ウィンドウで、次のいずれかの操作を行います。
    
    - 新しいラベルを作成するには: **[Add a new label]** (新しいラベルの追加) をクリックします。
    
    - 新しいサブラベルを作成するには: サブラベルを作成するラベルを右クリックするかコンテキスト メニュー ( **...** ) をクリックし、 **[サブラベルの追加]** をクリックします。

3. **[ラベル]** または **[サブラベル]** ペインで、この新しいラベルに使用するオプションを選択し、 **[保存]** をクリックします。
    
    表示名を指定する際、一部の文字 (円記号やアンパサンドなど) は使用できません。Azure Information Protection を使用するすべてのサービスとアプリケーションで、これらの文字をサポートできるとは限らないためです。 ブロックされる文字に加えて、 **#** 文字も指定しないでください。    
    
    新しいラベルには自動的に黒色が割り当てられます。 識別のための色を一覧から選択するか、赤、緑、青 (RGB) の色のコンポーネントの 16 進数コードを入力します。 たとえば、 **#DAA520** と入力します。 これらのコードの参照が必要な場合は、MSDN web ドキュメントの[\<色 >](https://developer.mozilla.org/docs/Web/CSS/color_value)のページから役に立つテーブルを見つけることができます。また、これらのコードは、画像を編集できる多くのアプリケーションでも見つかります。 たとえば、Microsoft ペイントでは、パレットからカスタム色を選択できます。RGB 値が自動的に表示されるので、それをコピーできます。

4. 新しいラベルをユーザーが利用できるようにするには、 **[分類]**  >  **[ポリシー]** メニュー オプションから、新しいラベルを含むポリシーを選択します。 **[ラベルの追加または削除]** を選択します。 **[ポリシー: ラベルの追加または削除]** ウィンドウでラベルを選択し、 **[OK]** を選択して **[保存]** を選択します。
    
    >[!TIP]
    >新しいラベルについては、まず、テストに使用するスコープ ポリシーに追加することを検討してください。 結果に満足したら、このテスト スコープからラベルを削除し、運用環境で使用するポリシーにラベルを追加します。     
    
    ラベルの追加について詳しくは、[ラベルを追加または削除する方法](configure-policy-add-remove-label.md)に関する記事をご覧ください。
    
    変更内容はユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

5. この新しいラベル名と説明をユーザーが他の言語で見られるようにするには、[異なる言語のラベルを構成する方法](configure-policy-languages.md)に関する記事の手順に従ってください。 

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  


