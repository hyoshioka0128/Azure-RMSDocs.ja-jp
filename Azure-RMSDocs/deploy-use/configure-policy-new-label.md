---
title: "Azure Information Protection の新しいラベル"
description: "Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: ac12ab9023499d5aac632159ef689a8f10a91418
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Azure Information Protection の新しいラベルを作成する方法

>*適用対象: Azure Information Protection*

Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。

新しいラベルを追加するか、分類のレベルをさらに細かくする必要がある場合は既存のラベルに新しいサブラベルを追加できます。 たとえば、[既定のポリシー](configure-policy-default.md)に含まれる最後のラベルにはサブラベルが含まれています。

Azure Information Protection ポリシーに新しいラベルを追加するには、次の手順に従います。

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザーのウィンドウで、セキュリティ管理者または全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 追加する新しいラベルがすべてのユーザーに適用される場合は、**[Policy: Global (ポリシー: グローバル)]** ブレードで次のいずれかを実行します。 

    - 新しいラベルを作成するには: **[Add a new label]** (新しいラベルの追加) をクリックします。

    - 新しいサブラベルを作成するには: サブラベルを作成するラベルを右クリックするかコンテキスト メニュー (**...**) をクリックし、**[Add a sub-label]** (サブラベルの追加) をクリックします。
    
     追加する新しいラベルが[スコープ ポリシー](configure-policy-scope.md)内にあり、選択されたユーザーだけに適用される場合は、まず、最初の **[Azure Information Protection]** ブレードで該当するスコープ ポリシーを選択します。

3. **[ラベル]** または **[サブラベル]** ブレードで、新しいラベルに適用するオプションを選択し、**[保存]** をクリックします。
    
    新しいラベルには自動的に黒色が割り当てられます。 識別のための色を一覧から選択するか、赤、緑、青 (RGB) の色のコンポーネントの 16 進数コードを入力します。 たとえば、**#DAA520** と入力します。 これらのコードの参照が必要な場合は、最初に MSDN ドキュメントの「[Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85)」(色の名前) を参照することをお勧めします。ここに掲載されているコードは Microsoft ペイントのような多くの画像編集プログラムで使用されており、パレットからカスタムの色を選択すると RGB の値が自動的に表示されます。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

5. この新しいラベル名と説明をユーザーが他の言語で見られるようにするには、「[How to configure labels for different languages (他の言語用ラベルを構成する方法)](configure-policy-languages.md)」の手順に従ってください。 

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

