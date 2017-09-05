---
title: "Azure Information Protection のラベルを変更する"
description: "Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを変更または改良できます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: 343b38caa14d3f67a932eedae37ed10c55f371ff
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Azure Information Protection の既存のラベルを変更またはカスタマイズする方法

>*適用対象: Azure Information Protection*

Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを変更または改良できます。

たとえば、ラベルまたはサブラベルの名前、ツールヒント、色、順序、フッターや透かしなどの視覚的なマーキングの適用の有無、Azure Rights Management による保護の適用の有無、推奨または自動分類を変更できます。

ラベルを変更するには、次の手順を実行します。

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザー ウィンドウを開き、セキュリティ管理者または全体管理者としてサインインします。次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. グローバル ポリシーのラベルを変更してすべてのユーザーに適用されるようにするには、**[Azure Information Protection - グローバル ポリシー]** ブレードで変更するラベルを選択し、必要に応じてその後のブレードで設定を行います。 選択したユーザーだけに適用される[スコープ付きポリシー](configure-policy-scope.md)のラベルを変更するには、最初に **[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードからスコープ付きポリシーを選びます。

    例外は、ラベルの順序を変更する場合です。これはグローバル ポリシーまたは選択されたスコープ ポリシーのブレードで行います。ラベルを右クリックするかラベルのコンテキスト メニューを選択してから、**[上へ移動]** または **[下へ移動]** オプションを選択します。

3. ブレードで変更を行い、その変更を維持する場合は、そのブレードの **[保存]** を必ずクリックします。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

5. ラベル名や説明を変更し、これらを追加の言語で構成している場合、Azure Information Protection ポリシーをもう一度エクスポートし、新たに翻訳して、その変更をインポートする必要があります。 詳しくは、「[How to configure labels for different languages (他の言語用ラベルを構成する方法)](configure-policy-languages.md)」をご覧ください。

> [!TIP]
>既定のラベルのいずれかを既定値に戻す場合は、[既定の Information Protection ポリシー](configure-policy-default.md)の情報を使用します。

## <a name="next-steps"></a>次のステップ

ラベルに実行できるオプションを構成する方法や、Azure Information Protection ポリシーのその他の設定について詳しくは、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


