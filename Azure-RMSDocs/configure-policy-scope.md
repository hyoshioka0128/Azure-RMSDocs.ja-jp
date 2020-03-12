---
title: Azure Information Protection のスコープ ポリシーの構成 - AIP
description: 特定のユーザーに対して異なる設定やラベルを構成するには、Azure Information Protection のスコープ ポリシーを構成する必要があります。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d0a370950bb5853453106e59af3da9c9a2f8f463
ms.sourcegitcommit: b66b249ab5681d02ec3b5af0b820eda262d5976a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "78972887"
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順: [Windows 用の Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストール済みのコンピューターに Azure Information Protection ポリシーがダウンロードされた場合、すべてのユーザーは既定のポリシーの設定とラベル、またはグローバル ポリシー用に構成された変更を取得します。 異なる設定やラベルを使用して、特定のユーザーに対してこの構成を補完する場合は、それらのユーザー用に構成された**スコープ付きポリシー**を作成する必要があります。

## <a name="how-scoped-policies-work"></a>スコープ付きポリシーのしくみ

Azure Information Protection クライアントをサポートするアプリケーションの場合、すべてのユーザーは、Information Protection バーに表示されるタイトルとツールヒント、グローバル設定、およびグローバル ラベルを含むグローバル ポリシーを受信します。 特定のユーザーに対してスコープ ポリシーがあらかじめ構成されている場合、これらのユーザーは追加の設定とラベルを受信します。 

Azure Information Protection クライアントをサポートする Office デスクトップ アプリケーションに加えて、ラベルも PowerShell および Azure Information Protection スキャナーでサポートされています。 つまり、Powershell コマンドまたはスキャナーを実行するアカウントに対して、スコープ ポリシーを作成し構成することができます。 

スコープ ポリシーは、ラベルと同じように、Azure Portal で順序が決まります。 ユーザーが複数のスコープに対して構成されている場合は、ポリシーのダウンロード前に、そのユーザーの有効なポリシーが計算されます。 ポリシーの順序に従って、最後のポリシー設定が適用されます。 グローバル ポリシーのラベル、およびユーザーが所属するスコープ ポリシーの追加ラベルがユーザーに表示されます。

例外は、テナントからのユーザーがラベル付きのドキュメントまたは電子メールを開く場合に、そのユーザーがラベルのスコープに含まれていない場合です。 このシナリオでは、ユーザーにラベルのセットの名前が表示されますが、ラベルは選択可能なものとして表示されません。  

スコープ ポリシーでは、グローバル ポリシーのラベルと設定が常に継承されるため、スコープ ポリシーを作成または編集した場合は、グローバル ポリシーのラベルが表示されます。 ただし、スコープ ポリシーの編集時にグローバル ポリシーのラベルを編集することはできません。 ただし、これらの継承されたラベルにサブラベルを追加することはできます。

たとえば、グローバル ポリシーに **Confidential** という名前のラベルがある場合、このラベルはすべてのユーザーに表示されます。 スコープ ポリシーでこのラベルを削除したり順序を変更したりすることはできません。 ただし、マーケティング部門に新しいサブラベルを Confidential に追加したスコープ ポリシーを作成して、この部門のユーザーに **Confidential \ Promotions** が表示されるようにすることはできます。 また、販売部門に新しいサブラベルを Confidential に追加した別のスコープ ポリシーを作成して、この部門のユーザーに **Confidential \ Partners** が表示されるようにすることもできます。 各サブラベルを異なる設定に構成して、それぞれの部門のユーザーにのみ表示させることができます。

## <a name="configure-a-scoped-policy"></a>スコープポリシーを構成する

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ペインに移動します。

    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、 **[Azure Information Protection]** を選択します。

2. [**分類** > **ポリシー** ] メニューオプションから: **[Azure Information Protection ポリシー]** ウィンドウで、 **[新しいポリシーの追加]** を選択します。 次に、既存のグローバルポリシーを表示する**ポリシー**ウィンドウが表示されます。ここで、新しいスコープ付きポリシーを構成できます。

3. Azure Portal で管理者のみに表示されるポリシー名と説明を指定します。 この名前はテナントで一意である必要があります。 次に、[**このポリシーを取得するユーザー/グループを指定**してください] を選択し、後続のウィンドウで、このポリシーのユーザーとグループを検索して選択します。 このスコープ ポリシーで構成したラベルと設定は、選択したユーザーにのみ適用されます。
    
    パフォーマンス上の理由から、スコープ ポリシー用のグループのメンバーシップは[キャッシュ](prepare.md#group-membership-caching-by-azure-information-protection)されます。

4. ここで、新しいラベルを追加したり、スコープ ポリシーの設定を構成します。 グローバル ポリシーは常に最初に適用されるため、新しいラベルでグローバル ポリシーを補い、グローバル設定をオーバーライドすることができます。 たとえば、グローバル ポリシーに既定のラベルが何も指定されていない場合は、特定の部門の別のスコープ ポリシーで、既定のラベルを別途構成することができます。

    ラベルまたは設定の構成に関するヘルプが必要な場合は、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

6. グローバルポリシーを編集するときと同様に、Azure Information Protection ウィンドウで変更を行うときは、 **[保存]** をクリックして変更を保存するか、 **[破棄]** をクリックして最後に保存した設定に戻します。 

7. このスコープポリシーに必要な変更が完了したら、[初期**Azure Information Protection-ポリシー** ] ウィンドウで、このスコープポリシーが適用する順序であることを確認します。 これは、複数のスコープ ポリシーに対して同じユーザーを選択した場合に重要になります。 順序を変更するには、コンテキスト メニュー **[...]** を選んで、 **[上へ移動]** または **[下へ移動]** を選びます。 

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時、またはエクスプローラーが開かれたときに常に変更の有無を確認します。 変更があった場合、クライアントはそのユーザーに適用されるグローバル ポリシーまたはスコープ ポリシーに変更をダウンロードします。

## <a name="next-steps"></a>次の手順

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、[ポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)に関するチュートリアルをご覧ください。
