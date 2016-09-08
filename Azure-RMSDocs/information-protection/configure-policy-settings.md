---
title: "Azure Information Protection のグローバル ポリシー設定を構成する方法 | Azure Rights Management"
description: "Azure Information Protection ポリシーには、すべてのユーザーとすべてのデバイスに適用される次の 3 つの設定があります。"
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: c48f5488e49a54b970f76012e0f2f17fe4158691


---

# Azure Information Protection のグローバル ポリシー設定を構成する方法

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

すべてのユーザーとすべてのデバイスに適用される Azure Information Protection ポリシーには、次の 3 つの設定があります。

![Azure Information Protection ポリシーのグローバル設定](../media/info-protect-policy-settings.png)


設定を構成するには:

1. [Azure ポータル](https://portal.azure.com)にまだサインインしていない場合はサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[参照]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[Azure Information Protection]** ブレードで、次のグローバル設定を構成します。

    - **All documents and emails must have a label** (すべてのドキュメントと電子メールにラベルを設定する必要があります): このオプションを **[オン]** に設定した場合は、すべての保存されるドキュメントと送信される電子メールにラベルを適用する必要があります。 ラベル付けは、ユーザーが手動で割り当てる、[条件](configure-policy-classification.md)の結果として自動的に割り当てる、または (**[Select the default label]** (既定のラベルを選択) オプションを設定することで) 既定で割り当てることができます。 

    ユーザーがドキュメントを保存または電子メールを送信するときにラベルが割り当てられなかった場合は、ラベルの選択を求めるプロンプトが表示されます。

    ![新しい分類が下位の場合の Azure Information Protection のプロンプト](../media/info-protect-enforce-label.png)

    - **Select the default label** (既定のラベルを選択します): このオプションを設定した場合、ラベルを持たないドキュメントや電子メールに割り当てるラベルを選択します。 サブラベルがあるラベルは、既定値として設定することはできません。 

    - **Users must provide justification when lowering the sensitivity level ** (秘密度レベルを下げるときは妥当性を示す必要があります): このオプションを **[オン]** に設定し、ユーザーが既存のドキュメントまたは電子メールのラベルを秘密度レベルが低いラベルに変更する (たとえば **[秘密]** から **[パブリック]** に変更する) 場合は、この操作の理由を求めるプロンプトが表示されます。 たとえば、ユーザーは、「このドキュメントにはもう秘密情報が含まれていない」という説明を入力します。 この操作と妥当性の説明は、次のローカルの Windows イベント ログに記録されます: **[アプリケーション]**  >  **[Microsoft Azure Information Protection]**  

    ![新しい分類が下位の場合の Azure Information Protection のプロンプト](../media/info-protect-lower-justification.png)

    このオプションは、サブラベルには適用されません。

3. 変更を保存するには、**[保存]** をクリックします。

4. 他のユーザーが変更を表示できるようにするには、**[公開]** をクリックします。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  












<!--HONumber=Aug16_HO4-->


