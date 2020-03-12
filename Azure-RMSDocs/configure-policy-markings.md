---
title: Azure Information Protection ラベルの視覚的なマーキングを構成する - AIP
description: ドキュメントまたは電子メール メッセージにラベルを割り当てるときに、選択した分類を見やすくするためのさまざまなオプションを選択できます。 これらの視覚的なマーキングには、ヘッダー、フッター、および透かしがあります。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 6492c4dcbe9ba408d2d4efd9c751933a6eefe6b4
ms.sourcegitcommit: b66b249ab5681d02ec3b5af0b820eda262d5976a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "78972806"
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Azure Information Protection 用の視覚的なマーキングのラベルを構成する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

ドキュメントまたは電子メール メッセージにラベルを割り当てるときに、選択した分類を見やすくするためのさまざまなオプションを選択できます。 これらの視覚的なマーキングには、ヘッダー、フッター、および透かしがあります。 

視覚的なマーキングに関する追加情報:

- ヘッダーとフッターは、Word、Excel、PowerPoint、および Outlook に適用されます。

- 透かしは、Word、Excel、および PowerPoint に適用されます。

    - Excel: 透かしが表示されるのは、ページ レイアウト モード、印刷プレビュー モード、および印刷時のみです。
    
    - PowerPoint: 透かしは、マスター スライドに背景画像として適用されます。 **[表示]** タブの **[スライド マスター]** で、 **[背景グラフィックを表示しない]** チェック ボックスがオフになっていることを確認します。

- 透かしと、Word、Excel、PowerPoint のヘッダーおよびフッターでは、複数の行がサポートされています。 Outlook で適用されるラベルのヘッダーまたはフッターに対して複数の行を指定した場合、その行は連結されます。 このシナリオでは、[Word、Excel、PowerPoint、Outlook にさまざまな視覚的なマーキングを設定する](#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)構成の使用を検討します。

- 文字列の最大長:
    
    - ヘッダーとフッターに入力できる文字列の最大長は 1024 文字です。 しかし、Excel にはヘッダーとフッターに合計 255 文字の制限があります。 この制限には、Excel で表示されない文字 (書式設定コードなど) が含まれます。 その制限に達すると、入力した文字列は Excel では表示されません。
    
    - 入力できる透かしの文字列の最大長は 255 文字です。

- ヘッダー、フッター、または透かしを適用するときに、単なるテキスト文字列を指定するか、[変数](#using-variables-in-the-text-string)を使用してテキスト文字列を動的に作成することができます。

- Word、PowerPoint、Outlook に加えて Excel でも、さまざまな色の視覚的なマーキングがサポートされるようになりました。

- 視覚的なマーキングがサポートする言語は 1 つのみです。

## <a name="when-visual-markings-are-applied"></a>視覚的なマーキングが適用されるタイミング

メール メッセージの場合、Outlook からメール メッセージが送信されたときに視覚的なマーキングが適用されます。 そのメール メッセージがラベルを変更されて転送または返信された場合、元の視覚的なマーキングは常に保持されます。

ドキュメントでは、視覚的なマーキングが次のように適用されます。

- Office アプリでは、ラベルの適用時に、ラベルからの視覚的なマーキングが適用されます。 ラベル付きのドキュメントを開いたときと、ドキュメントを最初に保存したときにも、視覚的なマーキングが適用されます。  

- エクスプローラー、PowerShell、Azure Information Protection スキャナーを使用してドキュメントにラベルを付けると、視覚的なマーキングはすぐには適用されませんが、ドキュメントを Office アプリで開いたときと、ドキュメントが最初に保存されるときに、Azure Information Protection クライアントによって適用されます。
    
    SharePoint Online、OneDrive、または OneDrive for Business に保存されているファイルに対して Office アプリで[自動](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5)保存を使用すると、[自動更新] がオンになっている場合を除き、分類をバックグラウンドで継続的に実行するように [[アドバンストクライアント] 設定](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)を構成しない限り、視覚的なマーキングは適用されません。 

## <a name="to-configure-visual-markings-for-a-label"></a>ラベルの視覚的なマーキングを構成するには

ラベルの視覚的なマーキングを構成するには、次の手順に従います。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、 **[Azure Information Protection]** を選択します。

2. [**分類** > **ラベル**] メニューオプションから: **[Azure Information Protection ラベル]** ウィンドウで、追加または変更する視覚的なマーキングが含まれているラベルを選択します。

3. **[ラベル]** ウィンドウの **[視覚的なマーキングの設定 (ヘッダーやフッターなど)]** セクションで、目的の視覚的なマーキングの設定を構成し、 **[保存]** をクリックします。
    
    - ヘッダーを構成するには: **[Documents with this label have a header]** (このラベルを持つドキュメントにヘッダーを設定する) で、ヘッダーを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、ヘッダーのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、ヘッダーの配置を指定します。
    
    - フッターを構成するには: **[Documents with this label have a footer]** (このラベルを持つドキュメントにフッターを設定する) で、フッターを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、フッターのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、フッターの配置を指定します。
    
    - 透かしを構成するには: **[Documents with this label have a watermark]** (このラベルを持つドキュメントに透かしを設定する) で、透かしを設定する場合は **[オン]** を、設定しない場合は **[オフ]** を選択します。 **[オン]** を選択した場合は、透かしのテキスト、サイズ、[フォント](#setting-the-font-name)、[色](#setting-the-font-color)、透かしの配置を指定します。
    
**[保存]** をクリックすると、変更内容がユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。


## <a name="using-variables-in-the-text-string"></a>テキスト文字列に変数を使用する

次の変数は、Azure Information Protection クラシッククライアントを使用しているときに一般に使用でき、Azure Information Protection 統合ラベル付けクライアントを使用するとパブリックプレビューの可用性になります。  

ヘッダー、フッター、または透かしのテキスト文字列には、次の変数を使用できます。

- `${Item.Label}`: 選択したラベル。 例: General

- `${Item.Name}`: ファイル名または電子メールの件名。 例: JulySales.docx

- `${Item.Location}`: ドキュメントのパスとファイル名、電子メールの件名。 例: \\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}`: ドキュメントまたは電子メールの所有者、Windows のサインイン ユーザー名。 例: rsimone 

- `${User.PrincipalName}`: ドキュメントまたは電子メールの所有者、Azure Information Protection クライアントのサインイン電子メール アドレス (UPN) 例: rsimone@vanarsdelltd.com

- `${Event.DateTime}`: 選択したラベルが設定された日時。 例: 8/16/2016 1:30 PM

> [!NOTE]
>この構文では、大文字と小文字が区別されます。

例: `Document: ${Item.Name}  Classification: ${Item.Label}`General**ラベル フッターに** という文字列を指定する場合、project.docx というドキュメントに適用されるフッター テキストは、**Document: project.docx  Classification: General** になります。

> [!NOTE]
> `${User.Name}` 変数と `${User.PrincipalName}` 変数のどちらを使用しても、Azure Information Protection の統合ラベル付けクライアントでは現在サポートされていません。 

>[!TIP]
> フィールドコードを使用し[て、ラベル名](faqs-infoprotect.md#can-i-create-a-document-template-that-automatically-includes-the-classification)をドキュメントまたはテンプレートに挿入することもできます。

## <a name="setting-different-visual-markings-for-word-excel-powerpoint-and-outlook"></a>Word、Excel、PowerPoint、Outlook にさまざまな視覚的マーキングを設定する

既定では、指定した視覚的マーキングは Word、Excel、PowerPoint、Outlook のすべてに適用されます。 ただし、テキスト文字列に "If.App" という変数ステートメントを入れると、Office アプリケーションごとに視覚的マーキングを指定できます。**Word**、**Excel**、**PowerPoint**、**Outlook** という値を利用し、アプリケーションの種類を区別できます。 このような値は省略することもできます。同じ If.App ステートメントで複数回指定する場合に必要になります。

使用する構文は以下のとおりです。

    ${If.App.<application type>}<your visual markings text> ${If.End}

> [!NOTE]
>このステートメントのこの構文では、大文字と小文字が区別されます。

例:

- **Word 文書だけにヘッダー テキストを設定する:**
    
    `${If.App.Word}This Word document is sensitive ${If.End}`
    
    Word 文書のヘッダーのみに、ラベルは "This Word document is sensitive" (この Word 文書では大文字と小文字が区別されます) という見出しテキストを適用します。 他の Office アプリケーションには、ヘッダー テキストは適用されません。

- **Word、Excel、Outlook と PowerPoint で異なるフッター テキストを設定する:**
    
    `${If.App.WXO}This content is confidential. ${If.End}${If.App.PowerPoint}This presentation is confidential. ${If.End}`
    
    Word、Excel、Outlook で、ラベルは "This content is confidential" (このコンテンツは社外秘です) というフッター テキストを適用します。 PowerPoint では、ラベルは "This presentation is confidential" (このプレゼンテーションは社外秘です) というフッター テキストを適用します。

- **Word と PowerPoint に特定の透かしテキストを設定し、Word、Excel、PowerPoint に透かしテキストを設定する:**
    
    `${If.App.WP}This content is ${If.End}Confidential`
    
    Word と PowerPoint で、ラベルは "This content is Confidential" (このコンテンツは社外秘です) という透かしテキストを適用します。 Excel で、ラベルは "Confidential" (社外秘) という透かしテキストを適用します。 Outlook では、視覚的マーキングとしての透かしが Outlook に対応していないため、ラベルはいかなる透かしテキストも適用しません。

> [!NOTE]
> Azure Information Protection の統一されたラベル付けクライアントを使用する場合、 **[フォント名]** の値を設定できるのは Azure Information Protection ポータルを使用した場合のみです。 5つの既定値の1つを超える**フォントの色**の値を設定する場合、は Azure Information Protection ポータルを使用することによってのみ可能です。

### <a name="setting-the-font-name"></a>フォント名を設定する

Calibri は、ヘッダー、フッター、透かしのテキストに使われる既定のフォントです。 別のフォント名を指定する場合、視覚的なマーキングを適用するクライアント デバイスでそれが利用できることを確認してください。 

指定したフォントが使用可能でない場合、クライアントは Calibri フォントの使用にフォールバックします。

### <a name="setting-the-font-color"></a>フォントの色を設定する

利用できる色の一覧から選択するか、赤、緑、青 (RGB) の色のコンポーネントの 16 進数コードを入力してカスタムの色を指定できます。 たとえば、 **#40e0d0**は水色の RGB 16 進値です。 

これらのコードの参照が必要な場合は、MSDN web ドキュメントの[\<色 >](https://developer.mozilla.org/docs/Web/CSS/color_value)のページから役に立つテーブルを見つけることができます。また、これらのコードは、画像を編集できる多くのアプリケーションでも見つかります。 たとえば、Microsoft ペイントでは、パレットからカスタム色を選択できます。RGB 値が自動的に表示されるので、それをコピーできます。

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

