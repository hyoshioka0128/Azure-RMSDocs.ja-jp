---
title: "Rights Management による保護を適用するようにラベルを構成する方法 | Azure Information Protection"
description: "暗号化ポリシー、ID ポリシー、および承認ポリシーによってデータ損失を防止する Rights Management サービスを使用することで、最も機密性の高いドキュメントや電子メールを保護することができます。 この保護は、Rights Management テンプレートを使用するようにラベルを構成したときに適用されます。"
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: f17cf257607b0f74ca8bdaef13130da2f62dd587
ms.openlocfilehash: 830e982fc1f0443545942c1deb1a2fc93431be17


---

# Rights Management による保護を適用するようにラベルを構成する方法

>*適用対象: Azure Information Protection*

暗号化ポリシー、ID ポリシー、および承認ポリシーによってデータ損失を防止する Rights Management サービスを使用することで、最も機密性の高いドキュメントや電子メールを保護することができます。 この保護は、Rights Management テンプレートを使用するようにラベルを構成したときに適用されます。 

テンプレートは、Azure Rights Management をアクティブ化したときに自動的に作成される既定のいずれかのテンプレート、またはカスタム テンプレートのどちらも使用できます。 Azure Rights Management の部門別テンプレートはサポートされていますが、保護は、ドキュメントまたは電子メールの作成者がテンプレートの構成範囲内にある場合にのみ適用されます。 ユーザーがその範囲外である場合は、Azure Information Protection でラベルを適用できないことを示すメッセージが表示されます。

## 保護のしくみ

Rights Management によって保護されるドキュメントまたは電子メールは、保存時および送信時に暗号化され、権限のあるユーザーのみが暗号化を解除できます。 この暗号化は、ドキュメントまたは電子メールの名前が変更された場合でも維持されます。 さらに、次の例のように、使用権限と制限を構成できます。

- 組織内のユーザーのみが社外秘のドキュメントまたは電子メールを開くことができます。

- マーケティング部門のユーザーのみが宣伝の通知ドキュメントまたは電子メールの編集と印刷を実行でき、組織内の他のすべてのユーザーはそれらの閲覧のみを実行できます。

- ユーザーは、社内の再編成に関するニュースを含む電子メールを転送できません。

- ビジネス パートナーに送信される現在の価格表は、指定日以降は開くことができません。

Azure Rights Management テンプレートおよびこれらの使用権限と制限を構成する方法の詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

Azure Rights Management とそのしくみの詳細については、[Azure Rights Management の概要に関するページ](../understand-explore/what-is-azure-rms.md)を参照してください。

> [!IMPORTANT]
> Azure Rights Management による保護を適用するようにラベルを構成するには、組織に対して Azure Rights Management サービスをアクティブにする必要があります。 この手順をまだ行っていない場合は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。


## Rights Management による保護を適用するようにラベルを構成するには

1. [Azure ポータル](https://portal.azure.com)にサインインしていない場合は新しいブラウザーのウィンドウを開き、全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 

    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[Azure Information Protection]** ブレードで、Rights Management による保護を適用するように構成するラベルを選択します。

3. **[ラベル]** ブレードの **[Set RMS template for protecting documents and emails containing this label]** (このラベルを含むドキュメントおよび電子メールを保護するための RMS テンプレートを設定する) セクションで、**[RMS テンプレートの選択]** を **[Azure RMS]** または **[AD RMS (プレビュー)]** に設定します。
    
    ほとんどの場合は、**[Azure RMS]** を選択します。 AD RMS 構成 ("*Hold Your Own Key*" (HYOK) とも呼ばれます) に付随する前提条件と制限事項を読み、理解してから、AD RMS を選択してください。 詳細については、「[AD RMS 保護の Hold Your Own Key (HYOK) の要件と制限事項](configure-adrms-restrictions.md)」を参照してください。
    
4. Azure RMS を選択した場合: **[RMS テンプレートの選択]** ドロップダウン ボックスをクリックし、このラベルを持つドキュメントや電子メールの保護に使用する[テンプレート](../deploy-use/configure-custom-templates.md)または権限管理オプションを選択します。
    
    オプションについての詳細:
    
    - **[ラベル]** ブレードを開いた後で新しいテンプレートを作成しましたか? このブレードを閉じて手順 2 に戻ります。新しく作成したテンプレートが Azure から取得され、選択できるようになります。
    
    - **[部門別テンプレート]**を選択する場合、または[オンボーディング コントロール](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成済みの場合:
    
        - 構成されたテンプレート範囲の外にいるユーザー、または Azure Rights Management 保護の適用から除外されているユーザーは、引き続きラベルを確認できますが、適用することはできません。 それらのユーザーがラベルを選択した場合、次のメッセージが表示されます: **Azure Information Protection はこのラベルを適用できません。この問題が引き続き発生する場合は、管理者に問い合わせてください。**
        
    - **[保護の削除]** を選択する場合:
        
        - このオプションを持つラベルを適用するには、ユーザーは Rights Management による保護を削除する権限を持っている必要があります。 このオプションでは **[エクスポート]** (Office ドキュメント用) または **[フル コントロール]** [使用権限](../deploy-use/configure-usage-rights.md)を持っている、Rights Management の所有者 (自動的にフル コントロール使用権限が付与されています) である、または[Azure Rights Management のスーパー ユーザー](../deploy-use/configure-super-users.md)である必要があります。 既定の権限管理テンプレートには、ユーザーに保護を削除させる使用権限は含まれません。 

            ユーザーが Rights Management による保護を削除する権限を持たずに **[保護の削除]** オプションを持つラベルを選択する場合、次のメッセージが表示されます: **Azure Information Protection はこのラベルを適用できません。この問題が引き続き発生する場合は、管理者に問い合わせてください。**

5. AD RMS を選択した場合: AD RMS クラスターのテンプレート GUID とライセンス URL を指定します。 [詳細情報](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

6. **[保存]** をクリックします。

7. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  



<!--HONumber=Oct16_HO1-->


