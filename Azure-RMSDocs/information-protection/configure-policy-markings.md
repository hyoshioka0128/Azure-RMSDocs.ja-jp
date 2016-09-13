---
title: "Azure Information Protection 用の視覚的なマーキングのラベルを構成する方法 | Azure Information Protection"
description: "ドキュメントまたは電子メール メッセージにラベルを割り当てるときに、選択した分類を見やすくするためのさまざまなオプションを選択できます。 これらの視覚的なマーキングには、ヘッダー、フッター、および透かしがあります。"
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: d70bfbe658b1c7d9a5a91c925a554974423699a7


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

- ヘッダー、フッター、または透かしを適用するときに、単なるテキスト文字列を指定するか、[変数](#using-variables-in-the-text-string)を使用してテキスト文字列を動的に作成することができます。 

ラベルの視覚的なマーキングを構成するには、次の手順に従います。

1. [Azure ポータル](https://portal.azure.com)にまだサインインしていない場合はサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[参照]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[Azure Information Protection]** ブレードで、視覚的なマーキングを構成するラベルを選択します。

3. **[ラベル]** ブレードで、**[Set visual marking (such as header or footer)]** (視覚的なマーキングの設定 (ヘッダーやフッターなど)) セクション、目的の視覚的なマーカーの設定を構成した後、**[保存]** をクリックします。

    - ヘッダーを構成するには: **[Documents with this label have a header]** (このラベルを持つドキュメントにヘッダーを設定する) で、ヘッダーを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、ヘッダーのテキスト、サイズ、色、およびヘッダーの配置を指定します。
    
    - フッターを構成するには: **[Documents with this label have a footer]** (このラベルを持つドキュメントにフッターを設定する) で、フッターを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、フッターのテキスト、サイズ、色、および配置を指定します。
    
    - 透かしを構成するには: **[Documents with this label have a watermark]** (このラベルを持つドキュメントに透かしを設定する) で、透かしを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、透かしのテキスト、サイズ、色、および配置を指定します。 

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## テキスト文字列に変数を使用する

ヘッダー、フッター、または透かしのテキスト文字列には、次の変数を使用できます。

- `${Item.Label}` 選択したラベル。 例: Internal

- `${Item.Name}` ファイル名または電子メールの件名。 例: JulySales.docx

- `${Item.Location}` ドキュメントのパスとファイル名、電子メールの件名。 例: \\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}` ドキュメントまたは電子メールの所有者、Windows のサインイン ユーザー名。 例: rsimone

- `${User.PrincipalName}` ドキュメントまたは電子メールの所有者、Azure Information Protection クライアントのサインイン電子メール アドレス (UPN) 例: rsimone@vanarsdelltd.com

- `${Event.DateTime}` 選択したラベルが設定された日時。 例: 8/16/2016 1:30 PM
    
例: Secret ラベル フッターに `Document: ${item.name}  Classification: ${item.label}` という文字列を指定する場合、project.docx というドキュメントに適用されるフッター テキストは、**Document: project.docx  Classification: Secret** になります。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  





<!--HONumber=Sep16_HO1-->


