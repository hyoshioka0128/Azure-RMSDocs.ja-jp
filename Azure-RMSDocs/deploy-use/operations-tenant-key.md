---
title: "Azure Rights Management テナント キーに対する操作 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 44408fd8f9da73d8050e0938aa1cc9bc76688bed


---

# Azure Rights Management テナント キーに対する操作

*適用対象: Azure Rights Management、Office 365*

組織のテナント キー トポロジ (Microsoft が管理またはお客様が管理) に応じて、実装後の Microsoft Azure Rights Management (Azure RMS) テナント キーに対する制御および責任のレベルは異なります。

独自のテナント キーを自分で管理する場合、これは一般に BYOK (Bring Your Own Key) と呼ばれます。 このシナリオの詳細のほか、2 つのテナント キー トポロジから選択する方法については、「[Azure Rights Management テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」を参照してください。

次の表に、Azure RMS テナント キーの選択したトポロジに応じて実行できる操作を示します。

|ライフサイクル操作|Microsoft が管理 (既定)|お客様が管理 (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|テナント キーを取り消します|いいえ (自動)|いいえ (自動)|
|テナント キーを再入力します|はい|はい|
|テナント キーをバックアップ/復旧します|いいえ|はい|
|テナント キーをエクスポートします|はい|いいえ|
|侵害に反応します|はい|○|

実装したトポロジを識別したら、次のいずれかを選択して、Azure RMS テナント キーに対するこれらの操作の詳細を参照してください。


- [Microsoft が管理するテナント キー](operations-microsoft-managed-tenant-key.md)
- [お客様が管理するテナント キー](operations-customer-managed-tenant-key.md)







<!--HONumber=Jul16_HO3-->


