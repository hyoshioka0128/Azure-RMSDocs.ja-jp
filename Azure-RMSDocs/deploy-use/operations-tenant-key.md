---
title: "Azure Information Protection テナント キーに対する操作"
description: "Azure Information Protection テナント キーに関するさまざまなレベルの制御および責任について確認してください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: afe33bcee3516589bd87642b0f15206b90a4bb41
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2017
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーに対する操作

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection のテナント キー トポロジに応じて、Azure Information Protection テナント キーに対する制御および責任のレベルは異なります。 キー トポロジには、**Microsoft が管理**するものと**お客様による管理**の 2 種類があります。

Azure Key Vault で独自のテナント キーを自分で管理する場合、これは一般に BYOK (Bring Your Own Key) と呼ばれます。 このシナリオの詳細のほか、2 つのテナント キー トポロジから選択する方法については、「[Azure Information Protection テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」を参照してください。

次の表に、Azure Information Protection テナント キーの選択したトポロジに応じて実行できる操作を示します。

|ライフサイクル操作|Microsoft が管理 (既定)|お客様が管理 (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|テナント キーの取り消し|いいえ (自動)|○|
|テナント キーの再入力|Yes|Yes|
|テナント キーのバックアップ/復旧|いいえ|Yes|
|テナント キーのエクスポート|Yes|いいえ|
|侵害への対応|Yes|○|

実装したトポロジを識別したら、次のいずれかのリンクを選択して、Azure Information Protection テナント キーに対するこれらの操作の詳細を参照してください。

- [Microsoft が管理するテナント キー](operations-microsoft-managed-tenant-key.md)
- [お客様が管理するテナント キー](operations-customer-managed-tenant-key.md)

ただし、信頼された発行ドメイン (TPD) を Active Directory Rights Management サービスからインポートして、Azure Information Protection テナント キーを作成する場合、このインポート操作は「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」作業の一部になります。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
