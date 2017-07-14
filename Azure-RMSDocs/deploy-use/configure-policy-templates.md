---
title: "Azure Information Protection ポリシーでテンプレートを構成して管理する"
description: "現在はプレビュー段階ですが、Azure Information Protection ポリシーで Rights Management テンプレートを構成および管理できるようになりました。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 1f41aad2d132e087e9122b2683be4b45185527de
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# Azure Information Protection ポリシーでテンプレートを構成して管理する
<a id="configuring-and-managing-templates-in-the-azure-information-protection-policy" class="xliff"></a>

>*適用対象: Azure Information Protection*

>[!NOTE]
>この機能は現在プレビュー段階にあり、頻繁に変更される可能性があります。
>
>Azure クラシック ポータルで作成したカスタム テンプレートを使用してこのプレビュー機能を試す前に、テンプレートの最新のバックアップがあることを確認してください。 PowerShell の [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate) コマンドレットを使用してカスタム テンプレートをバックアップできます。また必要に応じて、[Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate) を使用してテンプレートを復元できます。
>
>実装において違いがあるため、Azure クラシック ポータルと Azure Portal で同じテンプレートを管理することはお勧めしません。


Rights Management テンプレートは Azure Information Protection ポリシーに統合されました。 

**分類、ラベル付け、保護を含むサブスクリプションの場合 (Azure Information Protection P1 または P2)**

- テナントの Rights Management テンプレートは、ラベルの後の新しい **[テンプレート]** セクションに表示されます。 これらのテンプレートをラベルに変換できるほか、個別のテンプレートとして引き続き管理し、ラベルの保護を構成するときにテンプレートに関連付けることもできます。 

**保護のみを含むサブスクリプションの場合 (Azure Rights Management サービスを含む Office 365 サブスクリプション)**

- テナントの Rights Management テンプレートはラベルとして表示されます。また現時点では、分類とラベル付けに固有の構成設定を使用できます。 


## Azure Portal のテンプレートに関する考慮事項
<a id="considerations-for-templates-in-the-azure-portal" class="xliff"></a>

これらのテンプレートを編集したり Azure Portal でラベルに変換したりする前に、Azure クラシック ポータルのテンプレート管理からの、実装における次の変更点に注意してください。 一部の制限についてはプレビュー期間中に解消される見込みです。

- テンプレートを編集または変換して Azure Information Protection ポリシーを保存すると、元の[使用権限](configure-usage-rights.md)に次の変更が行われます。 必要に応じて PowerShell の [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) と [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition) コマンドレットを使用して、個々の使用権限を追加または削除できます。
    
    - **名前を付けて保存、エクスポート** (共通名) は削除されます。 Azure Portal ではこの使用権限を手動で指定できませんが、[フル コントロール] の使用権限に含まれるため、必要に応じて追加できます。
    
    - **マクロの許可** (共通名) が自動的に追加されます。 この使用権限は Office アプリの Azure Information Protection バーに必要です。
    
- 現時点では既定のテンプレートが表示されますが、編集または変換することはできません。 

- テンプレートをコピーまたは削除することはできません。 テンプレートを削除するには、PowerShell の [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) コマンドレットを使用します。 

- 現時点で、Azure クラシック ポータルまたは PowerShell を使用して言語の構成が行われたテンプレートでは、これらの言語で名前と説明は表示されませんが、設定は保持されます。

- **[ラベル]** ブレードで、**[公開済み]** の設定は **[有効]** が **[オン]**、**[アーカイブ済み]** の設定は **[有効]** が **[オフ]** と表示されます。

- 部門別テンプレート (スコープが構成されたテンプレート) はグローバル ポリシーに表示されます。 現時点では、部門別テンプレートを編集して保存すると、スコープの構成が削除されます。 Azure Information Protection ポリシーのスコープ テンプレートに相当するのが、[スコープ ポリシー](configure-policy-scope.md)です。 テンプレートをラベルに変換する場合は、既存のスコープを選択できます。
    
    また現時点では、部門別テンプレートのアプリケーションの互換性を設定できません。 必要な場合は、PowerShell の [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) コマンドレッドを使用して設定できます。

- **テンプレート** コンテナーでは新しいテンプレートを作成しません。代わりに、**[保護]** を設定したラベルを作成し、**[保護]** ブレードで使用権限と設定を構成します。 詳しい説明については、「[新しいテンプレートを作成するには](#to-create-a-new-template)」をご覧ください。

## Azure Information Protection ポリシーでテンプレートを構成するには
<a id="to-configure-the-templates-in-the-azure-information-protection-policy" class="xliff"></a>

1. 新しいブラウザー ウィンドウで、セキュリティ管理者または全体管理者として [Azure Portal](https://portal.azure.com) にサインインします。

2. **[Azure Information Protection]** ブレードに移動します。たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information Protection**」と入力します。 結果から [**Azure Information Protection**] を選択します。 

2. 構成するテンプレートがすべてのユーザーに適用される場合は、**[Azure Information Protection]** ブレードから **[グローバル]** を選択します。 ただし、構成するテンプレートが[スコープ ポリシー](configure-policy-scope.md)内にあり、選択したユーザーだけに適用される場合は、代わりにそのスコープ ポリシーを選択します。

3. [ポリシー] ブレードで、構成するテンプレートを見つけます。
    
    - 分類、ラベル付け、保護を含むサブスクリプションの場合は、ラベルの後に**テンプレート**を展開します。
    
    - 保護のみを含むサブスクリプションの場合、テンプレートはラベルとして表示されます。

4. テンプレートを選択し、**[ラベル]** ブレードで **[ラベル名]** と **[説明]** を編集することにより、必要に応じてテンプレートの名前と説明を変更できます。 次に、値が **Azure RMS** の **[保護]** を選択して **[保護]** ブレードを開きます。

5. **[保護]** ブレードでは、アクセス許可、コンテンツの期限、オフライン アクセスの設定を変更できます。 保護設定の構成の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。
    
    変更を保存するには **[OK]** をクリックし、**[ラベル]** ブレードで **[保存]** をクリックします。

6. ユーザーのアプリケーションとサービスで変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## テンプレートをラベルに変換するには
<a id="to-convert-templates-to-labels" class="xliff"></a>

分類、ラベル付け、保護を含むサブスクリプションの場合は、テンプレートをラベルに変換できます。 これを行った場合、元のテンプレートは保持されますが、Azure Portal では新しいラベルに含まれた形で元のテンプレートが表示されます。

たとえば、マーケティング グループに使用権限を付与する**マーケティング**という名前のラベルに変換すると、Azure Portal では、**マーケティング**という名前の、同一の保護設定のラベルが表示されます。 新しく作成したこのラベルの保護設定を変更する場合は、テンプレートで変更します。このテンプレートを使用するすべてのユーザーまたはサービスには、次にテンプレートが更新されるときに、新しい保護設定が適用されます。 

すべてのテンプレートをラベルに変換する必要はありませんが、すべて変換すると、保護設定がラベルのすべての機能と完全に統合されるため、個別に設定を維持する必要がなくなります。

テンプレートをラベルに変換するには、テンプレートを右クリックして、**[ラベルに変換]** を選択します。 または、コンテキスト メニューを使用してこのオプションを選択します。

テンプレートをラベルに変換する場合

- テンプレートの名前は新しいラベル名に変換され、テンプレートの説明はラベルのヒントに変換されます。 

- テンプレートの状態が [公開済み] の場合、ラベルではこの設定が **[有効]**: **[オン]** にマップされ、Azure Information Protection ポリシーが次に公開されるときにこのラベルがユーザーに表示されます。 テンプレートの状態が [アーカイブ済み] の場合、ラベルではこの設定が **[有効]**: **[オフ]** にマップされ、ユーザーが使用できるラベルとして表示されません。

- 保護設定は保持され、必要に応じて編集できます。また、視覚的なマーカーや条件などのラベルの他の設定を追加することもできます。

- 元のテンプレートは **[テンプレート]** に表示されなくなるため、Azure Portal で元のテンプレートを編集するには、作成したラベルを編集します。 Azure Rights Management サービスではこれまで通りテンプレートを使用できるほか、[PowerShell コマンド](administer-powershell.md)を使用してテンプレートを管理できます。  

## 新しいテンプレートを作成するには
<a id="to-create-a-new-template" class="xliff"></a>

**Azure RMS** の保護設定で新しいラベルを作成すると、その処理の裏では、Rights Management テンプレートと統合されるサービスとアプリケーションが次からアクセスできるようになる新しいカスタム テンプレートが作成されます。

1. 作成する新しいテンプレートがすべてのユーザーに適用される場合は、**[Policy: Global]\(ポリシー: グローバル\)** ブレードで **[新しいラベルの追加]** をクリックします。
    
     作成する新しいテンプレートが部門別テンプレートであり、選択されたユーザーだけに適用される場合は、まず、最初の **[Azure Information Protection]** ブレードでスコープ ポリシーを選択または作成します。

2. **[ラベル]** ブレードで、既定の **[有効]**: **[オン]** を変更せずにこの新しいテンプレートを公開するか、この設定を **[オフ]** に変更してテンプレートをアーカイブ済みとして作成します。 次に [テンプレート名] と [説明] に、ラベルの名前と説明を入力します。

3. **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** では、**[保護]** を選択してから、再び **[保護]** を選択します。
    
     ![Azure Information Protection ラベルの保護を構成する](../media/info-protect-protection-bar.png)

4. **[保護]** ブレードでは、アクセス許可、コンテンツの期限、オフライン アクセスの設定を変更できます。 保護設定の構成の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。
    
    変更を保存するには **[OK]** をクリックし、**[ラベル]** ブレードで **[保存]** をクリックします。

5. これらのテンプレートをユーザーのアプリケーションとサービスで使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。


## 次のステップ
<a id="next-steps" class="xliff"></a>

Azure Information Protection ポリシーに対するすべての変更と同様に、Azure Information Protection クライアントを実行するコンピューターでこれらのテンプレートのダウンロードを完了するには、最大 15 分かかります。 コンピューターとサービスにテンプレートをダウンロードおよび更新する方法の詳細については、[ユーザー用とサービス用のテンプレートの更新](refresh-templates.md)に関するページをご覧ください。

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
