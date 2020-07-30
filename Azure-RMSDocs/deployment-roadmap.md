---
title: Azure Information Protection デプロイ ロードマップ
description: 組織の Azure Information Protection を準備、実装、管理するには、これらの手順に従ってください。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8c82535a9173f59910e4b382c696c81f16ba5019
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298259"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Azure Information Protection デプロイ ロードマップ

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

> [!TIP]
> または、次のいずれかの記事を検索することもできます。
> - [Azure Information Protection を使用する一般的なシナリオに関する攻略ガイド](how-to-guides.md)
>- [Azure Information Protection リリースロードマップ](information-support.md#information-about-new-releases-and-updates)

次のロードマップページの手順を推奨事項として使用して、組織の Azure Information Protection を準備、実装、および管理することができます。

## <a name="identify-your-deployment-roadmap"></a>デプロイ ロードマップを特定する

AIP を展開する前に、 [AIP のシステム要件](./requirements.md)を確認してください。

次に、組織のニーズと[サブスクリプション](https://azure.microsoft.com/pricing/details/information-protection/)に応じて、次のいずれかのロードマップを選択します。

- **分類、ラベル付け、保護を使用**します。

    サポートサブスクリプションをご利用のお客様にお勧めします。 その他の機能として、機密情報の検出、分類用のドキュメントや電子メールのラベル付けなどがあります。 

    ラベルは保護を適用して、ユーザーにとってこの手順を簡略化することもできます。 

    このロードマップは、クラシッククライアントで作成された AIP ラベルと、統一された[ラベル付けプラットフォーム](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)を使用する機密ラベルの両方でサポートされています。

    詳細については、「 [AIP ロードマップによるデータの分類、ラベル付け、保護」を](deployment-roadmap-classify-label-protect.md)参照してください。

- **保護のみを使用する**: 

    分類とラベルの両方をサポートしていないが、ラベルのない保護をサポートするサブスクリプションをお持ちのお客様にお勧めします。 クラシッククライアントがインストールされている必要があります。

    詳細については、「 [AIP のデータ保護のロードマップ](deployment-roadmap-protect-only.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

Azure Information Protection を展開するときに、[よく寄せられる質問](faqs.md)と、その他のリソースの[情報とサポート](information-support.md)に関するページを確認すると役立つ場合があります。