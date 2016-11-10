---
title: "概要 | Azure RMS"
description: "RMS SDK 2.1 プラットフォームを使用すると、開発者は RMS 情報保護を利用するアプリケーションを作成できます。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 8c5b7d17b5feffa07028498e8d7f201b25626478


---
# <a name="getting-started"></a>はじめに

Rights Management サービス SDK 2.1 プラットフォームを使用すると、開発者は RMS サーバーまたは Azure RMS を介して RMS 情報保護を利用するアプリケーションを作成できます。 このプラットフォームでは、キー管理、暗号化、復号化処理などの複雑なセキュリティ プラクティスを処理し、容易なアプリケーション開発のために簡略化された API を提供します。

## <a name="get-started-with-rms-sdk-21"></a>RMS SDK 2.1 の概要

このトピックでは、テスト環境で権限保護対応アプリケーションをセットアップおよび実行するためのプロセスについて説明します。 次のトピックでは、開発環境をセットアップする方法について説明しています。これらのトピックは、推奨されるタスクの実行順序に従って紹介されています。

## <a name="in-this-sections"></a>このセクションの内容

| トピック | 説明 |
|-------|-------------|
| [リリース ノート](release-notes-rtm.md) | このトピックには、RMS SDK 2.1 のこのリリースとそれ以前のリリースに関する重要な情報が含まれています。|
| [SDK のインストール](install-the-rms-sdk.md) | このトピックでは、開発者ツールをインストールする方法について説明します。|
| [Visual Studio の構成](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md) | このトピックでは、RMS SDK 2.1 を使用するように Visual Studio プロジェクトを構成する手順について説明します。|
| [アプリケーションの開発](developing-your-application.md) | このトピックでは、RMS 対応アプリケーションの中心部分について基本的なことを説明します。独自のアプリケーションを開発する際に基礎となります。|
| [アプリケーションのテスト](how-to-set-up-your-test-environment.md) |このトピックでは、アプリケーション テストを設定する方法について説明します。|
| [運用環境にデプロイする](deploying-your-application.md) |このトピックでは、権利保護に対応したアプリケーションのデプロイ オプションについて順を追って各操作を説明します。|


これらのトピックのガイダンスに従って、RMS SDK 2.1 を使用してみてください。

- [SDK のインストール](install-the-rms-sdk.md)
- [Visual Studio の構成](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)
- [アプリケーションの開発](developing-your-application.md)
- [アプリケーションのテスト](how-to-set-up-your-test-environment.md)
- [運用環境にデプロイする](deploying-your-application.md)

### <a name="why-use-rms-sdk-21-for-protecting-your-content"></a>コンテンツの保護に RMS SDK 2.1 を使用する理由

RMS のサポートを新規および既存のアプリケーションに追加する開発者に向けて、RMS SDK 2.1 は、次の作業を簡略化します。

-   管理しやすく、規制に準拠した、堅牢な RMS 対応アプリケーションを作成する
-   ユーザー データを永続的に暗号化する 環境、デバイス、またはオペレーティング システムに関係なくデータの暗号化を維持する
-   機密データの画面キャプチャの防止など、さまざまな使用制限を適用する
-   企業が管理する保護ポリシーをサポートする
-   新しい認証メカニズムや暗号化アルゴリズムの登場と同時にサポートする

RMS SDK 2.1 では、重要なクライアントおよびサーバー プラットフォームを幅広くサポートします。 詳細については、「[サポートされているプラットフォーム](supported-platforms.md)」を参照してください。

## <a name="core-principles"></a>基本原則

**簡略化** - AD RMS SDK 1.0 のフィードバックと使用状況パターンを分析し、そのデータを最も困難なプログラミング タスクを簡略化または自動化するために使用しました。 通常、RMS SDK 2.1 を使用して作成する RMS アプリケーションに必要な RMS コードの行数は、AD RMS SDK 1.0 を使用して記述された RMS アプリケーションよりも 5 ～ 10 倍少なくなります。
**1 回の記述** - RMS SDK 2.1 アプリケーションでは、最新の RMS 機能を使用するためにコードの変更や再コンパイルは必要ありません。 RMS の新機能は、RMS サーバーに追加されるとすぐに既存のアプリケーションで使用可能になります。
**一貫性** - RMS SDK 2.1 により、さまざまな RMS 構成に一貫して従うアプリケーションを記述しやすくなります。 アプリケーション開発者が作成する必要のある RMS ユーザー インターフェイスの量が大幅に減少するので、ルック アンド フィールの一貫性が強化され、ユーザー教育の必要性を減らすこともできます。

## <a name="related-topics"></a>関連項目

* [RMS 開発者ガイド](developers-guide.md)
* [AD RMS Developer's Corner (AD RMS 開発者のコーナー)](http://blogs.msdn.com/b/rms/)

 

 



<!--HONumber=Nov16_HO1-->


