---
title: クイックスタート - Azure Information Protection (AIP) 統合ラベル付けクライアントのデプロイ
description: Azure Information Protection (AIP) 統合ラベル付けクライアントのデプロイに関する簡単な概要
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 74999f960b13c64cd16891060f373d669ac90bab
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240803"
---
# <a name="quickstart-deploying-the-azure-information-protection-aip-unified-labeling-client"></a>クイック スタート: Azure Information Protection (AIP) 統合ラベル付けクライアントのデプロイ

>***適用対象**:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***関連する内容**:[Windows 用の Azure Information Protection 統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection (AIP) 統合ラベル付けクライアントは、[Microsoft Information Protection](/microsoft-365/compliance/information-protection) ソリューションの一部であり、これによって、Microsoft 365 で提供される秘密度ラベル用の組み込み機能が拡張されます。 

このクライアントには、Office アプリケーションに加えて、エクスプローラーと PowerShell でのラベル付けおよび保護のエンドユーザー サポートが用意されています。 統合ラベル付けクライアントに付属するスキャナーを使用すると、管理者はネットワークやコンテンツ共有をスキャンして機密コンテンツを検索できます。 

情報保護プラットフォームを備えていない組織の場合は、Microsoft Information Protection を使用して他の組織が保護しているコンテンツに対するビューアーがこのクライアントによって提供されます。

## <a name="review-aip-client-prerequisites"></a>AIP クライアントの前提条件を確認する

以下のリンク先の記事を参照すれば、組織内で Azure Information Protection 統合ラベル付けをデプロイするための前提条件を容易に把握できます。

- **[Azure Information Protection の要件](requirements.md)** 。 Azure Information Protection サブスクリプションや Azure Active Directory など、組織に AIP クライアントをデプロイするためのシステム要件を詳細に説明します。 また、サポートされているクライアント デバイスとサポートされているアプリケーションの一覧も示します。

- **[統合ラベル付けクライアントの要件](./rms-client/reqs-ul-client.md)** 。 AIP クライアントがインストールされるコンピューターごとのシステム要件を一覧にします。

## <a name="install-the-aip-client"></a>AIP クライアントをインストールする

AIP には、次のクライアント インストール オプションが用意されています。

- **[.exe ファイルをダウンロードして実行する。](rms-client/clientv2-admin-guide-install.md#install-the-aip-unified-labeling-client-using-the-executable-installer)** このインストールは、ほとんどのユース ケースで推奨されるオプションです。 インストールは、対話形式でもサイレント モードでも実行することができます。

    インストールが完了すると、コンピューターまたは Office ソフトウェアの再起動を求めるメッセージが表示される場合があります。 必要に応じて再起動して続行します。

- **[.msi ファイルをダウンロードして実行する。](rms-client/clientv2-admin-guide-install.md#install-the-unified-labeling-client-using-the-msi-installer)** グループ ポリシー、構成マネージャー、Microsoft Intune など、一元的なデプロイ メカニズムを使用するサイレント インストールの場合にサポートされます。

AIP クライアント インストール ファイルは、[Microsoft ダウンロード サイト](https://www.microsoft.com/download/details.aspx?id=53018)から入手できます。 

詳細については、「[管理者ガイド:ユーザー向けに Azure Information Protection 統合ラベル付けクライアントをインストールする](rms-client/clientv2-admin-guide-install.md)」を参照してください。

> [!TIP]
> AIP クライアントで利用可能な最新の機能をテスト実行するには、テスト システムにパブリック プレビュー バージョンをデプロイしてください。 詳細については、AIP 統合ラベル付けクライアントの[バージョン リリース履歴](rms-client/unifiedlabelingclient-version-release-history.md)を参照してください。
> 

## <a name="next-steps"></a>次のステップ

Azure Information クライアントの使用を開始するには、以下のクイックスタートおよびチュートリアルのいずれかを参照してください。

- [チュートリアル:Azure Information Protection (AIP) 統合ラベル付けスキャナーのインストール](tutorial-install-scanner.md)
- [チュートリアル: Azure Information Protection (AIP) スキャナーを使用して機密コンテンツを検出する](tutorial-scan-networks-and-content.md)
- [チュートリアル: Azure Information Protection (AIP) を使用した過剰共有の防止](tutorial-preventing-oversharing.md)
- [チュートリアル: Azure Information Protection (AIP) クラシック クライアントから統合ラベル付けクライアントへの移行](tutorial-migrating-to-ul.md) 

**関連項目**:

- [既知の問題 - Azure Information Protection](known-issues.md) 
- [Azure Information Protection に関してよく寄せられる質問](faqs.md) 
- [管理者ガイド: Azure Information Protection 統合ラベル付けクライアントのカスタム構成](rms-client/clientv2-admin-guide-customizations.md)        
