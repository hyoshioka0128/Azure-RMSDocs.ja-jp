---
title: "Azure Information Protection のスコープ ポリシーの構成"
description: "特定のユーザーに対して異なる設定やラベルを構成するには、Azure Information Protection のスコープ ポリシーを構成する必要があります。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 253a08736352b04b4f730b250b888102836f7e6d
ms.sourcegitcommit: d814d2876cf56e8fff0b107a5e3ec6df2aeda9ae
translationtype: HT
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法

>*適用対象: Azure Information Protection*

[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストール済みのコンピューターに Azure Information Protection ポリシーがダウンロードされた場合、すべてのユーザーは既定のポリシーの設定とラベル、またはグローバル ポリシー用に構成された変更を取得します。 特定のユーザーに対して異なる設定やラベルを構成してこれらを補うには、特定のユーザーに構成された**スコープ ポリシー**を作成する必要があります。

すべてのユーザーは、Information Protection バーに表示されるタイトルとツールヒント、グローバル設定、およびグローバル ラベルを含むグローバル ポリシーを受信します。 特定のユーザーに対してスコープ ポリシーがあらかじめ構成されている場合、これらのユーザーは追加の設定とラベルを受信します。 

スコープ ポリシーは、ラベルと同じように、Azure Portal で順序が決まります。 ユーザーが複数のスコープに対して構成されている場合は、ポリシーのダウンロード前に、そのユーザーの有効なポリシーが計算されます。 ポリシーの順序に従って、最後のポリシー設定が適用されます。 グローバル ポリシーのラベル、およびユーザーが所属するスコープ ポリシーの追加ラベルがユーザーに表示されます。 

スコープ ポリシーでは、グローバル ポリシーのラベルと設定が常に継承されるため、スコープ ポリシーを作成または編集した場合は、グローバル ポリシーのラベルが表示されます。 ただし、スコープ ポリシーの編集時にグローバル ポリシーのラベルを編集することはできません。 これらの継承されたラベルにサブラベルを追加することはできます。

たとえば、グローバル ポリシーに **Confidential** という名前のラベルがある場合、このラベルはすべてのユーザーに表示されます。 スコープ ポリシーでこのラベルを削除したり順序を変更したりすることはできません。 ただし、マーケティング部門に新しいサブラベルを Confidential に追加したスコープ ポリシーを作成して、この部門のユーザーに **Confidential \ Promotions** が表示されるようにすることはできます。 また、販売部門に新しいサブラベルを Confidential に追加した別のスコープ ポリシーを作成して、この部門のユーザーに **Confidential \ Partners** が表示されるようにすることもできます。 各サブラベルを異なる設定に構成して、それぞれの部門のユーザーにのみ表示させることができます。


Azure Information Protection のスコープ ポリシーを構成するには:

1. 新しいブラウザー ウィンドウで、セキュリティ管理者または全体管理者として [Azure Portal](https://portal.azure.com) にサインインします。

2. **[Azure Information Protection]** ブレードに移動します。たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information Protection**」と入力します。 結果から [**Azure Information Protection**] を選択します。 

    最初の **[Azure Information Protection]** ブレードで、**[新しいポリシーの追加]** を選択します。 グローバル ポリシーの更新を示すために使用される 2 番目のブレードが表示されて、新しいスコープ ポリシーを構成できます。

3. Azure Portal で管理者のみに表示されるポリシー名と説明を指定します。 この名前はテナントで一意である必要があります。 **[Specify which users/groups get this policy (このポリシーを取得するユーザー/グループの指定)]** をクリックし、その後のブレードでこのポリシーを取得するユーザーとグループを検索して選択します。 このスコープ ポリシーで構成したラベルと設定は、選択したユーザーにのみ適用されます。

4. 新しいラベルを作成したり、スコープ ポリシーの設定を構成します。 グローバル ポリシーは常に最初に適用されるため、新しいラベルでグローバル ポリシーを補い、グローバル設定を上書きすることができます。 たとえば、グローバル ポリシーに既定のラベルが何も指定されていない場合は、特定の部門の別のスコープ ポリシーで、既定のラベルを別途構成することができます。

    ラベル付けや設定の構成でヘルプが必要な場合は、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

5. グローバル ポリシーを編集するときのように、[Azure Information Protection] ブレードで変更を行ったら、**[保存]** をクリックして変更を保存します。または、**[破棄]** をクリックして、最後に保存した設定に戻します。 

6. スコープ ポリシーの変更が完了したら、最初の **[Azure Information Protection]** ブレードで、このスコープ ポリシーの適用される順序が正しいことを確認します。 これは、複数のスコープ ポリシーに対して同じユーザーを選択した場合に重要になります。 **[公開]** をクリックします。 

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時、またはエクスプローラーが開かれたときに常に変更の有無を確認します。 変更があった場合、クライアントはそのユーザーに適用されるグローバル ポリシーまたはスコープ ポリシーに変更をダウンロードします。

> [!TIP]
> スコープ ポリシーを保存したら、最初の **[Azure Information Protection]** ブレードで **[Cross Policy Editor] \(クロス ポリシー エディター)** を使用して、Azure Information Protection ポリシーのすべてのラベルを表示および再構成できます。 この方法では、複数のポリシー (グローバル ポリシーおよびすべてのスコープ ポリシー) のラベルを簡単に比較できます。 ただし、このエディターでは、ラベルの追加または順序変更や、ポリシー設定の表示または構成を行うことはできません。

## <a name="next-steps"></a>次のステップ

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、「[Azure Information Protection のクイック スタート チュートリアル](../get-started/infoprotect-quick-start-tutorial.md)」をご覧ください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
