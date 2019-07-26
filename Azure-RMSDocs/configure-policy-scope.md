---
title: Azure Information Protection のスコープ ポリシーの構成 - AIP
description: 特定のユーザーに対して異なる設定やラベルを構成するには、Azure Information Protection のスコープ ポリシーを構成する必要があります。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 929032aeb98981e71ff6822ebc8fdccfb68b1ec6
ms.sourcegitcommit: 47182b6a65bfae3561cb34be3d6a6852a1edccb9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68446721"
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストール済みのコンピューターに Azure Information Protection ポリシーがダウンロードされた場合、すべてのユーザーは既定のポリシーの設定とラベル、またはグローバル ポリシー用に構成された変更を取得します。 異なる設定やラベルを使用して、特定のユーザーに対してこの構成を補完する場合は、それらのユーザー用に構成された**スコープ付きポリシー**を作成する必要があります。

## <a name="how-scoped-policies-work"></a>スコープ付きポリシーのしくみ

Azure Information Protection クライアントをサポートするアプリケーションの場合、すべてのユーザーは、Information Protection バーに表示されるタイトルとツールヒント、グローバル設定、およびグローバル ラベルを含むグローバル ポリシーを受信します。 特定のユーザーに対してスコープ ポリシーがあらかじめ構成されている場合、これらのユーザーは追加の設定とラベルを受信します。 

Azure Information Protection クライアントをサポートする Office デスクトップ アプリケーションに加えて、ラベルも PowerShell および Azure Information Protection スキャナーでサポートされています。 つまり、Powershell コマンドまたはスキャナーを実行するアカウントに対して、スコープ ポリシーを作成し構成することができます。 

スコープ ポリシーは、ラベルと同じように、Azure Portal で順序が決まります。 ユーザーが複数のスコープに対して構成されている場合は、ポリシーのダウンロード前に、そのユーザーの有効なポリシーが計算されます。 ポリシーの順序に従って、最後のポリシー設定が適用されます。 グローバル ポリシーのラベル、およびユーザーが所属するスコープ ポリシーの追加ラベルがユーザーに表示されます。

例外は、テナントからのユーザーがラベル付きのドキュメントまたは電子メールを開く場合に、そのユーザーがラベルのスコープに含まれていない場合です。 このシナリオでは、ユーザーにラベルのセットの名前が表示されますが、ラベルは選択可能なものとして表示されません。  

スコープ ポリシーでは、グローバル ポリシーのラベルと設定が常に継承されるため、スコープ ポリシーを作成または編集した場合は、グローバル ポリシーのラベルが表示されます。 ただし、スコープ ポリシーの編集時にグローバル ポリシーのラベルを編集することはできません。 ただし、これらの継承されたラベルにサブラベルを追加することはできます。

たとえば、グローバル ポリシーに **Confidential** という名前のラベルがある場合、このラベルはすべてのユーザーに表示されます。 スコープ ポリシーでこのラベルを削除したり順序を変更したりすることはできません。 ただし、マーケティング部門に新しいサブラベルを Confidential に追加したスコープ ポリシーを作成して、この部門のユーザーに **Confidential \ Promotions** が表示されるようにすることはできます。 また、販売部門に新しいサブラベルを Confidential に追加した別のスコープ ポリシーを作成して、この部門のユーザーに **Confidential \ Partners** が表示されるようにすることもできます。 各サブラベルを異なる設定に構成して、それぞれの部門のユーザーにのみ表示させることができます。

## <a name="configure-a-scoped-policy"></a>スコープポリシーを構成する

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ブレードに移動します。

    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[分類]**  >  **[ポリシー]** メニュー オプションから: **[Azure Information Protection - ポリシー]** ブレードで、 **[新しいポリシーの追加]** を選択します。 **[ポリシー]** ブレードに既存のグローバル ポリシーが表示され、新しいスコープ付きポリシーを構成できます。

3. Azure Portal で管理者のみに表示されるポリシー名と説明を指定します。 この名前はテナントで一意である必要があります。 **[Specify which users/groups get this policy]\(このポリシーを取得するユーザー/グループの指定\)** を選び、その後のブレードでこのポリシーを取得するユーザーとグループを検索して選びます。 このスコープ ポリシーで構成したラベルと設定は、選択したユーザーにのみ適用されます。
    
    パフォーマンス上の理由から、スコープ ポリシー用のグループのメンバーシップは[キャッシュ](prepare.md#group-membership-caching-by-azure-information-protection)されます。

4. ここで、新しいラベルを追加したり、スコープ ポリシーの設定を構成します。 グローバル ポリシーは常に最初に適用されるため、新しいラベルでグローバル ポリシーを補い、グローバル設定をオーバーライドすることができます。 たとえば、グローバル ポリシーに既定のラベルが何も指定されていない場合は、特定の部門の別のスコープ ポリシーで、既定のラベルを別途構成することができます。

    ラベルまたは設定の構成に関するヘルプが必要な場合は、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

6. グローバル ポリシーを編集するときのように、[Azure Information Protection] ブレードで変更を行ったら、 **[保存]** をクリックして変更を保存します。または、 **[破棄]** をクリックして、最後に保存した設定に戻します。 

7. このスコープ ポリシーの変更が完了したら、最初の **[Azure Information Protection - ポリシー]** ブレードで、このスコープ ポリシーの適用される順序が正しいことを確認します。 これは、複数のスコープ ポリシーに対して同じユーザーを選択した場合に重要になります。 順序を変更するには、コンテキスト メニュー **[...]** を選んで、 **[上へ移動]** または **[下へ移動]** を選びます。 

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時、またはエクスプローラーが開かれたときに常に変更の有無を確認します。 変更があった場合、クライアントはそのユーザーに適用されるグローバル ポリシーまたはスコープ ポリシーに変更をダウンロードします。

## <a name="next-steps"></a>次の手順

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、[ポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)に関するチュートリアルをご覧ください。
