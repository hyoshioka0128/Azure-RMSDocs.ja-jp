---
title: RMS API をサポートするその他のアプリ - インストールと構成 - AIP
description: 組織のデータを保護するために Azure Information Protection の Azure Rights Management サービスが他のアプリケーションをどのようにサポートするかを理解します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c50a8cbb-d12f-4a0e-bc29-74c463e6ac3e
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: fac36bf4c59608eb1393088024f39a9f936a9b5a
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384011"
---
# <a name="other-applications-that-support-the-rights-management-apis"></a>Rights Management API をサポートするその他のアプリケーション

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 *

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

次の情報は、Azure Information Protection の Azure Rights Management サービスが他のアプリケーションをサポートして組織のデータを保護する方法を理解するのに役立ちます。

Azure Information Protection SDK を使用すると、社内開発者は、Azure Rights Management サービスをネイティブでサポートする基幹業務アプリケーションを作成できます。 これらのアプリケーションと情報保護を統合する方法は、アプリケーションの作成方法によって決まります。 たとえば、ユーザーによる最小限の対話操作で統合を自動的に適用するか、またはより細かくカスタマイズされた場合は、ファイルの情報保護を適用するための設定を構成するようにユーザーに要求することができます。 詳細については、「[開発者ガイド](./develop/developers-guide.md)」を参照してください。

同様に、多くのソフトウェア ベンダーが情報保護ソリューションを提供するアプリケーションを提供しています。これらは ERM (Enterprise Rights Management) 製品とも呼ばれます。 一般的な例は、特定のプラットフォームで Azure Rights Management サービスをサポートする PDF リーダーです。 「[Azure Rights Management データ保護をサポートするアプリケーション](./requirements-applications.md)」にある表を使用して Rights Management をサポートするアプリケーション (RMS 対応アプリケーション) を特定してから、Web 検索を使用してそのアプリケーションを購入またはダウンロードすることができます。

## <a name="next-steps"></a>次のステップ

他のアプリケーションおよびサービスで Azure Rights Management サービスをサポートする方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」を参照してください。
