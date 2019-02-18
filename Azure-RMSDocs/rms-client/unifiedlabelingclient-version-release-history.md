---
title: Azure Information Protection 統合ラベル付けクライアント - バージョン リリース情報
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/23/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 939ae3e367b14f722c38be023c70d9dcce21004f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254834"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Azure Information Protection 統合ラベル付けクライアント:バージョン リリース情報

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*

> [!NOTE]
> このクライアントはプレビュー段階にあり、変更される可能性があります。 ここでは統合ラベル付けストアを使用し、Office 365 セキュリティ/コンプライアンス センターからラベルを含むポリシーをダウンロードします。 [詳細情報](/Office365/SecurityCompliance/sensitivity-labels)

Azure Information Protection 統合ラベル付けクライアントの最新プレビュー バージョンを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=57440)からダウンロードできます。

### <a name="release-information"></a>リリース情報

次の情報を使って、Azure Information Protection 統合ラベル付けクライアントの最新プレビュー情報のサポート内容を参照します。 

このクライアントは Windows コンピューターに Office アドオンとしてインストールします。また、Azure からポリシーをダウンロードする Azure Information Protection クライアントと同じ[前提条件](../requirements.md)があります。

## <a name="current-preview-version"></a>現在のプレビュー バージョン

**リリース日**: 2018 年 10 月 16 日

Windows 用 Azure Information Protection 統合ラベル付けクライアントのこのプレビュー バージョンでは、次の機能をサポートします。 

- Azure Information Protection クライアントからのアップグレード

- Word、Excel、PowerPoint、Outlook に分類と保護を適用する手動のラベル付け。

- 視覚的なマーキング (ヘッダー、フッター、透かし)

- 既定のラベル付け 

- 転送不可を適用するラベル

- ユーザーが機密レベルを下げるかどうかを確認する理由のメッセージ

- 設定のリセットとログのエクスポートを含む、ヘルプとフィードバックのダイアログ ボックス

- 4 時間ごとのセキュリティ/コンプライアンス センターからのポリシーの更新 (Office アプリごとに)。

次の機能はこのプレビュー バージョンでは実行できません。

- 自動分類と推奨される分類

- カスタムのアクセス許可

- 保護されたテキストとイメージ ファイル、保護された PDF ファイル、一般的に保護されているファイル用のビューアー

- エクスプローラーでの右クリック アクションによるファイルの分類と保護

- PowerShell コマンドでのコマンド ラインからのファイルの分類と保護

- スキャナーによるオンプレミスのデータ ストアでの検出、ラベル付け、保護

- 英語以外の言語のサポート

## <a name="instructions"></a>手順

1. 次の指示に従ってクライアントをインストールします。[ユーザー ガイド:Azure Information Protection クライアント (プレビュー) をダウンロードしてインストールする](install-unifiedlabelingclient-app.md) 

2. Office リボンのボタンが **[保護]** ではなく、**[機密度]** という名前の場合を除き、Azure Information Protection クライアントで行うように Office アプリでそのクライアントを使用します。
    
    - [ファイルや電子メールを分類する](client-classify.md) 
    
    - [ファイルや電子メールを分類して保護する](client-classify-protect.md)

3. 操作の共有 
    
    - このプレビュー クライアントについてフィードバックを提供したり、質問するには、[Azure Information Protection 用の Yammer サイト](https://www.yammer.com/AskIPTeam)に関するページを使用してください。
    
    - このプレビュー クライアントでの問題を報告するには、リボンの **[機密度]** ボタンから **[ヘルプとフィードバック]** を使用します。 ダイアログ ボックスから、ログをエクスポートして、**[問題の報告]** オプションで作成される電子メールにこれらのログ ファイルを添付してください。 

