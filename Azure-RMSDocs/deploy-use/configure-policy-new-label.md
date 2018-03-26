---
title: Azure Information Protection の新しいラベル
description: Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: cbfa670d3a80068754e604ebb77892f320095ae9
ms.sourcegitcommit: 32b233bc1f8cef0885d9f4782874f1781170b83d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2018
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Azure Information Protection の新しいラベルを作成する方法

>*適用対象: Azure Information Protection*

Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。

新しいラベルを追加するか、分類のレベルをさらに細かくする必要がある場合は既存のラベルに新しいサブラベルを追加できます。 たとえば、[既定のポリシー](configure-policy-default.md)に含まれる最後のラベルには、サブラベルが含まれています。

ラベルに最初のサブラベルを作成すると、ユーザーは元の親ラベルを選択できなくなります。 ユーザーが同じ設定を適用できるように、必要に応じて新しいサブラベルを作成して親ラベル設定を再作成してください。

Azure Information Protection ポリシーに新しいラベルを追加するには、次の手順に従います。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 追加する新しいラベルがすべてのユーザーに対するものである場合は、**[Azure Information Protection - グローバル ポリシー]** ブレードのままにします。
    
    追加する新しいラベルが[スコープ付きポリシー](configure-policy-scope.md)で選んだユーザーに対するものである場合は、**[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードからスコープ付きポリシーを選びます。

3. **[Azure Information Protection - グローバル ポリシー]** ブレードまたは **[ポリシー: \<名前>]** ブレードで、次のいずれかのアクションを行います。
    
    - 新しいラベルを作成するには: **[Add a new label]** (新しいラベルの追加) をクリックします。
    
    - 新しいサブラベルを作成するには: サブラベルを作成するラベルを右クリックするかコンテキスト メニュー (**...**) をクリックし、**[サブラベルの追加]** をクリックします。

4. **[ラベル]** または **[サブラベル]** ブレードで、新しいラベルに適用するオプションを選択し、**[保存]** をクリックします。
    
    表示名を指定する際、一部の文字 (円記号やアンパサンドなど) は使用できません。Azure Information Protection を使用するすべてのサービスとアプリケーションで、これらの文字をサポートできるとは限らないためです。 ブロックされる文字に加えて、**#** 文字も指定しないでください。    
    
    新しいラベルには自動的に黒色が割り当てられます。 識別のための色を一覧から選択するか、赤、緑、青 (RGB) の色のコンポーネントの 16 進数コードを入力します。 たとえば、**#DAA520** と入力します。 これらのコードの参照が必要な場合は、最初に MSDN ドキュメントの「[Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85)」(色の名前) を参照することをお勧めします。ここに掲載されているコードは Microsoft ペイントのような多くの画像編集プログラムで使用されており、パレットからカスタムの色を選択すると RGB の値が自動的に表示されます。

5. ユーザーが変更を使用できるようにするには、最初の **[Azure Information Protection]** ブレードで **[公開]** をクリックします。

6. この新しいラベル名と説明をユーザーが他の言語で見られるようにするには、「[How to configure labels for different languages (他の言語用ラベルを構成する方法)](configure-policy-languages.md)」の手順に従ってください。 

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

