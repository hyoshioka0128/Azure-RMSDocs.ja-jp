---
title: Azure Information Protection のラベルを変更する - AIP
description: Azure Information Protection ポリシー内に構成することで、Information Protection バーに表示されるラベルを変更または改良できます。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 4fbe251f6bc56d82c9ec9ef92359efc540f53634
ms.sourcegitcommit: b66b249ab5681d02ec3b5af0b820eda262d5976a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "78971336"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Azure Information Protection の既存のラベルを変更またはカスタマイズする方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順: [Windows 用の Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Portal でラベルを構成することにより、Information Protection バーに表示される任意のラベル、または Office リボンの **[保護]** ボタンのラベルを変更または改良できます。

たとえば、ラベル名またはサブラベル名、ヒント、色、および順序を変更できます。 ラベルでフッターや透かしなどの視覚的なマーキングを適用するかどうかを変更できます。 また、ラベルで保護、および推奨された分類または自動分類を適用するかどうかを変更することもできます。

ラベルを変更するには、次の手順を実行します。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、 **[Azure Information Protection]** を選択します。

2. [**分類** > **ラベル**] メニューオプションから: **[Azure Information Protection ラベル]** ウィンドウで、変更するラベルを選択します。

    例外は、ラベルの順序を変更する場合です。ラベルを選択する代わりに、ラベルを右クリックするか、ラベルのコンテキスト メニューを選択します。 次に、 **[上へ移動]** または **[下へ移動]** オプションを選択します。

3. 新しいウィンドウで変更を行う場合は常に、変更を保持するには、そのウィンドウの **[保存]** をクリックします。
    
    **[保存]** をクリックすると、変更内容がユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

4. ラベルの表示名や説明を変更し、これらを追加の言語で構成している場合、Azure Information Protection ポリシーをもう一度エクスポートし、新たに翻訳して、その変更をインポートします。 詳しくは、「[How to configure labels for different languages (他の言語用ラベルを構成する方法)](configure-policy-languages.md)」をご覧ください。

> [!TIP]
>既定のラベルのいずれかを既定値に戻す場合は、[既定の Information Protection ポリシー](configure-policy-default.md)の情報を使用します。

## <a name="next-steps"></a>次の手順

ラベルに実行できるオプションを構成する方法や、Azure Information Protection ポリシーのその他の設定について詳しくは、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。



