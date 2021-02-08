---
title: Azure Information Protection 統合されたラベル付けクライアント-バージョン履歴 & サポートポリシー
description: Windows 用の Azure Information Protection (AIP) の統合されたラベル付けクライアントの新機能について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/08/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3bfd20785f1af97352a6e8094f224a3647474ba6
ms.sourcegitcommit: 34b029c05998681ff4af845cc51ee13cf3f2b58b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99817807"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection 統合されたラベル付けクライアント-バージョンのリリース履歴とサポートポリシー

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP and Legacy Windows And office versions](../known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。*
>
>***関連**: [AIP 統合ラベルクライアントのみ](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 従来のクライアントについては、「 [AIP クラシッククライアントバージョンのリリース履歴とサポートポリシー](client-version-release-history.md)」を参照してください。

Azure Information Protection 統合されたラベル付けクライアントは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)からダウンロードできます。

通常は数週間の遅延が発生すると、最新の一般公開バージョンも Microsoft Update カタログに含まれます。 Azure Information Protection のバージョンには、 **Microsoft Azure Information Protection** の製品名  >  Microsoft Azure Information Protection 統一された **ラベル付けクライアント**、および **更新プログラム** の分類があります。

カタログに Azure Information Protection を含めることは、WSUS または Configuration Manager、または Microsoft Update を使用するその他のソフトウェア展開メカニズムを使用してクライアントをアップグレードできることを意味します。

詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」を参照してください。

## <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection 統合ラベルクライアントの各一般公開 (GA) バージョンは、以降の GA バージョンのリリースから最大6か月間サポートされます。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

現時点では、Azure Information Protection 機能はプレビュー段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。

### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン

|クライアントのバージョン|リリース日|
|--------------|-------------|
| 2.7.96  |01/20/2021 |
|2.6.111.0 | 03/09/2020|
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

最新バージョンの Azure Information Protection は現在プレビューの段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。

> [!NOTE]
> マイナー修正は記載されていないので、統一されたラベル付けクライアントで問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

統一されたラベル付けクライアントは、Azure Information Protection のクラシッククライアントに置き換わるものです。 従来のクライアントとの機能を比較するには、「 [Windows コンピューターのラベル付けソリューションの比較](use-client.md#compare-the-labeling-solutions-for-windows-computers)」を参照してください。

## <a name="version-29116"></a>バージョン2.9.116 

統一されたラベル付けスキャナーとクライアントバージョン2.9.116 

**リリース** 02/08/2021

**修正** 済みの問題次のシナリオでは、ユーザーは保護されたファイルを想定どおりに表示できるようになりました。

- 保護されたファイルが、外部ユーザーなどの AIP ポリシーが構成されていないユーザーと共有されている場合。 この問題は、 [AIP Viewer アプリ](clientv2-view-use-files.md)でのみ発生しました。

- スコープが指定されているラベルのコンテンツが、ラベルのスコープに含まれていないユーザーまたはグループと共有されている場合。 この問題は、 [AIP Viewer アプリ](clientv2-view-use-files.md) と、 [エクスプローラー](clientv2-classify-protect.md#using-file-explorer-to-classify-and-protect-files)を使用して共有コンテンツを表示または分類するときの両方で発生しました。

詳細については、「 [AIP ユニファイドクライアントユーザーガイド](clientv2-user-guide.md)」を参照してください。
## <a name="version-291110"></a>バージョン2.9.111.0

統一されたラベル付けスキャナーとクライアントバージョン2.9.111.0

**リリース** 01/13/2021

08/08/2021 **でサポート**

このバージョンには、統合されたラベル付けスキャナーとクライアントの次の新機能、修正プログラム、および拡張機能が含まれています。

- **スキャナーの新機能**:

    - [接続されていないスキャナーサーバーに対する PowerShell のサポート](#powershell-support-for-disconnected-scanner-servers)
    - [コンテンツスキャンジョブでの NFS リポジトリのサポート](#support-for-nfs-repositories-in-content-scan-jobs-public-preview) (パブリックプレビュー)
    - [追加の機密情報の種類のサポートを追加しました](#added-support-for-additional-sensitive-information-types)

- **クライアントの新機能**:

    - [ドキュメントアクセスの追跡とアクセスの取り消し](#track-document-access-and-revoke-access-public-preview) (パブリックプレビュー)
    - [追加の機密情報の種類のサポートを追加しました](#added-support-for-additional-sensitive-information-types)

- **修正と改善**:

    - [統一されたラベル付けスキャナーの修正と機能強化](#fixes-and-improvements-for-the-unified-labeling-scanner)
    - [統一されたラベル付けクライアントの修正と機能強化](#fixes-and-improvements-for-the-unified-labeling-client)

- **既知の問題**: 最新の GA バージョン (2.9.111) で問題が特定されました。一部のユーザーは、次のシナリオで保護されたファイルを表示できませんでした。

    - 保護されたファイルが、外部ユーザーなどの AIP ポリシーが構成されていないユーザーと共有されている場合。 この問題は、 [AIP Viewer アプリ](clientv2-view-use-files.md)でのみ発生します。

    - スコープが指定されているラベルのコンテンツが、ラベルのスコープに含まれていないユーザーまたはグループと共有されている場合。 この問題は、 [AIP Viewer アプリ](clientv2-view-use-files.md) と、 [エクスプローラー](clientv2-classify-protect.md#using-file-explorer-to-classify-and-protect-files)を使用して共有コンテンツを表示または分類する場合の両方で発生します。

### <a name="powershell-support-for-disconnected-scanner-servers"></a>接続されていないスキャナーサーバーに対する PowerShell のサポート

[オンプレミスの Azure Information Protection スキャナー](../deploy-aip-scanner.md)では、PowerShell、インターネットに接続できないスキャナーサーバー、または[Azure 中国の21Vianet 環境 (中国ソブリン cloud)](/microsoft-365/admin/services-in-china/parity-between-azure-information-protection#manage-azure-information-protection-content-scan-jobs)のスキャナーに対するコンテンツスキャンジョブの管理がサポートされるようになりました。

Disconnected または Azure 中国の 21Vianet scanner サーバーをサポートするために、次の新しいコマンドレットを追加しました。

|コマンドレット  |説明  |
|---------|---------|
|**[追加-Aipscanのリポジトリ](/powershell/module/azureinformationprotection/add-aipscannerrepository)**     | コンテンツスキャンジョブに新しいリポジトリを追加します。        |
|**[AIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-aipscannercontentscanjob)**     |      コンテンツスキャンジョブの詳細を取得します。   |
|**[Get-Aipscanのリポジトリ](/powershell/module/azureinformationprotection/get-aipscannerrepository)**     |  コンテンツスキャンジョブに対して定義されているリポジトリに関する詳細を取得します。       |
|**[AIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-aipscannercontentscanjob)**       |    コンテンツスキャンジョブを削除します。     |
| **[-Aipscanのリポジトリを削除します。](/powershell/module/azureinformationprotection/remove-aipscannerrepository)**    |   コンテンツスキャンジョブからリポジトリを削除します。      |
|**[AIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-aipscannercontentscanjob)**     |   コンテンツスキャンジョブの設定を定義します。      |
**[Set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository)**     |   コンテンツスキャンジョブ内の既存のリポジトリの設定を定義します。      |
| | |

[**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/set-mipnetworkdiscovery)コマンドレットは、追加のサポートを提供するために追加されました。これにより、PowerShell を使用してネットワーク探索サービスのインストール設定を更新することができます。

詳細については、「 [スキャナーサーバーがインターネットに接続できない場合](../deploy-aip-scanner-prereqs.md#restriction-the-scanner-server-cannot-have-internet-connectivity) 」と「 [スキャナーを構成](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal)する」を参照してください。

### <a name="support-for-nfs-repositories-in-content-scan-jobs-public-preview"></a>コンテンツスキャンジョブでの NFS リポジトリのサポート (パブリックプレビュー)

これで、SMB ファイル共有と SharePoint リポジトリに加えて、コンテンツスキャンジョブに NFS リポジトリを追加できるようになりました。

NFS 共有のスキャンをサポートするには、スキャナーコンピューターに NFS サービスを展開する必要があります。

1. コンピューターで、[ **windows の機能] ([windows の機能の有効化または無効化)** の設定] ダイアログに移動します。

1. 次の項目を選択します。

    - **NFS 用サービス**
        - **管理ツール**
        - **NFS クライアント**

詳細については、「 [コンテンツスキャンジョブの作成](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job)」を参照してください。

### <a name="added-support-for-additional-sensitive-information-types"></a>追加の機密情報の種類のサポートを追加しました

**オーストラリアの事業番号**、**オーストラリアの会社番号**、**オーストリアの id カード** など、Azure Information Protection でのその他の機密情報の種類のサポートが追加されました。

詳細については、Microsoft 365 のドキュメントで、 [機密情報の種類のエンティティの定義](/microsoft-365/compliance/sensitive-information-type-entity-definitions) を参照してください。

### <a name="track-document-access-and-revoke-access-public-preview"></a>ドキュメントアクセスの追跡とアクセスの取り消し (パブリックプレビュー)

バージョン2.9.111.0 にアップグレードした後、追跡用にまだ登録されていない保護されたドキュメントは、AIP 統合ラベルクライアントがインストールされているコンピューターで次回開いたときに登録されます。 保護されたドキュメントがラベル付けされていない場合でも、追跡と取り消しはサポートされます。

ドキュメントを追跡用に登録すると、管理者は PowerShell を使用してドキュメントへのアクセスを追跡し、必要に応じてアクセスを取り消すことができます。

アップグレードすると、エンドユーザーは保護されているドキュメントへのアクセスを取り消すこともできます。 Microsoft Office アプリからのアクセスを取り消すには、[**秘密度**] メニューの [新しい **取り消しアクセス**] オプションを使用します。

詳細については、次を参照してください。

- [管理者ガイド: Azure Information Protection を使用したドキュメントアクセスの追跡と取り消し](track-and-revoke-admin.md)
- [ユーザーガイド: Azure Information Protection を使用したドキュメントアクセスの取り消し](revoke-access-user.md)
- [ドキュメントアクセスの追跡と取り消しに関する既知の問題](../known-issues.md#known-issues-for-track-and-revoke-features-public-preview)

組織または地域でドキュメント追跡機能を無効にする必要があるプライバシー要件がある場合は、「 [管理者の追跡と取り消し](track-and-revoke-admin.md#turn-off-track-and-revoke-features-for-your-tenant)」の手順を参照してください。

**クラシッククライアントからのアップグレード**

AIP classic クライアントは、 [Microsoft 追跡ポータル](client-track-revoke.md#using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered)を使用した機能の追跡と取り消しをサポートしています。 この追跡ポータルは、統合されたラベル付けクライアントを使用する場合には関係ありません。
 
統一されたラベル付けクライアントを使用して追跡データを表示するには、 [管理者ガイド](track-and-revoke-admin.md)の説明に従って、PowerShell コマンドのみを使用します。

### <a name="fixes-and-improvements-for-the-unified-labeling-scanner"></a>統一されたラベル付けスキャナーの修正と機能強化

Azure Information Protection 統合された [ラベル付けスキャナー](../deploy-aip-scanner.md)のバージョン2.9.111.0 では、次の修正プログラムが提供されました。

- **-**[スキャナーデータベース](../deploy-aip-scanner-prereqs.md)名にハイフン () のサポートを追加しました
- **[[コンテンツに基づくラベルファイル](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job)**] オプションが **オフ** に設定されている場合のレポートの更新
- 大量の情報の種類の一致による[メモリ消費の向上](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance)
- スラッシュ () で終わる [SharePoint オンプレミス](../deploy-aip-scanner-prereqs.md#sharepoint-requirements)パスのサポート **/**
- SharePoint のスキャン[速度](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance)の向上
- SharePoint サーバーのスキャン時の [タイムアウトを回避](clientv2-admin-guide-customizations.md#avoid-scanner-timeouts-in-sharepoint) するためのサポート。

### <a name="fixes-and-improvements-for-the-unified-labeling-client"></a>統一されたラベル付けクライアントの修正と機能強化

- メールへの返信や電子メールの転送など、Office MSI からの [電子メールのラベル付け](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-emails) に関して修正された問題。

- [Newlabel 監査ログ](../audit-logs.md#new-label-audit-logs) イベントには、Outlook から送信された電子メールによって生成されるイベントのアクションソースが含まれるようになりました。

- [Microsoft 365 のラベルポリシーを変更](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)した後に、キャッシュをクリアせずにポリシーが更新されないことがある問題を修正しました。

- Outlook プレビューモードで[検出イベントの監査ログ](../audit-logs.md#discover-audit-logs)が生成されるようになりました

- [推奨ラベル](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) と [視覚的なマーキング](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) は、Outlook で想定どおりに適用されます。 

- [Outlookblocktrusteddomains](clientv2-admin-guide-customizations.md#to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels)と[OutlookBlockUntrustedCollaborationLabel](clientv2-admin-guide-customizations.md#to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels) settings が構成されている場合など、 [Outlook 配布リストの受信者を検索](clientv2-admin-guide-customizations.md#expand-outlook-distribution-lists-when-searching-for-email-recipients)するためのサポートが追加されました。

    この機能を有効にする場合は、 [Outlookgetemの Addressenomeoutmsproperty](clientv2-admin-guide-customizations.md#expand-outlook-distribution-lists-when-searching-for-email-recipients) 設定で定義されている既定のタイムアウト値も発生させることをお勧めします。

- 複数のラベルポリシーが1人のユーザーに対して構成されており、それぞれの詳細設定が競合している場合に使用される [優先順位の](clientv2-admin-guide-customizations.md#order-of-precedence---how-conflicting-settings-are-resolved) 更新。

    このような場合、管理センターのポリシーの順序に従って、最初のポリシーの詳細設定が常に適用されます。 これで、 *Outlookdefaultlabel* の例外が削除されました。

- **% APPDATA% (AppData\Roaming)** が既定以外の Windows フォルダー構造を指しているシナリオでは、ユーザーディレクトリにマップされているフォルダー内のファイルは、構成に基づいて適切な [ラベル付けと保護から除外](clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)されるようになりました。

- [新しい高度なクライアント設定](clientv2-admin-guide-customizations.md#remove-all-shapes-of-a-specific-shape-name) (**PowerPointRemoveAllShapesByShapeName**)。これは、PowerPoint のヘッダーまたはフッターから図形を削除するために追加されています。これは、図形内のテキストではなく、図形名を使用して行います。

## <a name="version-28850"></a>バージョン2.8.85.0

統一されたラベル付けスキャナーとクライアントバージョン2.8.85.0

**リリース** 09/22/2020

7/13/2021 **でサポート**

このバージョンには、統合されたラベル付けスキャナーとクライアントの次の新機能、修正プログラム、および拡張機能が含まれています。

- **スキャナーの新機能**:

    - [検出された変更のフル再スキャン (オプション)](#optional-full-rescans-for-changes-detected)
    - [SharePoint のタイムアウトを構成する](#configure-sharepoint-timeouts)
    - [ネットワーク探索のサポート](#network-discovery-support-public-preview) (パブリックプレビュー)

- **クライアントの新機能**:

    - [Outlook での AIP ポップアップの管理者によるカスタマイズ](#administrator-customizations-for-aip-popups-in-outlook)
    - [理由を確認するための管理者のカスタマイズ](#administrator-customizations-for-justification-prompts)
    - [監査ログの更新](#audit-log-updates)
    - [DKE テンプレートベースのラベル更新](#dke-template-based-labeling-updates)

- **修正と改善:**

    - [スキャナーの修正と機能強化](#azure-information-protection-scanner-fixed-issues-version-28850)
    - [クライアントの修正と機能強化](#azure-information-protection-client-fixed-issues-version-28850)


### <a name="optional-full-rescans-for-changes-detected"></a>検出された変更のフル再スキャン (オプション)

管理者は、ポリシーまたはコンテンツスキャンジョブを変更した後、完全な再スキャンをスキップできるようになりました。 完全な再スキャンをスキップすると、前回のスキャン以降に変更または作成されたファイルのみに変更が適用されます。

たとえば、視覚的なマーキングの場合など、エンドユーザーのみに影響を与える変更を行った場合、直ちに完全な再スキャンを実行するために必要な時間を取らないようにすることができます。

完全な再スキャンをスキップして後から戻ると、 [完全な再スキャンが実行](../deploy-aip-scanner-manage.md#rescanning-files) され、変更がリポジトリ全体に適用されます。

> [!IMPORTANT]
> 管理者がポリシーとコンテンツスキャンジョブを変更した場合、その変更がコンテンツに与える影響を理解し、完全な再スキャンが必要かどうかを判断する必要があります。
>
> たとえば、 **ポリシー実施** 設定を [ **強制] から** **[強制**] に変更した場合は、フルスキャンを実行して、コンテンツ全体にラベルを適用してください。
>

### <a name="configure-sharepoint-timeouts"></a>SharePoint のタイムアウトを構成する

SharePoint との対話の既定のタイムアウトが2分に更新され、その後、AIP 操作の試行が失敗します。

AIP 管理者は、すべての web 要求とファイル web 要求に対して個別に SharePoint タイムアウトを構成することもできます。

詳細については、「 [SharePoint のタイムアウトを構成する](clientv2-admin-guide-customizations.md#configure-sharepoint-timeouts)」を参照してください。

### <a name="network-discovery-support-public-preview"></a>ネットワーク探索のサポート (パブリックプレビュー)

統一されたラベル付けスキャナーに新しい **ネットワーク探索** サービスが含まれるようになりました。これにより、機密性の高いコンテンツを持つ可能性のあるネットワークファイル共有の指定した IP アドレスまたは範囲をスキャンできます。

**ネットワーク探索** サービスは、検出されたアクセス許可とアクセス権に基づいて、リスクがある可能性のある共有の場所の一覧を使用して **リポジトリ** のレポートを更新します。 更新された **リポジトリ** レポートで、スキャンする必要があるすべてのリポジトリがコンテンツスキャンジョブに含まれていることを確認します。

> [!TIP]
> 詳細については、「 [ネットワーク探索のコマンドレット](#network-discovery-cmdlets-public-preview)」を参照してください。

**ネットワーク探索サービスを使用するには**

1. スキャナーのバージョンをアップグレードし、スキャナークラスターが正しく構成されていることを確認してください。 詳細については、次を参照してください。
    - [スキャナーをアップグレードする](../deploy-aip-scanner-configure-install.md#upgrading-your-scanner)
    - [スキャナークラスターを作成する](../deploy-aip-scanner-configure-install.md#create-a-scanner-cluster)

1. Azure Information Protection analytics が有効になっていることを確認します。

    Azure portal で、[ **Azure Information Protection > [> 管理] [分析の構成] (プレビュー)** にアクセスします。

    詳細については、「 [Azure Information Protection の中央レポート (パブリックプレビュー)](../reports-aip.md)」を参照してください。

1. [**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) PowerShell コマンドレットを実行して、ネットワーク探索を有効にします。

    > [!IMPORTANT]
    > このコマンドレットを実行するときは、 **StandardDomainsUserAccount** パラメーターの値として脆弱なユーザーを使用して、リポジトリへのパブリックアクセスが確実に報告されるようにしてください。
    >
    > このユーザーは、 **Domain Users** グループのメンバーである必要があります。また、リポジトリへのパブリックアクセスをシミュレートするために使用されます。

1. Azure portal で、[Azure Information Protection > **ネットワークスキャンジョブ** ] にアクセスし、[ [ジョブの作成] を使用してネットワークの特定の領域をスキャン](../deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview)します。

1. [新しい [**リポジトリ**](../deploy-aip-scanner-configure-install.md#analyze-risky-repositories-found-public-preview) ] ウィンドウで生成されたレポートを使用して、危険にさらされる可能性のある追加のネットワークファイル共有を見つけます。 リスクの高いファイル共有を [コンテンツスキャンジョブ](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job) に追加して、追加されたリポジトリで機微なコンテンツをスキャンします。

#### <a name="network-discovery-cmdlets-public-preview"></a>ネットワーク探索のコマンドレット (パブリックプレビュー)

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


### <a name="administrator-customizations-for-aip-popups-in-outlook"></a>Outlook での AIP ポップアップの管理者によるカスタマイズ

AIP 管理者は、ブロックされた電子メールのポップアップ、警告メッセージ、および理由のプロンプトなど、Outlook に表示されるポップアップをカスタマイズできるようになりました。

一般的なユースケースシナリオのいくつかのサンプルルールを含む詳細については、「 [Outlook ポップアップメッセージをカスタマイズ](clientv2-admin-guide-customizations.md#customize-outlook-popup-messages)する」を参照してください。

### <a name="administrator-customizations-for-justification-prompts"></a>理由を確認するための管理者のカスタマイズ

AIP 管理者は、エンドユーザーがドキュメントや電子メールの分類ラベルを変更したときに表示される理由プロンプトで、オプションの1つをカスタマイズできるようになりました。

詳細については、「変更された [ラベルの理由プロンプトテキストをカスタマイズ](clientv2-admin-guide-customizations.md#customize-justification-prompt-texts-for-modified-labels)する」を参照してください。

### <a name="audit-log-updates"></a>監査ログの更新

ラベル付きまたは保護されたファイルをユーザーが開いたときにのみ、ユーザーアクセスを明確に示すために、統合されたラベル付けクライアントからのアクセスイベントの監査ログが送信されるようになりました。

詳細については、「 [監査ログへのアクセス](../audit-logs.md#access-audit-logs)」を参照してください。

### <a name="dke-template-based-labeling-updates"></a>DKE テンプレートベースのラベル更新

Azure Information Protection は、スキャナーでのダブルキー暗号化 (DKE) テンプレートベースのラベル付けと、エクスプローラーと PowerShell の使用をサポートするようになりました。

詳細については、次を参照してください。

- [Azure Information Protection テナント キーを計画して実装する](../plan-implement-tenant-key.md)
- Microsoft 365 ドキュメントの[二重キー暗号化](/microsoft-365/compliance/double-key-encryption)

### <a name="azure-information-protection-scanner-fixed-issues-version-28850"></a>Azure Information Protection スキャナーの修正済みの問題、バージョン2.8.85.0

Azure Information Protection 統合されたラベル付けスキャナーのバージョン2.8.85.0 では、次の修正プログラムが提供されました。

- [長いパスを使用したファイルのスキャン](../deploy-aip-scanner-prereqs.md#file-path-requirements)の機能強化
- AIP スキャナーでは、複数の ContentDatabases がある場合に、 [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) 環境全体をスキャンするようになりました。
- AIP スキャナーでは、パスにピリオドが付いた [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) ファイルがサポートされるようになりましたが、拡張子はありません。 たとえば、パスがで拡張子が付けら `https://sharepoint.contoso.com/shared documents/meeting-notes` れていないファイルは、正常にスキャンされるようになりました。
- AIP スキャナーは、Microsoft のセキュリティとコンプライアンスセンターで作成され、どのポリシーにも属していない [カスタム機微な情報の種類](../deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types) をサポートするようになりました。

### <a name="azure-information-protection-client-fixed-issues-version-28850"></a>Azure Information Protection クライアントの修正済みの問題、バージョン2.8.85.0

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

3/22/2021 **でサポート**

**修正**:

ファイルのフリーズ、クラッシュ、または保護、ウォーターマーク、コンテンツマーキングで構成された必須ラベルに関連付けられた保存の繰り返しが発生した、PPT、Excel、Word ユーザーの問題を修正しました。

## <a name="version-27990"></a>バージョン2.7.99.0

統一されたラベル付けスキャナーとクライアントバージョン2.7.99.0

**リリース** 07/20/2020

2/23/2021 **でサポート**

**修正と改善**:

**新しいラベル** 監査ログのファイルラベル付け操作の問題を修正した。

詳細については、「 [Version 2.7.96.0](#version-27960) and [Azure Information Protection audit log reference (public preview)](../audit-logs.md)」を参照してください。

## <a name="version-27960"></a>バージョン2.7.96.0

統一されたラベル付けスキャナーとクライアントバージョン2.7.96.0

**リリース** 06/29/2020

1/20/2021 **でサポート**

- [統一されたラベル付けクライアントバージョン2.7.96.0 の新機能](#new-features-for-the-unified-labeling-client-version-27960)
- [統一されたラベル付けスキャナーの新機能、バージョン2.7.96.0](#new-features-for-the-unified-labeling-scanner-version-27960)
- [削除されたファイルに対して生成された新しい監査ログ](#new-audit-logs-generated-for-removed-files)
- [TLS 1.2 の適用](#tls-12-enforcement)
- [修正プログラムと機能強化、バージョン2.7.96.0](#fixes-and-improvements-version-27960)
### <a name="new-features-for-the-unified-labeling-scanner-version-27960"></a>統一されたラベル付けスキャナーの新機能、バージョン2.7.96.0

- [スキャナーを使用して、推奨される条件に基づいてラベルを適用](../deploy-aip-scanner-prereqs.md)します。 AIP のお客様は、autolabeling のみを実装することを選択できるようになりました。 この機能により、AIP エンドユーザーは、前のシナリオではなく、常に推奨事項に従うことができます。これにより、ユーザー側での自動ラベル付けのみが有効になります。

- [スキャナーによって以前に検出されたファイルをスキャンしたリポジトリから削除したこと](../reports-aip.md) を確認するこれらの削除されたファイルは、以前に AIP analytics で報告されていなかったため、スキャナー検出レポートで使用できるようになりました。

- [エラー発生時にスキャナーからレポートを取得して、アクションイベントを適用](../reports-aip.md#friendly-schema-reference-for-event-functions)します。 レポートを使用して、失敗したアクションイベントの詳細を確認し、今後発生しないようにする方法を見つけます。

- 一般的なスキャナーエラーの検出と分析を行うための AIP scanner diagnostics analyzer ツールの導入。 AIP スキャナー診断の使用を開始するには、 [ **Start-Aipscan** コマンドレットを実行](../deploy-aip-scanner-tsg.md#troubleshooting-using-the-scanner-diagnostic-tool)します。

- スキャナーコンピューターの最大 CPU 消費量を管理し、制限できるようになりました。 100% の CPU 使用率を防ぎ、CPU 使用率を管理する方法について説明します。 [2 つの新しい詳細設定である [ **Scan@ cpu**] と [ **scan、cpu**](./clientv2-admin-guide-customizations.md#limit-cpu-consumption)] を使用します。

- これで、ファイル属性に応じて特定のファイルをスキップするように、統一されたラベル付けスキャナーを構成できるようになりました。 新しい **[Scanthe Fsattributestoskip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes)** 設定を使用してスキップするファイルをトリガーするファイル属性の一覧を定義します。

### <a name="new-features-for-the-unified-labeling-client-version-27960"></a>統一されたラベル付けクライアントバージョン2.7.96.0 の新機能

- 統一されたラベル付けクライアントの既定のラベルに加えられた変更に対して、[**理由ポップアップ**](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)が表示されるようになりました。

- Office によって適用されたビジュアルコンテンツマーキングとの円滑な統合。 Office ドキュメントでコンテンツのマーキングを構成する方法の詳細については、「 [Azure information protection の視覚的なマーキングのラベルを構成する方法](../configure-policy-markings.md)」を参照してください。

- New **WordShapeNameToRemove** advanced プロパティを使用すると、サードパーティ製のアプリケーションによって作成された Word 文書でコンテンツマークを削除できます。 [ **WordShapeNameToRemove** を使用して、既存の図形名を識別し、削除対象と](./clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)して定義する方法について説明します。

- **二重キー暗号化 (DKE)** のサポート (パブリックプレビュー)。

    これで、統一されたラベル付けクライアントを使用して、キーの完全な制御を維持しながら、機密性の高いコンテンツを保護することができます。 保護されたコンテンツにアクセスするには、2つのキーが必要です。1つのキーが Azure に格納され、もう一方のキーは顧客によって保持されます。

    既定のクラウドベースのテナントルートキーの詳細については、「 [Azure Information Protection テナントキーの計画と実装](../plan-implement-tenant-key.md)」を参照してください。 二重キー暗号化の実装の詳細については、Microsoft 365 ドキュメントの「 [double キー encryption](/microsoft-365/compliance/double-key-encryption) 」を参照してください。

### <a name="new-audit-logs-generated-for-removed-files"></a>削除されたファイルに対して生成された新しい監査ログ

スキャン済みのファイルが削除されたことをスキャナーが検出するたびに、監査ログが生成されるようになりました。

詳細については、次を参照してください。

- [ファイルが削除された監査ログ](../audit-logs.md#file-removed-audit-logs)
- [Azure Information Protection の Central Reporting](../reports-aip.md)

> [!IMPORTANT]
> このバージョンでは、ファイルのラベル付け操作によって **新しいラベル** 監査ログが生成されません。
> **[強制**] モードでスキャナーを実行する場合は、[バージョン 2.7.99.0](#version-27990)にアップグレードすることをお勧めします。
>

### <a name="tls-12-enforcement"></a>TLS 1.2 の適用

このバージョンの Azure Information Protection クライアント以降では、TLS バージョン1.2 以降のみがサポートされています。

Tls 1.2 をサポートしていない TLS セットアップを使用しているお客様は、Azure Information Protection ポリシー、トークン、監査、および保護を使用し、Azure Information Protection ベースの通信を受信するために、tls 1.2 をサポートするセットアップに移行する必要があります。

要件の詳細については、「 [ファイアウォールとネットワークインフラストラクチャの要件](../requirements.md#firewalls-and-network-infrastructure)」を参照してください。

### <a name="fixes-and-improvements-version-27960"></a>修正プログラムと機能強化、バージョン2.7.96.0

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

- 複数の Exchange アカウントが構成されていて、Azure Information Protection Outlook クライアントが有効になっている場合、メールは正常にセカンダリアカウントから送信されます。 Outlook で統一されたラベル付けクライアントを構成する方法の詳細については、「 [AIP を無効にするためのグループポリシーの構成](reqs-ul-client.md#configure-your-group-policy-to-prevent-disabling-aip)」を参照してください。

- 高いレベルの機密性ラベルを持つドキュメントをドラッグして電子メールにドロップすると、電子メールでは、より高い機密性ラベルが期待どおりに自動的に受信されるようになります。 クライアント機能のラベル付けの詳細については、「 [クライアント比較表](use-client.md#compare-the-labeling-solutions-for-windows-computers)」を参照してください。

- 電子メールアドレスにアポストロフィ (') とピリオド (.) の両方が含まれている場合、カスタムアクセス許可が意図したとおりに電子メールに適用されるようになりました。Outlook で統一されたラベル付けクライアントを構成する方法の詳細については、「 [AIP を無効にするためのグループポリシーの構成](reqs-ul-client.md#configure-your-group-policy-to-prevent-disabling-aip)」を参照してください。


- 既定では、ファイルの NTFS 所有者は、統一されたラベル付けスキャナー、PowerShell、またはエクスプローラーの拡張機能によってラベルが付けられたときに失われます。 これで、新しい **[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** advanced 設定を **true** に設定して、ファイルの NTFS 所有者を保持するようにシステムを構成できます。

    **UseCopyAndPreserveNTFSOwner** の詳細設定では、スキャナーとスキャンされたリポジトリの間に、待機時間が短く、信頼性の高いネットワーク接続が必要です。

## <a name="next-steps"></a>次の手順

統合ラベルが適切なクライアントでインストールされているかどうかわからない場合は、  「 [Windows のラベル付けソリューションを選択する」を](use-client.md#choose-your-windows-labeling-solution)参照してください。

統合ラベル付けクライアントのインストールと使用の詳細については、次を参照してください。

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-unifiedlabelingclient-app.md)

- 管理者向け: Azure Information Protection 統一された [ラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)
