---
title: Azure Information Protection のコンプライアンスと情報
description: 法律、コンプライアンス、SLA を含む Azure Information Protection のサポート情報を紹介します。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/12/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 55d3b303a84a557ad5f65760d963221878a7b521
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39488853"
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Azure Information Protection のコンプライアンスとサポート情報

Azure Information Protection は他のサービスをサポートし、また、他のサービスに依存しています。 Azure Information Protection サービスの使用方法以外で、Azure Information Protection の関連情報をお探しの場合は、以下のリソースを参照してください。

## <a name="suitability-for-different-countries"></a>国ごとの適合性

国、ユース ケースやシナリオ、業種ごとの要件によって法律や規則に違いがあるため、Azure Information Protection がお住まいの国に適しているかどうかについては法的なアドバイザーにご相談ください。

ただし、法的なアドバイザーが判断を行ううえで役に立つ情報がいくつかあります。

- Azure Information Protection は、ドキュメントの暗号化に AES 256 と AES 128 を使用します。 [詳細情報](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Azure Information Protection で使用されるすべての暗号化キーは RSA 2048 ビットを使用する顧客固有のルート キーを使用して保護されます。 RSA 1024 も下位互換性のためにサポートされています。 [詳細情報](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- 顧客固有のルート キーは Microsoft によって管理されるか、または Thales HSM の顧客が "[Bring Your Own Key](plan-implement-tenant-key.md)"(BYOK) を使用してプロビジョニングします。 Azure Information Protection は、クラウドベースのキーで保護すべきでないことを示す要件の影響を受けるコンテンツに対して "[Hold Your Own Key](configure-adrms-restrictions.md)" (HYOK) を使ってオンプレミスのキーの制限付き機能もサポートします。

- Azure Information Protection サービスは世界中のリージョンのデータ センターでホストされています。 Azure Information Protection のキーとポリシーは常に最初にデプロイされたリージョン内に保持されます。
 
- Azure Information Protection は、Azure Information Protection サービスにクライアントからのドキュメントの内容を送信しません。 コンテンツの暗号化と復号化の操作は、クライアント デバイスでインプレース実行されます。 または、サービス ベースのレンダリングの場合、これらの操作はコンテンツをレンダリングしているサービス内で実行されます。 [詳細情報](./how-does-it-work.md)

## <a name="legal-and-privacy"></a>法律およびプライバシー

- Microsoft Azure の契約情報について: [Microsoft Azure の契約](http://azure.microsoft.com/support/legal/subscription-agreement/)

- Microsoft Azure のプライバシー情報について: [Microsoft Azure のプライバシーに関する声明](http://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>セキュリティ、コンプライアンス、監査

Azure Rights Management サービスの特定の認証についての情報については、記事「[Azure RMS が解決する問題の種類](./azure-rms-problems-it-solves.md)」の「[セキュリティ、コンプライアンス、および規制の要件](./azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements)」のセクションを参照してください。 さらに

- Azure Information Protection の外部認証について: [Microsoft Azure セキュリティ センター](http://azure.microsoft.com/support/trust-center/)

- FIPS 140 について: [FIPS 140 検証](https://technet.microsoft.com/library/security/cc750357.aspx)

保護テクノロジのしくみに関する詳細な技術情報については、「[Azure RMS の機能の詳細](./how-does-it-work.md)」を参照してください。 

## <a name="service-level-agreements"></a>サービス レベル アグリーメント

- [Azure Information Protection の SLA](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Azure Active Directory の SLA](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)

- [Azure Key Vault の SLA](https://azure.microsoft.com/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>ドキュメント

- Azure Active Directory のドキュメント: [Azure Active Directory](/active-directory/)

- Office 365 ライブラリ: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

