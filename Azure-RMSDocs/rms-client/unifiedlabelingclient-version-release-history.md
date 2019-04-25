---
title: 統合、azure Information Protection クライアントのバージョンをラベル付けリリース履歴とサポート ポリシー
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 1262a2f1a70002686aed0bad47354cdc5ac23bac
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180887"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>統合、azure Information Protection クライアントのバージョンをラベル付けリリース履歴とサポート ポリシー

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Azure Information Protection の統合されたラベル付けクライアントをダウンロードすることができます、 [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)します。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection の統合されたラベル付けクライアントの各一般 (公開 GA) バージョンは最大 6 か月間、後続の GA バージョンのリリース後でサポートされています。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

> [!NOTE]
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

### <a name="release-information"></a>リリース情報

次の情報を使用すると、Azure Information Protection の統合されたラベル付けクライアントの一般公開バージョンでサポートされる機能を参照してください。

このクライアントでは、Windows コンピューター用の Office アドオン、エクスプローラー用の拡張機能、および PowerShell モジュールがインストールされます。 このクライアントには、Azure からポリシーをダウンロードする Azure Information Protection クライアントと同じ[前提条件](../requirements.md)があります。

Azure Information Protection クライアントと機能を比較するには、「[クライアントの機能比較](use-client.md#compare-the-clients)」をご覧ください。

## <a name="version-20778"></a>バージョン 2.0.778

**リリース日**: 04/16/2019

この最初の一般公開バージョンの Windows 用 Azure Information Protection のクライアントを統一されたにラベル付けには、次の機能がサポートされています。 

- Azure Information Protection クライアントからのアップグレード。

- 手動、自動、および推奨ラベル付け:このクライアントの自動ラベル付けおよび推奨ラベル付けを構成する方法について詳しくは、「[機密ラベルをコンテンツに自動的に適用する](/Office365/SecurityCompliance/apply_sensitivity_label_automatically)」をご覧ください。

- エクスプローラー、右クリック アクションによるファイルの分類と保護、保護の削除、およびカスタムのアクセス許可の適用。

- 保護されたテキストとイメージ ファイル、保護された PDF ファイル、一般的に保護されているファイル用のビューアー。

- 次を実行するための PowerShell コマンド:
    - [ドキュメント上のラベルを設定または削除する](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [内容を検査してからドキュメントをラベル付けする](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [ドキュメントに適用されているラベル情報を読み取る](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [無人の PowerShell セッションをサポートするために認証する](/powershell/module/azureinformationprotection/set-aipauthentication)

- 監査を使用して中央レポートのデータとエンドポイントの検出サポート[Azure Information Protection analytics](../reports-aip.md)します。

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


## <a name="next-steps"></a>次の手順

完全な詳細については、[比較表](use-client.md#compare-the-clients)をご覧ください。

インストールして、このクライアントを使用しての詳細については。 

- ユーザー向け: [クライアントのダウンロードとインストール](install-unifiedlabelingclient-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイドのラベル付けを統合します。](clientv2-admin-guide.md)

