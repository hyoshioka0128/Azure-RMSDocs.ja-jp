---
title: "Azure Information Protection テナント キーに対する操作"
description: "Azure Information Protection テナント キーに関するさまざまなレベルの制御および責任について確認してください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/11/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 10ce24e72dae1225505592508d4bf88cadb131a2
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# Azure Information Protection テナント キーに対する操作
<a id="operations-for-your-azure-information-protection-tenant-key" class="xliff"></a>

>*適用対象: Azure Information Protection、Office 365*

テナント キー トポロジ (Microsoft が管理またはお客様が管理) に応じて、実装後の Azure Information Protection テナント キーに対する制御および責任のレベルは異なります。

Azure Key Vault で独自のテナント キーを自分で管理する場合、これは一般に BYOK (Bring Your Own Key) と呼ばれます。 このシナリオの詳細のほか、2 つのテナント キー トポロジから選択する方法については、「[Azure Rights Management テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」を参照してください。

次の表に、Azure Information Protection テナント キーの選択したトポロジに応じて実行できる操作を示します。

|ライフサイクル操作|Microsoft が管理 (既定)|お客様が管理 (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|テナント キーを取り消します|いいえ (自動)|[はい]|
|テナント キーを再入力します|[はい]|Yes|
|テナント キーをバックアップ/復旧します|いいえ|Yes|
|テナント キーをエクスポートします|Yes|いいえ|
|侵害に反応します|Yes|Yes|

実装したトポロジを識別したら、次のいずれかを選択して、Azure Information Protection テナント キーに対するこれらの操作の詳細を参照してください。

- [Microsoft が管理するテナント キー](operations-microsoft-managed-tenant-key.md)
- [お客様が管理するテナント キー](operations-customer-managed-tenant-key.md)

ただし、信頼された発行ドメイン (TPD) を Active Directory Rights Management サービスからインポートして、Azure Information Protection テナント キーを作成する場合、このインポート操作は「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」作業の一部になります。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
