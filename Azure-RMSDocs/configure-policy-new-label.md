---
title: Azure Information Protection の新しいラベル - AIP
description: Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、Information Protection バーに表示される独自のラベルを作成することもできます。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 963a86e37112fb2c4a2f9ca10162995a131c49ac
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2018
ms.locfileid: "53023432"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Azure Information Protection の新しいラベルを作成する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection にはカスタマイズできる既定のラベルが付属していますが、独自のラベルを作成することもできます。

新しいラベルを追加するか、分類のレベルをさらに細かくする必要がある場合は既存のラベルに新しいサブラベルを追加できます。 たとえば、[既定のポリシー](configure-policy-default.md)に含まれる最後のラベルには、サブラベルが含まれています。

ラベルに最初のサブラベルを作成すると、ユーザーは元の親ラベルを選択できなくなります。 ユーザーが同じ設定を適用できるように、必要に応じて新しいサブラベルを作成して親ラベル設定を再作成してください。

Azure Information Protection ポリシーに追加できる新しいラベルを追加するには、次の手順に従います。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[分類]** > **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ブレードで、次のいずれかのアクションを実行します。
    
    - 新しいラベルを作成するには: **[Add a new label]** (新しいラベルの追加) をクリックします。
    
    - 新しいサブラベルを作成するには: サブラベルを作成するラベルを右クリックするかコンテキスト メニュー (**...**) をクリックし、**[サブラベルの追加]** をクリックします。

4. **[ラベル]** または **[サブラベル]** ブレードで、新しいラベルに適用するオプションを選択し、**[保存]** をクリックします。
    
    表示名を指定する際、一部の文字 (円記号やアンパサンドなど) は使用できません。Azure Information Protection を使用するすべてのサービスとアプリケーションで、これらの文字をサポートできるとは限らないためです。 ブロックされる文字に加えて、**#** 文字も指定しないでください。    
    
    新しいラベルには自動的に黒色が割り当てられます。 識別のための色を一覧から選択するか、赤、緑、青 (RGB) の色のコンポーネントの 16 進数コードを入力します。 たとえば、**#DAA520** と入力します。 これらのコードの参照が必要な場合は、最初に MSDN ドキュメントの「 [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85).aspx) 」(色の名前) を参照することをお勧めします。ここに掲載されているコードは Microsoft ペイントのような多くの画像編集プログラムで使用されており、パレットからカスタムの色を選択すると RGB の値が自動的に表示されます。

5. 新しいラベルをユーザーが利用できるようにするには、**[分類]** > **[ポリシー]** メニュー オプションから、新しいラベルを含むポリシーを選択します。 **[ラベルの追加または削除]** を選択します。 **[ポリシー: ラベルの追加または削除]** ブレードからラベルを選択し、**[OK]**、**[保存]** の順に選択します。
    
    >[!TIP]
    >新しいラベルについては、まず、テストに使用するスコープ ポリシーに追加することを検討してください。 結果に満足したら、このテスト スコープからラベルを削除し、運用環境で使用するポリシーにラベルを追加します。     
    
    ラベルの追加について詳しくは、[ラベルを追加または削除する方法](configure-policy-add-remove-label.md)に関する記事をご覧ください。
    
    変更内容はユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

6. この新しいラベル名と説明をユーザーが他の言語で見られるようにするには、[異なる言語のラベルを構成する方法](configure-policy-languages.md)に関する記事の手順に従ってください。 

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  


