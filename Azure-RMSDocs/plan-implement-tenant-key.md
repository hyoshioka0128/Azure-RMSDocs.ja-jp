---
title: Azure Information Protection テナント キー
description: Azure Information Protection のルートキーをマイクロソフトが管理するのではなく、特定の規制に準拠するために、テナントのこのキーを作成して管理することをお勧めします。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 24479014fcbd0bd93b65d6958d004deb9c7e0c95
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570391"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーを計画して実装する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と **ラベル管理** は、**2021 年 3 月 31 日** で **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection テナント キーは組織のルート キーです。 その他のキーは、ユーザーキー、コンピューターキー、ドキュメント暗号化キーなど、このルートキーから派生できます。 Azure Information Protection が組織でこれらのキーを使用するたびに、暗号化された Azure Information Protection ルートテナントキーにチェーンされます。

テナントのルートキーに加えて、組織は特定のドキュメントに対してオンプレミスのセキュリティを必要とする場合があります。 通常、オンプレミスのキー保護は少量のコンテンツに対してのみ必要であり、そのため、テナントルートキーと共に構成されます。

## <a name="azure-information-protection-key-types"></a>Azure Information Protection キーの種類

テナントのルートキーは次のいずれかになります。

- [Microsoft によって生成](#tenant-root-keys-generated-by-microsoft)
- [Bring Your Own Key (BYOK)](#bring-your-own-key-byok-protection)保護を使用している顧客によって生成されます。

オンプレミスのキー managements は、AIP クライアントの種類によって異なります。 オンプレミスの追加の保護を必要とする非常に機密性の高いコンテンツがある場合は、次のいずれかの方法を使用します。

- [独自のキーを保持する (HYOK)](#hold-your-own-key-hyok-aip-classic-client-only) (クラシッククライアントのみ)
- [二重キー暗号化 (DKE)](#double-key-encryption-dke-aip-unified-labeling-client-only) (統一されたラベル付けクライアントのみ)

コンテンツは、クラシッククライアントを使用している場合にのみ、HYOK protection を使用して暗号化できます。 ただし、HYOK で保護されたコンテンツがある場合は、クラシックラベルクライアントと統合ラベルクライアントの両方で表示できます。 

> [!TIP]
> 従来のクライアントと、統一されたラベル付けクライアントの違いについては、 詳細については、この [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)を参照してください。
>

## <a name="tenant-root-keys-generated-by-microsoft"></a>Microsoft によって生成されたテナントルートキー

Microsoft によって自動的に生成された既定のキーは、テナントキーのライフサイクルのほとんどの側面を管理するために Azure Information Protection 専用に使用される既定のキーです。

特別なハードウェア、ソフトウェア、または Azure サブスクリプションを使用せずに Azure Information Protection をすばやくデプロイする場合は、既定の Microsoft キーを使い続けます。 例としては、キー管理に関する規制要件のないテスト環境や組織などがあります。

既定のキーの場合、これ以上の手順は必要ありません。また、 [テナントのルートキー](get-started-tenant-root-keys.md)の概要に直接進むことができます。

> [!NOTE]
> Microsoft によって生成される既定のキーは、管理オーバーヘッドが最も少ない、最も簡単なオプションです。
>
> 多くの場合、テナントキーがあることはわかりません。 Azure Information Protection にサインアップすることができ、残りのキー管理プロセスは Microsoft によって処理されます。

## <a name="bring-your-own-key-byok-protection"></a>Bring Your Own Key (BYOK) 保護

BYOK-保護では、顧客組織の Azure Key Vault またはオンプレミスのいずれかで、顧客によって作成されたキーが使用されます。 これらのキーは、さらに管理するために Azure Key Vault に転送されます。

すべてのライフサイクル操作の制御など、キーの生成に関するコンプライアンスの規制が組織にある場合は、BYOK を使用します。 たとえば、キーがハードウェアセキュリティモジュールによって保護されている必要がある場合です。

詳細については、「 [BYOK 保護の構成](byok-price-restrictions.md)」を参照してください。 

構成が完了したら、「 [テナントルートキー](get-started-tenant-root-keys.md) の概要」に進み、キーの使用と管理の詳細について説明します。

## <a name="hold-your-own-key-hyok-aip-classic-client-only"></a>独自のキーを保持する (HYOK) (AIP classic client のみ)

HYOK は、クラウドから分離された場所で、顧客によって作成および保持されるキーを使用します。 HYOK 保護ではオンプレミスのアプリケーションとサービスのデータへのアクセスのみが可能であるため、HYOK を使用するお客様はクラウドドキュメント用のクラウドベースのキーも持っています。

次のようなドキュメントには、HYOK を使用します。

- 少数の人員に限定
- 組織外では共有されません
- は、内部ネットワークでのみ使用されます。

これらのドキュメントでは、通常、組織内で最も高い分類が "上位シークレット" として使用されています。

詳細については、「 [独自のキーの保持 (HYOK) の詳細](configure-adrms-restrictions.md)」を参照してください。

## <a name="double-key-encryption-dke-aip-unified-labeling-client-only"></a>二重キー暗号化 (DKE) (AIP のラベル付けクライアントのみ)

DKE 保護では、2つのキーを使用してコンテンツのセキュリティを強化します。1つは Azure で作成して保持するキーで、もう1つは顧客がオンプレミスで作成して保持するキーです。

DKE では、保護されたコンテンツにアクセスするために両方のキーが必要です。これにより、マイクロソフトとその他のサードパーティが自分で保護されたデータにアクセスできなくなります。

DKE はクラウドとオンプレミスのどちらにでもデプロイできるため、ストレージの場所を最大限に柔軟に実現できます。

組織で DKE を使用する:

- では、すべての状況で、保護されたコンテンツの暗号化を解除できるようにする必要があります。
- 保護されたデータへのアクセスをマイクロソフトに許可しないようにしてください。
- 地理的境界内のキーを保持するための規制要件があります。 DKE では、顧客保持キーは顧客データセンター内に保持されます。

> [!NOTE]
> DKE は、アクセス権を取得するために銀行キーと顧客キーの両方を必要とする安全預金箱に似ています。
> 保護されたコンテンツの暗号化を解除するには、Microsoft によって保持されているキーと、ユーザーが保持するキーの両方が必要です。

詳細については、Microsoft 365 ドキュメントの「 [Double キー encryption](/microsoft-365/compliance/double-key-encryption) 」を参照してください。