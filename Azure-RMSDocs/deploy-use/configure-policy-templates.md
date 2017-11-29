---
title: "Azure Information Protection のテンプレートを構成して管理する"
description: "Azure Portal から Rights Management テンプレートを構成して管理します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/17/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 74f3f9e22e5607c8b85b752bcd3881d5b7a092b1
ms.sourcegitcommit: 0ef66a8479b4105c00bf1b1df46d2ddf044b7670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2017
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Azure Information Protection のテンプレートを構成して管理する

>*適用対象: Azure Information Protection*

>[!NOTE]
>これは、Azure クラシック ポータルのカスタム テンプレート構成の後継にあたる機能です。 マッピングの概要は「[Azure クラシック ポータルで行っていたタスク](migrate-portal.md)」でご覧いただけます。
>
>Azure クラシック ポータルでも引き続きテンプレートを作成し、管理できますが、Azure クラシック ポータルと Azure Portal から同じテンプレートを管理する行為は推奨されません。 テンプレートの構成方法はポータルによって異なります。異なるポータルで同じテンプレートを構成すると、構成の信頼性が失われる可能性があります。


Rights Management テンプレートは Azure Information Protection ポリシーに統合されました。 

**分類、ラベル付け、保護を含むサブスクリプションの場合 (Azure Information Protection P1 または P2)**

- テナントのラベルと統合されない Rights Management テンプレートは、**[Azure Information Protection - グローバル ポリシー]** ブレードで、ラベルの後の **[保護テンプレート]** セクションに表示されます。 これらのテンプレートをラベルに変換できるほか、ラベルの保護を構成するときにテンプレートに関連付けることもできます。 

**保護のみを含むサブスクリプションの場合 (Azure Rights Management サービスを含む Office 365 サブスクリプション)**

- テナントの Rights Management テンプレートは、**[Azure Information Protection - グローバル ポリシー]** ブレードの **[保護テンプレート]** セクションに表示されます。 ラベルは表示されません。 分類とラベル付けに固有の構成設定も表示されますが、テンプレートには反映されず、構成することはできません。 

## <a name="default-templates"></a>既定のテンプレート

Azure Rights Management サービスが含まれる Azure Information Protection サブスクリプションまたは Office 365 サブスクリプションを入手すると、組織内で権限を与えられたユーザーにアクセスを制限する既定のテンプレートが 2 つテナントに自動的に作成されます。 この 2 つのテンプレートは、作成されると、ドキュメント「[Azure Rights Management の使用権限を構成する](configure-usage-rights.md#rights-included-in-the-default-templates)」に一覧表示されているアクセス許可を使用します。

さらに、テンプレートは、7 日間オフライン アクセスを許可し、有効期限がないように構成されます。

>[!NOTE]
> これらの設定および既定のテンプレートの名前と説明は変更できます。 この機能は、Azure クラシック ポータルでは不可能であり、PowerShell ではサポートされないままです。

これらの既定のテンプレートを利用することで、組織の機密データの保護をすぐに開始できます。 これらのテンプレートは Azure Information Protection ラベルと組み合わせて利用するか、Rights Management テンプレートを利用できる[アプリケーションやサービス](../understand-explore/applications-support.md)で単体で利用できます。

また、独自のカスタム テンプレートを作成することもできます。 必要なテンプレートはおそらく数個のみですが、最大 500 個のカスタム テンプレートを Azure に保存することができます。

### <a name="default-template-names"></a>既定のテンプレート名

Azure Information Protection のサブスクリプションを最近入手した場合、既定のテンプレートは次の名前で作成されます。

- **社外秘 \ すべての従業員**: 保護されたコンテンツの読み取りアクセス許可または変更アクセス許可を付与します。

- **非常に機密性の高い社外秘 \ すべての従業員**: 保護されたコンテンツの読み取り専用アクセス許可を付与します。

Azure Information Protection サブスクリプションを入手してからしばらく経過している場合、あるいは Azure Information Protection サブスクリプションを持っていないが、Azure Rights Management が含まれる Office 365 サブスクリプションを持っている場合、既定のテンプレートは次の名前で作成されます。

- **\<組織の名前> - 社外秘**: 保護されたコンテンツの読み取りアクセス許可または変更アクセス許可を付与します。

- **\<組織の名前> - 社外秘、表示のみ**: 保護されたコンテンツの読み取り専用アクセス許可を付与します。 

Azure Portal を使っている場合、これらの既定テンプレートの名前を変更 (および再構成) できます。

>[!NOTE]
>**[Azure Information Protection - グローバル ポリシー]** ブレードに既定のテンプレートが表示されない場合、ラベルに変換されるか、ラベルにリンクされています。 テンプレートとして存在していますが、Azure ポータルでは、Azure RMS 保護を含むラベル構成の一部として表示されます。 テナントに設定されているテンプレートはいつでも確認できます。[AADRM PowerShell モジュール](administer-powershell.md)から [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) を実行してください。
>
>「[テンプレートをラベルに変更するには](#to-convert-templates-to-labels)」セクションに説明があるとおり、テンプレートは手動で変換できます。変換後、必要に応じて名前を変更します。 あるいは、既定の Azure Information Protection ポリシーが最近作成され、そのとき、テナントの Azure Rights Management サービスが有効化された場合、自動的に変換されます。

アーカイブ済みのテンプレートは **[Azure Information Protection - グローバル ポリシー]** ブレードに利用不可として表示されます。 そのようなテンプレートはラベルとして選択できませんが、ラベルに変換することはできます。

## <a name="considerations-for-templates-in-the-azure-portal"></a>Azure Portal のテンプレートに関する考慮事項

テンプレートを編集したり、ラベルに変換したりする前に、次の変更内容と考慮事項に注意してください。 実装変更のため、Azure クラシック ポータルで以前、テンプレートを管理していた場合、次のリストが特に重要になります。

- テンプレートを編集または変換して Azure Information Protection ポリシーを保存すると、元の[使用権限](configure-usage-rights.md)に次の変更が行われます。 必要に応じて PowerShell の [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) と [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition) コマンドレットを使用して、個々の使用権限を追加または削除できます。
    
    - **名前を付けて保存、エクスポート** (共通名) は削除されます。 Azure Portal ではこの使用権限を手動で指定できませんが、[フル コントロール] の使用権限に含まれるため、必要に応じて追加できます。
    
    - **マクロの許可** (共通名) が自動的に追加されます。 この使用権限は Office アプリの Azure Information Protection バーに必要です。
    

- **[ラベル]** ブレードで、**[公開済み]** の設定は **[有効]** が **[オン]**、**[アーカイブ済み]** の設定は **[有効]** が **[オフ]** と表示されます。 維持するがユーザーには表示しないテンプレートの場合、**[有効]**: **[オフ]** に設定します。

- Azure ポータルでは、テンプレートをコピーまたは削除することはできません。 テンプレートがラベルに変換されると、テンプレートの使用を停止するようにラベルを構成できます。**[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** オプションに **[構成されていません]** を選択します。 あるいは、ラベルを削除できます。 ただし、いずれのシナリオでもテンプレートは削除されず、アーカイブされた状態で残ります。
    
    これで PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) コマンドレットを利用し、テンプレートを削除できます。 ラベルに変換されていないテンプレートにもこの PowerShell コマンドレットを使用できます。 ただし、コンテンツの保護に利用されていたテンプレートを削除すると、そのコンテンツを開けなくなります。 運用環境で文書やメールの保護に使用されなかったことが確かな場合にのみ、テンプレートを削除してください。 念のために、[Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate) コマンドレットを利用し、テンプレートをバックアップとしてエクスポートしておくことが推奨されます。 

- 部門別テンプレート (スコープが構成されたテンプレート) はグローバル ポリシーに表示されます。 現時点では、部門別テンプレートを編集して保存すると、スコープの構成が削除されます。 Azure Information Protection ポリシーのスコープ テンプレートに相当するのが、[スコープ ポリシー](configure-policy-scope.md)です。 テンプレートをラベルに変換する場合は、既存のスコープを選択できます。
    
    また現時点では、部門別テンプレートのアプリケーションの互換性を設定できません。 必要な場合は、PowerShell と [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) コマンドレッドを使用して、アプリケーションの互換性設定を設定することができます。

- テンプレートをラベルに変換またはリンクすると、多のラベルで利用できなくなります。 また、このテンプレートは **[保護テンプレート]** セクションに表示されなくなりました。 

- **[保護テンプレート]** セクションからは新しいテンプレートを作成しません。 代わりに、**[保護]** を設定したラベルを作成し、**[保護]** ブレードで使用権限と設定を構成します。 詳しい説明については、「[新しいテンプレートを作成するには](#to-create-a-new-template)」をご覧ください。

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーでテンプレートを構成するには

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザー ウィンドウを開き、セキュリティ管理者または全体管理者としてサインインします。次に、**[Azure Information Protection]** ブレードに移動します。     
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 構成するテンプレートがすべてのユーザーに対するものである場合は、**[Azure Information Protection - グローバル ポリシー]** ブレードのままにします。
    
    構成するテンプレートが[スコープ付きポリシー](configure-policy-scope.md)内にあり、選択したユーザーだけに適用される場合は、**[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードからスコープ付きポリシーを選びます。

3. **[Azure Information Protection - グローバル ポリシー]** ブレードまたは **[ポリシー: \<名前>]** ブレードで、構成するテンプレートを探します。
    
    - 分類、ラベル付け、保護を含むサブスクリプションの場合は、ラベルの後に**保護テンプレート**を展開します。
    
    - 保護のみを含むサブスクリプションの場合、テンプレートはラベルとして表示されます。

4. テンプレートを選択し、**[ラベル]** ブレードで **[ラベル名]** と **[説明]** を編集することにより、必要に応じてテンプレートの名前と説明を変更できます。 次に、値が **Azure (クラウド キー)** になっている **[保護]** を選択して **[保護]** ブレードを開きます。

5. **[保護]** ブレードでは、アクセス許可、コンテンツの期限、オフライン アクセスの設定を変更できます。 保護設定の構成の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。
    
    変更を保存するには **[OK]** をクリックし、**[ラベル]** ブレードで **[保存]** をクリックします。

6. ユーザーのアプリケーションとサービスで変更を使用できるようにするには、最初の **[Azure Information Protection]** ブレードで **[公開]** をクリックします。

> [!NOTE]
> 定義済みのテンプレートを使うためのラベルを構成した場合は、**[保護]** ブレードの **[テンプレートの編集]** ボタンを使ってテンプレートを編集することもできます。 選択したテンプレートを使っているラベルが他にない場合、このボタンはテンプレートをラベルに変換し、手順 5 に移動します。 テンプレートがラベルに変換される場合の処理について詳しくは、次のセクションをご覧ください。

## <a name="to-convert-templates-to-labels"></a>テンプレートをラベルに変換するには

分類、ラベル付け、保護を含むサブスクリプションの場合は、テンプレートをラベルに変換できます。 これを行った場合、元のテンプレートは保持されますが、Azure Portal では新しいラベルに含まれた形で元のテンプレートが表示されます。

たとえば、マーケティング グループに使用権限を付与する**マーケティング**という名前のラベルに変換すると、Azure Portal では、**マーケティング**という名前の、同一の保護設定のラベルが表示されます。 新しく作成したこのラベルの保護設定を変更する場合は、テンプレートで変更します。このテンプレートを使用するすべてのユーザーまたはサービスには、次にテンプレートが更新されるときに、新しい保護設定が適用されます。 

すべてのテンプレートをラベルに変換する必要はありませんが、すべて変換すると、保護設定がラベルのすべての機能と完全に統合されるため、個別に設定を維持する必要がなくなります。

テンプレートをラベルに変換するには、テンプレートを右クリックして、**[ラベルに変換]** を選択します。 または、コンテキスト メニューを使用してこのオプションを選択します。 

保護および定義済みテンプレートのラベルを構成するときに、**[テンプレートの編集]** ボタンを使って、テンプレートをラベルに変換することもできます。 

テンプレートをラベルに変換する場合

- テンプレートの名前は新しいラベル名に変換され、テンプレートの説明はラベルのヒントに変換されます。 

- テンプレートの状態が [公開済み] の場合、ラベルではこの設定が **[有効]**: **[オン]** にマップされ、Azure Information Protection ポリシーが次に公開されるときにこのラベルがユーザーに表示されます。 テンプレートの状態が [アーカイブ済み] の場合、ラベルではこの設定が **[有効]**: **[オフ]** にマップされ、ユーザーが使用できるラベルとして表示されません。

- 保護設定は保持され、必要に応じて編集できます。また、視覚的なマーカーや条件などのラベルの他の設定を追加することもできます。

- 元のテンプレートは **[保護テンプレート]** に表示されなくなり、ラベルの保護の設定時に、事前定義済みテンプレートとして選択できません。 Azure Portal でこのテンプレートを編集するには、テンプレートの変換時に作成したラベルを編集します。 Azure Rights Management サービスではこれまで通りテンプレートを使用できるほか、[PowerShell コマンド](administer-powershell.md)を使用してテンプレートを管理できます。  

## <a name="to-create-a-new-template"></a>新しいテンプレートを作成するには

**Azure RMS** または **Azure (クラウド キー)** の保護設定で新しいラベルを作成すると、その処理の裏では、Rights Management テンプレートと統合されるサービスとアプリケーションが次からアクセスできるようになる新しいカスタム テンプレートが作成されます。

1. 新しいテンプレートがすべてのユーザーに対するものである場合は、**[Azure Information Protection - グローバル ポリシー]** ブレードのままにします。
    
     新しいテンプレートが部門テンプレートであり、選択したユーザーだけに適用される場合は、**[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードから[スコープ付きポリシー](configure-policy-scope.md)を作成または選択します。

2. **[Azure Information Protection - グローバル ポリシー]** ブレードまたは **[ポリシー: \<名前>]** ブレードで、**[新しいラベルの追加]** をクリックします。

3. **[ラベル]** ブレードで、既定の **[有効]**: **[オン]** を変更せずにこの新しいテンプレートを公開するか、この設定を **[オフ]** に変更してテンプレートをアーカイブ済みとして作成します。 次に [テンプレート名] と [説明] に、ラベルの名前と説明を入力します。

4. **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** では、**[保護]** を選択してから、再び **[保護]** を選択します。
    
     ![Azure Information Protection ラベルの保護を構成する](../media/info-protect-protection-bar-configured.png)

5. **[保護]** ブレードでは、アクセス許可、コンテンツの期限、オフライン アクセスの設定を変更できます。 保護設定の構成の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。
    
    変更を保存するには **[OK]** をクリックし、**[ラベル]** ブレードで **[保存]** をクリックします。

6. これらのテンプレートをユーザーのアプリケーションとサービスで使用できるようにするには、最初の **[Azure Information Protection]** ブレードで **[公開]** をクリックします。


## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーに対するすべての変更と同様に、Azure Information Protection クライアントを実行するコンピューターでこれらのテンプレートのダウンロードを完了するには、最大 15 分かかります。 コンピューターとサービスにテンプレートをダウンロードおよび更新する方法の詳細については、[ユーザー用とサービス用のテンプレートの更新](refresh-templates.md)に関するページをご覧ください。

テンプレートを作成し、管理するために Azure Portal でテンプレートで設定できたことはすべて、PowerShell を利用してできます。 また、PowerShell は、ポータルでは利用できないオプションも提供します。 詳細については、[保護テンプレートの PowerShell リファレンス](configure-templates-with-powershell.md)に関するページを参照してください。 

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
