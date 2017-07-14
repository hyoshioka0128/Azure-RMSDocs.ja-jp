---
title: "Azure Information Protection で他の言語用ラベルを構成する"
description: "Azure Information Protection ポリシーで言語を指定して翻訳をインポートすることにより、Information Protection バーでユーザーに表示されるラベルに、他言語のサポートを追加できます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.openlocfilehash: ec99bf36e8904a7304a9d33c32d17ba92e2e22d2
ms.sourcegitcommit: 8b768e7e249e124f24acdf630d165eaf743f9c21
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/05/2017
---
# Azure Information Protection で他の言語用ラベルを構成する方法
<a id="how-to-configure-labels-for-different-languages-in-azure-information-protection" class="xliff"></a>

>*適用対象: Azure Information Protection*

>[!NOTE]
>現在プレビュー段階のこの機能は、Azure Information Protection クライアントの**プレビュー** バージョンと組み合わせて利用します。こちらのバージョンは [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。

既定では、ラベルの名前と説明では 1 つの言語がサポートされ、この言語で組織内のすべてのユーザーに表示されます。 必要な言語を選択して他の言語のサポートを追加し、ラベルの現在の名前と説明をファイルにエクスポートし、ファイルを編集して翻訳を入力して Azure Information Protection ポリシーにこのファイルを再びインポートすることができます。

ユーザーの Office と Windows の言語設定に一致する言語を選択します。 これらのラベル名と説明は、Office アプリの Azure Information Protection バーと **[Classify and protection - Azure Information Protection]\(分類と保護 - Azure Information Protection\)** ダイアログ ボックスにそれぞれ表示されます。 選択する言語の詳細については、このページの「[Azure Information Protection クライアントで表示言語が決定されるしくみ](#how-the-azure-information-protection-client-determines-the-language-to- display)」をご覧ください。 

## 他の言語で表示するようにラベルを構成するには
<a id="to-configure-labels-to-display-in-different-languages" class="xliff"></a>

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザーのウィンドウで、セキュリティ管理者または全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 最初の **[Azure Information Protection]** ブレードで、**[管理]** を見つけて、**[Languages (Preview)\(言語 (プレビュー)\)]** を選択します。

3. **[Azure Information Protection - Languages (Preview)]\(Azure Information Protection - 言語 (プレビュー)\)** ブレードで、検索ボックスに言語名を入力するか、使用可能な言語の一覧をスクロールして、最初に追加する言語を見つけます。 

4. 言語を選択し、**[OK]** をクリックします。

5. 次のブレードで、選択した言語が追加された一覧が表示されます。
    
    - 別の言語を追加するには、**[Add a new language for translation]\(翻訳する新しい言語を追加\)** を選択して手順 3 と手順 4 を繰り返します。 
        
        > [!NOTE]
        > ユーザーが Office と Windows で使用できる言語を選択してください。 場合によっては、コンピューターごとに 2 つの異なる選択が必要なことがあります。
        
    - 追加した言語を変更する場合は、一覧から該当するエントリを選択して、**[削除]** をクリックします。

6. サポートするすべての言語が一覧表示されたら、**[言語名]** の横のチェック ボックスをオンにしてすべてのエントリを選択 (または代わりに個々のエントリを選択) し、**[エクスポート]** をクリックして既存のラベル名と説明のローカル コピーをファイルに保存します。 
    
    ダウンロードされたファイルは **exported localization.zip** の名前で、ローカルのダウンロード フォルダーに保存されます。 また、Azure Portal のステータス バーでこのファイル名を選択することで、ファイルにアクセスできます。

7. **exported localization.zip** からファイルを抽出して、ダウンロードを選択した各言語の .xml ファイルを取得します。 

8. 各 .xml ファイルを編集します。`<LocalizedText>` タグ内の各文字列に、選択した言語ごとに翻訳を入力します。 

9. 各 .xml ファイルを編集したら、これらのファイルを含めた新しい圧縮 (zip 形式) フォルダーを作成します。 圧縮フォルダーには任意の名前を付けることができますが、.zip の拡張子が必要です。

10. [Azure Portal] ブレードに戻り、**[インポート]** を選択します。 このオプションが使用できない場合は、まず **[言語名]** のチェック ボックス、または個別に選択した言語のチェック ボックスをオフにします。
    
    インポートが完了すると、Azure Information Protection ポリシーが次に公開された後に、ローカライズされたラベル名と説明がユーザーにダウンロードされます。 **[グローバル ポリシー]** または **[スコープ付きポリシー]** ブレードで **[公開]** をクリックできます。

## Azure Information Protection クライアントで表示言語が決定されるしくみ
<a id="how-the-azure-information-protection-client-determines-the-language-to-display" class="xliff"></a>

他の言語をサポートする Azure Information Protection ポリシーをユーザーがダウンロードする場合、ラベルの名前とヒントでユーザーに表示される言語は、次のロジックに従って決定されます。

**Office アプリの Azure Information Protection バーでユーザーに表示されるラベルとヒント**

- ユーザーの Office アプリの言語と直接一致する言語がある場合は、その言語を使用してラベルの名前と説明が表示されます。

- ユーザーの Office アプリの言語と一致する言語がない場合は、管理者がすべてのユーザーに対して既定で指定した言語を使用して、ラベルの名前と説明が表示されます。 通常、この言語は、既定のポリシーで使用される英語です。

**ユーザーが右クリックしてファイルまたはフォルダーを分類および保護するときに表示されるラベルとヒント**

- ユーザーのオペレーティング システムの言語と直接一致する言語がある場合は、その言語を使用してラベルの名前と説明が表示されます。

- ユーザーのオペレーティング システムの言語と一致する言語がない場合は、管理者がすべてのユーザーに対して既定で指定した言語を使用して、ラベルの名前と説明が表示されます。 通常、この言語は、既定のポリシーで使用される英語です。

## ローカライズされたラベル名が使用されない場合
<a id="when-localized-label-names-are-not-used" class="xliff"></a>

次のシナリオでは、ローカライズされたラベル (およびサブラベル) の名前は使用されません。 テナント全体の一貫性のために、次の項目に関しては既定の言語が常に使用されます。

- クライアントの利用状況ログ

- PowerShell (Get-AIPFileStatus からの出力)

- ドキュメント メタデータと電子メール ヘッダー


## 次のステップ
<a id="next-steps" class="xliff"></a>

ラベルに実行できるオプションを構成する方法や、Azure Information Protection ポリシーのその他の設定について詳しくは、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


