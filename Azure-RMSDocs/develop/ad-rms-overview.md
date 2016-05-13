---
# required metadata

title: 概要 | Azure RMS
description: Rights Management サービス (RMS) は、デジタル情報を権限のない使用から保護するために役立つ情報保護テクノロジです。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a58894d5-3271-46d7-bb1c-fbd22eae8530

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 概要

Rights Management サービス (RMS) は、デジタル情報を権限のない使用から保護するために役立つ情報保護テクノロジです。 コンテンツの所有者は、権限を有効にしたアプリケーションを通じて、そのコンテンツを開く、変更する、印刷する、転送する、などの操作を実行できるユーザーを定義することができます。

## 概要

AD RMS は、[サーバー](ad-rms-server.md) コンポーネントと[クライアント](ad-rms-client.md) コンポーネントの両方で構成されます。 サーバー コンポーネントには、Windows Server 2008 R2 など、Windows Server 上で実行される複数の Web サービスや、Azure の RMS Web サービスを通じてクラウド経由で実行される Web サービスが含まれます。 クライアント コンポーネントは、クライアントまたはサーバーのオペレーティング システムで実行でき、アプリケーションでコンテンツの暗号化と復号化、テンプレートと失効リストの取得、サーバーからのライセンスと証明書の入手、およびその他の関連する権限管理タスクを有効にする機能が含まれています。

詳細については、「[Application types (アプリケーションの種類)](application-types.md)」を参照してください。

Rights Management サービス SDK 2.1 に基づいて構築したアプリケーションを適用できるシナリオの一部を次に示します。

-   機密情報を含む電子メール メッセージを印刷または転送されないようにすることを望む法律事務所。
-   パスワードを使用することなく、描画のアクセスを研究部門内の小規模のユーザー グループに制限することを希望する CAD/CAM ソフトウェアの開発者。
-   1 つのライセンスを使用して、イメージの低解像度のコピーは無料で表示できるが、高解像度のコピーを表示する場合は支払いを求めるようにすることを望む、グラフィック デザインの Web サイト所有者。
-   ユーザーの ID に基づいて、ドキュメントの表示、印刷、または編集の権限を有効にすることを望むオンライン ドキュメント ライブラリの所有者。
-   表示と編集の権限を特定のユーザーに制限する社内の Web サイトに従業員の機密情報を公開することを望む企業。

AD RMS サーバー、AD RMS クライアントおよびそれらの機能の詳細については、[AD RMS の IT Pro ドキュメント](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)に関する TechNet のコンテンツを参照してください。

開始する方法については、「[Getting started (はじめに)](getting-started-with-ad-rms-2-0.md)」を参照してください。

## 関連項目

* [AD RMS の概念](application-types.md)
* [AD RMS と AD RMS 2.1 の違い](differences-between-ad-rms-and-ad-rms-2-0.md)
* [概要](getting-started-with-ad-rms-2-0.md)
* [AD RMS の IT Pro ドキュメント](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)
* [サーバー](ad-rms-server.md)
* [クライアント](ad-rms-client.md)
 

 





<!--HONumber=Apr16_HO3-->


