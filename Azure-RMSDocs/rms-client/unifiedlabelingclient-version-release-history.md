---
title: Azure Information Protection 統合されたラベル付けクライアント-バージョン履歴 & サポートポリシー
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b1e91bcbfca3d4f925750fd8d1f135bd8f4ff2c4
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2020
ms.locfileid: "84250053"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection 統合されたラベル付けクライアント-バージョンのリリース履歴とサポートポリシー

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection 統合されたラベル付けクライアントは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)からダウンロードできます。

通常、数週間の遅延が発生すると、最新の一般公開バージョンが Microsoft Update カタログにも含まれます。これには、 **Microsoft Azure Information Protection**Microsoft Azure Information Protection の製品名と、  >  **Microsoft Azure Information Protection Unified Labeling Client****更新プログラム**の分類が含まれます。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」を参照してください。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection 統合ラベルクライアントの各一般公開 (GA) バージョンは、以降の GA バージョンのリリースから最大6か月間サポートされます。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン:

|クライアントのバージョン|リリース日|
|--------------|-------------|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|

このページで使用される日付形式は、*月/日/年*です。


### <a name="release-information"></a>リリース情報

次の情報を使用して、Windows 用の Azure Information Protection 統合ラベルクライアントのサポートされているリリースの新機能と変更点を確認してください。 最新のリリースは一番上に表示されます。 このページで使用される日付形式は、*月/日/年*です。

> [!NOTE]
> マイナー修正は記載されていないので、統一されたラベル付けクライアントで問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

このクライアントは Azure Information Protection クライアント (クラシック) に置き換わるものです。 従来のクライアントとの機能を比較するには、「 [Windows コンピューターのラベル付けクライアント](use-client.md#compare-the-labeling-clients-for-windows-computers)」を参照してください。

## <a name="version-27950-public-preview"></a>バージョン2.7.95.0 パブリックプレビュー

統一されたラベル付けスキャナーとクライアント (パブリックプレビュー) バージョン2.7.95.0

**リリース**06/01/2020

**統一されたラベル付けスキャナーの新機能:**

- [スキャナーを使用して、推奨される条件に基づいてラベルを適用](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#prerequisites-for-the-azure-information-protection-scanner)します。 AIP のお客様は、サービス側のみの自動ラベル付けを実装することを選択できるようになりました。 この機能により、AIP エンドユーザーは、前のシナリオではなく、常に推奨事項に従うことができます。これにより、ユーザー側での自動ラベル付けのみが有効になります。

- [スキャナーによって以前に検出されたファイルをスキャンしたリポジトリから削除したこと](https://docs.microsoft.com/azure/information-protection/reports-aip)を確認するこれらの削除されたファイルは、以前に AIP analytics で報告されていなかったため、スキャナー検出レポートで使用できるようになりました。

- [エラー発生時にスキャナーからレポートを取得して、アクションイベントを適用](https://docs.microsoft.com/azure/information-protection/reports-aip#friendly-schema-reference-for-event-functions)します。 レポートを使用して、失敗したアクションイベントの詳細を確認し、今後発生しないようにする方法を見つけます。 

- 一般的なスキャナーエラーの検出と分析を行うための AIP scanner diagnostics analyzer ツールの導入。 AIP スキャナー診断の使用を開始するには、[新しい**Start-Aipscan**コマンドレットを実行](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#troubleshooting-using-scanner-diagnostic-tool)します。 

- スキャナーコンピューターの最大 CPU 消費量を管理し、制限できるようになりました。 100% の CPU 使用率を防ぎ、CPU 使用率を管理する方法について説明します。 [2 つの新しい詳細設定である [ **Scan@ cpu**] と [ **scan、cpu**](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#limit-cpu-consumption)] を使用します。 

- これで、ファイル属性に応じて特定のファイルをスキップするように、統一されたラベル付けスキャナーを構成できるようになりました。 新しい**[Scanthe Fsattributestoskip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes-public-preview)** 設定を使用してスキップするファイルをトリガーするファイル属性の一覧を定義します。

**統一されたラベル付けクライアントの新機能:**

- 統一されたラベル付けクライアントの既定のラベルに加えられた変更に対して、[理由ポップアップ](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)が表示されるようになりました。
    
- Office によって適用されたビジュアルコンテンツマーキングとの円滑な統合。 Office ドキュメントでコンテンツのマーキングを構成する方法の詳細については、「 [Azure information protection の視覚的なマーキングのラベルを構成する方法](../configure-policy-markings.md)」を参照してください。

- New **WordShapeNameToRemove** advanced プロパティを使用すると、サードパーティ製のアプリケーションによって作成された Word 文書でコンテンツマークを削除できます。 [ **WordShapeNameToRemove**を使用して、既存の図形名を識別し、削除対象と](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#remove-headers-and-footers-from-other-labeling-solutions)して定義する方法について説明します。

**削除されたファイルに対して生成された新しい監査ログ**

スキャン済みのファイルが削除されたことをスキャナーが検出するたびに、監査ログが生成されるようになりました。

詳細については、次を参照してください。
- [ファイルが削除された監査ログ](../audit-logs.md#file-removed-audit-logs)
- [Azure Information Protection の Central Reporting](../reports-aip.md)

**TLS 1.2 の適用**

このバージョンの Azure Information Protection クライアント以降では、1.2 以上の TLS バージョンのみがサポートされています。
    
Tls 1.2 をサポートしていない TLS セットアップを使用しているお客様は、Azure Information Protection ポリシー、トークン、監査、および保護を使用し、Azure Information Protection ベースの通信を受信するために、tls 1.2 をサポートするセットアップに移行する必要があります。 
    
要件の詳細については、「[ファイアウォールとネットワークインフラストラクチャの要件](../requirements.md#firewalls-and-network-infrastructure)」を参照してください。

**修正プログラムと機能強化** 
- スキャナー SQL の機能強化:
    - パフォーマンス
    - 大量の情報の種類が含まれるファイル
    
- SharePoint のスキャンの機能強化:
    - スキャンのパフォーマンス
    - パスに特殊文字が含まれるファイル
    - ファイル数が大きいライブラリ
    
    SharePoint で Azure Information Protection を使用するためのクイックスタートを表示するには、「[クイックスタート: オンプレミスに格納されているファイルに保存されている機密情報を検索](../quickstart-findsensitiveinfo.md)する」を参照してください。
        
- ポリシーが不足している場合のユーザー通知の向上。 統一されたラベル付けクライアントのラベルポリシーの詳細については、Microsoft 365 のドキュメントで、[どのようなラベルポリシーを使用できるか](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do)を参照してください。

- [自動ラベル](../configure-policy-classification.md)が Excel で適用されるようになりました。ユーザーがファイルをアクティブに保存する場合と同じように、ユーザーが保存せずにファイルを閉じようとする場合です。

- [Externalcontentmarkingtoremove](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)設定が構成されている場合、ヘッダーとフッターは想定どおりに削除され、各ドキュメントの保存では削除されません。

- [動的ユーザー変数](../configure-policy-markings.md#using-variables-in-the-text-string)が、ドキュメントの視覚的なマーキングに期待どおりに表示されるようになりました。

- 複数の Exchange アカウントが構成されていて、Azure Information Protection Outlook クライアントが有効になっている場合、メールは正常にセカンダリアカウントから送信されます。 Outlook で統一されたラベル付けクライアントを構成する方法の詳細については、「 [Azure Information Protection の統合ラベル付けクライアントの追加の前提条件](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)」を参照してください。

- 高いレベルの機密性ラベルを持つドキュメントをドラッグして電子メールにドロップすると、電子メールでは、より高い機密性ラベルが期待どおりに自動的に受信されるようになります。 クライアント機能のラベル付けの詳細については、「[クライアント比較表](use-client.md#compare-the-labeling-clients-for-windows-computers)」を参照してください。

- 電子メールアドレスにアポストロフィ (') とピリオド (.) の両方が含まれている場合、カスタムアクセス許可が意図したとおりに電子メールに適用されるようになりました。Outlook で統一されたラベル付けクライアントを構成する方法の詳細については、「 [Azure Information Protection の統合ラベル付けクライアントの追加の前提条件](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)」を参照してください。

- 既定では、ファイルの NTFS 所有者は、統一されたラベル付けスキャナー、PowerShell、またはエクスプローラーの拡張機能によってラベルが付けられたときに失われます。 これで、新しい**[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** advanced 設定を**true**に設定して、ファイルの NTFS 所有者を保持するようにシステムを構成できます。 

    **UseCopyAndPreserveNTFSOwner**の詳細設定では、スキャナーとスキャンされたリポジトリの間に、待機時間が短く、信頼性の高いネットワーク接続が必要です。


## <a name="version-261110"></a>バージョン2.6.111.0 

**リリース**03/09/2020

**新機能:**

- [スキャナー](../deploy-aip-scanner.md)の一般公開バージョン。オンプレミスのデータストアのドキュメントを検査してラベル付けします。 

- [スキャナー](../deploy-aip-scanner.md)関連:
    - [SharePoint オンプレミスおよびサブサイトの検出が容易に](https://docs.microsoft.com/azure/information-protection/quickstart-findsensitiveinfo#permission-users-to-scan-sharepoint-repositories)なりました。 各サイトの設定は必須ではなくなりました。 
    - [SQL チャンクのサイズ変更](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#storage-requirements-and-capacity-planning-for-sql-server)の詳細プロパティが追加されました。
    - 管理者は、既存の[スキャンを停止し](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#stop-a-scan)、既定のラベルが変更された場合に再スキャンを実行できるようになりました。
    - 既定では、スキャナーは、高速なスキャンのために最小のテレメトリを設定し、ログのサイズを小さくし、情報の種類をデータベースにキャッシュするようになりました。 [スキャナーの最適化](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#optimizing-the-performance-of-the-scanner)の詳細についてはこちらをご覧ください。 
    - スキャナーはデータベースとサービスの個別の配置をサポートするようになりましたが、 **Sysadmin**権限はデータベースの配置にのみ必要です。
    - スキャナーのパフォーマンスが向上しました。 

- PST、rar、7zip、および MSG ファイルからの保護の削除を有効にするための[PowerShell](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-powershell)コマンドレットの**set-aipfilelabel**の変更。 この機能は既定で無効になっており、[ここで](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#enable-removal-of-protection-from-compressed-files)説明するように、 [Set labelpolicy](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations)コマンドレットを使用して有効にする必要があります。  

- Azure Information Protection の管理者がファイルに対して pfile 拡張機能を使用するかどうかを制御できるようになりました。 [保護されたファイルの種類の変更](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#change-which-file-types-to-protect)に関する詳細情報。 

- アプリケーションと変数に対して動的な視覚的マーキングのサポートが追加されました。 [視覚的なマーキングのラベルを構成](https://docs.microsoft.com/azure/information-protection/configure-policy-markings)する方法については、こちらを参照してください。 

- [自動および推奨ラベルに対するカスタマイズ可能なポリシーのヒント](use-client.md)が強化されました。   

- 統一されたラベル付けクライアントで Office アプリを使用して、[オフラインラベル機能](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#support-for-disconnected-computers)のサポートが追加されました。

**修正:**

- RightFax によって作成された、保護された TIFF ファイルと TIFF ファイルを開こうとしてユーザーが失敗したインスタンスでは、TIFF ファイルが開き、予想どおりに安定した状態が維持されるようになりました。  
- 保護された txt ファイルと PDF ファイルの以前の破損が解決されます。
- Log Analytics の**自動**と**手動**の間に一貫性のないラベル付けが修正されました。 
- 新しいメールとユーザーの最後に開いた電子メールの間で、予期しない継承の問題が解決されました。  
- .Msg ファイルの保護が正常に機能するようになりました。 
- Office ユーザー定義の設定から追加された共同所有者のアクセス許可が、期待どおりに適用されるようになりました。 
- [アクセス許可のダウングレードを入力する] をオンにすると、他のオプションが既に選択されている場合はテキストを入力できなくなります。 


## <a name="version-25330"></a>バージョン2.5.33.0

**リリース**日: 10/23/2019

09/09/2020 でサポート

**新機能:**

- [スキャナー](../deploy-aip-scanner.md)のプレビューバージョン。オンプレミスのデータストアを検査してラベル付けします。 このバージョンのスキャナーでは、次のことを行います。
    
    - 同じスキャナープロファイルを使用するようにスキャナーを構成するときに、複数のスキャナーが同じ SQL Server データベースを共有できます。 この構成により、複数のスキャナーの管理が容易になり、スキャン時間が短縮されます。 この構成を使用する場合は、スキャナーのインストールが完了するのを待ってから、同じプロファイルを使用して別のスキャナーをインストールします。
    
    - スキャナーをインストールするときにプロファイルを指定する必要があります。スキャナーデータベースには**AIPScannerUL_ \<profile_name> **という名前が付けられます。 *プロファイル*パラメーターは、Set-AIPScanner にも必須です。
    
    - ドキュメントにラベルが既に付いている場合でも、すべてのドキュメントに既定のラベルを設定できます。 スキャナープロファイルまたはリポジトリの設定で、[ラベルの再設定 **] オプションを** **[オン**] に設定し、新しい [既定の**ラベルを強制**する] チェックボックスをオンにします。
    
    - すべてのドキュメントから既存のラベルを削除できます。ラベルによって以前に適用されていた場合、この操作には保護の削除が含まれます。 ラベルとは独立して適用された保護が保持されます。 このスキャナーの構成は、スキャナープロファイルまたはリポジトリの設定で次の設定を使用して実現されます。
        - **コンテンツに基づいてファイルにラベルを付ける**:**オフ**
        - **既定のラベル**:**なし**
        - **ファイル**のラベルの再設定: **[** **既定のラベルを強制**する] チェックボックスがオンになっている
    
    - 従来のクライアントのスキャナーと同様、既定では、スキャナーは Office ファイルと PDF ファイルを保護します。 [PowerShell の詳細設定](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)を使用すると、他の種類のファイルを保護できます。
    
    - スキャナーサイクルの開始と終了に関するイベント Id は、Windows イベントログには書き込まれません。 代わりに、この情報に Azure portal を使用します。
    
    - 既知の問題: 新しいラベルと名前が変更されたラベルは、スキャナープロファイルまたはリポジトリの設定の既定のラベルとして選択できません。 回避策:
        - 新しいラベルの場合: Azure portal で、グローバルポリシーまたはスコープポリシーに使用する[ラベルを追加](../configure-policy-add-remove-label.md)します。
        - 名前を変更したラベルの場合: Azure portal を閉じてから再度開きます。
    
    Azure Information Protection クライアント (クラシック) からスキャナーをアップグレードすることができます。 アップグレード後に新しいデータベースが作成されると、スキャナーは初回実行時にすべてのファイルを再スキャンします。 手順については、管理者ガイドの「 [Azure Information Protection スキャナーをアップグレードする](clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)」を参照してください。
    
    詳細については、ブログ投稿のお知らせを参照してください。統合された[ラベル付け AIP スキャナーのプレビューにより、スケールアウトなど](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Unified-labeling-AIP-scanner-preview-brings-scaling-out-and-more/ba-p/862552)ができます。

- PowerShell コマンドレットの[セット-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)は、ファイルに非対話形式でラベルを付ける場合の新しいパラメーター (*AppId*、 *appsecret*、 *TenantId*、 *DelegatedUser*、 *OnBehalfOf*) を備えています。また、新しい手順では、アプリを Azure AD に登録します。 シナリオ例としては、スキャナーや、ドキュメントにラベルを付けるための自動 PowerShell スクリプトがあります。 手順については、管理者ガイドの「[非対話形式でファイルにラベルを付ける方法](clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」を参照してください。
    
    *DelegatedUser*は、統合されたラベル付けクライアントの最後のプレビューバージョン以降の新しいパラメーターであり、登録済みアプリの API アクセス許可が変更されたことに注意してください。

- [保護するファイルの種類を変更](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)するための新しい PowerShell ラベルポリシーの詳細設定。

- 新しい PowerShell ラベルポリシーの詳細設定を[使用して、ラベルの移行ルールを SharePoint プロパティに拡張](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-sharepoint-properties)します。

- 一致したカスタム機密情報の種類が[Azure Information Protection analytics](../reports-aip.md)に送信されます。

- 適用されたラベルには、[色が構成され](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)ている場合、ラベルに構成されている色が表示されます。

- ラベルに保護設定を追加または変更すると、クライアントは、ドキュメントが次に保存されるときに、これらの最新の保護設定でラベルを再適用します。 同様に、スキャナーは、強制モードでドキュメントが次回スキャンされるときに、これらの最新の保護設定でラベルを再適用します。

- 1つのクライアントからファイルをエクスポートし、切断されたコンピューターに手動でコピーすることによって、切断された[コンピューターをサポート](clientv2-admin-guide-customizations.md#support-for-disconnected-computers)します。 この構成は、ファイルエクスプローラー、PowerShell、およびスキャナーを使用したラベル付けでサポートされていることに注意してください。 この構成は、Office アプリのラベル付けではサポートされていません。

- %Localappdata%\Microsoft\MSIP\Logs からすべてのログファイルを収集し、.zip 形式の1つの圧縮されたファイルに保存する新しいコマンドレットである[Export](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs)。 このファイルは、報告された問題の調査に役立つログファイルを送信するように要求された場合に Microsoft サポートに送信できます。

**修正:**

- ファイルエクスプローラーを使用して保護されたファイルを正常に変更できます。ファイルのパスワードが削除されたら、右クリックします。

- ネイティブ保護されたファイルをビューアーで正常に開くには、[名前を付けて保存]、[エクスポート (エクスポート) [] の使用権限](../configure-usage-rights.md#usage-rights-and-descriptions)を必要としません。

- ラベルとポリシー設定は[、クリア-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication?)を実行しなくても期待どおりに更新されます。または、%LocalAppData%\Microsoft\MSIP\mip フォルダーを手動で削除します。

**追加の変更**

- [設定をリセット](clientv2-admin-guide.md#more-information-about-the-reset-settings-option)すると、 \\ *\<ProcessName.exe\>* %LocalAppData%\Microsoft\MSIP\mip/ \\ *\<ProcessName\>* mip フォルダーではなく%LocalAppData%\Microsoft\MSIP\mip フォルダーが削除されるようになりました。

- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)に、保護されたドキュメントのコンテンツ ID が含まれるようになりました。


## <a name="next-steps"></a>次の手順

統合ラベルが適切なクライアントでインストールされているかどうかわからない場合は、  「 [Windows コンピューターに使用するラベル付けクライアントを選択](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)する」を参照してください。

統合ラベル付けクライアントのインストールと使用の詳細については、次を参照してください。 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-unifiedlabelingclient-app.md)

- 管理者向け: Azure Information Protection 統一された[ラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)

