---
title: Azure Information Protection classic クライアント-バージョン履歴 & サポートポリシー
description: Azure Information Protection クラシッククライアントのリリースの新機能と変更点、およびサポートのライフサイクルポリシーについて説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: def8ba403e961f6e64b0bd34eb5c7ac5bd50632a
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807077"
---
# <a name="azure-information-protection-classic-client-version-release-history-and-support-policy"></a>クラシッククライアントの Azure Information Protection: バージョンリリース履歴とサポートポリシー


>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、「 [クライアントのバージョン履歴の統合](unifiedlabelingclient-version-release-history.md)」を参照してください。

> [!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure Portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

**AIP クラシック クライアントをデプロイする** には、サポート チケットを作成してダウンロードへのアクセスを取得します。

詳細については、「[Azure Information Protection クライアントのアップグレードと保守](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)」をご覧ください。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection クライアントの各一般公開 (GA) バージョンは、後続の GA バージョンがリリースされた後も最長で 6 か月間はサポートされます。 このセクションを除き、ドキュメントにはサポートされていないバージョンのクライアントに関する情報は含まれていません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン:

|クライアントのバージョン|リリース日|
|--------------|-------------|
|1.54.33.0 | 2019/10/23|
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

このページで使用される日付形式は、 *月/日/年* です。

6/2/2019 以降、Azure Information Protection のラベル付けサービスには、TLS 1.2 を使用する接続が必要です。

1.4.21.0 リリース03/15/2017 のすべてのクライアントバージョンが TLS 1.2 をサポートしています。 クライアントバージョン **1.3.155.2**、 **1.2.4.0**、および **1.1.23.0** は TLS 1.2 を使用しないため、Azure Information Protection ポリシーをダウンロードできなくなります。

### <a name="release-history"></a>リリース履歴

次の情報を使用して、サポートされている Windows 用 Azure Information Protection クラシッククライアントのリリースの新機能と変更点を確認してください。 最新のリリースは一番上に表示されます。

現時点では、Azure Information Protection 機能はプレビュー段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、最新の GA リリースで問題が修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="version-154590"></a>バージョン1.54.59.0

**リリース** 日: 02/12/2020

このバージョンには、修正プログラムのみが含まれています。 

**修正内容**:

- 保護が削除された後に、IQP によって保護されているファイルが [ **回復** ] オプションまたは [保存] オプションを選択 **して** 解決される問題。 

- わかりやすく、理解しやすいように、多くの製品機能のツールヒントが改善されました。 

- 保護された PDF ファイルを操作するときに、クライアントの安定性に関連する問題が解決されます。 

- 電子メールの作成プロセス中に電子メールでラベルが削除されると、保護ラベルが期待どおりに削除されるようになりました。 

## <a name="next-steps"></a>次のステップ

インストールするクライアントが適切かどうかは確認できません。  「 [Windows のラベル付けソリューションを選択する」を](use-client.md#choose-your-windows-labeling-solution)参照してください。

クライアントのインストールと使用の詳細: 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)
