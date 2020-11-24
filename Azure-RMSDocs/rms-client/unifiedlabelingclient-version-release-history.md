---
title: Azure Information Protection 統合されたラベル付けクライアント-バージョン履歴 & サポートポリシー
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b9eaa35d1fde58863a9f9ef9c5160a2bb103d031
ms.sourcegitcommit: 3780bd234c0af60d4376f1cae093b8b0ab035a9f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "95570879"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection 統合されたラベル付けクライアント-バージョンのリリース履歴とサポートポリシー

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP For windows And office versions in extended support](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。*
>
> *手順: [Windows 用の Azure Information Protection 統合ラベル付けクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection 統合されたラベル付けクライアントは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)からダウンロードできます。

通常は数週間の遅延が発生すると、最新の一般公開バージョンも Microsoft Update カタログに含まれます。 Azure Information Protection のバージョンには、 **Microsoft Azure Information Protection** の製品名  >  Microsoft Azure Information Protection 統一された **ラベル付けクライアント**、および **更新プログラム** の分類があります。 

カタログに Azure Information Protection を含めることは、WSUS または Configuration Manager、または Microsoft Update を使用するその他のソフトウェア展開メカニズムを使用してクライアントをアップグレードできることを意味します。

詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」を参照してください。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection 統合ラベルクライアントの各一般公開 (GA) バージョンは、以降の GA バージョンのリリースから最大6か月間サポートされます。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

現時点では、Azure Information Protection 機能はプレビュー段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン:

|クライアントのバージョン|リリース日|
|--------------|-------------|
|2.5.33.0 |2019/10/23|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|
| | |

このページで使用される日付形式は、 *月/日/年* です。


### <a name="release-information"></a>リリース情報

次の情報を使用して、Windows 用の Azure Information Protection 統合ラベルクライアントのサポートされているリリースの新機能と変更点を確認してください。 最新のリリースは一番上に表示されます。 このページで使用される日付形式は、 *月/日/年* です。

> [!NOTE]
> マイナー修正は記載されていないので、統一されたラベル付けクライアントで問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

このクライアントは Azure Information Protection クライアント (クラシック) に置き換わるものです。 従来のクライアントとの機能を比較するには、「 [Windows コンピューターのラベル付けクライアント](use-client.md#compare-the-labeling-clients-for-windows-computers)」を参照してください。

## <a name="version-28850"></a>バージョン2.8.85.0

統一されたラベル付けスキャナーとクライアントバージョン2.8.85.0

**リリース** 09/22/2020

このバージョンには、統合されたラベル付けスキャナーとクライアントの次の新機能、修正プログラム、および拡張機能が含まれています。

- [統一されたラベル付けスキャナーの新機能](#new-features-for-the-unified-labeling-scanner)
- [統一されたラベル付けクライアントの新機能](#new-features-for-the-unified-labeling-client)
- [修正プログラムと機能強化](#fixes-and-improvements)

### <a name="new-features-for-the-unified-labeling-scanner"></a>統一されたラベル付けスキャナーの新機能

- [検出された変更のフル再スキャン (オプション)](#optional-full-rescans-for-changes-detected)
- [SharePoint のタイムアウトを構成する](#configure-sharepoint-timeouts)
- [ネットワーク探索のサポート](#network-discovery-support) 

#### <a name="optional-full-rescans-for-changes-detected"></a>検出された変更のフル再スキャン (オプション)

管理者は、ポリシーまたはコンテンツスキャンジョブを変更した後、完全な再スキャンをスキップできるようになりました。 完全な再スキャンをスキップすると、前回のスキャン以降に変更または作成されたファイルのみに変更が適用されます。

たとえば、視覚的なマーキングの場合など、エンドユーザーのみに影響を与える変更を行った場合、直ちに完全な再スキャンを実行するために必要な時間を取らないようにすることができます。 

完全な再スキャンをスキップして後から戻ると、 [完全な再スキャンが実行](../deploy-aip-scanner-manage.md#rescanning-files) され、変更がリポジトリ全体に適用されます。

> [!IMPORTANT]
> 管理者がポリシーとコンテンツスキャンジョブを変更した場合、その変更がコンテンツに与える影響を理解し、完全な再スキャンが必要かどうかを判断する必要があります。
> 
> たとえば、 **ポリシー実施** 設定を [ **強制** ] から **[強制]** に変更した場合は、フルスキャンを実行して、コンテンツ全体にラベルを適用してください。
>

#### <a name="configure-sharepoint-timeouts"></a>SharePoint のタイムアウトを構成する

SharePoint との対話の既定のタイムアウトが2分に更新され、その後、AIP 操作の試行が失敗します。

AIP 管理者は、すべての web 要求とファイル web 要求に対して個別に SharePoint タイムアウトを構成することもできます。 

詳細については、「 [SharePoint のタイムアウトを構成する](clientv2-admin-guide-customizations.md#configure-sharepoint-timeouts)」を参照してください。

#### <a name="network-discovery-support"></a>ネットワーク探索のサポート

統一されたラベル付けスキャナーに新しい **ネットワーク探索** サービスが含まれるようになりました。これにより、機密性の高いコンテンツを持つ可能性のあるネットワークファイル共有の指定した IP アドレスまたは範囲をスキャンできます。 

**ネットワーク探索** サービスは、検出されたアクセス許可とアクセス権に基づいて、リスクがある可能性のある共有の場所の一覧を使用して **リポジトリ** のレポートを更新します。 更新された **リポジトリ** レポートで、スキャンする必要があるすべてのリポジトリがコンテンツスキャンジョブに含まれていることを確認します。

> [!TIP]
> 詳細については、「 [ネットワーク探索のコマンドレット](#network-discovery-cmdlets)」を参照してください。

**ネットワーク探索サービスを使用するには**

1. スキャナーのバージョンをアップグレードし、スキャナークラスターが正しく構成されていることを確認してください。 詳細については次を参照してください:
    - [スキャナーをアップグレードする](../deploy-aip-scanner-configure-install.md#upgrading-your-scanner)
    - [スキャナークラスターを作成する](../deploy-aip-scanner-configure-install.md#create-a-scanner-cluster) 
    
1. Azure Information Protection analytics が有効になっていることを確認します。 

    Azure portal で、[ **Azure Information Protection > [> 管理] [分析の構成] (プレビュー) にアクセスします。** 

    詳細については、「 [Azure Information Protection の中央レポート (パブリックプレビュー)](../reports-aip.md)」を参照してください。

1. [**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) PowerShell コマンドレットを実行して、ネットワーク探索を有効にします。 

    > [!IMPORTANT]
    > このコマンドレットを実行するときは、 **StandardDomainsUserAccount** パラメーターの値として脆弱なユーザーを使用して、リポジトリへのパブリックアクセスが確実に報告されるようにしてください。 
    >
    > このユーザーは、 **Domain Users** グループのメンバーである必要があります。また、リポジトリへのパブリックアクセスをシミュレートするために使用されます。

1. Azure portal で、[Azure Information Protection > **ネットワークスキャンジョブ** ] にアクセスし、[ [ジョブの作成] を使用してネットワークの特定の領域をスキャン](../deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview)します。 

1. [新しい [**リポジトリ**](../deploy-aip-scanner-configure-install.md#analyze-risky-repositories-found-public-preview) ] ウィンドウで生成されたレポートを使用して、危険にさらされる可能性のある追加のネットワークファイル共有を見つけます。 リスクの高いファイル共有を [コンテンツスキャンジョブ](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job) に追加して、追加されたリポジトリで機微なコンテンツをスキャンします。

##### <a name="network-discovery-cmdlets"></a>ネットワーク探索のコマンドレット

ネットワーク探索用に追加された PowerShell コマンドレットは次のとおりです。

|コマンドレット  |説明  |
|---------|---------|
|[**MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryConfiguration)     |   ネットワーク探索サービスがネットワークスキャンデータを既定、オンライン構成、または Azure portal からエクスポートされたオフラインファイルからプルするかどうかの現在の設定を取得します。      |
|[**MIPNetworkDiscoveryJobs**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryJobs)     |    現在構成されているネットワークスキャンジョブの一覧を取得します。     |
|[**MIPNetworkDiscoveryStatus**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryStatus)     |     テナントで構成されているすべてのネットワークスキャンジョブの現在の状態を取得します。    |
| [**MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Import-MIPNetworkDiscoveryConfiguration)     |    ファイルからネットワークスキャンジョブの構成をインポートします。     |
| [**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery)| ネットワーク探索サービスをインストールします。 |
|[**MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Set-MIPNetworkDiscoveryConfiguration)     |   ネットワーク探索サービスがネットワークスキャンデータを既定、オンライン構成、または Azure portal からエクスポートされたオフラインファイルからプルするかどうかの構成を設定します。      |
|[**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Start-MIPNetworkDiscovery)     |  特定のネットワークスキャンジョブを直ちに実行します。       |
|[**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Uninstall-MIPNetworkDiscovery)     |  ネットワーク探索サービスをアンインストールします。       |
| | |

### <a name="new-features-for-the-unified-labeling-client"></a>統一されたラベル付けクライアントの新機能

- [Outlook での AIP ポップアップの管理者によるカスタマイズ](#administrator-customizations-for-aip-popups-in-outlook) 
- [理由を確認するための管理者のカスタマイズ](#administrator-customizations-for-justification-prompts) 
- [監査ログの更新](#audit-log-updates) 
- [DKE テンプレートベースのラベル更新](#dke-template-based-labeling-updates)

#### <a name="administrator-customizations-for-aip-popups-in-outlook"></a>Outlook での AIP ポップアップの管理者によるカスタマイズ

AIP 管理者は、ブロックされた電子メールのポップアップ、警告メッセージ、および理由のプロンプトなど、Outlook に表示されるポップアップをカスタマイズできるようになりました。

一般的なユースケースシナリオのいくつかのサンプルルールを含む詳細については、「 [Outlook ポップアップメッセージをカスタマイズ](clientv2-admin-guide-customizations.md#customize-outlook-popup-messages)する」を参照してください。

#### <a name="administrator-customizations-for-justification-prompts"></a>理由を確認するための管理者のカスタマイズ

AIP 管理者は、エンドユーザーがドキュメントや電子メールの分類ラベルを変更したときに表示される理由プロンプトで、オプションの1つをカスタマイズできるようになりました。 

詳細については、「変更された [ラベルの理由プロンプトテキストをカスタマイズ](clientv2-admin-guide-customizations.md#customize-justification-prompt-texts-for-modified-labels)する」を参照してください。

#### <a name="audit-log-updates"></a>監査ログの更新

ラベル付きまたは保護されたファイルをユーザーが開いたときにのみ、ユーザーアクセスを明確に示すために、統合されたラベル付けクライアントからのアクセスイベントの監査ログが送信されるようになりました。

詳細については、「 [監査ログへのアクセス](../audit-logs.md#access-audit-logs)」を参照してください。

#### <a name="dke-template-based-labeling-updates"></a>DKE テンプレートベースのラベル更新

Azure Information Protection は、スキャナーでのダブルキー暗号化 (DKE) テンプレートベースのラベル付けと、エクスプローラーと PowerShell の使用をサポートするようになりました。

詳細については次を参照してください:

- [Azure Information Protection テナント キーを計画して実装する](../plan-implement-tenant-key.md)
- Microsoft 365 ドキュメントの[二重キー暗号化](/microsoft-365/compliance/double-key-encryption)

### <a name="fixes-and-improvements"></a>修正プログラムと機能強化

- [スキャナーの修正と機能強化](#azure-information-protection-scanner-fixed-issues)
- [クライアントの修正と機能強化](#azure-information-protection-client-fixed-issues)

#### <a name="azure-information-protection-scanner-fixed-issues"></a>Azure Information Protection スキャナーの修正済みの問題

Azure Information Protection 統合されたラベル付けスキャナーのバージョン2.8.85.0 では、次の修正プログラムが提供されました。

- [長いパスを使用したファイルのスキャン](../deploy-aip-scanner-prereqs.md#file-path-requirements)の機能強化
- AIP スキャナーでは、複数の ContentDatabases がある場合に、 [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) 環境全体をスキャンするようになりました。
- AIP スキャナーでは、パスにピリオドが付いた [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) ファイルがサポートされるようになりましたが、拡張子はありません。 たとえば、パスがで拡張子が付けら `https://sharepoint.contoso.com/shared documents/meeting-notes` れていないファイルは、正常にスキャンされるようになりました。
- AIP スキャナーは、Microsoft のセキュリティとコンプライアンスセンターで作成され、どのポリシーにも属していない [カスタム機微な情報の種類](../deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types) をサポートするようになりました。

#### <a name="azure-information-protection-client-fixed-issues"></a>Azure Information Protection クライアントの修正済みの問題

Azure Information Protection 統合されたラベル付けクライアントのバージョン2.8.85.0 では、次の修正プログラムが提供されました。

- Office アプリの [**秘密度**![列] アイコン](../media/selected-sensitivity-options.png "列アイコン")メニューで現在選択されている項目について、新しい担当が表示されます。 詳細については、 [Microsoft 365 docs の機密ラベル](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do)に関するページを参照してください。
- [AIP ビューアー](clientv2-view-use-files.md)で JPEG ファイルを表示するための修正
- ラベルのダウングレードにより、[監査イベント](../audit-logs.md#downgrade-label-audit-logs)の **前に protectionownerbefore** 自動的に追加されるようになりました
- 変更イベントに [監査ログ](../audit-logs.md#change-protection-audit-logs)の **LastModifiedDate** が含まれるようになりました。
- プロキシを使用してトークンを取得するときの、 **proxy.config** ファイルのサポートが追加されました。 詳細については、「 [ファイアウォールとネットワークインフラストラクチャの要件](../requirements.md#firewalls-and-network-infrastructure)」を参照してください。
- [ポリシーを更新](../configure-policy.md#making-changes-to-the-policy)するときの認証に関する修正
- 読み取り専用モードでの PowerPoint の [自動コンテンツマーク](../configure-policy-markings.md) 更新の修正
- ポップアップとエラーテキストの機能強化
- 電子メールと添付ファイルの分類の両方を考慮して、 [電子メールの添付ファイルの](../faqs-infoprotect.md#when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling)最高の分類を表示するツールヒントが更新されています。 
- [**設定-LabelPolicy**](/powershell/module/exchange/set-labelpolicy)コマンドレットを使用して感度ラベルポリシーを変更するときの問題のテキストを **報告** する修正
- 無効なラベル ID で [**set-aipfilelabel**](/powershell/module/azureinformationprotection/set-aipfilelabel) コマンドレットを使用した場合に表示されるエラーの修正。
- Outlook の閲覧ウィンドウで SMIME メールの暗号化を解除するためのパフォーマンスの修正。 この修正プログラムを実装するには、 [**OutlookSkipSmimeOnReadingPaneEnabled**](clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) advanced プロパティを有効にします。
- パスワードで暗号化されたファイルを含む [PST ファイルの暗号化を解除](clientv2-admin-guide-file-types.md) するための修正。 Pst ファイルにパスワードで保護されたファイルが含まれている場合は、PST ファイルの暗号化解除が失敗しなくなりました。
- スコープポリシーに含まれていない保護ラベルを削除すると、コンテンツからラベルと保護の両方が削除されるようになります。

## <a name="version-271010"></a>バージョン2.7.101.0
統一されたラベル付けスキャナーとクライアントバージョン2.7.101.0

**リリース** 08/23/2020

**ファイル**

ファイルのフリーズ、クラッシュ、または保護、ウォーターマーク、コンテンツマーキングで構成された必須ラベルに関連付けられた保存の繰り返しが発生した、PPT、Excel、Word ユーザーの問題を修正しました。

## <a name="version-27990"></a>バージョン2.7.99.0

統一されたラベル付けスキャナーとクライアントバージョン2.7.99.0

**リリース** 07/20/2020

**修正と改善:**

**新しいラベル** 監査ログのファイルラベル付け操作の問題を修正した。

詳細については、「 [Version 2.7.96.0](#version-27960) and [Azure Information Protection audit log reference (public preview)](../audit-logs.md)」を参照してください。

## <a name="version-27960"></a>バージョン2.7.96.0

統一されたラベル付けスキャナーとクライアントバージョン2.7.96.0

**リリース** 06/29/2020

**統一されたラベル付けスキャナーの新機能:**

- [スキャナーを使用して、推奨される条件に基づいてラベルを適用](../deploy-aip-scanner-prereqs.md)します。 AIP のお客様は、autolabeling のみを実装することを選択できるようになりました。 この機能により、AIP エンドユーザーは、前のシナリオではなく、常に推奨事項に従うことができます。これにより、ユーザー側での自動ラベル付けのみが有効になります。

- [スキャナーによって以前に検出されたファイルをスキャンしたリポジトリから削除したこと](../reports-aip.md) を確認するこれらの削除されたファイルは、以前に AIP analytics で報告されていなかったため、スキャナー検出レポートで使用できるようになりました。

- [エラー発生時にスキャナーからレポートを取得して、アクションイベントを適用](../reports-aip.md#friendly-schema-reference-for-event-functions)します。 レポートを使用して、失敗したアクションイベントの詳細を確認し、今後発生しないようにする方法を見つけます。 

- 一般的なスキャナーエラーの検出と分析を行うための AIP scanner diagnostics analyzer ツールの導入。 AIP スキャナー診断の使用を開始するには、 [新しい **Start-Aipscan** コマンドレットを実行](../deploy-aip-scanner-manage.md#troubleshooting-using-the-scanner-diagnostic-tool)します。 

- スキャナーコンピューターの最大 CPU 消費量を管理し、制限できるようになりました。 100% の CPU 使用率を防ぎ、CPU 使用率を管理する方法について説明します。 [2 つの新しい詳細設定である [ **Scan@ cpu**] と [ **scan、cpu**](./clientv2-admin-guide-customizations.md#limit-cpu-consumption)] を使用します。 

- これで、ファイル属性に応じて特定のファイルをスキップするように、統一されたラベル付けスキャナーを構成できるようになりました。 新しい **[Scanthe Fsattributestoskip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes)** 設定を使用してスキップするファイルをトリガーするファイル属性の一覧を定義します。

**統一されたラベル付けクライアントの新機能:**

- 統一されたラベル付けクライアントの既定のラベルに加えられた変更に対して、[**理由ポップアップ**](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)が表示されるようになりました。
    
- Office によって適用されたビジュアルコンテンツマーキングとの円滑な統合。 Office ドキュメントでコンテンツのマーキングを構成する方法の詳細については、「 [Azure information protection の視覚的なマーキングのラベルを構成する方法](../configure-policy-markings.md)」を参照してください。

- New **WordShapeNameToRemove** advanced プロパティを使用すると、サードパーティ製のアプリケーションによって作成された Word 文書でコンテンツマークを削除できます。 [ **WordShapeNameToRemove** を使用して、既存の図形名を識別し、削除対象と](./clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)して定義する方法について説明します。

- **二重キー暗号化 (DKE)** のサポート (パブリックプレビュー)。 

    これで、統一されたラベル付けクライアントを使用して、キーの完全な制御を維持しながら、機密性の高いコンテンツを保護することができます。 保護されたコンテンツにアクセスするには、2つのキーが必要です。1つのキーが Azure に格納され、もう一方のキーは顧客によって保持されます。 

    既定のクラウドベースのテナントルートキーの詳細については、「 [Azure Information Protection テナントキーの計画と実装](../plan-implement-tenant-key.md)」を参照してください。 二重キー暗号化の実装の詳細については、Microsoft 365 ドキュメントの「 [double キー encryption](/microsoft-365/compliance/double-key-encryption) 」を参照してください。

**削除されたファイルに対して生成された新しい監査ログ**

スキャン済みのファイルが削除されたことをスキャナーが検出するたびに、監査ログが生成されるようになりました。

詳細については次を参照してください:
- [ファイルが削除された監査ログ](../audit-logs.md#file-removed-audit-logs)
- [Azure Information Protection の Central Reporting](../reports-aip.md)

> [!IMPORTANT]
> このバージョンでは、ファイルのラベル付け操作によって **新しいラベル** 監査ログが生成されません。
> **[強制**] モードでスキャナーを実行する場合は、[バージョン 2.7.99.0](#version-27990)にアップグレードすることをお勧めします。
> 

**TLS 1.2 の適用**

このバージョンの Azure Information Protection クライアント以降では、TLS バージョン1.2 以降のみがサポートされています。
    
Tls 1.2 をサポートしていない TLS セットアップを使用しているお客様は、Azure Information Protection ポリシー、トークン、監査、および保護を使用し、Azure Information Protection ベースの通信を受信するために、tls 1.2 をサポートするセットアップに移行する必要があります。 
    
要件の詳細については、「 [ファイアウォールとネットワークインフラストラクチャの要件](../requirements.md#firewalls-and-network-infrastructure)」を参照してください。

**修正プログラムと機能強化** 
- スキャナー SQL の機能強化:
    - パフォーマンス
    - 大量の情報の種類が含まれるファイル
    
- SharePoint のスキャンの機能強化:
    - スキャンのパフォーマンス
    - パスに特殊文字が含まれるファイル
    - ファイル数が大きいライブラリ
    
    SharePoint で Azure Information Protection を使用するためのクイックスタートを表示するには、「 [クイックスタート: オンプレミスに格納されているファイルに保存されている機密情報を検索](../quickstart-findsensitiveinfo.md)する」を参照してください。
        
- ポリシーが不足している場合のユーザー通知の向上。 統一されたラベル付けクライアントのラベルポリシーの詳細については、Microsoft 365 のドキュメントで、 [どのようなラベルポリシーを使用できるか](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do) を参照してください。

- [自動ラベル](../configure-policy-classification.md) が Excel で適用されるようになりました。ユーザーがファイルをアクティブに保存する場合と同じように、ユーザーが保存せずにファイルを閉じようとする場合です。

- [Externalcontentmarkingtoremove](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)設定が構成されている場合、ヘッダーとフッターは想定どおりに削除され、各ドキュメントの保存では削除されません。

- [動的ユーザー変数](../configure-policy-markings.md#using-variables-in-the-text-string) が、ドキュメントの視覚的なマーキングに期待どおりに表示されるようになりました。

- オート分類規則の適用に使用されていた PDF コンテンツの最初のページのみが解決され、PDF のすべてのコンテンツに基づく自動分類が期待どおりに実行されるようになりました。 分類とラベル付けの詳細については、「 [分類とラベル付け](../faqs-infoprotect.md)に関する FAQ」を参照してください。 

- 複数の Exchange アカウントが構成されていて、Azure Information Protection Outlook クライアントが有効になっている場合、メールは正常にセカンダリアカウントから送信されます。 Outlook で統一されたラベル付けクライアントを構成する方法の詳細については、「 [Azure Information Protection の統合ラベル付けクライアントの追加の前提条件](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)」を参照してください。

- 高いレベルの機密性ラベルを持つドキュメントをドラッグして電子メールにドロップすると、電子メールでは、より高い機密性ラベルが期待どおりに自動的に受信されるようになります。 クライアント機能のラベル付けの詳細については、「 [クライアント比較表](use-client.md#compare-the-labeling-clients-for-windows-computers)」を参照してください。

- 電子メールアドレスにアポストロフィ (') とピリオド (.) の両方が含まれている場合、カスタムアクセス許可が意図したとおりに電子メールに適用されるようになりました。Outlook で統一されたラベル付けクライアントを構成する方法の詳細については、「 [Azure Information Protection の統合ラベル付けクライアントの追加の前提条件](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)」を参照してください。

- 既定では、ファイルの NTFS 所有者は、統一されたラベル付けスキャナー、PowerShell、またはエクスプローラーの拡張機能によってラベルが付けられたときに失われます。 これで、新しい **[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** advanced 設定を **true** に設定して、ファイルの NTFS 所有者を保持するようにシステムを構成できます。 

    **UseCopyAndPreserveNTFSOwner** の詳細設定では、スキャナーとスキャンされたリポジトリの間に、待機時間が短く、信頼性の高いネットワーク接続が必要です。

## <a name="version-261110"></a>バージョン2.6.111.0 

**リリース** 03/09/2020

12/29/2020 でサポート

**新機能:**

- [スキャナー](../deploy-aip-scanner.md)の一般公開バージョン。オンプレミスのデータストアのドキュメントを検査してラベル付けします。 

- [スキャナー](../deploy-aip-scanner.md) 関連:
    - [SharePoint オンプレミスおよびサブサイトの検出が容易に](../quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories)なりました。 各サイトの設定は必須ではなくなりました。 
    - [SQL チャンクのサイズ変更](../deploy-aip-scanner-prereqs.md#storage-requirements-and-capacity-planning-for-sql-server)の詳細プロパティが追加されました。
    - 管理者は、既定のラベルが変更された場合に、 [既存のスキャンを停止し、再スキャンを実行](../deploy-aip-scanner-manage.md#stopping-a-scan) できるようになりました。
    - 既定では、スキャナーは、高速なスキャンのために最小のテレメトリを設定し、ログのサイズを小さくし、情報の種類をデータベースにキャッシュするようになりました。 [スキャナーの最適化](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance)の詳細についてはこちらをご覧ください。 
    - スキャナーはデータベースとサービスの個別の配置をサポートするようになりましたが、 **Sysadmin** 権限はデータベースの配置にのみ必要です。
    - スキャナーのパフォーマンスが向上しました。 

- PST、rar、7zip、および MSG ファイルからの保護の削除を有効にするための [PowerShell](./clientv2-admin-guide-powershell.md) コマンドレットの **set-aipfilelabel** の変更。 この機能は既定で無効になっており、[ここで](./clientv2-admin-guide-customizations.md#enable-removal-of-protection-from-compressed-files)説明するように、 [Set labelpolicy](./clientv2-admin-guide-customizations.md)コマンドレットを使用して有効にする必要があります。  

- Azure Information Protection の管理者がファイルに対して pfile 拡張機能を使用するかどうかを制御できるようになりました。 [保護されたファイルの種類の変更](./clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)に関する詳細情報。 

- アプリケーションと変数に対して動的な視覚的マーキングのサポートが追加されました。 [視覚的なマーキングのラベルを構成](../configure-policy-markings.md)する方法については、こちらを参照してください。 

- [自動および推奨ラベルに対するカスタマイズ可能なポリシーのヒント](use-client.md)が強化されました。   

- 統一されたラベル付けクライアントで Office アプリを使用して、 [オフラインラベル機能](./clientv2-admin-guide-customizations.md#support-for-disconnected-computers) のサポートが追加されました。

**修正:**

- RightFax によって作成された、保護された TIFF ファイルと TIFF ファイルを開こうとしてユーザーが失敗したインスタンスでは、TIFF ファイルが開き、予想どおりに安定した状態が維持されるようになりました。  
- 保護された txt ファイルと PDF ファイルの以前の破損が解決されます。
- Log Analytics の **自動** と **手動** の間に一貫性のないラベル付けが修正されました。 
- 新しいメールとユーザーの最後に開いた電子メールの間で、予期しない継承の問題が解決されました。  
- **.Msg ファイルの保護** が正常に機能 **するようになりました**。 
- Office ユーザー定義の設定から追加された共同所有者のアクセス許可が、期待どおりに適用されるようになりました。 
- [アクセス許可のダウングレードを入力する] をオンにすると、他のオプションが既に選択されている場合はテキストを入力できなくなります。 

## <a name="next-steps"></a>次のステップ

統合ラベルが適切なクライアントでインストールされているかどうかわからない場合は、  「 [Windows コンピューターに使用するラベル付けクライアントを選択](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)する」を参照してください。

統合ラベル付けクライアントのインストールと使用の詳細については、次を参照してください。 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-unifiedlabelingclient-app.md)

- 管理者向け: Azure Information Protection 統一された [ラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)