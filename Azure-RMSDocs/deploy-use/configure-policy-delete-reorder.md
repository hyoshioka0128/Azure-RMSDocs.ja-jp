---
title: "ラベルを削除または順序変更する方法 | Azure Information Protection"
description: "Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを削除または順序変更することができます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: 4fcfcebc7da5a22a91911d70d4d787dc525d3485
ms.openlocfilehash: 743741fc63adfd959074986aab5c697d817f69c7


---

# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Azure Information Protection のラベルを削除または順序変更する方法

>*適用対象: Azure Information Protection*

Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを削除または順序変更することができます。

![Azure Information Protection のラベルを削除または順序変更する](../media/info-protect-contextmenu.png)

ラベルの構成は維持するが Information Protection バーにラベルが表示されないようにする場合は、ラベルを削除するのではなく、単に無効にすることができます。

Information Protection バーにラベルが論理的な流れで表示されるように、ラベルの順序を設定します。 たとえば、最も秘密度が低いラベルが最初に、最も秘密度が高いラベルが最後に表示されるようにラベルを秘密度で順序付けできます。 既定のポリシーの構成については、[こちら](configure-policy-default.md)をご覧ください。

> [!IMPORTANT]
>複数のラベルに適用される可能性がある[条件](configure-policy-classification.md)を構成する場合は、最も秘密度の低いラベルから最も秘密度の高いラベルの順にする必要があります。 この順序により、条件が評価されるときに、最も秘密度の高いラベルが確実に適用されます。


これらの変更を行うには、次の手順を実行します。

1. [Azure ポータル](https://portal.azure.com)にサインインしていない場合は新しいブラウザーのウィンドウで全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 削除、無効化、または順序を変更するラベルがすべてのユーザーに適用される場合は、**[Policy:Global]**(ポリシー:グローバル) ブレードで次のいずれかを実行します。 

    - ラベルを削除する: 削除するラベルを右クリックするかコンテキスト メニュー (**...**) を選択し、**[Delete this label]** (このラベルを削除する) をクリックし、**[はい]** をクリックして確定します。 次に、**[保存]** をクリックします。 

    - ラベルを無効にする: 無効にするラベルを選択します。 **[ラベル]** ブレードで、**[有効]** の **[オフ]** をクリックし、**[保存]** をクリックします。

    - ラベルの順序を変更する: 順序を変更するラベルを右クリックするかコンテキスト メニュー (**...**) を選択し、ラベルが目的の順序になるまで、**[上へ移動]** または **[下へ移動]** をクリックします。 次に、**[保存]** をクリックします。 

     削除、無効化、または順序を変更するラベルが[スコープ ポリシー](configure-policy-scope.md)内にあり、選択されたユーザーだけに適用される場合は、まず、最初の **[Azure Information Protection]** ブレードで該当するスコープ ポリシーを選択します。

3. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  





<!--HONumber=Dec16_HO1-->


