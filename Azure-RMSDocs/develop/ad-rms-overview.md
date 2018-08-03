---
title: 概要 - RMS SDK 2.1 | Azure RMS
description: Rights Management サービス (RMS) は、デジタル情報を権限のない使用から保護するために役立つ情報保護テクノロジです。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: B546B6C1-ADC1-4EBD-95E2-B4A74E4E980B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 3557dbf0d9f659bb5ffebd9afb4d4ef69e749985
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39370754"
---
# <a name="overview"></a>概要

Rights Management サービス SDK 2.1 は、デジタル情報を権限のない使用から保護するために役立つ情報保護テクノロジです。 コンテンツの所有者は、権限を有効にしたアプリケーションを通じて、そのコンテンツを開く、変更する、印刷する、転送する、などの操作を実行できるユーザーを定義することができます。

AD RMS は、[サーバー](ad-rms-server.md) コンポーネントと[クライアント](ad-rms-client.md) コンポーネントの両方で構成されます。 Azure または Windows Server で実行されるサーバーは、複数の Web サービスで構成されます。

[クライアント](ad-rms-client.md) コンポーネントは、クライアントまたはサーバーのオペレーティング システムで実行でき、アプリケーションでコンテンツの暗号化と復号化、テンプレートと失効リストの取得、サーバーからのライセンスと証明書の入手、およびその他の関連する権限管理タスクを有効にする機能が含まれています。

詳細については、「[Application types](application-types.md)」 (アプリケーションの種類) を参照してください。

Rights Management サービス SDK 2.1 に基づいて構築したアプリケーションを適用できるシナリオの一部を次に示します。

-   機密情報を含む電子メール メッセージを印刷または転送されないようにすることを望む法律事務所。
-   パスワードを使用することなく、描画のアクセスを研究部門内の小規模のユーザー グループに制限することを希望する CAD/CAM ソフトウェアの開発者。
-   1 つのライセンスを使用して、イメージの低解像度のコピーは無料で表示できるが、高解像度のコピーを表示する場合は支払いを求めるようにすることを望む、グラフィック デザインの Web サイト所有者。
-   ユーザーの ID に基づいて、ドキュメントの表示、印刷、または編集の権限を有効にすることを望むオンライン ドキュメント ライブラリの所有者。
-   表示と編集の権限を特定のユーザーに制限する社内の Web サイトに従業員の機密情報を公開することを望む企業。

AD RMS サーバー、AD RMS クライアントおよびそれらの機能の詳細については、[AD RMS の IT Pro ドキュメント](https://TechNet.Microsoft.Com/library/cc771234.aspx)に関する TechNet のコンテンツを参照してください。

このセクションの残りのトピックでは、RMS アーキテクチャとその実装について説明します。

## <a name="in-this-section"></a>このセクションの内容

| トピック | 説明 |
|-------|-------------|
|[クライアント](ad-rms-client.md) |このトピックでは、Rights Management Service Client 2.1 の用途と機能について説明します。 |
|[サーバー](ad-rms-server.md) | このトピックでは、Azure と Windows Server を対象に、RMS サーバーの目的と機能について説明します。|


## <a name="related-topics"></a>関連項目

* [RMS の概念](application-types.md)
* [作業開始](getting-started-with-ad-rms-2-0.md)
* [AD RMS の IT Pro ドキュメント](https://technet.microsoft.com/library/cc771234.aspx)
