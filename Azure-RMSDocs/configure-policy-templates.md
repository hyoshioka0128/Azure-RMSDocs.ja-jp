---
title: Azure Information Protection のテンプレートを構成して管理する - AIP
description: Azure portal から、rights management テンプレートとも呼ばれる保護テンプレートを構成および管理します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/24/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 797fcbbffd91882b2400fc1f5350d2782420a762
ms.sourcegitcommit: 47a6def47b8a121eb5aa8071863a765bfc31fc9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2020
ms.locfileid: "83825410"
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Azure Information Protection のテンプレートを構成して管理する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *手順: [Windows 用の Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

保護テンプレート (Rights Management テンプレート) は、Azure Information Protection 用の管理者が定義した保護設定のグループです。 これらの設定には、承認されたユーザー向けの選択した[使用権限](configure-usage-rights.md)や、有効期限やオフライン アクセス向けのアクセス制御が含まれます。 これらのテンプレートは Azure Information Protection ポリシーに統合されています。 

**分類、ラベル付け、保護を含むサブスクリプションの場合 (Azure Information Protection P1 または P2)**

- テナントのラベルと統合されていないテンプレートは、[ **Azure Information Protection ラベル**] ウィンドウのラベルの後の [**保護テンプレート**] セクションに表示されます。 このペインに移動するには、[**分類**  >  **ラベル**] メニューオプションを選択します。 これらのテンプレートをラベルに変換できるほか、ラベルの保護を構成するときにテンプレートに関連付けることもできます。 

**保護のみを含むサブスクリプションの場合 (Azure Rights Management サービスを含む Office 365 サブスクリプション)**

- テナントのテンプレートは、[ **Azure Information Protection ラベル**] ウィンドウの [**保護テンプレート**] セクションに表示されます。 このペインに移動するには、[**分類**  >  **ラベル**] メニューオプションを選択します。 ラベルは表示されません。 分類とラベル付けに固有の構成設定も表示されますが、これらの設定はテンプレートには反映されず、構成することはできません。 

>[!NOTE]
>一部のアプリケーションやサービスでは、[[転送不可]](configure-usage-rights.md#do-not-forward-option-for-emails) や [[暗号化のみ]](configure-usage-rights.md#encrypt-only-option-for-emails) (または **[暗号化]**) がテンプレートとして表示される場合があります。 これらは編集したり削除したりできるテンプレートではなく、Exchange サービスでの既定のオプションです。

## <a name="default-templates"></a>既定のテンプレート

Azure Rights Management サービスが含まれる Azure Information Protection サブスクリプションまたは Office 365 サブスクリプションを入手すると、2 つの既定のテンプレートがテナントに自動的に作成されます。 これらのテンプレートは、組織内の許可されたユーザーだけにアクセスを制限します。 これらのテンプレートを作成すると、 [Azure Information Protection ドキュメントの使用権限の構成](configure-usage-rights.md#rights-included-in-the-default-templates)に関するドキュメントに記載されているアクセス許可が付与されます。

さらに、テンプレートは、7 日間のオフライン アクセスを許可し、有効期限を設定しないように構成されます。

>[!NOTE]
> これらの設定および既定のテンプレートの名前と説明は変更できます。 この機能は、Azure クラシック ポータルでは不可能であり、PowerShell ではサポートされないままです。

これらの既定のテンプレートを利用することで、組織の機密データの保護をすぐに開始できます。 これらのテンプレートは Azure Information Protection ラベルと組み合わせて利用するか、Rights Management テンプレートを利用できる[アプリケーションやサービス](applications-support.md)で単体で利用できます。

また、独自のカスタム テンプレートを作成することもできます。 必要なテンプレートはおそらく数個のみですが、最大 500 個のカスタム テンプレートを Azure に保存することができます。


### <a name="default-template-names"></a>既定のテンプレート名

サブスクリプションを最近入手した場合、既定のテンプレートは次の名前で作成されます。

- **社外秘 \ すべての従業員**

- **非常に機密性の高い社外秘 \ すべての従業員**

しばらく前にサブスクリプションを取得した場合、既定のテンプレートは次の名前で作成される可能性があります。

- **\<組織名>-社外秘**

- **\<組織名>-社外秘、表示のみ** 

Azure Portal を使っている場合、これらの既定テンプレートの名前を変更 (および再構成) できます。

>[!NOTE]
>[ **Azure Information Protection ラベル**] ペインに既定のテンプレートが表示されない場合は、ラベルに変換されるか、ラベルにリンクされます。 テンプレートとして存在していますが、Azure Portal では、クラウド キーの保護設定を含むラベル構成の一部として表示されます。 [Aipservice PowerShell モジュール](administer-powershell.md)から[Get AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)を実行すると、いつでもテナントのテンプレートを確認できます。
>
>後の「[テンプレートをラベルに変更するには](#to-convert-templates-to-labels)」セクションで説明するように、テンプレートは手動で変換できます。変換後、必要に応じて名前を変更します。 あるいは、既定の Azure Information Protection ポリシーが最近作成され、そのときにテナントの Azure Rights Management サービスが有効にされた場合は、自動的に変換されます。

アーカイブされたテンプレートは、[ **Azure Information Protection ラベル**] ウィンドウに使用できないものとして表示されます。 そのようなテンプレートはラベルとして選択できませんが、ラベルに変換することはできます。

## <a name="considerations-for-templates-in-the-azure-portal"></a>Azure Portal のテンプレートに関する考慮事項

テンプレートを編集したり、ラベルに変換したりする前に、次の変更内容と考慮事項に注意してください。 実装が変更されたため、Azure クラシック ポータルで以前にテンプレートを管理していた場合は、次のリストが特に重要になります。

- テンプレートを編集または変換して Azure Information Protection ポリシーを保存すると、元の[使用権限](configure-usage-rights.md)に次の変更が行われます。 必要に応じて、Azure Portal を使用して個々の使用権限を追加するか削除します。 または、 [AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)および[Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)コマンドレットで PowerShell を使用します。
    
    - **マクロの許可** (共通名) が自動的に追加されます。 この使用権限は、Office アプリの Azure Information Protection バーに必要です。

- **発行済み**および**アーカイブ**済みの設定が**有効**として表示されます: **on**と**enabled**: それぞれ**ラベル**ペインで**オフ**にします。 維持するものの、ユーザーまたはサービスには表示しないテンプレートの場合は、**[有効]**: **[オフ]** に設定します。

- Azure Portal では、テンプレートをコピーまたは削除することはできません。 テンプレートがラベルに変換されると、テンプレートの使用を停止するようにラベルを構成できます。**[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** オプションで **[構成されていません]** を選択します。 または、ラベルを削除できます。 ただし、いずれのシナリオでもテンプレートは削除されず、アーカイブされた状態で残ります。
    
    これで、PowerShell の[Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)コマンドレットを使用して、テンプレートを削除できます。 ラベルに変換されていないテンプレートにも、この PowerShell コマンドレットを使用できます。 ただし、それ以前に保護されていたコンテンツを意図したとおり確実に開いたり使用したりできるようにするため、通常は、テンプレートを削除しないことをお勧めします。 ベスト プラクティスとしては、運用環境で文書やメールの保護に使用されなかったことが確かな場合にのみ、テンプレートを削除してください。 念のため、 [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)コマンドレットを使用して、最初にテンプレートをバックアップとしてエクスポートすることを検討してください。 

- 現時点では、部門別テンプレートを編集して保存すると、スコープの構成が削除されます。 Azure Information Protection ポリシーでスコープ テンプレートに相当するのが、[スコープ ポリシー](configure-policy-scope.md)です。 テンプレートをラベルに変換する場合は、既存のスコープを選択できます。
    
    また、Azure Portal では部門別テンプレートのアプリケーションの互換性を設定できません。 必要に応じて、 [set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)コマンドレットと*EnableInLegacyApps*パラメーターを使用して、このアプリケーションの互換性設定を設定できます。

- テンプレートをラベルに変換またはリンクすると、他のラベルで利用できなくなります。 また、このテンプレートは **[保護テンプレート]** セクションに表示されなくなります。 

- **[保護テンプレート]** セクションでは、新しいテンプレートを作成しません。 代わりに、**保護**設定を含むラベルを作成し、[**保護**] ウィンドウで使用権限と設定を構成します。 詳しい手順については、「[新しいテンプレートを作成するには](#to-create-a-new-template)」を参照してください。

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーでテンプレートを構成するには

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、[ **Azure Information Protection ラベル**] ウィンドウに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、[ **Azure Information Protection**] を選択します。

2. [**分類**  >  **ラベル**] メニューオプションから: [ **Azure Information Protection ラベル**] ウィンドウで [**保護テンプレート**] を展開し、構成するテンプレートを見つけます。
    
3. テンプレートを選択し、[**ラベル**] ウィンドウで、**ラベルの表示名**と**説明**を編集することによって、必要に応じてテンプレートの名前と説明を変更できます。 次に、値が**Azure (クラウドキー)** の**保護**を選択して [**保護**] ウィンドウを開きます。

4. [**保護**] ウィンドウでは、アクセス許可、コンテンツの有効期限、およびオフラインアクセスの設定を変更できます。 保護設定の構成の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」を参照してください。
    
    [ **OK** ] をクリックして変更を保存し、[**ラベル**] ウィンドウで [**保存**] をクリックします。
    
> [!NOTE]
> 定義済みのテンプレートを使用するようにラベルを構成している場合は、[**保護**] ウィンドウの [**テンプレートの編集**] ボタンを使用してテンプレートを編集することもできます。 選択したテンプレートを使っているラベルが他にない場合、このボタンはテンプレートをラベルに変換し、手順 5. に移動します。 テンプレートがラベルに変換される場合の処理の詳細については、次のセクションを参照してください。

## <a name="to-convert-templates-to-labels"></a>テンプレートをラベルに変換するには

分類、ラベル付け、保護を含むサブスクリプションの場合は、テンプレートをラベルに変換できます。 テンプレートの変換を行った場合、元のテンプレートは保持されますが、Azure Portal では新しいラベルに含まれた形で元のテンプレートが表示されます。

たとえば、マーケティング グループに使用権限を付与する**マーケティング**という名前のラベルを変換すると、Azure Portal では**マーケティング**という名前の、同一の保護設定を持つラベルとして表示されます。 新しく作成したこのラベルの保護設定を変更する場合は、テンプレートで変更します。このテンプレートを使用するすべてのユーザーまたはサービスには、次にテンプレートが更新されるときに、新しい保護設定が適用されます。 

すべてのテンプレートをラベルに変換する必要はありませんが、すべて変換すると、保護設定がラベルのすべての機能と完全に統合されるため、個別に設定を維持する必要がなくなります。

テンプレートをラベルに変換するには、テンプレートを右クリックして、**[ラベルに変換]** を選択します。 または、コンテキスト メニューを使用してこのオプションを選択します。 

ラベルの保護と定義済みテンプレートを構成するときに、**[テンプレートの編集]** ボタンを使用して、テンプレートをラベルに変換することもできます。 

テンプレートをラベルに変換すると、次のようになります。

- テンプレートの名前は新しいラベル名に変換され、テンプレートの説明はラベルのヒントに変換されます。 

- テンプレートの状態が [公開済み] の場合、ラベルではこの設定が **[有効]**: **[オン]** にマップされ、Azure Information Protection ポリシーが次に公開されるときにこのラベルがユーザーに表示されます。 テンプレートの状態が [アーカイブ済み] の場合、ラベルではこの設定が **[有効]**: **[オフ]** にマップされ、ユーザーが使用できるラベルとして表示されません。

- 保護設定は保持され、必要に応じて編集できます。また、視覚的なマーカーや条件などのラベルの他の設定を追加することもできます。

- 元のテンプレートは **[保護テンプレート]** に表示されなくなり、ラベルの保護の構成時に、事前定義済みテンプレートとして選択できません。 Azure Portal でこのテンプレートを編集するには、テンプレートの変換時に作成したラベルを編集します。 Azure Rights Management サービスではこれまでどおりにテンプレートを使用できるほか、[PowerShell コマンド](administer-powershell.md)を使用してテンプレートを管理できます。  

## <a name="to-create-a-new-template"></a>新しいテンプレートを作成するには

テンプレートは、ポータルまたは PowerShell を使用して作成できます。 

### <a name="template-creation-using-powershell"></a>PowerShell を使用したテンプレートの作成

指定された名前、説明、ポリシー、および必要な状態の設定で PowerShell を使用して新しい保護テンプレートを作成するには、 [Add-AipServiceTemplate](https://docs.microsoft.com/powershell/module/aipservice/add-aipservicetemplate?view=azureipps)コマンドレットを使用します。 


### <a name="template-creation-using-the-portal"></a>ポータルを使用したテンプレートの作成

**Azure (クラウドキー)** の保護設定でポータルを使用して新しいラベルを作成すると、この操作によって新しいカスタムテンプレートが作成され、Rights Management テンプレートと統合されるサービスとアプリケーションからアクセスできるようになります。

1. [**分類**  >  **ラベル**] メニューオプションから: [ **Azure Information Protection ラベル**] ウィンドウで、[**新しいラベルの追加**] を選択します。

2. [**ラベル**] ウィンドウで、[**有効**]: **[オン**] のままにして、テンプレート名と説明のラベル名と説明を入力します。

3. **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** では、**[保護]** を選択してから、再び **[保護]** を選択します。
    
     ![Azure Information Protection ラベルの保護を構成する](./media/info-protect-protection-bar-configured.png)

4. [**保護**] ウィンドウでは、アクセス許可、コンテンツの有効期限、およびオフラインアクセスの設定を変更できます。 これらの保護設定の構成の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」を参照してください。
    
    [ **OK** ] をクリックして変更を保存し、[**ラベル**] ウィンドウで [**保存**] をクリックします。
    
    [ **Azure Information Protection ラベル**] ウィンドウに新しいラベルが表示され、**保護の設定**が含まれていることが示されます。 これらの保護設定は、Azure Rights Management サービスをサポートするアプリケーションとサービスに対してテンプレートとして表示されます。
    
    ラベルは有効ですが (既定)、テンプレートはアーカイブされます。 アプリケーションとサービスでテンプレートを使用してドキュメントや電子メールを保護できるようにするには、テンプレートを発行する最後の手順を完了します。

5. [**分類**  >  **ポリシー** ] メニューオプションから、新しい保護設定を含めるポリシーを選択します。 次に **[ラベルの追加または削除]** を選択します。 [**ポリシー: ラベルの追加または削除**] ウィンドウで、保護設定を含む新しく作成されたラベルを選択し、[ **OK**]、[**保存**] の順に選択します。

## <a name="next-steps"></a>次のステップ

Azure Information Protection クライアントを実行しているコンピューターが変更された設定を取得するまで、最大で 15 分間かかる場合があります。 コンピューターおよびサービスでテンプレートをダウンロードして更新する方法については、「[ユーザーとサービスのためのテンプレートの更新](refresh-templates.md)」を参照してください。

テンプレートの作成と管理のために Azure Portal で構成できたことはすべて、PowerShell を利用して行うことができます。 また、PowerShell は、ポータルでは利用できないオプションも提供します。 詳細については、[保護テンプレートの PowerShell リファレンス](configure-templates-with-powershell.md)を参照してください。 

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

