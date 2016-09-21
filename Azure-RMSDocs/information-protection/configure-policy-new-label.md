---
title: "Azure Information Protection の新しいラベルを作成する方法 | Azure Information Protection"
description: "Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。"
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: 801ca11da602d4acb9c398c9a89aeb33e45cb0f4
ms.openlocfilehash: 4edbdde88444304c314251124618d563a3662477


---

# Azure Information Protection の新しいラベルを作成する方法

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。

新しいラベルを追加するか、分類のレベルをさらに細かくする必要がある場合は既存のラベルに新しいサブラベルを追加できます。 たとえば、[既定のポリシー](configure-policy-default.md)に含まれる**[秘密]** ラベルにサブレベルを含めます。

Azure Information Protection ポリシーに新しいラベルを追加するには、次の手順に従います。

1. [Azure ポータル](https://portal.azure.com)にサインインしていない場合は新しいブラウザーのウィンドウでサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[Azure Information Protection]** ブレードで、次のいずれかの操作を行います。

    - 新しいラベルを作成するには: **[Add a new label]** (新しいラベルの追加) をクリックします。

    - 新しいサブラベルを作成するには: サブラベルを作成するラベルを右クリックするかコンテキスト メニュー (**...**) をクリックし、**[Add a sub-label]** (サブラベルの追加) をクリックします。

3. **[ラベル]** または **[サブラベル]** ブレードで、新しいラベルに適用するオプションを選択し、**[保存]** をクリックします。

    > [!NOTE]
    >保護の設定の詳細については、「[保護を適用するためのラベルを構成する方法](configure-policy-protection.md)」を参照してください。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  





<!--HONumber=Sep16_HO3-->


