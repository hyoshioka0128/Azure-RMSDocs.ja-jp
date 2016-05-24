---
# required metadata

title: 概要 | Azure RMS
description: RMS SDK 2.1 プラットフォームを使用すると、開発者は RMS 情報保護を利用するアプリケーションを作成できます。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 概要

Rights Management サービス SDK 2.1 プラットフォームを使用すると、開発者は RMS 情報保護を利用するアプリケーションを作成できます。 このプラットフォームでは、キー管理、暗号化、復号化処理などの複雑なセキュリティ プラクティスを処理し、容易なアプリケーション開発のために簡略化された API を提供します。

## RMS SDK 2.1 の概要

以下のセクションをお読みください。

-   コンテンツの保護に RMS SDK 2.1 を使用する理由
-   基本原則

これらのトピックのガイダンスに従って、RMS SDK 2.1 を使用してみてください。

-   [SDK のインストール](create-your-first-rights-aware-application.md)
-   [権限保護対応アプリケーションのテスト](running-your-first-application.md)
-   [IPCHelloWorld - サンプル アプリケーション](how-to-build-your-first-application.md)

開始したら、他のいくつかの [RMS サンプル](samples.md)を確認してください。 その後は、「[RMS 開発者のコーナー](http://blogs.msdn.com/b/rms/)」で最新情報を入手ください。

### コンテンツの保護に RMS SDK 2.1 を使用する理由

RMS のサポートを新規および既存のアプリケーションに追加する開発者に向けて、RMS SDK 2.1 は、次の作業を簡略化します。

-   管理しやすく、規制に準拠した、堅牢な RMS 対応アプリケーションを作成する
-   ユーザー データを永続的に暗号化する 環境、デバイス、またはオペレーティング システムに関係なくデータの暗号化を維持する
-   機密データの画面キャプチャの防止など、さまざまな使用制限を適用する
-   企業が管理する保護ポリシーをサポートする
-   新しい認証メカニズムや暗号化アルゴリズムの登場と同時にサポートする

RMS SDK 2.1 では、重要なクライアントおよびサーバー プラットフォームを幅広くサポートします。 詳細については、「[サポートされているプラットフォーム](supported-platforms.md)」を参照してください。

## 基本原則

**簡略化** - AD RMS SDK 1.0 のフィードバックと使用状況パターンを分析し、そのデータを最も困難なプログラミング タスクを簡略化または自動化するために使用しました。 通常、RMS SDK 2.1 を使用して作成する RMS アプリケーションに必要な RMS コードの行数は、AD RMS SDK 1.0 を使用して記述された RMS アプリケーションよりも 5 ～ 10 倍少なくなります。
**1 回の記述** - RMS SDK 2.1 アプリケーションでは、最新の RMS 機能を使用するためにコードの変更や再コンパイルは必要ありません。 RMS の新機能は、RMS サーバーに追加されるとすぐに既存のアプリケーションで使用可能になります。
**一貫性** - RMS SDK 2.1 により、さまざまな RMS 構成に一貫して従うアプリケーションを記述しやすくなります。 アプリケーション開発者が作成する必要のある RMS ユーザー インターフェイスの量が大幅に減少するので、ルック アンド フィールの一貫性が強化され、ユーザー教育の必要性を減らすこともできます。

## 関連項目

* [AD RMS samples (AD RMS サンプル)](samples.md)
* [AD RMS 開発者のコーナー](http://blogs.msdn.com/b/rms/)
* [SDK のインストール](create-your-first-rights-aware-application.md)
* [IPCHelloWorld - サンプル アプリケーション](how-to-build-your-first-application.md)
* [概要](ad-rms-overview.md)
* [サポートされているプラットフォーム](supported-platforms.md)
* [権限保護対応アプリケーションのテスト](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO4-->


