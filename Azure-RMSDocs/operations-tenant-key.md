---
title: Azure Information Protection テナント キーに対する操作
description: Azure Information Protection テナント キーに関するさまざまなレベルの制御および責任について確認してください。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c8fc10aed7bcb0d42dab72afd4c1fc100a3962ba
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136368"
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーに対する操作

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection のテナント キー トポロジに応じて、Azure Information Protection テナント キーに対する制御および責任のレベルは異なります。 キー トポロジには、**Microsoft が管理**するものと**お客様による管理**の 2 種類があります。

Azure Key Vault で独自のテナント キーを自分で管理する場合、これは一般に BYOK (Bring Your Own Key) と呼ばれます。 このシナリオの詳細のほか、2 つのテナント キー トポロジから選択する方法については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

次の表に、Azure Information Protection テナント キーの選択したトポロジに応じて実行できる操作を示します。

|ライフサイクル操作|Microsoft が管理 (既定)|お客様が管理 (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|テナント キーを取り消します|いいえ (自動)|はい|
|テナント キーの再入力|はい|はい|
|テナント キーをバックアップ/復旧します|いいえ|はい|
|テナント キーをエクスポートします|はい|いいえ|
|侵害に反応します|はい|はい|

実装したトポロジを識別したら、次のいずれかのリンクを選択して、Azure Information Protection テナント キーに対するこれらの操作の詳細を参照してください。

- [Microsoft が管理するテナント キー](operations-microsoft-managed-tenant-key.md)
- [お客様が管理するテナント キー](operations-customer-managed-tenant-key.md)

ただし、信頼された発行ドメイン (TPD) を Active Directory Rights Management サービスからインポートして、Azure Information Protection テナント キーを作成する場合、このインポート操作は「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」作業の一部になります。  

