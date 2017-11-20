---
title: "Azure RMS および AD RMS 用の環境を準備する"
description: "AD RMS がデプロイされた Azure Rights Management の場合のガイダンス。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/10/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b20bbc1fe0de90b9b0151098e1b77d3c7a98c431
ms.sourcegitcommit: e9a24fc5303b21f5eeebf16afed44db0d163ac77
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2017
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Active Directory Rights Management サービス (AD RMS) もある場合の Azure Rights Management 用の環境の準備

>*適用対象: Azure Information Protection、Office 365*

Active Directory Rights Management サービス (AD RMS) を既に使用している場合の重要なガイダンスです。以下のシナリオが適用されます。

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Azure Information Protection を構成する際に保護をアクティブにするためのオプションが表示される

**[Azure Information Protection - 保護のアクティブ化]** のブレードには、Azure Rights Management サービス (Azure RMS) をアクティブにするためのオプションがあります。 

Active Directory Rights Management サービス (AD RMS) も使用する場合は、**[アクティブ化]** オプションは選択しないでください。 AD RMS もある場合に Azure Rights Management をアクティブ化することは、互換性のある組み合わせではありません。 このシナリオはサポートされておらず、信頼できる結果が得られないため、この時点では Azure Rights Management をアクティブにしないことが重要です。 

AD RMS から Azure Rights Management サービスにコンピューターを移動する準備ができたら、移行プロセスを開始することができます。 移行手順の 1 つはサービスをアクティブにすることですが、これは AD RMS から Azure Rights Management サービスに構成情報をエクスポートした後で行います。 このプロセスにより、AD RMS で保護されたドキュメントと電子メールを引き続き開けるようになります。

Azure Rights Management サービスがアクティブになっていない場合でも、分類のみを適用するラベルで Azure Information Protection を使用できます。 データ保護を含まない特別な既定ポリシーが自動的に作成されます。これらの構成オプションは、Azure Rights Management サービスがアクティブになるまで使用不可のままです。

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>手順 1: 分類とラベル付けのために Azure Information Protection ポリシーを構成する (保護なし)

**Azure Information Protection** の最初のブレードから、**[グローバル ポリシー]** を選択し、データ保護のオプションを含まない既定のポリシーを表示して構成します。 詳しくは、「[Configuring Azure Information Protection policy](configure-policy.md)」 (Azure Information Protection ポリシーの構成) をご覧ください。

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行ガイダンス「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」に従います。

### <a name="step-3-start-to-configure-labels-for-protection"></a>手順 3: 保護のためのラベルの構成を開始する

移行プロセス時に Azure Rights Management サービスをアクティブにした場合は、データ保護のためにラベルを構成できます。 ただし、ユーザーをバッチで移行する場合は、保護を適用するラベルの[範囲](configure-policy-scope.md)が移行対象のユーザーのみに指定されていることを確認してください。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


