---
title: "Azure Information Protection ラベルの変更"
description: "Information Protection バーに表示されるラベルは、Azure Information Protection ポリシー内に構成することで、変更または改良することができます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: f1ffd4c459f2fa194372450f5713c920422f744d
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Azure Information Protection の既存のラベルを変更またはカスタマイズする方法

>*適用対象: Azure Information Protection*

Information Protection バーに表示されるラベルは、Azure Information Protection ポリシー内に構成することで、変更または改良することができます。

たとえば、ラベルまたはサブラベルの名前、ツールヒント、色、順序を変更できます。 フッターや透かしなどの視覚的なマーキングをラベルで適用するかどうかを変更することができます。 さらに、保護と、推奨分類または自動分類をラベルで適用するかどうかも変更できます

ラベルを変更するには、次の手順を実行します。

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザー ウィンドウで、セキュリティ管理者または全体管理者としてサインインします。次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 **[Azure Information Protection]** を選択します。

2. グローバル ポリシーのラベルを変更してすべてのユーザーに適用されるようにするには、**[Azure Information Protection - グローバル ポリシー]** ブレードで変更するラベルを選択し、必要に応じてその後のブレードで設定を行います。 選択したユーザーだけに適用されるように[スコープ付きポリシー](configure-policy-scope.md)のラベルを変更するには、最初に **[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードからスコープ付きポリシーを選びます。

    ラベルの順序を変更する場合は例外です。 グローバル ポリシーまたは選択されたスコープ ポリシーのポリシー ブレードで、ラベルを右クリックするかラベルのコンテキスト メニューを選択してから **[上へ移動]** オプションまたは **[下へ移動]** オプションを選択します。

3. ブレードで変更を行い、その変更を維持する場合は、そのブレードの **[保存]** をクリックします。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

5. ラベルの表示名や説明を変更し、これらを追加の言語で構成している場合は、Azure Information Protection ポリシーをもう一度エクスポートし、新たに翻訳して、その変更をインポートする必要があります。 詳細については、「[Azure Information Protection で異なる言語のラベルとテンプレートを構成する方法](configure-policy-languages.md)」をご覧ください。

> [!TIP]
>既定のラベルのいずれかを既定値に戻す場合は、[既定の Information Protection ポリシー](configure-policy-default.md)に関する情報を使用します。

## <a name="next-steps"></a>次の手順

ラベルに実行できるオプションを構成する方法や、Azure Information Protection ポリシーのその他の設定の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


