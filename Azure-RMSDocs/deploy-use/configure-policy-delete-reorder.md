---
title: "Azure Information Protection ラベルの削除または順序変更"
description: "Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを削除または順序変更することができます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.openlocfilehash: f17e149dcd8cfb7398909cbe3a83cdcf71b80b33
ms.sourcegitcommit: 2bca892231ca8393b88bd5da7d0890a573770a09
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2017
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Azure Information Protection のラベルを削除または順序変更する方法

>*適用対象: Azure Information Protection*

Azure Information Protection ポリシーでこれらのアクションを選択することで、Information Protection バーに表示されるラベルを削除または順序変更することができます。

![Azure Information Protection のラベルを削除または順序変更する](../media/info-protect-contextmenu.png)

ドキュメントや電子メールに適用されているラベルを削除してから Azure Information Protection ポリシーを公開すると、そのラベルは、Azure Information Protection クライアントによって次回開かれたときに自動的にドキュメントや電子メールから削除されます。

ただし、ラベルで保護が適用されている場合、その保護は解除されません。 ラベルの保護設定は維持され、**[保護テンプレート]** に表示されます。 このテンプレートは新しいラベルに変換するか、ラベルにリンクできます。 このテンプレートが残っている間は、削除したラベルと同じ名前で新しいラベルを作成することはできません。 同じ名前でラベルを作成する場合、次の方法があります。

- テンプレートをラベルに変換する。 
    
    これは推奨される方法です。必要であれば、テンプレートの名前を変更したり、保護設定を変更したりできるからです。

- PowerShell を利用し、テンプレートの名前を変更するか、削除します。
    
    変更または削除する前に、他の管理者やサービスがテンプレートを利用していないか考慮し、現在の名前で確認します。 テンプレートで保護されていたドキュメントやメールを開く必要がない場合にのみ、テンプレートを削除してください。

保護テンプレートの管理の詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

ラベルを削除するのではなく、その前に無効にするかどうかを検討してください。 ドキュメントや電子メールに適用されているラベルを無効にすると、適用されているラベルはこれらのドキュメントや電子メールからは削除されませんが、ユーザーが Information Protection バーで選択できるラベルとしては表示されなくなります。 ラベルを無効にすれば、ユーザーに後でラベルを選択させる必要が生じたときのために元の構成を保持することもでき、この場合は再度有効化するだけで済みます。

Information Protection バーにラベルが論理的な流れで表示されるように、ラベルの順序を設定します。 たとえば、最も秘密度が低いラベルが最初に、最も秘密度が高いラベルが最後に表示されるようにラベルを秘密度で順序付けできます。 [既定ポリシー](configure-policy-default.md)では、この構成が使用され、ラベル名には高くなっていく順序の秘密度が反映されます。

> [!IMPORTANT]
>複数のラベルに適用される可能性がある[条件](configure-policy-classification.md)を構成する場合は、最も秘密度の低いラベルから最も秘密度の高いラベルの順にする必要があります。 この順序により、条件が評価されるときに、最も秘密度の高いラベルが確実に適用されます。


これらの変更を行うには、次の手順を実行します。

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザー ウィンドウを開き、セキュリティ管理者または全体管理者としてサインインします。次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 構成するラベルがすべてのユーザーに適用される場合は、**[Azure Information Protection - グローバル ポリシー]** ブレードのままにします。
    
    構成するラベルが[スコープ付きポリシー](configure-policy-scope.md)内にあり、選択したユーザーだけに適用される場合は、**[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードからスコープ付きポリシーを選びます。

3. **[Azure Information Protection - グローバル ポリシー]** ブレードまたは **[ポリシー: \<名前>]** ブレードで、次のアクションを 1 つ以上行います。 

    - ラベルを削除する: 削除するラベルを右クリックするかコンテキスト メニュー (**...**) を選択し、**[Delete this label]** (このラベルを削除する) をクリックし、**[はい]** をクリックして確定します。 次に、**[保存]** をクリックします。 

    - ラベルを無効にする: 無効にするラベルを選択します。 **[ラベル]** ブレードで、**[有効]** の **[オフ]** をクリックし、**[保存]** をクリックします。

    - ラベルの順序を変更する: 順序を変更するラベルを右クリックするかコンテキスト メニュー (**...**) を選択し、ラベルが目的の順序になるまで、**[上へ移動]** または **[下へ移動]** をクリックします。 次に、**[保存]** をクリックします。 

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

