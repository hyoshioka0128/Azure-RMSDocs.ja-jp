---
title: Azure Information Protection のコンプライアンスと情報
description: 法律、コンプライアンス、SLA を含む Azure Information Protection のサポート情報を紹介します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d3de605c8427745e51df2ea1ffbee110c9106138
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383889"
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Azure Information Protection のコンプライアンスとサポート情報

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection は他のサービスをサポートし、また、他のサービスに依存しています。 Azure Information Protection サービスの使用方法以外で、Azure Information Protection の関連情報をお探しの場合は、以下のリソースを参照してください。

## <a name="suitability-for-different-countries"></a>国ごとの適合性

国、ユース ケースやシナリオ、業種ごとの要件によって法律や規則に違いがあるため、Azure Information Protection がお住まいの国に適しているかどうかについては法的なアドバイザーにご相談ください。

ただし、法的なアドバイザーが判断を行ううえで役に立つ情報がいくつかあります。

- Azure Information Protection は、ドキュメントの暗号化に AES 256 と AES 128 を使用します。 [詳細情報](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Azure Information Protection で使用されるすべての暗号化キーは RSA 2048 ビットを使用する顧客固有のルート キーを使用して保護されます。 RSA 1024 ビットも下位互換性用にサポートされています。 [詳細情報](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- 顧客固有のルートキーは、Microsoft によって管理されているか、"nCipher" キーを使用して、顧客によって "独自のキーを持ち込む" (BYOK) を使用してプロビジョニングされています。 Azure Information Protection は、クラウドベースのキーで保護できないコンテンツに対して、オンプレミスの保護機能もサポートしています。 詳しくは、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」をご覧ください。

- Azure Information Protection サービスは世界中のリージョンのデータ センターでホストされています。 Azure Information Protection のキーとポリシーは常に最初にデプロイされたリージョン内に保持されます。

    > [!NOTE]
    > Azure Information Protection ポリシーは、AIP classic クライアントのみに関連します。
    >
  
- Azure Information Protection は、Azure Information Protection サービスにクライアントからのドキュメントの内容を送信しません。 コンテンツの暗号化と復号化の操作は、クライアント デバイスでインプレース実行されます。 または、サービス ベースのレンダリングの場合、これらの操作はコンテンツをレンダリングしているサービス内で実行されます。 [詳細情報](./how-does-it-work.md)

## <a name="legal-and-privacy"></a>法律およびプライバシー

- Microsoft Azure の契約情報について: [Microsoft Azure の契約](https://azure.microsoft.com/support/legal/subscription-agreement/)

- Microsoft Azure のプライバシー情報について: [Microsoft Azure のプライバシーに関する声明](https://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>セキュリティ、コンプライアンス、監査

Azure Rights Management サービスの特定の認証についての情報については、記事「[Azure RMS が解決する問題の種類](./what-is-azure-rms.md#business-problems-solved-by-azure-rights-management)」の「[セキュリティ、コンプライアンス、および規制の要件](./what-is-azure-rms.md#security-compliance-and-regulatory-requirements)」のセクションを参照してください。 さらに:

- Azure Information Protection の外部認証について: [Microsoft Azure セキュリティ センター](https://azure.microsoft.com/support/trust-center/)

- FIPS 140 について: [FIPS 140 検証](/windows/security/threat-protection/fips-140-validation)

保護テクノロジのしくみに関する詳細な技術情報については、「[Azure RMS の機能の詳細](./how-does-it-work.md)」を参照してください。 

## <a name="service-level-agreements"></a>サービス レベル アグリーメント

- [Azure Information Protection の SLA](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Azure Active Directory の SLA](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)

- [Azure Key Vault の SLA](https://azure.microsoft.com/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>ドキュメント

- Azure Active Directory のドキュメント: [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis)

- Microsoft 365 のドキュメント: [エンタープライズのドキュメントとリソースの Microsoft 365](/Office365/Enterprise/)

