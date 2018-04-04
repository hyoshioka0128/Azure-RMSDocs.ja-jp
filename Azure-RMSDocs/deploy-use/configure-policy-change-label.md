---
title: Azure Information Protection のラベルを変更する
description: Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを変更または改良できます。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: aac1d87fb76848e31a21a046f14442293d29aa9f
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Azure Information Protection の既存のラベルを変更またはカスタマイズする方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを変更または改良できます。

たとえば、ラベル名またはサブラベル名、ヒント、色、および順序を変更できます。 ラベルでフッターや透かしなどの視覚的なマーキングを適用するかどうかを変更できます。 また、ラベルで保護、および推奨された分類または自動分類を適用するかどうかを変更することもできます。

ラベルを変更するには、次の手順を実行します。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. グローバル ポリシーのラベルを変更してすべてのユーザーに適用されるようにするには、**[Azure Information Protection - グローバル ポリシー]** ブレードで変更するラベルを選択し、必要に応じてその後のブレードで設定を行います。 選択したユーザーだけに適用される[スコープ付きポリシー](configure-policy-scope.md)のラベルを変更するには、最初に **[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードからスコープ付きポリシーを選びます。

    例外は、ラベルの順序を変更する必要がある場合です。 グローバル ポリシーまたは選択したスコープ付きポリシーのポリシー ブレードで、ラベルを右クリックするか、ラベルのコンテキスト メニューを選択します。 次に、**[上へ移動]** または **[下へ移動]** オプションを選択します。

3. ブレードで変更を行い、その変更を維持する場合は、そのブレードの **[保存]** を必ずクリックします。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

5. ラベルの表示名や説明を変更し、これらを追加の言語で構成している場合、Azure Information Protection ポリシーをもう一度エクスポートし、新たに翻訳して、その変更をインポートします。 詳細については、[他の言語用ラベルを構成する方法](configure-policy-languages.md)に関するページをご覧ください。

> [!TIP]
>既定のラベルのいずれかを既定値に戻す場合は、[既定の Information Protection ポリシー](configure-policy-default.md)の情報を使用します。

## <a name="next-steps"></a>次の手順

ラベルに実行できるオプションを構成する方法や、Azure Information Protection ポリシーのその他の設定について詳しくは、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


