---
title: "Azure Information Protection テナント キーに対する操作"
description: "Azure Information Protection テナント キーに関するさまざまなレベルの制御および責任について確認してください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 24368df01f680958310b8d01c4f9a5a939e6f706
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーに対する操作

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

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
