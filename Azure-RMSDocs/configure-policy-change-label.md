---
title: Azure Information Protection のラベルを変更する - AIP
description: Information Protection バーに表示されるラベルは、Azure Information Protection ポリシー内に構成することで、変更または改良することができます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 6c0561c62beab39f8e958c6547d7654cb457ccc3
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383399"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Azure Information Protection の既存のラベルを変更またはカスタマイズする方法

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、Microsoft 365 のドキュメントの「 [秘密度ラベルについて](/microsoft-365/compliance/sensitivity-labels) 」を参照してください。 *

> [!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Portal でラベルを構成することにより、Information Protection バーに表示される任意のラベル、または Office リボンの **[保護]** ボタンのラベルを変更または改良できます。

たとえば、ラベルまたはサブラベルの名前、ツールヒント、色、順序を変更できます。 フッターや透かしなどの視覚的なマーキングをラベルで適用するかどうかを変更することができます。 さらに、保護と、推奨分類または自動分類をラベルで適用するかどうかも変更できます

ラベルを変更するには、次の手順を実行します。

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

2. [**分類**  >  **ラベル**] メニューオプションから: [ **Azure Information Protection ラベル**] ウィンドウで、変更するラベルを選択します。

    例外は、ラベルの順序を変更する場合です。ラベルを選択する代わりに、ラベルを右クリックするか、ラベルのコンテキスト メニューを選択します。 **[上へ移動]** オプションまたは **[下へ移動]** オプションを選択します。

3. 新しいウィンドウで変更を行う場合は常に、変更を保持するには、そのウィンドウの [ **保存** ] をクリックします。
    
    **[保存]** をクリックすると、変更内容がユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

4. ラベルの表示名や説明を変更し、これらを追加の言語で構成している場合は、Azure Information Protection ポリシーをもう一度エクスポートし、新たに翻訳して、その変更をインポートする必要があります。 詳細については、「[Azure Information Protection で異なる言語のラベルとテンプレートを構成する方法](configure-policy-languages.md)」をご覧ください。

> [!TIP]
>既定のラベルのいずれかを既定値に戻す場合は、[既定の Information Protection ポリシー](configure-policy-default.md)に関する情報を使用します。

## <a name="next-steps"></a>次のステップ

ラベルに実行できるオプションを構成する方法や、Azure Information Protection ポリシーのその他の設定の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。



