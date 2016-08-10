---
title: "Rights Management による保護を適用するようにラベルを構成する方法 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 00b4cd2b1e7b1196cedd39d7052db534e781bb13
ms.openlocfilehash: 7a20b59c404959c4ec209e8c29ac61ab71233e87


---

# Rights Management による保護を適用するようにラベルを構成する方法

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

暗号化ポリシー、ID ポリシー、および承認ポリシーによってデータ損失を防止する Azure Rights Management を使用することで、最も機密性の高いドキュメントや電子メールを保護することができます。 この保護は、Rights Management テンプレートを使用するようにラベルを構成したときに適用されます。 

テンプレートは、Azure Rights Management をアクティブ化したときに自動的に作成される既定のいずれかのテンプレート、またはカスタム テンプレートのどちらも使用できます。 部門別テンプレートはサポートされていますが、保護は、ドキュメントまたは電子メールの作成者がテンプレートの構成範囲内にある場合にのみ適用されます。 ユーザーがその範囲外である場合は、Azure Information Protection でラベルを適用できないことを示すメッセージが表示されます。

## 保護のしくみ

Azure Rights Management によって保護されるドキュメントまたは電子メールは、保存時および送信時に暗号化され、権限のあるユーザーのみが暗号化を解除できます。 この暗号化は、ドキュメントまたは電子メールの名前が変更された場合でも維持されます。 さらに、次の例のように、使用権限と制限を構成できます。

- 組織内のユーザーのみがドキュメントまたは電子メールを開くことができます。

- マーケティング部門のユーザーのみがドキュメントまたは電子メールの編集と印刷を実行でき、組織内の他のすべてのユーザーはそれらの表示のみを実行できます。

- ユーザーは電子メールを転送できません。

- ビジネス パートナーに送信されるドキュメントまたは電子メールは、指定日以降は開くことができません。

テンプレートおよびこれらの使用権限と制限を構成する方法の詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

Azure Rights Management とそのしくみの詳細については、[Azure Rights Management の概要に関するページ](../understand-explore/what-is-azure-rms.md)を参照してください。

> [!IMPORTANT]
> Rights Management による保護を適用するようにラベルを構成するには、組織に対して Azure Rights Management サービスをアクティブにする必要があります。 この手順をまだ行っていない場合は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。


## Rights Management による保護を適用するようにラベルを構成するには

1. [Azure ポータル](https://portal.azure.com)にサインインします。
 
2. ハブ メニューで **[参照]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

3. **[Azure Information Protection]** ブレードで、Rights Management による保護を適用するように構成するラベルを選択します。

4. **[ラベル]** ブレードで、**[Set RMS template for protecting documents and emails containing this label]** (このラベルを含むドキュメントおよび電子メールを保護するための RMS テンプレートを設定する) セクションで、以下を構成します。

    - **[Select RMS template from]** (RMS テンプレートの選択元) が表示される場合: **[Azure RMS]** を選択します。 
    
        **[AD RMS]** および関連する構成オプションは、マイクロソフトのサポートなしで選択しないでください。 Azure Information Protection の Active Directory Rights Management サービスによるテストをご希望の場合は、askipteam@microsoft.com にメールをお送りください。 
    
    - **[RMS テンプレートの選択]**: ドロップダウン ボックスをクリックし、このラベルでドキュメントと電子メールを保護するために使用するテンプレートを選択します。

        > [!NOTE] **[ラベル]** ブレードを開いた後で新しいテンプレートを作成した場合は、このブレードを閉じて手順 3 に戻ります。新しく作成したテンプレートが Azure から取得され、選択できるようになります。

5. **[保存]** をクリックします。

6. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## 次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organization-s-policy)」セクションのリンクを使用してください。  



<!--HONumber=Jul16_HO5-->


