---
title: Azure Information Protection 統合ラベル付けクライアント - バージョン リリース情報
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 7eb7ffd98651ed35be7ecd8043e49c1d15a65e8e
ms.sourcegitcommit: 8da0aa8f9bb9f91375580a703682d23a81a441bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2019
ms.locfileid: "58809711"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Azure Information Protection 統合ラベル付けクライアント:バージョン リリース情報

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*

> [!NOTE]
> このクライアントはプレビュー段階にあり、変更される可能性があります。 ここでは統合ラベル付けストアを使用し、次の管理センターからラベルを含むポリシーをダウンロードします: Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センター。 [詳細情報](/Office365/SecurityCompliance/sensitivity-labels)

Azure Information Protection 統合ラベル付けクライアントの最新プレビュー バージョンを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=57440)からダウンロードできます。

### <a name="release-information"></a>リリース情報

次の情報を使って、Azure Information Protection 統合ラベル付けクライアントの最新プレビュー情報のサポート内容を参照します。

このクライアントでは、Windows コンピューター用の Office アドオン、エクスプローラー用の拡張機能、および PowerShell モジュールがインストールされます。 このクライアントには、Azure からポリシーをダウンロードする Azure Information Protection クライアントと同じ[前提条件](../requirements.md)があります。

Azure Information Protection クライアントと機能を比較するには、「[クライアントの機能比較](use-client.md#feature-comparisons-for-the-clients)」をご覧ください。

## <a name="current-preview-version"></a>現在のプレビュー バージョン

**リリース日**: 2019 年 2 月 25 日

Windows 用 Azure Information Protection 統合ラベル付けクライアントのこのプレビュー バージョンでは、次の機能をサポートします。 

- Azure Information Protection クライアントからのアップグレード。

- 手動、自動、および推奨ラベル付け:このクライアントの自動ラベル付けおよび推奨ラベル付けを構成する方法について詳しくは、「[機密ラベルをコンテンツに自動的に適用する](/Office365/SecurityCompliance/apply_sensitivity_label_automatically)」をご覧ください。

- エクスプローラー、右クリック アクションによるファイルの分類と保護、保護の削除、およびカスタムのアクセス許可の適用。

- 保護されたテキストとイメージ ファイル、保護された PDF ファイル、一般的に保護されているファイル用のビューアー。

- 次を実行するための PowerShell コマンド:
    - [ドキュメント上のラベルを設定または削除する](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [内容を検査してからドキュメントをラベル付けする](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [ドキュメントに適用されているラベル情報を読み取る](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [無人の PowerShell セッションをサポートするために認証する](/powershell/module/azureinformationprotection/set-aipauthentication)

- [Azure Information Protection 分析](../reports-aip.md)を使った中央レポート機能のサポート。

- 次のラベルおよびポリシー設定:
    - 視覚的なマーキング (ヘッダー、フッター、透かし)
    - 既定のラベル付け
    - 転送不可を適用し、Outlook でのみ表示されるラベル
    - ユーザーが分類レベルを下げるかどうか、またはラベルを削除するかどうかを確認する理由プロンプト
    - ラベルの色

- 管理センターからのポリシー更新:
    - Office アプリの起動ごと、および 4 時間ごと
    - 右クリックしてファイルまたはフォルダーを分類して保護したとき
    - ラベル付けと保護のために PowerShell コマンドレット を実行したとき

- 設定のリセットとログのエクスポートを含む、ヘルプとフィードバックのダイアログ ボックス。

### <a name="features-that-do-not-work-in-this-preview-version-or-are-not-available"></a>このプレビュー バージョンでは機能しない、または使用できない機能

主な機能:

- オンプレミスのデータ ストア上のファイルを検出、ラベル付け、保護するためのスキャナーは使用できません。

- Azure portal から移行され、HYOK 保護用に構成されたラベルは、公開されるとクライアントに表示されますが、これらのラベルでは保護が適用されません。

- AzureInformationProtection モジュールのコマンドレットの完全なセットは使用できません。これには保護サービスに直接接続するコマンドレットが含まれます。 たとえば、ファイルを一括で保護解除する、Unprotect-RMSFile です。

完全な詳細については、[比較表](use-client.md#feature-comparisons-for-the-clients)をご覧ください。

## <a name="instructions"></a>手順

1. 次の指示に従ってクライアントをインストールします。[ユーザー ガイド:Azure Information Protection クライアント (プレビュー) をダウンロードしてインストールする](install-unifiedlabelingclient-app.md) 

2. Azure Information Protection クライアントの場合と同じようにクライアントを使いますが、Office アプリに関して次の例外があります。
    - Office リボン上のボタンの名前は、**[保護]** ではなく **[秘密度]** です。
    - 管理者は、既定で Information Protection バーを表示することができません。ただし、ユーザーは、**[秘密度]** ボタンから **[バーの表示]** を選択することでこれを表示できます。 
    - カスタムのアクセス許可は使用できません
    - 追跡と取り消しは使用できません
    
    ユーザーの手順について:
    
    - [ファイルや電子メールを分類する](client-classify.md) 
    
    - [ファイルや電子メールを分類して保護する](client-classify-protect.md)

3. 操作の共有 
    
    - このプレビュー クライアントについてフィードバックを提供したり、質問するには、[Azure Information Protection 用の Yammer サイト](https://www.yammer.com/AskIPTeam)に関するページを使用してください。
