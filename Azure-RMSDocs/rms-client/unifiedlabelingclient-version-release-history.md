---
title: Azure Information Protection unified ラベル付けのクライアントのバージョンの履歴とサポート ポリシー
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: d0122c41123bb47f0facf2bdf96e73ad10f8fe3d
ms.sourcegitcommit: b92f60a87f824fc2da1e599f526898e3a0c919c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2019
ms.locfileid: "67343656"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>統合、azure Information Protection クライアントのバージョンをラベル付けリリース履歴とサポート ポリシー

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Azure Information Protection の統合されたラベル付けクライアントをダウンロードすることができます、 [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)します。

最新の一般提供バージョンにも製品名を持つ、Microsoft Update カタログに含まれているは、通常 2 週間の短い遅延の後**Microsoft Azure Information Protection**  >  **Microsoft Azure Information Protection Unified ラベル付けクライアント**との分類**更新**します。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、次を参照してください。[アップグレードと維持、Azure Information Protection の統合のラベル付けクライアント](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)します。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection の統合されたラベル付けクライアントの各一般 (公開 GA) バージョンは最大 6 か月間、後続の GA バージョンのリリース後でサポートされています。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

> [!NOTE]
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

### <a name="release-information"></a>リリース情報

次の情報を使用すると、Azure Information Protection の統合されたラベル付けクライアントの一般公開バージョンでサポートされる機能を参照してください。

このクライアントでは、Windows コンピューター用の Office アドオン、エクスプローラー用の拡張機能、および PowerShell モジュールがインストールされます。 このクライアントには、Azure からポリシーをダウンロードする Azure Information Protection クライアントと同じ[前提条件](../requirements.md)があります。

機能と、Azure Information Protection クライアントを使用して機能を比較するを参照してください。[クライアントの比較](use-client.md#compare-the-clients)します。

## <a name="versions-later-than-207790"></a>2\.0.779.0 より後のバージョン

**リリース日**: 06/20/2019

2\.0.779.0 より後のクライアントのバージョン 2 を使っている場合は、テストおよび評価目的のプレビュー ビルドです。 

**新機能:**

- サポート[詳細設定](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)セキュリティ/コンプライアンス センターの PowerShell を構成します。
    
    これらの高度な設定は、次のカスタマイズをサポートします。
     - [Office アプリの Information Protection バーを表示します](clientv2-admin-guide-customizations.md#display-the-information-protection-bar-in-office-apps)
    - [Outlook で推奨分類を有効にする](clientv2-admin-guide-customizations.md#enable-recommended-classification-in-outlook)
    - [Outlook に別の既定ラベルを設定する](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [必須のラベル付けを使用するときにドキュメントの "後で" を削除する](clientv2-admin-guide-customizations.md#remove-not-now-for-documents-when-you-use-mandatory-labeling)
    - [他のラベル付けソリューションからヘッダーとフッターを削除する](clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)
    - [Outlook に別の既定ラベルを設定する](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [ファイル エクスプ ローラーでのカスタム アクセス許可を無効にします。](clientv2-admin-guide-customizations.md#disable-custom-permissions-in-file-explorer)
    - [カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する](clientv2-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)
    - [添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します](clientv2-admin-guide-customizations.md#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
    - [ユーザーの "問題の報告" を追加する](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)
    - [Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - [Azure Information Protection analytics へのドキュメントで検出された機密情報を送信を無効にします。](clientv2-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)
    - [ユーザーのサブセットに対して送信情報の種類の一致を無効にする](clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - [Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [ラベルが適用されるときに、カスタム プロパティを適用します。](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [ラベルを構成して Outlook で S/MIME 保護を適用する](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [親ラベルの既定のサブラベルを指定します。](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [ラベルの色を指定します。](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Word、Excel、PowerPoint、およびエクスプ ローラーのユーザー定義のアクセス許可が構成されているラベルのサポート:
    - この構成は、Azure portal を使用してラベルがあれば、現在管理センターの同等の構成はありませんが、統一されたラベル付けクライアントでようになりましたサポートがされます。
    - ユーザーは、この構成を持つラベルを選択するときにユーザーとドキュメントの保護設定を選択するように求められます。

- AzureInformationProtection モジュールで PowerShell の変更:
    - 新しいコマンドレット:[新規 AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -カスタム アクセス許可については、アドホック ポリシーを作成するには、新規-RMSProtectionLicense が置き換えられます
    - 新しいパラメーター:
        -  *CustomPermissions*と*RemoveProtection*に追加 - [Set-aipfilelabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *OnBeHalfOf*に追加 - [Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)の代わりに使用される、*トークン*非対話型セッションのパラメーター
        -  *WhatIf*と*DiscoveryInfoTypes*に追加 - [Set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification)このコマンドレットは、ラベルを適用せず検出モードで実行できるように、
    - 非推奨のコマンドレット:Clear-RMSAuthentication, Get-RMSFileStatus, Get-RMSServer, Get-RMSServerAuthentication, Get-RMSTemplate, Protect-RMSFile, Set-RMSServerAuthentication, Unprotect-RMSFile


**修正:**

- 自動ラベル付け機能が構成されている場合、ラベルには、初めてドキュメントを保存するが適用されます。

- 既定のサポート サブラベルのラベル付けします。

## <a name="version-207790"></a>バージョン 2.0.779.0

**リリース日**: 05/01/2019

このリリースでは、場合によっては、ラベル表示しない Office アプリ、またはファイル エクスプ ローラーで、競合状態の問題を解決するのには 1 つの修正。

## <a name="version-207780"></a>バージョン 2.0.778.0

**リリース日**: 04/16/2019

11/01/2019 によってサポートされています

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
    - 既定のラベル付け - サブラベルなしのラベルに現在制限があります。
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

