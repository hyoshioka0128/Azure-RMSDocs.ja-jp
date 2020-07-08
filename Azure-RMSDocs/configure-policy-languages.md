---
title: Azure Information Protection で他の言語用ラベルを構成する
description: Azure Information Protection ポリシーで言語を指定して翻訳をインポートすることにより、Information Protection バーでユーザーに表示されるラベルおよびあらゆるテンプレートに、異なる言語のサポートを追加できます。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: a582a32a149fcaf6146c5deb13d8b88f682d7b0d
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048274"
---
# <a name="how-to-configure-labels-and-templates-for-different-languages-in-azure-information-protection"></a>Azure Information Protection で異なる言語のラベルとテンプレートを構成する方法

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

> [!NOTE]
> これらの手順は、Azure Information Protection の統合ラベル付けクライアントではなく、Azure Information Protection クライアント (クラシック) に適用されます。 これらのクライアントの違いがわからない場合は、 こちらの [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) を参照してください。
> 
> 機密ラベル用にさまざまな言語を構成する方法については、Office 365 Security & コンプライアンス PowerShell と、 *LocaleSettings*パラメーター[を使用してください。](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)

Azure Information Protection の既定のラベルは複数の言語をサポートしますが、指定するラベルの名前と説明のサポートを構成する必要があります。 この構成では、次のことを行う必要があります。

1. ユーザーが使う言語を選択します。 

2. 現在のラベルの名前と説明をファイルにエクスポートします。

3. 翻訳を提供するようにファイルを編集します。

4. ファイルをインポートして Azure Information Protection ポリシーに戻します。

次のいずれかの条件が当てはまるときは、異なる言語のテンプレートを構成することもできます。 この構成は、ユーザーまたは管理者が、現在のテンプレートの名前と説明をローカライズされた言語で表示する必要がある場合に適しています。

- テンプレートが Azure クラシック ポータルまたは PowerShell で作成されており、**[定義済みのテンプレートを選択する]** 保護設定を使ってテンプレートがラベルにリンクされていない場合。

- ラベルをサポートするサブスクリプションがないため、Azure Portal でのみテンプレートを作成および管理できる場合。

ユーザーの Office と Windows の言語設定に一致する言語を選択します。 これらのラベル名と説明は、Office アプリの Azure Information Protection バーと **[分類と保護 - Azure Information Protection]** ダイアログ ボックスにそれぞれ表示されます。 選択する言語の詳細については、このページの「[Azure Information Protection クライアントで表示言語が決定されるしくみ](#how-the-azure-information-protection-client-determines-the-language-to-display)」をご覧ください。 

## <a name="to-configure-labels-and-templates-for-different-languages"></a>異なる言語のラベルとテンプレートを構成するには

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

2. [言語**の管理**  >  **Languages** ] メニューオプションから: [ **Azure Information Protection の言語**] ウィンドウで、[**翻訳する新しい言語を追加する**] を選択します。 追加する言語を選択して、**[OK]** を選択します。 [検索] ボックスに言語の名前を入力するか、使用可能な言語の一覧をスクロールします。

3. 選択した言語が [ **Azure Information Protection の言語**] ウィンドウに表示されるようになりました。
    
    - 別の言語を追加するには、**[翻訳する新しい言語の追加]** を選択して前の手順を繰り返します。 
        
        > [!NOTE]
        > ユーザーが Office と Windows で使用できる言語を選択してください。 場合によっては、コンピューターごとに 2 つの異なる選択が必要なことがあります。
        
    - 追加した言語を変更する場合は、一覧から該当するエントリを選択して、**[削除]** をクリックします。

4. サポートするすべての言語が一覧表示されたら、**[言語名]** の横のチェック ボックスをオンにしてすべてのエントリを選択 (または代わりに個々のエントリを選択) し、**[エクスポート]** をクリックして既存のラベル名と説明のローカル コピーをファイルに保存します。 
    
    ダウンロードされたファイルは **exported localization.zip** の名前で、ローカルのダウンロード フォルダーに保存されます。 また、Azure Portal のステータス バーでこのファイル名を選択することで、ファイルにアクセスできます。

5. **exported localization.zip** からファイルを抽出して、ダウンロードを選択した各言語の .xml ファイルを取得します。 

6. 各 .xml ファイルを編集します。`<LocalizedText>` タグ内の各文字列に、選択した言語ごとに翻訳を入力します。 

7. 各 .xml ファイルを編集したら、これらのファイルを含めた新しい圧縮 (zip 形式) フォルダーを作成します。 圧縮フォルダーには任意の名前を付けることができますが、.zip の拡張子が必要です。
    
    ヒント: ダウンロードした各言語ファイルを編集するまで待つ必要はありません。 代わりに、ダウンロードしたすべてのファイルのサブセットを .zip ファイルに含めることで、段階的に異なる言語をロールアウトできます。 その後、他の言語の翻訳を完了した時点で、手順 7 と 8 を繰り返します。

8. **Azure Information Protection の言語**] ウィンドウに戻り、[**インポート**] を選択します。 このオプションが使用できない場合は、まず **[言語名]** のチェック ボックス、または個別に選択した言語のチェック ボックスをオフにします。
    
    インポートが完了したら、ローカライズされた名前と説明をユーザーにダウンロードします。

新しい言語をサポートするか、新しいラベルを作成する必要がある場合、または Azure portal でラベルの名前や説明を変更した場合は、この手順を繰り返す必要があります。

## <a name="how-the-azure-information-protection-client-determines-the-language-to-display"></a>Azure Information Protection クライアントで表示言語が決定されるしくみ

他の言語をサポートする Azure Information Protection ポリシーをユーザーがダウンロードする場合、ラベルの名前とヒントでユーザーに表示される言語は、次のロジックに従って決定されます。

**Office アプリの Azure Information Protection バーでユーザーに表示されるラベルとヒント**

- ユーザーの Office アプリの言語と直接一致する言語がある場合は、その言語を使用してラベルの名前と説明が表示されます。

- ユーザーの Office アプリの言語と一致する言語がない場合は、管理者がすべてのユーザーに対して既定で指定した言語を使用して、ラベルの名前と説明が表示されます。 通常、この言語は、既定のポリシーで使用される英語です。

**ユーザーが右クリックしてファイルまたはフォルダーを分類および保護するときに表示されるラベルとヒント**

- ユーザーのオペレーティング システムの言語と直接一致する言語がある場合は、その言語を使用してラベルの名前と説明が表示されます。

- ユーザーのオペレーティング システムの言語と一致する言語がない場合は、管理者がすべてのユーザーに対して既定で指定した言語を使用して、ラベルの名前と説明が表示されます。 通常、この言語は、既定のポリシーで使用される英語です。

## <a name="when-localized-label-names-are-not-used"></a>ローカライズされたラベル名が使用されない場合

次のシナリオでは、ローカライズされたラベル (およびサブラベル) の名前は使用されません。 テナント全体の一貫性のために、次の項目に関しては既定の言語が常に使用されます。

- クライアントの利用状況ログ

- PowerShell (Get-AIPFileStatus からの出力)

- ドキュメント メタデータと電子メール ヘッダー


## <a name="next-steps"></a>次のステップ

ラベルに実行できるオプションを構成する方法や、Azure Information Protection ポリシーのその他の設定について詳しくは、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。



