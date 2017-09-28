---
title: "Azure Information Protection ラベルの視覚的なマーキングを構成する"
description: "ドキュメントまたは電子メール メッセージにラベルを割り当てるときに、選択した分類を見やすくするためのさまざまなオプションを選択できます。 これらの視覚的なマーキングには、ヘッダー、フッター、および透かしがあります。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: 0da5df139d98f0468f49e7e3f17cd1cd2358a015
ms.sourcegitcommit: 76bf1f93b02fd75bead8ccdaaf34da1a6aad571f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2017
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Azure Information Protection 用の視覚的なマーキングのラベルを構成する方法

>*適用対象: Azure Information Protection*

ドキュメントまたは電子メール メッセージにラベルを割り当てるときに、選択した分類を見やすくするためのさまざまなオプションを選択できます。 これらの視覚的なマーキングには、ヘッダー、フッター、および透かしがあります。

視覚的なマーカーの追加情報:

- ヘッダーとフッターは、Word、Excel、PowerPoint、および Outlook に適用されます。

- 透かしは、Word、Excel、および PowerPoint に適用されます。

    - Excel: 透かしが表示されるのは、ページ レイアウト モード、印刷プレビュー モード、および印刷時のみです。
    
    - PowerPoint: 透かしは、マスター スライドに背景画像として適用されます。
    
    - 複数行のテキストがサポートされます。

- ヘッダー、フッター、または透かしを適用するときに、単なるテキスト文字列を指定するか、[変数](#using-variables-in-the-text-string)を使用してテキスト文字列を動的に作成することができます。

- 視覚的なマーカーがサポートするのは、1 つの言語のみです。

## <a name="when-visual-markings-are-applied"></a>視覚的なマーキングが適用されるタイミング

電子メール メッセージの場合、Outlook から電子メール メッセージが送信されたときに視覚的なマーキングが適用されます。

ドキュメントでは、視覚的なマーキングが次のように適用されます。

- Office アプリでは、ラベルの適用時に、ラベルからの視覚的なマーキングが適用されます。 ラベル付きのドキュメントを開いたときと、ドキュメントを最初に保存したときにも、視覚的なマーキングが適用されます。  

- エクスプローラーまたは PowerShell を使用してドキュメントにラベルを付ける場合は、視覚的なマーキングはすぐには適用されませんが、ドキュメントを Office アプリで開いたときと、ドキュメントが最初に保存されるときに適用されます。

## <a name="to-configure-visual-markings-for-a-label"></a>ラベルの視覚的なマーキングを構成するには

ラベルの視覚的なマーキングを構成するには、次の手順に従います。

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザー ウィンドウを開き、セキュリティ管理者または全体管理者としてサインインします。次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 構成するラベルがすべてのユーザーに適用される場合は、**[Azure Information Protection - グローバル ポリシー]** ブレードのままにします。
    
    構成するラベルが[スコープ付きポリシー](configure-policy-scope.md)内にあり、選択したユーザーだけに適用される場合は、**[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードからスコープ付きポリシーを選びます。

3. **[ラベル]** ブレードで、**[Set visual marking (such as header or footer)]** (視覚的なマーキングの設定 (ヘッダーやフッターなど)) セクション、目的の視覚的なマーカーの設定を構成した後、**[保存]** をクリックします。
    
    - ヘッダーを構成するには: **[Documents with this label have a header]** (このラベルを持つドキュメントにヘッダーを設定する) で、ヘッダーを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、ヘッダーのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、ヘッダーの配置を指定します。
    
    - フッターを構成するには: **[Documents with this label have a footer]** (このラベルを持つドキュメントにフッターを設定する) で、フッターを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、フッターのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、フッターの配置を指定します。
    
    - 透かしを構成するには: **[Documents with this label have a watermark]** (このラベルを持つドキュメントに透かしを設定する) で、透かしを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、透かしのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、透かしの配置を指定します。

4. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## <a name="using-variables-in-the-text-string"></a>テキスト文字列に変数を使用する

ヘッダー、フッター、または透かしのテキスト文字列には、次の変数を使用できます。

- `${Item.Label}`: 選択したラベル。 例: Internal

- `${Item.Name}`: ファイル名または電子メールの件名。 例: JulySales.docx

- `${Item.Location}`: ドキュメントのパスとファイル名、電子メールの件名。 例: \\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}`: ドキュメントまたは電子メールの所有者、Windows のサインイン ユーザー名。 例: rsimone

- `${User.PrincipalName}`: ドキュメントまたは電子メールの所有者、Azure Information Protection クライアントのサインイン電子メール アドレス (UPN) 例: rsimone@vanarsdelltd.com

- `${Event.DateTime}`: 選択したラベルが設定された日時。 例: 8/16/2016 1:30 PM

例: **General** ラベル フッターに `Document: ${item.name}  Classification: ${item.label}` という文字列を指定する場合、project.docx というドキュメントに適用されるフッター テキストは、**Document: project.docx  Classification: General** になります。

### <a name="setting-the-font-name"></a>フォント名を設定する

この設定は現在プレビュー段階です。

Calibri は、ヘッダー、フッター、透かしのテキストに使われる既定のフォントです。 別のフォント名を指定する場合、ビジュアル マーカーを適用するクライアント デバイスでそれが利用できることを確認してください。 利用できない場合、使用されるフォントは不明確になります。 

### <a name="setting-the-font-color"></a>フォントの色を設定する

利用できる色の一覧から選択するか、赤、緑、青 (RGB) の色のコンポーネントの 16 進数コードを入力してカスタムの色を指定できます。 たとえば、**#DAA520** と入力します。 

コードの参照が必要な場合、MSDN ドキュメントの「[Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85)」 (名前別の色) が便利です。 画像編集できるさまざまなアプリケーションでもコードを参照できます。 たとえば、Microsoft ペイントでは、パレットからカスタム色を選択できます。RGB 値が自動的に表示されるので、それをコピーできます。

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
