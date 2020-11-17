---
title: Azure Information Protection (AIP) とは
description: Azure Information Protection (AIP) を使用すると、Microsoft Information Protection (MIP) フレームワークを拡張して、Microsoft 365 によって提供されるラベル付けおよび分類の機能を拡張することができます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to extend Microsoft 365's labeling and classification functionality to the File Explorer, PowerShell, third party apps and services, and more.
ms.custom: contperfq1
search.appverid:
- MET150
ms.openlocfilehash: 5167d790c557661181b03f90055dfc75b0b1cf72
ms.sourcegitcommit: 1086cf04a29bb12cdb25c1fd8429f93d423bcc69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94379264"
---
# <a name="what-is-azure-information-protection"></a>Azure Information Protection とは

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection (AIP) はクラウドベースのソリューションです。これにより、組織はコンテンツにラベルを適用してドキュメントや電子メールの検出、分類、および保護を行うことができます。

AIP は、Microsoft Information Protection (MIP) ソリューションの一部です。これにより、Microsoft 365 で提供されるラベル付けおよび分類の機能が拡張されます。

次の図に、MIP に追加された Azure Information Protection を示します。これには、[統合ラベル付けクライアント](#aip-unified-labeling-client)、[スキャナー](#aip-on-premises-scanner)、[SDK](#microsoft-information-protection-sdk) が含まれます。

:::image type="content" source="media/what-is-mip.png" alt-text="Microsoft Information Protection フレームワークの Azure Information Protection 領域":::

Microsoft Information Protection は、AIP 統合ラベル付けクライアントによって活用される共通の情報保護スタックです。 詳細については、[Microsoft 365 のドキュメント](/microsoft-365/compliance/protect-information)を参照してください。

## <a name="aip-unified-labeling-client"></a>AIP 統合ラベル付けクライアント

Azure Information Protection 統合ラベル付けクライアントにより、ラベル付け、分類、保護の各機能の対象が追加のファイルの種類に、さらにエクスプローラーおよび PowerShell にまで拡張されます。 

たとえば、エクスプローラーで、1 つまたは複数のファイルを右クリックし、 **[分類して保護する]** を選択すると、選択されたファイルに対する AIP 機能を管理できます。

:::image type="content" source="media/protect-from-file-explorer.png" alt-text="エクスプローラーから分類して保護する":::

統合ラベル付けクライアントの最新機能およびパブリック プレビュー バージョンの詳細については、「[Azure Information Protection 統合ラベル付けクライアント - バージョン リリース履歴とサポート ポリシー](rms-client/unifiedlabelingclient-version-release-history.md)」を参照してください。

このクライアントは、[Microsoft Azure Information Protection ダウンロード ページ](https://www.microsoft.com/download/details.aspx?id=53018)からダウンロードできます。
    
## <a name="aip-on-premises-scanner"></a>AIP オンプレミス スキャナー

Azure Information Protection オンプレミス スキャナーを使用すると、管理者は自分のネットワークおよびファイル共有をスキャンして、ラベル付け、分類、保護を必要とする機密コンテンツを検索することができます。

オンプレミス スキャナーは、統合ラベル付けクライアントの一部として提供されている PowerShell コマンドレットを使用してインストールします。そして、PowerShell、および Azure portal の Azure Information Protection 領域を使用して管理することができます。

たとえば、Azure portal に表示されるスキャナー データを使用すれば、ご利用のネットワーク上で、危険にさらされる機密コンテンツを含んでいる可能性のあるリポジトリを見つけることができます。

:::image type="content" source="media/risky-repos-small.png" alt-text="危険なリポジトリがないか、スキャンされたネットワークを調べる" lightbox="media/risky-repos.png":::

詳細については、次を参照してください。

- [AIP の統合ラベル付けスキャナーとは](deploy-aip-scanner.md)
- [AIP 統合ラベル付けクライアント - バージョン リリース履歴](rms-client/unifiedlabelingclient-version-release-history.md)のスキャナー セクション

スキャナーのインストールは、クライアントと共に [Microsoft Azure Information Protection ダウンロード ページ](https://www.microsoft.com/download/details.aspx?id=53018)からダウンロードできます。


## <a name="microsoft-information-protection-sdk"></a>Microsoft Information Protection SDK

Microsoft Information Protection SDK により、機密ラベルの対象がサードパーティのアプリおよびサービスまで拡張されます。 開発者は SDK を使用して、ファイルにラベルと保護を適用するためのネイティブ サポートを構築することができます。

たとえば、次の場合に MIP SDK を使用できます。

- エクスポート時に分類ラベルをファイルに適用する基幹業務アプリケーション。
- CAD/CAM 設計プリケーションが、Microsoft Information Protection のラベル作成に対して、ネイティブ サポートを提供する。
- Cloud Access Security Broker またはデータ損失防止ソリューションが、Azure Information Protection で暗号化されたデータに対して推論する。

詳細については、[Microsoft Information Protection SDK の概要](/information-protection/develop/overview)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

**AIP の使用を開始するには、** 統合ラベル付けクライアントとスキャナーをダウンロードしてインストールします。

- [無料評価版にサインアップする](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)  (Enterprise Mobility + Security E5)
- [クライアントのダウンロード](https://www.microsoft.com/download/details.aspx?id=53018)
- [クイック スタート: 統合ラベル付けクライアントのデプロイ](quickstart-deploy-client.md)

以下の最初のチュートリアルを使用して、**AIP について理解を深めます**。

- [チュートリアル:Azure Information Protection (AIP) 統合ラベル付けスキャナーのインストール](tutorial-install-scanner.md)
- [チュートリアル: Azure Information Protection (AIP) スキャナーを使用して機密コンテンツを検出する](tutorial-scan-networks-and-content.md)
- [チュートリアル: Azure Information Protection (AIP) を使用した Outlook での過剰共有の防止](tutorial-preventing-oversharing.md)

**AIP をさらにカスタマイズする準備ができたら**、「[管理者ガイド: Azure Information Protection 統合ラベル付けクライアントのカスタム構成](rms-client/clientv2-admin-guide-customizations.md)」を参照してください。

**MIP SDK の使用を開始するには**、「[Microsoft Information Protection (MIP) SDK のセットアップと構成](/information-protection/develop/setup-configure-mip)」を参照してください。

### <a name="additional-resources"></a>その他のリソース

|リソース  |リンクと説明  |
|---------|---------|
|**サブスクリプションのオプションと価格**     |    [Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)     |
|**FAQ と既知の問題**     | [Azure Information Protection に関してよく寄せられる質問](faqs.md) </br> [既知の問題 - Azure Information Protection](known-issues.md)       |
|**サポート オプション**     | [Azure Information Protection のサポート オプション](information-support.md)        |
|**Yammer**     |  [Azure Information Protection](https://www.yammer.com/AskIPTeam)       |
|**Ignite 2020**     |  - [クラウド、オンプレミス、エンドポイント、およびリモート ワークの環境にわたって情報の保護と統制を強化する](https://myignite.microsoft.com/sessions/ceba117f-9bc7-4426-9ebc-753d94c6a476)</br>- [インテリジェントなデータ保護およびコンプライアンス ソリューションを使用してリスク管理のヒーローになる](https://myignite.microsoft.com/sessions/9a1e2716-55f5-4c3e-8626-0cb77e60eb87)</br>- [Microsoft Information Protection でデータの把握、保護を行い、データ損失を防ぐ](https://myignite.microsoft.com/sessions/46ff69cf-2c8f-4e61-a923-f72f5740f02f)</br>- [エキスパートに質問する: 情報保護と統制、インサイダー リスク、コンプライアンス管理など、Microsoft コンプライアンスに関することを何でも質問してください。](https://myignite.microsoft.com/sessions/5ce48b36-9827-4d60-8540-90546333063d)       |
|**新機能**     | Microsoft 365 および SharePoint 管理センターでの AIP に関連する新機能については、以下をご覧ください。   </br>- [Microsoft 365 管理センターの新機能](/microsoft-365/admin/whats-new-in-preview) </br>- [SharePoint 管理センターの新機能](/sharepoint/what-s-new-in-admin-center)     |
|     |         |

## <a name="aips-classic-client"></a>AIP のクラシック クライアント

Azure Information Protection クラシック クライアントは、AIP の以前のバージョンで、管理者は Azure portal 内で分類ラベルを直接管理することができます。

Azure portal 内で管理される AIP ラベルは、統合ラベル付けプラットフォームではサポート "*されず*"、Azure Information Protection クライアントおよびスキャナーと、Microsoft Cloud App Security での使用に限定されています。 

これらの機能に加えて、SharePoint、Microsoft 365 アプリ、Web およびモバイル デバイス用 Outlook、PowerBI データ保護などをサポートする統合ラベルに移行することをお勧めします。 詳細については、「[チュートリアル:  Azure Information Protection (AIP) クラシック クライアントから、統合ラベル付けクライアントへの移行](tutorial-migrating-to-ul.md)」を参照してください。

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と **ラベル管理** は、**2021 年 3 月 31 日** で **非推奨** になります。 
>
> このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けソリューションを使用する統一されたラベル付けに移行することができます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。
