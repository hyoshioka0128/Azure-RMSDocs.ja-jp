---
title: Azure Information Protection の一般的なシナリオの手順
description: Azure Information Protection を使用して、組織のデータを分類して保護するユースケースを特定します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1a7662b0262e2c46e3b88861a967287070a5a1ed
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794082"
---
# <a name="how-to-guides-for-common-scenarios-that-use-azure-information-protection"></a>Azure Information Protection を使用する一般的なシナリオに関する操作ガイド

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection を使用して組織のドキュメントや電子メールを分類したり、必要に応じて保護したりするためには、多くの方法があります。 

展開が最も成功するのは、組織にとってビジネス上の利益が最大になる特定のユース ケースを見つけた場合です。 一般的なシナリオと手順に関する以下の一覧を使用して、展開を開始しましょう。

## <a name="common-scenarios"></a>一般的なシナリオ

|シナリオ:目的:|手順|
|----------------|---------------|
|組織がオンプレミスに格納している機密情報を検索する|[クイック スタート: オンプレミスに格納しているファイル内の機密情報を検索する](quickstart-findsensitiveinfo.md)|
|ユーザーが機密情報を含む電子メールを簡単に保護できるようにする|[クイック スタート: ラベルを構成して、ユーザーが機密情報を含む電子メールを簡単に保護できるようにする](quickstart-label-dnf-protectedemail.md)|
|ユーザーがデータを作成または編集したときに簡単に分類し、機密情報を含む場合は保護できるようにする| [チュートリアル: ポリシーを編集して新しいラベルを作成する](infoprotect-quick-start-tutorial.md)|
|ユーザーが保護されたドキュメントに対して簡単に共同作業できるようにする|[Azure Information Protection を使用したセキュアなドキュメント コラボレーションの構成](secure-collaboration-documents.md)|
|組織の外部に送信されるユーザーの電子メールを自動的に保護する| [Azure Information Protection ラベルのメール フロー ルールの構成](configure-exo-rules.md)
|オンプレミスのデータ ストアにある既存のデータを自動的に分類して保護する|[Azure Information Protection スキャナーの展開](deploy-aip-scanner.md)|
|自分のキーを使用して自分の組織のデータを保護する| [テナント キーの計画と実装](plan-implement-tenant-key.md)|
|AD RMS から移行する|[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)|

## <a name="additional-deployment-instructions"></a>デプロイの追加手順

[Azure Information Protection テクニカルブログ](https://aka.ms/AIPblog)には、最前線からの追加のガイダンスが含まれています。

たとえば、ビジネスの意思決定者や IT の実装担当者向けのベスト プラクティスを使った方法:

- [Azure Information Protection デプロイの高速化ガイド](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Deployment-Acceleration-Guide/ba-p/334423)

詳しい手順:

- [Microsoft Information Protection と Azure AD ログインデータを使用して、より豊富なレポートを作成する](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Create-richer-reports-with-Microsoft-Information-Protection-and/ba-p/392713)

- [Microsoft Cloud App Security を活用してクラウドに Azure Information Protection ラベルを適用する](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Leverage-Microsoft-Cloud-App-Security-to-apply-Azure-Information/ba-p/388638)

- [Azure Information Protection "Cloud Exit" プランを準備する方法](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631)

- [テナント間のラベルの視覚化](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cross-Tenant-Label-Visualization/ba-p/356588)

- [Using Azure Information Protection to protect PDF’s and Adobe Acrobat Reader to view them](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Using-Azure-Information-Protection-to-protect-PDF-s-and-Adobe/ba-p/282010) (Azure Information Protection を使用して PDF および Adobe Acrobat Reader を保護して表示する)

- [Cataloging your Sensitive Data with AIP, Even Before Configuring Labels!](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cataloging-your-Sensitive-Data-with-AIP-Even-Before-Configuring/ba-p/267241) (AIP を使用してラベルを構成する前に、機密データをカタログ化する)

- [Azure Information Protection Scanner Express Installation](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Scanner-Express-Installation/ba-p/265424) (Azure Information Protection スキャナーの簡易インストール)

- [Discovery of Sensitive Data Using the AIP Scanner (AIP Premium P1)](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discovery-of-Sensitive-Data-Using-the-AIP-Scanner-AIP-Premium-P1/ba-p/252040) (AIP スキャナーを使用した機密データの検出 (AIP Premium P1))

## <a name="next-steps"></a>次の手順

目的のシナリオが見つかりませんでしたか。 計画と展開の手順に関する完全な一覧については、[デプロイ ロードマップ](deployment-roadmap.md)を参照してください。

Azure Information Protection を使用した経験がない場合は、ご自身の展開を開始する前に、サービスの概略を説明した「[Azure Information Protection とは](what-is-information-protection.md)」をご覧ください。
