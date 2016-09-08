---
title: "Azure Information Protection のラベルを削除または順序変更する方法 | Azure Rights Management"
description: "Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを削除または順序変更することができます。"
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: 43b43657627135886f6d0be42fef41ba939bdae1


---

# Azure Information Protection のラベルを削除または順序変更する方法

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを削除または順序変更することができます。

![Azure Information Protection のラベルを削除または順序変更する](../media/info-protect-contextmenu.png)

ラベルの構成は維持するが Information Protection バーにラベルが表示されないようにする場合は、ラベルを削除するのではなく、単に無効にすることができます。

Information Protection バーにラベルが論理的な流れで表示されるように、ラベルの順序を設定します。 たとえば、最も秘密度が低いラベルが最初に、最も秘密度が高いラベルが最後に表示されるようにラベルを秘密度で順序付けできます。 既定のポリシーの構成については、[こちら](configure-policy-default.md)をご覧ください。

> [!IMPORTANT]
>複数のラベルに適用される可能性がある[条件](configure-policy-classification.md)を構成する場合は、最も秘密度の低いラベルから最も秘密度の高いラベルの順にする必要があります。 この順序により、条件が評価されるときに、最も秘密度の高いラベルが確実に適用されます。


これらの変更を行うには、次の手順を実行します。

1. [Azure ポータル](https://portal.azure.com)にまだサインインしていない場合はサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[参照]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[Azure Information Protection]** ブレードで、目的 (ラベルを削除、無効化、または順序変更) に応じて、次のいずれかの操作を行います。

    - ラベルを削除する: 削除するラベルを右クリックするかコンテキスト メニュー (**...**) を選択し、**[Delete this label]** (このラベルを削除する) をクリックし、**[はい]** をクリックして確定します。 次に、**[保存]** をクリックします。 

    - ラベルを無効にする: 無効にするラベルを選択します。 **[ラベル]** ブレードで、**[有効]** の **[オフ]** をクリックし、**[保存]** をクリックします。

    - ラベルの順序を変更する: 順序を変更するラベルを右クリックするかコンテキスト メニュー (**...**) を選択し、ラベルが目的の順序になるまで、**[上へ移動]** または **[下へ移動]** をクリックします。 次に、**[保存]** をクリックします。 

3. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  





<!--HONumber=Aug16_HO4-->


