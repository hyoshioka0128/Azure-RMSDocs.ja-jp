---
title: "Azure Information Protection の新しいラベルを作成する方法 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: c2f8f3204e3d5947137e7e9111ba4eba2628293b


---

# Azure Information Protection の新しいラベルを作成する方法

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。

新しいラベルを追加するか、分類のレベルをさらに細かくする必要がある場合は既存のラベルに新しいサブラベルを追加できます。 たとえば、[既定のポリシー](configure-policy-default.md)に含まれる**[秘密]** ラベルにサブレベルを含めます。

Azure Information Protection ポリシーに新しいラベルを追加するには、次の手順に従います。

1. [Azure ポータル](https://portal.azure.com)にまだサインインしていない場合はサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[参照]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[Azure Information Protection]** ブレードで、次のいずれかの操作を行います。

    - 新しいラベルを作成するには: **[Add a new label]** (新しいラベルの追加) をクリックします。

    - 新しいサブラベルを作成するには: サブラベルを作成するラベルを右クリックするかコンテキスト メニュー (**...**) をクリックし、**[Add a sub-label]** (サブラベルの追加) をクリックします。

3. **[ラベル]** または **[サブラベル]** ブレードで、新しいラベルに適用するオプションを選択し、**[保存]** をクリックします。

    > [!NOTE]
    >保護の設定の詳細については、「[保護を適用するためのラベルを構成する方法](configure-policy-protection.md)」を参照してください。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  





<!--HONumber=Aug16_HO2-->


