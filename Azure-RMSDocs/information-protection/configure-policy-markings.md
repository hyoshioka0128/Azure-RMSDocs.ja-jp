---
title: "Azure Information Protection 用の視覚的なマーキングのラベルを構成する方法 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 9f2d28e4f162891497a7b0518322338628118b9d


---

# Azure Information Protection 用の視覚的なマーキングのラベルを構成する方法

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

ドキュメントまたは電子メール メッセージにラベルを割り当てるときに、選択した分類を見やすくするためのさまざまなオプションを選択できます。 これらの視覚的なマーキングには、ヘッダー、フッター、および透かしがあります。

視覚的なマーキングは、Word、Excel、および PowerPoint ドキュメントにラベルが適用されるときと、ドキュメントが保存されるときに適用されます。 電子メール メッセージでは、視覚的なマーキングは、電子メール メッセージが送信されるときに適用されます。

視覚的なマーカーの追加情報:

- ヘッダーとフッターは、Word、Excel、PowerPoint、および Outlook に適用されます。

- 透かしは、Word、Excel、および PowerPoint に適用されます。

    - Excel: 透かしが表示されるのは、ページ レイアウト モード、印刷プレビュー モード、および印刷時のみです。

    - PowerPoint: 透かしは、マスター スライドに背景画像として適用されます。

ラベルの視覚的なマーキングを構成するには、次の手順に従います。

1. [Azure ポータル](https://portal.azure.com)にサインインします。
 
2. ハブ メニューで **[参照]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

3. **[Azure Information Protection]** ブレードで、視覚的なマーキングを構成するラベルを選択します。

4. **[ラベル]** ブレードで、**[Set visual marking (such as header or footer)]** (視覚的なマーキングの設定 (ヘッダーやフッターなど)) セクション、目的の視覚的なマーカーの設定を構成した後、**[保存]** をクリックします。

    - ヘッダーを構成するには: **[Documents with this label have a header]** (このラベルを持つドキュメントにヘッダーを設定する) で、ヘッダーを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、ヘッダーのテキスト、サイズ、色、およびヘッダーの配置を指定します。

    - フッターを構成するには: **[Documents with this label have a footer]** (このラベルを持つドキュメントにフッターを設定する) で、フッターを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、フッターのテキスト、サイズ、色、および配置を指定します。

    - 透かしを構成するには: **[Documents with this label have a watermark]** (このラベルを持つドキュメントに透かしを設定する) で、透かしを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、透かしのテキスト、サイズ、色、および配置を指定します。

5. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  





<!--HONumber=Jul16_HO5-->


