---
title: Azure Information Protection クライアント-バージョン履歴 & サポートポリシー
description: Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点、サポートのライフサイクル ポリシーについて説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1a51376fc2d6114f7d23ec937b4d8ea1238d1655
ms.sourcegitcommit: 2cb5fa2a8758c916da8265ae53dfb35112c41861
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88953237"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure Information Protection クライアント: バージョン リリース履歴とサポート ポリシー


>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> *手順:[Windows 用 Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

> [!TIP]
> ラベルが Office 365 セキュリティ & コンプライアンスセンター、Microsoft 365 security Center、または Microsoft 365 コンプライアンスセンターから公開されているため、Azure Information Protection 統合ラベルクライアントの使用に関心がある場合は、 Microsoft ダウンロードセンターから、統合されたラベル付けクライアントをダウンロードしてインストールすると、Azure Information Protection クライアントを、統一された [ラベル付けクライアント](unifiedlabelingclient-version-release-history.md)にアップグレードできます。

**AIP クラシック クライアントをデプロイするには**、サポート チケットを作成してダウンロード アクセスを取得します。

詳細については、「[Azure Information Protection クライアントのアップグレードと保守](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)」をご覧ください。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection クライアントの各一般公開 (GA) バージョンは、後続の GA バージョンがリリースされた後も最長で 6 か月間はサポートされます。 このセクションを除き、ドキュメントにはサポートされていないバージョンのクライアントに関する情報は含まれていません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン:

|クライアントのバージョン|リリース日|
|--------------|-------------|
|1.53.10|07/15/2019|
|1.48.204.0|04/16/2019|
|1.41.51.0|2018 年 11 月 27 日|
|1.37.19.0|2018 年 9 月 17 日|
|1.29.5.0|2018 年 6 月 26 日|
|1.27.48.0|2018 年 5 月 30 日|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|03/15/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|10/27/2016|
|1.1.23.0|10/01/2016|

このページで使用される日付形式は、 *月/日/年*です。

6/2/2019 以降、Azure Information Protection のラベル付けサービスには、TLS 1.2 を使用する接続が必要です。

1.4.21.0 リリース03/15/2017 のすべてのクライアントバージョンが TLS 1.2 をサポートしています。 クライアントバージョン **1.3.155.2**、 **1.2.4.0**、および **1.1.23.0** は TLS 1.2 を使用しないため、Azure Information Protection ポリシーをダウンロードできなくなります。

### <a name="release-history"></a>リリース履歴

Windows 用 Azure Information Protection クライアントのサポートされているリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、最新の GA リリースで問題が修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="version-154590"></a>バージョン1.54.59.0

**リリース**日: 12/02/2020

このバージョンには、修正プログラムのみが含まれています。 

**修正内容**:

- 保護が削除された後に、IQP によって保護されているファイルが [ **回復** ] オプションまたは [保存] オプションを選択 **して** 解決される問題。 

- わかりやすく、理解しやすいように、多くの製品機能のツールヒントが改善されました。 

- 保護された PDF ファイルを操作するときに、クライアントの安定性に関連する問題が解決されます。 

- 電子メールの作成プロセス中に電子メールでラベルが削除されると、保護ラベルが期待どおりに削除されるようになりました。 

## <a name="version-154330"></a>バージョン1.54.33.0

**リリース**日: 10/23/2019

08/12/2020 でサポート

このバージョンには、RMS クライアントの MSIPC バージョン1.0.4008.0813 が含まれています。

このリリースには、安定性とパフォーマンスに関する一般的な修正が含まれています。

## <a name="next-steps"></a>次のステップ

インストールするクライアントが適切かどうかは確認できません。  「 [Windows コンピューターに使用するラベル付けクライアントを選択](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)する」を参照してください。

クライアントのインストールと使用の詳細: 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)
