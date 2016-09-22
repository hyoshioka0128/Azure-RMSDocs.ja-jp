---
title: "Azure Information Protection のグローバル ポリシー設定を構成する方法 | Azure Information Protection"
description: "Azure Information Protection ポリシーには、すべてのユーザーとすべてのデバイスに適用される次の 3 つの設定があります。"
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: 801ca11da602d4acb9c398c9a89aeb33e45cb0f4
ms.openlocfilehash: d4e96321069b27ed832af3bfb6d995e0d3c5d450


---

# Azure Information Protection のグローバル ポリシー設定を構成する方法

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

すべてのユーザーとすべてのデバイスに適用される Azure Information Protection ポリシーには、次の 3 つの設定があります。

![Azure Information Protection ポリシーのグローバル設定](../media/info-protect-policy-settings.png)


設定を構成するには:

1. [Azure ポータル](https://portal.azure.com)にサインインしていない場合は新しいブラウザーのウィンドウでサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[Azure Information Protection]** ブレードで、次のグローバル設定を構成します。

    - **All documents and emails must have a label** (すべてのドキュメントと電子メールにラベルを設定する必要があります): このオプションを **[オン]** に設定した場合は、すべての保存されるドキュメントと送信される電子メールにラベルを適用する必要があります。 ラベル付けは、ユーザーが手動で割り当てる、[条件](configure-policy-classification.md)の結果として自動的に割り当てる、または (**[Select the default label]** (既定のラベルを選択) オプションを設定することで) 既定で割り当てることができます。 

    ユーザーがドキュメントを保存または電子メールを送信するときにラベルが割り当てられなかった場合は、ラベルの選択を求めるプロンプトが表示されます。

    ![新しい分類が下位の場合の Azure Information Protection のプロンプト](../media/info-protect-enforce-label.png)

    - **Select the default label** (既定のラベルを選択します): このオプションを設定した場合、ラベルを持たないドキュメントや電子メールに割り当てるラベルを選択します。 サブラベルがあるラベルは、既定値として設定することはできません。 

    - **Users must provide justification to set a lower classification label, remove a label, or remove protection** (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります): このオプションが **[オン]** に設定されているときは、ユーザーがこれらの操作を行うと (たとえば **[Secret]** (秘密) ラベルを **[Personal]** (個人用) に変更)、その操作の理由を入力する画面が表示されます。 たとえば、ユーザーは、「このドキュメントにはもう秘密情報が含まれていない」という説明を入力します。 この操作と妥当性の説明は、次のローカルの Windows イベント ログに記録されます: **[アプリケーション]**  >  **[Microsoft Azure Information Protection]**  

    ![新しい分類が下位の場合の Azure Information Protection のプロンプト](../media/info-protect-lower-justification.png)

    このオプションは、サブラベルには適用されません。

3. 変更を保存するには、**[保存]** をクリックします。

4. 他のユーザーが変更を表示できるようにするには、**[公開]** をクリックします。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  












<!--HONumber=Sep16_HO3-->


