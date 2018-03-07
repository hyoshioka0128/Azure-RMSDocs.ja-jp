---
title: "Azure RMS および AD RMS 用の環境を準備する"
description: "AD RMS がデプロイされた Azure Rights Management の場合のガイダンス。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: de42f0d87f42c304c2df906fe037816be7f2ba25
ms.sourcegitcommit: 23d98a405057d61a737313c8dfef042996131d3e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2018
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Active Directory Rights Management サービス (AD RMS) もある場合の Azure Rights Management 用の環境の準備

>*適用対象: Azure Information Protection、Office 365*

Active Directory Rights Management サービス (AD RMS) を既に使用している場合の重要なガイダンスです。次のいずれかのシナリオが適用されます。

- [2018 年 2 月以降に購入した Azure Rights Management を含むサブスクリプションの場合](#your-subscription-was-purchased-during-or-after-february-2018)

- [Azure Portal で Azure Information Protection ポリシーを構成するときに保護をアクティブにするためのオプションが表示される場合](#you-see-an-option-to activate-azure-rights-management-when-you-configure-azure-information-protection)

## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>2018 年 2 月以降に購入したサブスクリプション

2018 年 2 月末日まで、Azure Information Protection を含む新しいサブスクリプションでは、既定により Azure Rights Management サービスがアクティブになります。 このサービスが自動的にアクティブ化されていて、Active Directory Rights Management サービス (AD RMS) も使用している場合は、この組み合わせには互換性がありません。 追加の手順を行うことなく、一部のコンピューターでは、Azure Rights Management サービスの使用が自動的に開始され、AD RMS クラスターへの接続も行われる場合があります。 このシナリオはサポートされておらず、信頼できる結果が得られないため、すぐに Azure Rights Management サービスを非アクティブ化することが重要です。 

AD RMS から Azure Rights Management サービスにコンピューターを移動する準備ができたら、移行プロセスを開始することができます。 移行手順の 1 つはサービスをもう一度アクティブにすることですが、この手順は AD RMS から Azure Rights Management サービスに構成情報をエクスポートした後で行います。 この順序により、AD RMS で保護されたドキュメントと電子メールを引き続き開けるようになります。

最初の手順は、Azure Rights Management サービスを非アクティブ化することです。

### <a name="step-1-deactivate-azure-rights-management"></a>手順 1: Azure Rights Management を非アクティブ化する
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を非アクティブ化するには、次のいずれかの手順を使用します。

> [!TIP]
> Windows PowerShell の [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) コマンドレットを使用して [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] を非アクティブ化することもできます。

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Office 365 管理センターから Rights Management を非アクティブ化するには

1. Office 365 管理者向けの [Rights Management ページ](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) に移動します。
    
    サインインを求められたら、Office 365 のグローバル管理者であるアカウントを使用します。

2. **[Rights Management]** ページで、**[非アクティブ化]** をクリックします。

3.  **[Rights Management を非アクティブ化しますか?]** というメッセージが表示されたら、**[非アクティブ化]** をクリックします。

**[Rights Management がアクティブ化されていません]** というテキストとアクティブ化するオプションが表示されます。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Azure ポータルから Rights Management を非アクティブ化するには

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
    以前に [Azure Information Protection] ブレードにアクセスしたことがない場合、このブレードをポータルに追加するには、1 回限りの[追加の手順](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time)を参照してください。

2. 最初の **[Azure Information Protection]** ブレードで、**[Protection activation]\(保護のアクティブ化\)** を選択します。 

3.  **[Azure Information Protection - Protection activation]\(Azure Information Protection - 保護のアクティブ化\)** ブレードで、**[非アクティブ化]** を選びます。 **[はい]** を選択して選択肢を確定します。

情報バーに **[非アクティブ化が正常に完了しました]\(Deactivation finished successfully\)** と表示され、**[非アクティブ化]** が **[アクティブ化]** に変わります。 

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行ガイダンス「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Azure Information Protection を構成する際に保護をアクティブにするためのオプションが表示される

**[Azure Information Protection - 保護のアクティブ化]** のブレードには、Azure Rights Management サービス (Azure RMS) をアクティブにするためのオプションがあります。  

Active Directory Rights Management サービス (AD RMS) も使用する場合は、**[アクティブ化]** オプションは選択しないでください。 AD RMS もある場合に Azure Rights Management をアクティブ化することは、互換性のある組み合わせではありません。 このシナリオはサポートされておらず、信頼できる結果が得られないため、この時点では Azure Rights Management をアクティブにしないことが重要です。  

AD RMS から Azure Rights Management サービスにコンピューターを移動する準備ができたら、移行プロセスを開始することができます。 移行手順の 1 つはサービスをアクティブにすることですが、これは AD RMS から Azure Rights Management サービスに構成情報をエクスポートした後で行います。 このプロセスにより、AD RMS で保護されたドキュメントと電子メールを引き続き開けるようになります。 

Azure Rights Management サービスがアクティブになっていない場合でも、分類のみを適用するラベルで Azure Information Protection を使用できます。 データ保護を含まない特別な既定ポリシーが自動的に作成されます。これらの構成オプションは、Azure Rights Management サービスがアクティブになるまで使用不可のままです。

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>手順 1: 分類とラベル付けのために Azure Information Protection ポリシーを構成する (保護なし)

**Azure Information Protection** の最初のブレードから、**[グローバル ポリシー]** を選択し、データ保護のオプションを含まない既定のポリシーを表示して構成します。 詳しくは、「[Configuring Azure Information Protection policy](configure-policy.md)」 (Azure Information Protection ポリシーの構成) をご覧ください。

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行ガイダンス「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

### <a name="step-3-start-to-configure-labels-for-protection"></a>手順 3: 保護のためのラベルの構成を開始する

移行プロセス時に Azure Rights Management サービスをアクティブにした場合は、データ保護のためにラベルを構成できます。 ただし、ユーザーをバッチで移行する場合は、保護を適用するラベルの範囲が移行対象のユーザーのみに指定されていることを確認してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

