---
title: "Azure Information Protection ラベルを保護するように構成する"
description: "Rights Management 保護を使用するようにラベルを構成すると、最も機密性の高いドキュメントや電子メールを保護できます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: cd0fa432bbec97b39e7c32f0b40594840d57fb04
ms.lasthandoff: 02/24/2017


---

# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Rights Management による保護でラベルを構成する方法

>*適用対象: Azure Information Protection*

暗号化ポリシー、ID ポリシー、および承認ポリシーによってデータ損失を防止する Rights Management サービスを使用することで、最も機密性の高いドキュメントや電子メールを保護することができます。 この保護は、ドキュメントおよび電子メールの Rights Management テンプレートを使用するようにラベルを構成した場合、または Outlook の電子メール メッセージの **[転送不可]** オプションに適用されます。 

テンプレートは、Azure Rights Management をアクティブ化したときに自動的に作成される既定のいずれかのテンプレート、またはカスタム テンプレートのどちらも使用できます。 Azure Rights Management の部門別テンプレートはサポートされていますが、保護は、ドキュメントまたは電子メールの作成者がテンプレートの構成範囲内にある場合にのみ適用されます。 ユーザーがその範囲外である場合は、Azure Information Protection でラベルを適用できないことを示すメッセージが表示されます。

## <a name="how-the-protection-works"></a>保護のしくみ

Rights Management によって保護されるドキュメントまたは電子メールは、保存時および送信時に暗号化され、権限のあるユーザーのみが暗号化を解除できます。 この暗号化は、ドキュメントまたは電子メールの名前が変更された場合でも維持されます。 さらに、次の例のように、使用権限と制限を構成できます。

- 組織内のユーザーのみが社外秘のドキュメントまたは電子メールを開くことができます。

- マーケティング部門のユーザーのみが宣伝の通知ドキュメントまたは電子メールの編集と印刷を実行でき、組織内の他のすべてのユーザーはそれらの閲覧のみを実行できます。

- ユーザーは、社内の再編成に関するニュースを含む電子メールを転送できません。

- ビジネス パートナーに送信される現在の価格表は、指定日以降は開くことができません。

Azure Rights Management テンプレートおよびこれらの使用権限と制限を構成する方法の詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

Azure Rights Management とそのしくみの詳細については、[Azure Rights Management の概要に関するページ](../understand-explore/what-is-azure-rms.md)を参照してください。

> [!IMPORTANT]
> Azure Rights Management による保護を適用するようにラベルを構成するには、組織に対して Azure Rights Management サービスをアクティブにする必要があります。 この手順をまだ行っていない場合は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

ユーザーが電子メールを保護するラベルを Outlook で適用するために、Information Rights Management (IRM) 用に Exchange を構成する必要はありません。 ただし、Exchange が IRM 用に構成されるまで、Exchange で Azure Rights Management による保護を使用するすべての機能を利用できません。 たとえば、ユーザーは保護された電子メールを携帯電話や Outlook Web Access で表示できなくなります。また、保護された電子メールには検索のインデックスを作成できません。権限管理の保護のために Exchange Online DLP も構成できなくなります。 このような追加のシナリオをサポートするように Exchange を構成するには、以下のリソースを参照してください。

- Exchange Online の場合: 「[Exchange Online: IRM 構成](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」の手順を参照してください。

- オンプレミスの Exchange の場合: [RMS コネクタを展開し、Exchange サーバーを構成する](../deploy-use/deploy-rms-connector.md)必要があります。 


## <a name="to-configure-a-label-for-rights-management-protection"></a>Rights Management による保護にラベルを構成するには

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は新しいブラウザーのウィンドウを開き、全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 

    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 構成するラベルがすべてのユーザーに適用される場合は、**[Azure Information Protection]** ブレードから **[Global]** (全体) を選択します。 ただし、構成するラベルが[スコープ ポリシー](configure-policy-scope.md)内にあり、選択したユーザーだけに適用される場合は、代わりにそのスコープ ポリシーを選択します。

3. **[ポリシー]** ブレードで、構成するラベルを選択すると、**[ラベル]** ブレードが開きます。 

4. **[ラベル]** ブレードで、**[Set permissions for documents and emails containing this label]** (このラベルを含むドキュメントと電子メールにアクセス許可を設定する) を見つけ、下記オプションから&1; つ選択します。
    
    - **[未構成]**: 現在、ラベルが保護を適用するように構成されており、選択したラベルにこれ以上保護を適用しない場合は、このオプションを選択します。 次に手順 10 に進みます。
    
    - **[保護]**: 保護を適用するには、このオプションを選択し、手順 5. に進みます。
    
    - **[保護の削除]**: ドキュメントまたは電子メールに構成されている保護を削除するには、このオプションを選択します。 次に手順 10 に進みます。
        
        このオプションを持つラベルを適用するには、ユーザーは Rights Management による保護を削除する権限を持っている必要があるので、注意してください。 このオプションを使用するには、ユーザーは **[エクスポート]** または **[フル コントロール]** [usage right (使用権限)](../deploy-use/configure-usage-rights.md)を持っている、Rights Management の所有者 (自動的にフル コントロール使用権限が付与されています) である、または [super user for Azure Rights Management (Azure Rights Management のスーパー ユーザー)](../deploy-use/configure-super-users.md) である必要があります。 既定の Azure Rights Management テンプレートには、ユーザーに保護を削除させる使用権限は含まれません。 
        
        ユーザーが Rights Management による保護を削除する権限を持たずに **[保護の削除]** オプションを持つラベルを選択する場合、次のメッセージが表示されます: **Azure Information Protection ではこのラベルを適用できません。この問題が引き続き発生する場合は、管理者に問い合わせてください。**

5. **[保護]** を選択した場合、**[保護]** を選択して **[アクセス許可]** ブレードを開きます。
    
    ![Azure Information Protection ラベルの保護を構成する](../media/info-protect-protection-bar.png)

6. **[アクセス許可]** ブレードで、**[Azure RMS]** または **[HYOK (AD RMS)]** を選択します。 
    
    ほとんどの場合、アクセス許可の設定には **[Azure RMS]** を選択します。 この "*Hold Your Own Key*" (HYOK) 構成に付随する前提条件と制限事項を読み、理解するまでは **[HYOK (AD RMS)]** を選択しないでください。 詳細については、「[AD RMS 保護の Hold Your Own Key (HYOK) の要件と制限事項](configure-adrms-restrictions.md)」を参照してください。 HYOK (AD RMS) の構成を続行するには、手順 9 に進みます。
    
7. 電子メールにこの Outlook オプションを設定する場合は **[転送しない]** を、または **[テンプレートの選択]** のどちらかを選択してください。 
    
8. **[Azure RMS]** で **[テンプレートの選択]** を選択した場合、ドロップ ダウン ボックスをクリックし、このラベルでドキュメントと電子メールを保護するために使用する[テンプレート](../deploy-use/configure-custom-templates.md)を選択します。
    
    **[部門別テンプレート]**を選択する場合、または[オンボーディング コントロール](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成済みの場合:
    
    - 構成されたテンプレート範囲の外にいるユーザー、または Azure Rights Management 保護の適用から除外されているユーザーは、引き続きラベルを確認できますが、適用することはできません。 それらのユーザーがラベルを選択した場合、次のメッセージが表示されます: **Azure Information Protection はこのラベルを適用できません。この問題が引き続き発生する場合は、管理者に問い合わせてください。**
    
        スコープ ポリシーを構成する場合でも、すべてのテンプレートが常に表示されることに注意してください。 たとえば、マーケティング グループのスコープ ポリシーを構成しているとします。 選択可能な Azure RMS テンプレートは、マーケティング グループにスコープされたテンプレートに制限されることはなく、選択されたユーザーが使用できない部門別のテンプレートを選択することが可能です。 構成を簡単にしてトラブルシューティングを最小限に抑えるために、部門別テンプレートの名前がスコープ ポリシーのラベルに一致するように名前を付けることを考慮してください。 
            
9. **[HYOK (AD RMS)]** で **[テンプレートの選択]** を選択した場合: AD RMS クラスターのテンプレート GUID とライセンス URL を指定します。 [詳細情報](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

10. **[完了]** をクリックして **[アクセス許可]** ブレードを閉じ、選択した **[転送不可]** または選択したテンプレートが **[ラベル]** ブレードの **[保護]** オプションに表示されていることを確認します。

10. **[ラベル]** ブレードで、**[保存]** をクリックします。

11. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
