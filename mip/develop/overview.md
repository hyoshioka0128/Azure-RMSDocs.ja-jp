---
title: 概要 - Microsoft Information Protection SDK。
description: Microsoft Information Protection (MIP) は、Microsoft の分類、ラベル作成、および保護の各サービスを 1 つの管理エクスペリエンスとソフトウェア開発キット (SDK) に統合したものです。
author: msmbaldwin
ms.service: information-protection
ms.topic: overview
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: d8efb7ceef890d0c2a0ea72f64d3047e0cfb25a5
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184945"
---
# <a name="overview"></a>概要

## <a name="microsoft-information-protection"></a>Microsoft Information Protection

Microsoft Information Protection (MIP) は、Microsoft の分類、ラベル付け、および保護サービスの統合を示します。

- Office 365、Azure Information Protection、Windows Information Protection、およびその他の Microsoft サービスの全体で統一された管理が提供されます。 
- サード パーティは、MIP SDK を使用して、サービスのスキーマと保護のラベルを付け、標準的な一貫性のあるデータを使用して、アプリケーションと統合することができます。

* [Office 365 セキュリティとコンプライアンス センターとは](https://docs.microsoft.com/office365/securitycompliance/)
* [Azure Information Protection とは](/azure/information-protection/understand-explore/what-is-information-protection)
* [Azure Information Protection での保護のしくみ](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>Microsoft Information Protection SDK

MIP SDK では、サード パーティ製アプリケーションとサービスから Office 365 セキュリティ/コンプライアンス センターでは、ラベル付け、保護サービスを公開します。 開発者は SDK を使用して、ファイルにラベルと保護を適用するためのネイティブ サポートを構築することができます。 開発者は、特定のラベルが検出されたときにどのアクションを実行する必要があるかを推論したり、MIP で暗号化された情報に対して推論したりすることができます。 

一連の Microsoft サービス全体に適用されるラベルと保護には、**一貫性**があります。 一貫性が、MIP をサポートするアプリケーションとサービスが、共通の予測可能な方法でラベルを読み書きすることを可能にします。

高度な MIP SDK のユース ケースには次のものがあります。

* エクスポート時に分類ラベルをファイルに適用する基幹業務アプリケーション。
* CAD/CAM 設計プリケーションが、Microsoft Information Protection のラベル作成に対して、ネイティブ サポートを提供する。
* Cloud Access Security Broker またはデータ損失防止ソリューションが、Azure Information Protection で暗号化されたデータに対して推論する。

より網羅された一覧は、[API の概念](concept-apis-use-cases.md)に関するページを参照してください。

MIP SDK は、次のプラットフォームで使用できます。

[!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

## <a name="next-steps"></a>次の手順

これで SDK を使用する準備ができました。 実行する必要がありますまず[MIP SDK のセットアップと構成の手順を完了](setup-configure-mip.md)します。 次の手順は、Office 365 サブスクリプションを確認し、クライアント コンピューターが正しく設定されています。

