---
title: Azure Information Protection ラベルの視覚的なマーキングを構成する
description: ドキュメントまたは電子メール メッセージにラベルを割り当てるときに、選択した分類を見やすくするためのさまざまなオプションを選択できます。 これらの視覚的なマーキングには、ヘッダー、フッター、および透かしがあります。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/10/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: 1c88c81966fa85ac12dd25f03ad8b90842230e46
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490275"
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Azure Information Protection 用の視覚的なマーキングのラベルを構成する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

ドキュメントまたは電子メール メッセージにラベルを割り当てるときに、選択した分類を見やすくするためのさまざまなオプションを選択できます。 これらの視覚的なマーキングには、ヘッダー、フッター、および透かしがあります。

視覚的なマーキングに関する追加情報:

- ヘッダーとフッターは、Word、Excel、PowerPoint、および Outlook に適用されます。

- 透かしは、Word、Excel、および PowerPoint に適用されます。

    - Excel: 透かしが表示されるのは、ページ レイアウト モード、印刷プレビュー モード、および印刷時のみです。
    
    - PowerPoint: 透かしは、マスター スライドに背景画像として適用されます。 **[表示]** タブの **[スライド マスター]** で、**[背景グラフィックを表示しない]** チェック ボックスがオフになっていることを確認します。
    
    - 複数行のテキストがサポートされます。

- ヘッダー、フッター、または透かしを適用するときに、単なるテキスト文字列を指定するか、[変数](#using-variables-in-the-text-string)を使用してテキスト文字列を動的に作成することができます。

- Word、PowerPoint、Outlook では、さまざまな色の視覚的なマーキングがサポートされます。 色に対して構成された視覚的なマーキングは、Excel では常に黒く表示されます。

- 視覚的なマーキングがサポートする言語は 1 つのみです。

## <a name="when-visual-markings-are-applied"></a>視覚的なマーキングが適用されるタイミング

電子メール メッセージの場合、Outlook から電子メール メッセージが送信されたときに視覚的なマーキングが適用されます。

ドキュメントでは、視覚的なマーキングが次のように適用されます。

- Office アプリでは、ラベルの適用時に、ラベルからの視覚的なマーキングが適用されます。 ラベル付きのドキュメントを開いたときと、ドキュメントを最初に保存したときにも、視覚的なマーキングが適用されます。  

- エクスプローラー、PowerShell、Azure Information Protection スキャナーを使用してドキュメントにラベルを付けると、視覚的なマーキングはすぐには適用されませんが、ドキュメントを Office アプリで開いたときと、ドキュメントが最初に保存されるときに、Azure Information Protection クライアントによって適用されます。
    
    例外は、SharePoint Online、OneDrive、または OneDrive for Business に保存されているファイルに対して Office 2016 で[自動保存](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5)を使用している場合です。自動保存が有効な場合、[高度なクライアント設定](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)でバックグラウンドで連続的に実行する分類を有効にします。 

## <a name="to-configure-visual-markings-for-a-label"></a>ラベルの視覚的なマーキングを構成するには

ラベルの視覚的なマーキングを構成するには、次の手順に従います。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[分類]** > **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ブレードで、追加または変更する視覚的なマーキングを含むラベルを選択します。

3. **[ラベル]** ブレードの **[視覚的なマーキングの設定 (ヘッダーやフッターなど)]** セクションで、使用する視覚的なマーキングの設定を構成した後、**[保存]** をクリックします。
    
    - ヘッダーを構成するには: **[Documents with this label have a header]** (このラベルを持つドキュメントにヘッダーを設定する) で、ヘッダーを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、ヘッダーのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、ヘッダーの配置を指定します。
    
    - フッターを構成するには: **[Documents with this label have a footer]** (このラベルを持つドキュメントにフッターを設定する) で、フッターを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、フッターのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、フッターの配置を指定します。
    
    - 透かしを構成するには: **[Documents with this label have a watermark]** (このラベルを持つドキュメントに透かしを設定する) で、透かしを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、透かしのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、透かしの配置を指定します。
    
**[保存]** をクリックすると、変更内容がユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。


## <a name="using-variables-in-the-text-string"></a>テキスト文字列に変数を使用する

ヘッダー、フッター、または透かしのテキスト文字列には、次の変数を使用できます。

- `${Item.Label}`: 選択したラベル。 例: Internal

- `${Item.Name}`: ファイル名または電子メールの件名。 例: JulySales.docx

- `${Item.Location}`: ドキュメントのパスとファイル名、電子メールの件名。 例: \\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}`: ドキュメントまたは電子メールの所有者、Windows のサインイン ユーザー名。 例: rsimone

- `${User.PrincipalName}`: ドキュメントまたは電子メールの所有者、Azure Information Protection クライアントのサインイン電子メール アドレス (UPN) 例: rsimone@vanarsdelltd.com

- `${Event.DateTime}`: 選択したラベルが設定された日時。 例: 8/16/2016 1:30 PM

例: **General** ラベル フッターに `Document: ${item.name}  Classification: ${item.label}` という文字列を指定する場合、project.docx というドキュメントに適用されるフッター テキストは、**Document: project.docx  Classification: General** になります。

## <a name="setting-different-visual-markings-for-word-excel-powerpoint-and-outlook"></a>Word、Excel、PowerPoint、Outlook にさまざまな視覚的マーキングを設定する

既定では、指定した視覚的マーキングは Word、Excel、PowerPoint、Outlook のすべてに適用されます。 ただし、テキスト文字列に "If.App" という変数ステートメントを入れると、Office アプリケーションごとに視覚的マーキングを指定できます。**Word**、**Excel**、**PowerPoint**、**Outlook** という値を利用し、アプリケーションの種類を区別できます。 このような値は省略することもできます。同じ If.App ステートメントで複数回指定する場合に必要になります。

次の構文を使用します。

    ${If.App.<application type>}<your visual markings text> ${If.End}

このステートメントのこの構文では、大文字と小文字が区別されます。

例:

- **Word 文書だけにヘッダー テキストを設定する:**
    
    `${If.App.Word}This Word document is sensitive ${If.End}`
    
    Word 文書のヘッダーのみに、ラベルは "This Word document is sensitive" (この Word 文書では大文字と小文字が区別されます) という見出しテキストを適用します。 他の Office アプリケーションには、ヘッダー テキストは適用されません。

- **Word、Excel、Outlook と PowerPoint で異なるフッター テキストを設定する:**
    
    `${If.App.WXO}This content is confidential. ${If.End}${If.App.PowerPoint}This presentation is confidential. ${If.End}`
    
    Word、Excel、Outlook で、ラベルは "This content is confidential" (このコンテンツは社外秘です) というフッター テキストを適用します。 PowerPoint では、ラベルは "This presentation is confidential" (このプレゼンテーションは社外秘です) というフッター テキストを適用します。

- **Word と PowerPoint に特定の透かしテキストを設定し、Word、Excel、PowerPoint に透かしテキストを設定する:**
    
    `${If.App.WP}This content is ${If.End}Confidential`
    
    Word と PointPoint で、ラベルは "This content is Confidential" (このコンテンツは社外秘です) という透かしテキストを適用します。 Excel で、ラベルは "Confidential" (社外秘) という透かしテキストを適用します。 Outlook では、視覚的マーキングとしての透かしが Outlook に対応していないため、ラベルは透かしテキストを適用しません。

### <a name="setting-the-font-name"></a>フォント名を設定する

Calibri は、ヘッダー、フッター、透かしのテキストに使われる既定のフォントです。 別のフォント名を指定する場合、視覚的なマーキングを適用するクライアント デバイスでそれが利用できることを確認してください。 

指定したフォントが使用可能でない場合、クライアントは Calibri フォントの使用にフォールバックします。

### <a name="setting-the-font-color"></a>フォントの色を設定する

利用できる色の一覧から選択するか、赤、緑、青 (RGB) の色のコンポーネントの 16 進数コードを入力してカスタムの色を指定できます。 たとえば、**#DAA520** と入力します。 

これらのコードの参照が必要な場合、MSDN ドキュメントの[名前別の色](https://msdn.microsoft.com/library/aa358802\(v=vs.85\).aspx)に関するページが役に立ちます。 画像編集できるさまざまなアプリケーションでもコードを参照できます。 たとえば、Microsoft ペイントでは、パレットからカスタム色を選択できます。RGB 値が自動的に表示されるので、それをコピーできます。

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

