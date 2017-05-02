---
title: "Azure Information Protection のラベルを変更する"
description: "Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを変更または改良できます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: 48faf9703176ba8f67f57582ea584733fe3e9b01
ms.sourcegitcommit: d814d2876cf56e8fff0b107a5e3ec6df2aeda9ae
translationtype: HT
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Azure Information Protection の既存のラベルを変更またはカスタマイズする方法

>*適用対象: Azure Information Protection*

Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを変更または改良できます。

たとえば、ラベルまたはサブラベルの名前、ツールヒント、色、順序、フッターや透かしなどの視覚的なマーキングの適用の有無、Azure Rights Management による保護の適用の有無、推奨または自動分類を変更できます。

ラベルを変更するには、次の手順を実行します。


1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザーのウィンドウで、セキュリティ管理者または全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. グローバル ポリシーのラベルを変更してすべてのユーザーに適用されるようにするには、**[Policy: Global (ポリシー: グローバル)]** ブレードで変更するラベルを選択し、**[ラベル]** ブレードで変更を行い、必要に応じてその後のブレードで設定を行います。 [スコープ ポリシー](configure-policy-scope.md)のラベルを変更し、選択されたユーザーだけに適用されるようにするには、まず、最初の **[Azure Information Protection]** ブレードで該当するスコープ ポリシーを選択します。

    例外は、ラベルの順序を変更する場合です。これはグローバル ポリシーまたは選択されたスコープ ポリシーのブレードで行います。ラベルを右クリックするかラベルのコンテキスト メニューを選択してから、**[上へ移動]** または **[下へ移動]** オプションを選択します。

3. ブレードで変更を行い、その変更を維持する場合は、そのブレードの **[保存]** を必ずクリックします。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

> [!TIP]
>既定のラベルのいずれかを既定値に戻す場合は、[既定の Information Protection ポリシー](configure-policy-default.md)の情報を使用します。

## <a name="next-steps"></a>次のステップ

ラベルに実行できるオプションを構成する方法や、Azure Information Protection ポリシーのその他の設定について詳しくは、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


