---
title: "Azure Information Protection のスコープ付きポリシーを構成する"
description: "特定のユーザーに異なる設定とラベルを構成するには、Azure Information Protection のスコープ付きポリシーを構成する必要があります。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: c7aa1c3aa18a246457c00a5a61c6004e55f76b4b
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2018
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法

>*適用対象: Azure Information Protection*

[Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) クライアントがインストールされているコンピューターに Azure Information Protection ポリシーがダウンロードされると、すべてのユーザーは、既定のポリシーから設定とラベルを取得するか、グローバル ポリシー用に構成された変更を取得します。 特定のユーザーに対して、設定やラベルを変更して構成を補完する場合は、それらのユーザー用に構成された**スコープ付きポリシー**を作成する必要があります。

すべてのユーザーは、Information Protection バーのタイトルとツールヒント、グローバル設定、およびグローバル ラベルを含むグローバル ポリシーを受け取ります。 特定のユーザーに対してスコープ付きポリシーを構成した場合、それらのユーザーは追加の設定とラベルを受け取ります。 

スコープ付きポリシーは、ラベルと同様に Azure Portal で順序付けされます。 ユーザーが複数のスコープに対して構成されている場合、ダウンロード前に、そのユーザーの有効なポリシーが計算されます。 ポリシーの順序に従って、最後のポリシー設定が適用されます。 ユーザーに表示されるラベルは、グローバル ポリシーのラベルと、ユーザーが属するスコープ付きポリシーの追加ラベルです。 

スコープ付きポリシーは、グローバル ポリシーのラベルと設定を常に継承します。グローバル ポリシーのラベルは、スコープ付きポリシーを作成または編集するときに表示されます。 ただし、スコープ付きポリシーを編集するときに、グローバル ポリシーのラベルを編集することはできません。 ただし、これらの継承されたラベルにサブラベルを追加することはできます。

たとえば、グローバル ポリシーに **Confidential** というラベルがある場合、すべてのユーザーにこのラベルが表示されます。 スコープ付きポリシーでは削除したり並べ替えたりすることはできません。 ただし、Confidential に新しいサブラベルを追加するマーケティング部門のスコープ付きポリシーを作成して、この部門のユーザーに **Confidential \ Promotions** を表示することができます。 また、Confidential に新しいサブラベルを追加する営業部門の別のスコープ付きポリシーを作成し、この部門のユーザーに **Confidential \ Partners** に表示することもできます。 各サブラベルは異なる設定用に構成することができます。また、サブラベルは各部門のユーザーにのみ表示することができます。

Azure Information Protection のスコープ付きポリシーを構成するには:

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザー ウィンドウで、セキュリティ管理者または全体管理者としてサインインします。次に、**[Azure Information Protection]** ブレードに移動します。 

    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 **[Azure Information Protection]** を選択します。

2. **[ポリシー]** メニュー セクションから **[スコープ付きポリシー]** を選択します。

3. **[Azure Information Protection - スコープ付きポリシー]** ブレードで、**[新しいポリシーの追加]** を選択します。 既存のグローバル ポリシーを表示する **[ポリシー]** ブレードが表示されます。ここで、新しいスコープ付きポリシーを構成できます。

4. Azure Portal で管理者にのみ表示されるポリシー名と説明を指定します。 名前はテナントに対して一意である必要があります。 **[Specify which users/groups get this policy]\(このポリシーを取得するユーザー/グループを指定する\)** を選択します。以降のブレードで、このポリシーのユーザーとグループを検索および選択できます。 このスコープ付きポリシーで構成するラベルと設定は、これらのユーザーにのみ適用されます。
    
    パフォーマンス上の理由から、スコープ付きポリシーのグループ メンバーシップは[キャッシュ](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection)されます。

5. 次に、新しいラベルを作成するか、スコープ付きポリシー設定を構成します。 グローバル ポリシーは常に最初に適用されるので、新しいラベルでグローバル ポリシーを補完し、グローバル設定を上書きすることができます。 たとえば、グローバル ポリシーに既定のラベルを指定せず、特定の部門に対して異なるスコープ付きポリシーの異なる既定のラベルを構成します。

    ラベルまたは設定の構成について不明な点がある場合は、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを参照してください。

6. グローバル ポリシーを編集するときと同様に、Azure Information Protection ブレードを変更するときは、**[保存]** をクリックして変更を保存するか、**[破棄]** をクリックして最後に保存した設定に戻します。 

7. このスコープ付きポリシーに必要な変更を完了したら、最初の **[Azure Information Protection - スコープ付きポリシー]** ブレードで、このスコープ付きポリシーが目的の適用順序であることを確認します。 この手順は、複数のスコープ付きポリシーに対して同じユーザーを選択した場合に重要です。 順序を変更するには、コンテキスト メニュー (**[...]**) を選択し、**[上へ移動]** または **[下へ移動]** を選択します。 

8. 変更をデプロイするには、**[発行]** をクリックします。 

Azure Information Protection クライアントは、サポートされている Office アプリケーションが起動するか、ファイル エクスプローラーが開かれるたびに変更がないかどうかを確認します。 クライアントは、グローバル ポリシー、またはそのユーザーに適用されるスコープ付きポリシーの変更をダウンロードします。

> [!TIP]
> スコープ付きポリシーを保存した後は、**[ポリシー]** セクションから **[すべて: クロス ポリシー ビュー]** オプションを使用して、Azure Information Protection ポリシーのすべてのラベルを表示および再構成できます。 この方法を使用すると、グローバル ポリシーとすべてのスコープ付きポリシーのラベルを簡単に比較できます。 

## <a name="next-steps"></a>次の手順

既定のポリシーをカスタマイズし、Office アプリケーションでその動作を確認する方法の例については、「[Azure Information Protection のクイック スタート チュートリアル](../get-started/infoprotect-quick-start-tutorial.md)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
