---
title: "Azure Information Protection の新しいラベル"
description: "Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 602fef628f882eb79fe78b5acf89bde1721aa0ec
ms.lasthandoff: 02/24/2017


---

# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Azure Information Protection の新しいラベルを作成する方法

>*適用対象: Azure Information Protection*

Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。

新しいラベルを追加するか、分類のレベルをさらに細かくする必要がある場合は既存のラベルに新しいサブラベルを追加できます。 たとえば、[既定のポリシー](configure-policy-default.md)に含まれる**[秘密]** ラベルにサブレベルを含めます。

Azure Information Protection ポリシーに新しいラベルを追加するには、次の手順に従います。

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は新しいブラウザーのウィンドウで全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 追加する新しいラベルがすべてのユーザーに適用される場合は、**[Policy:Global]**(ポリシー:グローバル) ブレードで次のいずれかを実行します。 

    - 新しいラベルを作成するには: **[Add a new label]** (新しいラベルの追加) をクリックします。

    - 新しいサブラベルを作成するには: サブラベルを作成するラベルを右クリックするかコンテキスト メニュー (**...**) をクリックし、**[Add a sub-label]** (サブラベルの追加) をクリックします。


     追加する新しいラベルが[スコープ ポリシー](configure-policy-scope.md)内にあり、選択されたユーザーだけに適用される場合は、まず、最初の **[Azure Information Protection]** ブレードで該当するスコープ ポリシーを選択します。

3. **[ラベル]** または **[サブラベル]** ブレードで、新しいラベルに適用するオプションを選択し、**[保存]** をクリックします。

    > [!NOTE]
    >保護の設定の詳細については、「[保護を適用するためのラベルを構成する方法](configure-policy-protection.md)」を参照してください。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


