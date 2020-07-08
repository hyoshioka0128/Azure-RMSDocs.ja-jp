---
title: Azure Information Protection ラベルの削除または順序変更 - AIP
description: ユーザーに表示される Azure Information Protection ラベルを削除または順序変更できます。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 8c273bd483a7a29c3475841183592135eff0841c
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048529"
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Azure Information Protection のラベルを削除または順序変更する方法

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

ラベルに対してこれらのアクションを選択することで、Office アプリケーションでユーザーに表示される Azure Information Protection ラベルを削除または順序変更することができます。

![Azure Information Protection のラベルを削除または順序変更する](./media/info-protect-contextmenu.png)

ドキュメントや電子メールに適用されているラベルを削除すると、これらのドキュメントや電子メールが Azure Information Protection クライアントによって次に開かれたときに、ユーザーにはラベルの状態が "**未設定**" と表示されます。 ただし、ラベル情報はメタデータに残り、このラベル情報を検索するサービスで読み取ることができます。

また、削除されたラベルに保護が適用されている場合、その保護は解除されません。 ラベルの保護設定は維持され、**[保護テンプレート]** セクションに表示されます。 これで、このテンプレートを新しいラベルに変換することができます。 このテンプレートが残っている間は、削除したラベルと同じ名前で新しいラベルを作成することはできません。 同じ名前でラベルを作成する場合、次の方法があります。

- テンプレートをラベルに変換する。 
    
    これは推奨される方法です。必要であれば、テンプレートの名前を変更したり、保護設定を変更したりできるからです。

- PowerShell を利用し、テンプレートの名前を変更するか、削除します。
    
    これらの操作を行う前に、他の管理者やサービスがそのテンプレートを使用しているかどうか、または過去に使用したかどうかを確認します。 テンプレートは、変更されることのないテンプレート ID または名前 (変更される可能性があります) で識別できます。 ベスト プラクティスとしては、将来的にユーザーがそのテンプレートによって保護されていたドキュメントやメールを開く必要がないことが確実である場合にのみ、テンプレートを削除します。

保護テンプレートの管理の詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

ラベルを削除する前に、ポリシーから無効化または削除することを検討してください。
    
- ドキュメントや電子メールに適用されているラベルを無効にした場合、適用されたラベルはこれらのドキュメントや電子メールから削除されません。 ラベルはポリシーに残りますが、ユーザーが Information Protection バーで選択できるラベルとしては表示されなくなります。 ラベルを無効にすれば、同じポリシーでユーザーに後でラベルを選択させる必要が生じたときのために元の構成を保持することができ、この場合はラベルをもう一度有効化するだけで済みます。

- ポリシーからラベルを削除した場合、適用されたラベルはこれらのドキュメントと電子メールから削除されません。 しかし、ポリシーからラベルを削除した場合、このラベルを別のポリシーに追加するために使用できるようになります。 詳しくは、「[Azure Information Protection ポリシーにラベルを追加または削除する](configure-policy-add-remove-label.md)」をご覧ください。

Information Protection バーにラベルが論理的な流れで表示されるように、ラベルの順序を設定します。 たとえば、最も秘密度が低いラベルが最初に、最も秘密度が高いラベルが最後に表示されるようにラベルを秘密度で順序付けできます。 [既定ポリシー](configure-policy-default.md)では、この構成が使用され、ラベル名には高くなっていく順序の秘密度が反映されます。

> [!IMPORTANT]
>複数のラベルに適用される可能性がある[条件](configure-policy-classification.md)を構成する場合は、最も秘密度の低いラベルから最も秘密度の高いラベルの順にする必要があります。 この順序により、条件が評価されるときに、最も秘密度の高いラベルが確実に適用されます。


これらの変更を行うには、次の手順を実行します。

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

2. [**分類**  >  **ラベル**] メニューオプションから: [ **Azure Information Protection ラベル**] ウィンドウで、次の操作の1つまたは複数を実行します。 

    - ラベルを削除するには: 削除するラベルを右クリックするかコンテキスト メニュー (**[...]**) を選択し、**[Delete this label]\(このラベルを削除する\)** をクリックし、**[OK]** をクリックして確定します。 

    - ラベルを無効にする: 無効にするラベルを選択します。 [**ラベル**] ウィンドウで、[**有効**] の [**オフ**] を選択し、[**保存**] をクリックします。

    - ラベルの順序を変更する: 順序を変更するラベルを右クリックするかコンテキスト メニュー (**...**) を選択し、ラベルが目的の順序になるまで、**[上へ移動]** または **[下へ移動]** をクリックします。  

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  


