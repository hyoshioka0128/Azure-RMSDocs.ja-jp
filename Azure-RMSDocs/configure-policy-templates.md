---
title: Azure Information Protection のテンプレートを構成して管理する - AIP
description: Azure portal から、rights management テンプレートとも呼ばれる保護テンプレートを構成および管理します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: fbb1e4792d4be7c725009a23db22ea176f374a11
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2019
ms.locfileid: "74934995"
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Azure Information Protection のテンプレートを構成して管理する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *手順: [Windows 用の Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

保護テンプレート (Rights Management テンプレート) は、Azure Information Protection 用の管理者が定義した保護設定のグループです。 これらの設定には、承認されたユーザー向けの選択した[使用権限](configure-usage-rights.md)や、有効期限やオフライン アクセス向けのアクセス制御が含まれます。 これらのテンプレートは Azure Information Protection ポリシーに統合されています。 

**分類、ラベル付け、保護を含むサブスクリプションの場合 (Azure Information Protection P1 または P2)**

- テナントのラベルと統合されていないテンプレートは、 **[Azure Information Protection ラベル]** ウィンドウのラベルの後の **[保護テンプレート]** セクションに表示されます。 このペインに移動するには、[**分類** > **ラベル**] メニューオプションを選択します。 これらのテンプレートをラベルに変換できるほか、ラベルの保護を構成するときにテンプレートに関連付けることもできます。 

**保護のみを含むサブスクリプションの場合 (Azure Rights Management サービスを含む Office 365 サブスクリプション)**

- テナントのテンプレートは、 **[Azure Information Protection ラベル]** ウィンドウの **[保護テンプレート]** セクションに表示されます。 このペインに移動するには、[**分類** > **ラベル**] メニューオプションを選択します。 ラベルは表示されません。 分類とラベル付けに固有の構成設定も表示されますが、これらの設定はテンプレートには反映されず、構成することはできません。 

>[!NOTE]
>一部のアプリケーションやサービスでは、[[転送不可]](configure-usage-rights.md#do-not-forward-option-for-emails) や [[暗号化のみ]](configure-usage-rights.md#encrypt-only-option-for-emails) (または **[暗号化]** ) がテンプレートとして表示される場合があります。 これらは編集したり削除したりできるテンプレートではなく、Exchange サービスでの既定のオプションです。

## <a name="default-templates"></a>既定のテンプレート

Azure Rights Management サービスが含まれる Azure Information Protection サブスクリプションまたは Office 365 サブスクリプションを入手すると、既定のテンプレートが 2 つテナントに自動的に作成されます。 これらのテンプレートは、組織内の許可されたユーザーにアクセスを制限します。 これらのテンプレートを作成すると、 [Azure Information Protection ドキュメントの使用権限の構成](configure-usage-rights.md#rights-included-in-the-default-templates)に関するドキュメントに記載されているアクセス許可が付与されます。

さらに、テンプレートは、7 日間オフライン アクセスを許可し、有効期限がないように構成されます。

>[!NOTE]
> これらの設定および既定のテンプレートの名前と説明は変更できます。 この機能は、Azure クラシック ポータルでは不可能であり、PowerShell ではサポートされないままです。

これらの既定のテンプレートを利用することで、組織の機密データの保護をすぐに開始できます。 これらのテンプレートは Azure Information Protection ラベルと組み合わせて利用するか、Rights Management テンプレートを利用できる[アプリケーションやサービス](applications-support.md)で単体で利用できます。

また、独自のカスタム テンプレートを作成することもできます。 必要なテンプレートはおそらく数個のみですが、最大 500 個のカスタム テンプレートを Azure に保存することができます。


### <a name="default-template-names"></a>既定のテンプレート名

サブスクリプションを最近入手した場合、既定のテンプレートは次の名前で作成されます。

- **社外秘 \ すべての従業員**

- **非常に機密性の高い社外秘 \ すべての従業員**

しばらく前にサブスクリプションを取得した場合、既定のテンプレートは次の名前で作成される可能性があります。

- **\<組織名 >-社外秘**

- **\<組織名> - 社外秘、表示のみ** 

Azure Portal を使っている場合、これらの既定テンプレートの名前を変更 (および再構成) できます。

>[!NOTE]
>**[Azure Information Protection ラベル]** ペインに既定のテンプレートが表示されない場合は、ラベルに変換されるか、ラベルにリンクされます。 テンプレートとして存在していますが、Azure Portal では、クラウド キーの保護設定を含むラベル構成の一部として表示されます。 [Aipservice PowerShell モジュール](administer-powershell.md)から[Get AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)を実行すると、いつでもテナントのテンプレートを確認できます。
>
>「[テンプレートをラベルに変更するには](#to-convert-templates-to-labels)」セクションに説明があるとおり、テンプレートは手動で変換できます。変換後、必要に応じて名前を変更します。 あるいは、既定の Azure Information Protection ポリシーが最近作成され、そのとき、テナントの Azure Rights Management サービスが有効化された場合、自動的に変換されます。

アーカイブされたテンプレートは、 **[Azure Information Protection ラベル]** ウィンドウに使用できないものとして表示されます。 そのようなテンプレートはラベルとして選択できませんが、ラベルに変換することはできます。

## <a name="considerations-for-templates-in-the-azure-portal"></a>Azure Portal のテンプレートに関する考慮事項

テンプレートを編集したり、ラベルに変換したりする前に、次の変更内容と考慮事項に注意してください。 実装変更のため、Azure クラシック ポータルで以前、テンプレートを管理していた場合、次のリストが特に重要になります。

- テンプレートを編集または変換して Azure Information Protection ポリシーを保存すると、元の[使用権限](configure-usage-rights.md)に次の変更が行われます。 必要な場合は、Azure Portal を使用して、個々の使用権限を追加または削除できます。 または、 [AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)および[Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)コマンドレットで PowerShell を使用します。
    
    - **マクロの許可** (共通名) が自動的に追加されます。 この使用権限は Office アプリの Azure Information Protection バーに必要です。

- **発行済み**および**アーカイブ**済みの設定が**有効**として表示されます: **on**と**enabled**: それぞれ**ラベル**ペインで**オフ**にします。 維持するがユーザーまたはサービスには表示しないテンプレートの場合、これらのテンプレートを **[有効]** : **[オフ]** に設定します。

- Azure ポータルでは、テンプレートをコピーまたは削除することはできません。 テンプレートがラベルに変換されると、テンプレートの使用を停止するようにラベルを構成できます。 **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** オプションに **[構成されていません]** を選択します。 あるいは、ラベルを削除できます。 ただし、いずれのシナリオでもテンプレートは削除されず、アーカイブされた状態で残ります。
    
    これで、PowerShell の[Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)コマンドレットを使用して、テンプレートを削除できます。 ラベルに変換されていないテンプレートにもこの PowerShell コマンドレットを使用できます。 ただし、それ以前に保護されていたコンテンツを意図したとおり確実に開いたり使用したりできるようにするため、通常は、テンプレートを削除しないことをお勧めします。 ベスト プラクティスとしては、運用環境で文書やメールの保護に使用されなかったことが確かな場合にのみ、テンプレートを削除してください。 念のため、 [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)コマンドレットを使用して、最初にテンプレートをバックアップとしてエクスポートすることを検討してください。 

- 現時点では、部門別テンプレートを編集して保存すると、スコープの構成が削除されます。 Azure Information Protection ポリシーのスコープ テンプレートに相当するのが、[スコープ ポリシー](configure-policy-scope.md)です。 テンプレートをラベルに変換する場合は、既存のスコープを選択できます。
    
    また、Azure Portal では部門別テンプレートのアプリケーションの互換性を設定できません。 必要に応じて、 [set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)コマンドレットと*EnableInLegacyApps*パラメーターを使用して、このアプリケーションの互換性設定を設定できます。

- テンプレートをラベルに変換またはリンクすると、多のラベルで利用できなくなります。 また、このテンプレートは **[保護テンプレート]** セクションに表示されなくなりました。 

- **[保護テンプレート]** セクションからは新しいテンプレートを作成しません。 代わりに、**保護**設定を含むラベルを作成し、 **[保護]** ウィンドウで使用権限と設定を構成します。 詳しい説明については、「[新しいテンプレートを作成するには](#to-create-a-new-template)」をご覧ください。

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーでテンプレートを構成するには

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection ラベル]** ウィンドウに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、 **[Azure Information Protection]** を選択します。

2. [**分類** > **ラベル**] メニューオプションから: **[Azure Information Protection ラベル]** ウィンドウで **[保護テンプレート]** を展開し、構成するテンプレートを見つけます。
    
3. テンプレートを選択し、 **[ラベル]** ウィンドウで、**ラベルの表示名**と**説明**を編集することによって、必要に応じてテンプレートの名前と説明を変更できます。 次に、値が**Azure (クラウドキー)** の**保護**を選択して **[保護]** ウィンドウを開きます。

4. **[保護]** ウィンドウでは、アクセス許可、コンテンツの有効期限、およびオフラインアクセスの設定を変更できます。 保護設定の構成の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。
    
    **[OK]** をクリックして変更を保存し、 **[ラベル]** ウィンドウで **[保存]** をクリックします。
    
> [!NOTE]
> 定義済みのテンプレートを使用するようにラベルを構成している場合は、 **[保護]** ウィンドウの **[テンプレートの編集]** ボタンを使用してテンプレートを編集することもできます。 選択したテンプレートを使っているラベルが他にない場合、このボタンはテンプレートをラベルに変換し、手順 5 に移動します。 テンプレートがラベルに変換される場合の処理について詳しくは、次のセクションをご覧ください。

## <a name="to-convert-templates-to-labels"></a>テンプレートをラベルに変換するには

分類、ラベル付け、保護を含むサブスクリプションの場合は、テンプレートをラベルに変換できます。 テンプレートの変換を行った場合、元のテンプレートは保持されますが、Azure Portal では新しいラベルに含まれた形で元のテンプレートが表示されます。

たとえば、マーケティング グループに使用権限を付与する**マーケティング**という名前のラベルに変換すると、Azure Portal では、**マーケティング**という名前の、同一の保護設定のラベルが表示されます。 新しく作成したこのラベルの保護設定を変更する場合は、テンプレートで変更します。このテンプレートを使用するすべてのユーザーまたはサービスには、次にテンプレートが更新されるときに、新しい保護設定が適用されます。 

すべてのテンプレートをラベルに変換する必要はありませんが、すべて変換すると、保護設定がラベルのすべての機能と完全に統合されるため、個別に設定を維持する必要がなくなります。

テンプレートをラベルに変換するには、テンプレートを右クリックして、 **[ラベルに変換]** を選択します。 または、コンテキスト メニューを使用してこのオプションを選択します。 

保護および定義済みテンプレートのラベルを構成するときに、 **[テンプレートの編集]** ボタンを使って、テンプレートをラベルに変換することもできます。 

テンプレートをラベルに変換する場合

- テンプレートの名前は新しいラベル名に変換され、テンプレートの説明はラベルのヒントに変換されます。 

- テンプレートの状態が [公開済み] の場合、ラベルではこの設定が **[有効]** : **[オン]** にマップされ、Azure Information Protection ポリシーが次に公開されるときにこのラベルがユーザーに表示されます。 テンプレートの状態が [アーカイブ済み] の場合、ラベルではこの設定が **[有効]** : **[オフ]** にマップされ、ユーザーが使用できるラベルとして表示されません。

- 保護設定は保持され、必要に応じて編集できます。また、視覚的なマーカーや条件などのラベルの他の設定を追加することもできます。

- 元のテンプレートは **[保護テンプレート]** に表示されなくなり、ラベルの保護の設定時に、事前定義済みテンプレートとして選択できません。 Azure Portal でこのテンプレートを編集するには、テンプレートの変換時に作成したラベルを編集します。 Azure Rights Management サービスではこれまで通りテンプレートを使用できるほか、[PowerShell コマンド](administer-powershell.md)を使用してテンプレートを管理できます。  

## <a name="to-create-a-new-template"></a>新しいテンプレートを作成するには

**Azure (クラウド キー)** の保護設定で新しいラベルを作成すると、この処理の裏では、Rights Management テンプレートと統合されるサービスとアプリケーションが次からアクセスできるようになる新しいカスタム テンプレートが作成されます。

1. [**分類** > **ラベル**] メニューオプションから: **[Azure Information Protection ラベル]** ウィンドウで、 **[新しいラベルの追加]** を選択します。

2. **[ラベル]** ウィンドウで、 **[有効]** : **[オン**] のままにして、テンプレート名と説明のラベル名と説明を入力します。

3. **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** では、 **[保護]** を選択してから、再び **[保護]** を選択します。
    
     ![Azure Information Protection ラベルの保護を構成する](./media/info-protect-protection-bar-configured.png)

4. **[保護]** ウィンドウでは、アクセス許可、コンテンツの有効期限、およびオフラインアクセスの設定を変更できます。 保護設定の構成の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。
    
    **[OK]** をクリックして変更を保存し、 **[ラベル]** ウィンドウで **[保存]** をクリックします。
    
    **[Azure Information Protection ラベル]** ウィンドウに新しいラベルが表示され、**保護の設定**が含まれていることが示されます。 これらの保護設定は、Azure Rights Management サービスをサポートするアプリケーションとサービスに対してテンプレートとして表示されます。
    
    ラベルは有効ですが (既定)、テンプレートはアーカイブされます。 アプリケーションとサービスでテンプレートを使用してドキュメントや電子メールを保護できるようにするには、テンプレートを発行する最後の手順を完了します。

5. **[分類]**  >  **[ポリシー]** メニュー オプションから、新しい保護設定を含むポリシーを選択します。 次に **[ラベルの追加または削除]** を選択します。 **[ポリシー: ラベルの追加または削除]** ウィンドウで、保護設定を含む新しく作成されたラベルを選択し、 **[OK]** 、 **[保存]** の順に選択します。

## <a name="next-steps"></a>次のステップ

Azure Information Protection クライアントを実行しているコンピューターが変更された設定を取得するまで、最大で 15 分間かかる場合があります。 コンピューターとサービスにテンプレートをダウンロードおよび更新する方法の詳細については、[ユーザー用とサービス用のテンプレートの更新](refresh-templates.md)に関するページをご覧ください。

テンプレートを作成し、管理するために Azure Portal でテンプレートで設定できたことはすべて、PowerShell を利用してできます。 また、PowerShell は、ポータルでは利用できないオプションも提供します。 詳細については、[保護テンプレートの PowerShell リファレンス](configure-templates-with-powershell.md)に関するページを参照してください。 

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

