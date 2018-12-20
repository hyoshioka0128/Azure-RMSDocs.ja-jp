---
title: Azure Information Protection クライアント - バージョン リリース履歴とサポート ポリシー
description: Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点、サポートのライフサイクル ポリシーについて説明します。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/13/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c6312d3f10a70ffcb3cc48447fcbc751b7072a0d
ms.sourcegitcommit: db24caa96033fd0c7a0fad4e36518a816a570c94
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2018
ms.locfileid: "53335525"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure Information Protection クライアント:バージョン リリース履歴とサポート ポリシー

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*

Azure Information Protection チームは、Azure Information Protection クライアントの修正点と新機能を定期的に更新しています。 

最新の一般公開リリース バージョンと現在のプレビュー バージョン (利用できる場合) を [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。 通常数週間の短い遅延の後で、一般公開バージョンもまた Microsoft Update カタログに含められます (カテゴリ: **Azure Information Protection**)。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、「[Azure Information Protection クライアントのアップグレードと保守](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)」をご覧ください。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection クライアントの各一般公開 (GA) バージョンは、後続の GA バージョンがリリースされた後も最長で 6 か月間はサポートされます。 サポートされていないクライアント バージョンはこのページに含まれていません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

### <a name="release-history"></a>リリース履歴

Windows 用 Azure Information Protection クライアントのサポートされるリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。 

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、最新の GA リリースで問題が修正されているかどうかを確認することをお勧めします。 問題が解決されていない場合は、最新のプレビュー バージョンを確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="version-141510"></a>バージョン 1.41.51.0

> [!TIP]
> Office 365 セキュリティ/コンプライアンス センターからラベルを公開するため、Azure Information Protection の統合ラベル付けクライアントを評価することに関心をお持ちですか。 「[Azure Information Protection 統合ラベル付けクライアント:バージョン リリース情報](unifiedlabelingclient-version-release-history.md)」を参照してください。

**リリース日**: 2018 年 11 月 27 日

このバージョンには、MSIPC バージョン 1.0.3592.627 の RMS クライアントが含まれています。

**新機能:**

- Azure Information Protection により、既定で PDF 暗号化の ISO 標準を使用して PDF ファイルが保護されるようになりました。 以前は、クライアントの詳細設定を使ってこのサポートを有効にする必要がありました。
    
    クライアントを元に戻して、ファイル名拡張子 .ppdf を使って PDF ファイルを保護させるようにするには、同じ[クライアントの詳細設定](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)を使いますが、ここでは **False** を指定します。

- Microsoft Ignite で発表された Azure Information Protection 分析機能の[中央レポート機能](../reports-aip.md)のサポート。

- Excel で異なる色の[視覚的なマーキング](../configure-policy-markings.md)もサポートされるようになりました。

- 既存の S/MIME の展開について、Outlook で S/MIME の保護を自動的に適用するようにラベルを構成する、新しいクライアントの詳細設定 (プレビュー)。 [詳細情報](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- [切断されたコンピューター](client-admin-guide-customizations.md#support-for-disconnected-computers)に対して Azure Information Protection サービスのサインイン プロンプトが表示されないようにするためのレジストリの編集に代わる、新しいクライアントの詳細設定。

**修正内容**:

- Azure Information Protection クライアントで、エクスプローラー (右クリック) や PowerShell コマンドに対してファイル名拡張子 .msg、.rar、.zip が除外されなくなりました。 ただし、これらのファイル名拡張子は、スキャナーに対しては既定で除外されたままです。 

- Azure Information Protection クライアントでは、エクスプローラー (右クリック) を使う場合に、複数のファイル (複数選択および保護されたファイルを含むフォルダー) の保護を解除できます。

- Excel の場合:
    
    - セルの編集中にスプレッドシートを保存する場合、視覚的なマーキングが適用されるようになりました。
    
    - Excel 2010: スプレッドシートが共同作成者の[アクセス許可レベル](../configure-usage-rights.md#rights-included-in-permissions-levels)を使って保護されている場合、ファイルを右クリックして **[分類して保護する]** を選択したときに、**[ラベルの削除]** ボタンを使用できるようになりました。

- [他のラベル付けソリューションからヘッダーとフッターを削除する](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)ことができるクライアントの詳細設定で、カスタム レイアウトがサポートされるようになりました。

**その他の変更:**

- スキャナーのスケジュールを **[常時]** に設定した場合、スキャンの間に 30 秒の遅延が追加されるようになりました。

- スキャナーで、ファイルが既に保護されていた場合にそれがラベル付けする、ファイルの Rights Management 所有者が変更されなくなりました。

## <a name="version-137190"></a>バージョン 1.37.19.0

**リリース日**: 2018 年 9 月 17 日

このバージョンには、MSIPC バージョン 1.0.3592.627 の RMS クライアントが含まれています。

**新機能**: 

- 新しい[高度なクライアント構成](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)による、PDF 暗号化のための ISO 標準のサポート。 このオプションを **True** に設定すると、保護対象の PDF ドキュメントの .pdf ファイル名拡張子が保持され (.ppdf には変更されません)、この ISO 標準をサポートしている PDF リーダーで開くことができます。 現時点では、Azure Information Protection ビューアーを使用して手動でこれらの保護された PDF を開くよう、ユーザーに指示する必要があります。 これをサポートするために、ユーザーがこれらの保護された PDF ファイルのいずれかを開くと、各自のオペレーティング システム用に選択するためのアイコンを含むページが表示されます。

- 個人情報が含まれているドキュメントの分類に役立つ、新しい種類の機密情報のサポート。 [詳細情報](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- ユーザーに Azure Rights Management (Azure Information Protection for Office 365 とも呼ばれます) のライセンスが割り当てられている場合は、保護を適用するラベルが Office 2016 アプリ (最小バージョン 1805、ビルド 9330.2078) で表示されるようになりました。

- Word、Excel、および PowerPoint ファイルの**厳格な Open XML ドキュメント**形式に対するラベリングのサポート。 Open XML 形式の詳細については、Office のブログ記事「[New file format options in the new Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/)」(新しい Office の新しいファイル形式オプション) を参照してください。 

- Secure Islands によって保護されているファイルが PDF または Office ドキュメント以外である場合のサポート。 たとえば、保護されているテキストや画像のファイルなど。 もしくは、ファイル名拡張子が .pfile のファイル。 このサポートにより、Azure Information Protection スキャナーがファイルに機密情報があるかを検査して自動的に Azure Information Protection 向けにラベルを変更できるようにする、などの新しいシナリオが有効になります。 [詳細情報](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- 他のラベル付けソリューションによってドキュメントに適用されたヘッダーおよびフッターを削除するための、新しいクライアントの詳細設定。 [詳細情報](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)

- Azure Information Protection スキャナー:

    - 新しいコマンドレット [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner): 前の GA バージョン (1.29.5.0) 以前からアップグレードした後に 1 回実行する必要があります。
    
    - 新しいコマンドレット [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus): スキャナーのサービスの現在の状態を取得します。  
    
    - 新しいコマンドレット [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan): スケジュールが手動に設定されている場合に、スキャナーに 1 回限りのスキャン サイクルを開始するように指示します。
    
    - PDF 暗号化の ISO 標準を使用する際に、既定で PDF ドキュメントが保護されるようになりました。
    
    - [このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様向けに SharePoint Server 2010 がサポートされています。
    
- 1 つの場所からスキャナーを管理できる、Azure portal の新しい **[Azure Information Protection - Nodes (Preview)]\(Azure Information Protection - ノード (プレビュー)\)** ブレードのサポート。 Azure と接続されたスキャナーを配置すると、5 分ごとにそのスキャナーからの情報が更新されます。 このブレードからスキャナーを起動して、1 回限りのスキャン、すべてのファイルの再スキャン、スキャナーの状態のチェック、スキャン率の確認を行うことができます。

**修正内容**

- Azure Information Protection スキャナー:
    
    - SharePoint ライブラリで保護されたドキュメントで、*DefaultOwner* パラメーターがデータ リポジトリに使用されていない場合は、既定値として作成者の値の代わりに SharePoint エディターの値が使用されるようになりました。
    
    - スキャナー レポートには、Office ドキュメントの "最終変更者" が含まれます。
    
    - 「[スキャナーのレジストリの編集](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner)」セクションで説明されているように、レジストリを編集するときに、`*` ワイルドカードを使用してあらゆる種類のファイルを保護できるようになりました。

- クイック アクセス ツールバーの [次の項目] と [前の項目] の矢印アイコンを使用して電子メールを表示すると、各電子メールに正しいラベルが表示されます。

- エクスプローラー、PowerShell、またはスキャナーを使用して分類と保護を行う場合、Office ドキュメントのメタデータは削除も暗号化もされません。

- カスタムのアクセス許可では、アポストロフィを含む受信者のメール アドレスがサポートされます。

- SharePoint Online に格納されている保護されたドキュメントを開くことでこの操作が開始された場合、このコンピューター環境での初期化 (ブートストラップ) が成功します。

- ファイル エクスプローラー、PowerShell、またはスキャナーでの右クリックに対してクライアントを使用する場合、これはサポートされていないシナリオであるため、WebDav の場所のファイルではラベル付けがブロックされます。

- **[すべてのドキュメントとメールにラベルを付ける]** という[ポリシー設定](../configure-policy-settings.md)を構成する場合、クライアント アプリ (Word、Excel、PowerPoint、Outlook) 内で [ラベルの削除] アイコンが表示されません。

**その他の変更**:

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration):
    
    - *Schedule* パラメーターの値が **OneTime**、**Continuous**、**Never** ではなく、**Manual** と **Always** になりました。
        
    - *Type* パラメーターは削除されたため、[Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration) の実行時の出力からも削除されます。 既定では、最初のスキャン サイクル後に調査されるのは新しいファイルまたは変更されたファイルのみです。 以前にすべてのファイルを再スキャンするために *Type* パラメーターを **Full** に設定した場合、ここで *Reset* パラメーターと共に [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) を実行します。 また、手動スケジュールに対してもスキャナーを構成する必要があり、その場合、*Schedule* パラメーターを [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) で **Manual** に設定します。
    
- クライアントとスキャナーの既定の除外リストに .msg、.rar、.zip ファイルが含まれるようになりました。 スキャナーでは.rtf ファイルも除外されます。 [詳細情報](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- ポリシーのバージョンは、1.4 に変更されます。 [切断されたコンピューターを構成する](client-admin-guide-customizations.md#support-for-disconnected-computers)には、バージョン番号の特定が必要です。

- **[ヘルプとフィードバック]** ダイアログ ボックスの **[フィードバックの送信]** リンクが削除されました。 これは **[問題の報告]** に一時的に置き換えられていたもので、既定では Microsoft に電子メールが送信されていました。 2018 年 12 月以降、**[問題の報告]** オプションは既定で表示されなくなりますが、リンクの HTTP 文字列を指定する[クライアントの詳細設定](client-admin-guide-customizations.md#add-report-an-issue-for-users)を使用して追加することができます。 たとえば、ユーザーが問題を報告するための、カスタマイズされた独自の Web ページや、ヘルプ デスクに送信される電子メール アドレスです。 

## <a name="version-12950"></a>バージョン 1.29.5.0 

**リリース日**: 2018 年 6 月 26 日

このバージョンには、MSIPC バージョン 1.0.3403.1224 の RMS クライアントが含まれています。

**修正内容**:

- Outlook バージョン 16.0.9324.1000 以降 (クイック実行) の場合、Azure Information Protection バーに最新のモニター ディスプレイ オプションが表示されます。以前は Outlook アプリケーションの外部にバーが表示されることがありました。

- [Office アプリケーションごとに](../configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)構成する視覚的マーキングが、以前は Azure Information Protection ラベルによって適用されていたヘッダーやフッターに置き換わりました。

- Excel ファイルが既にラベル付けされていてラベルが視覚的なマーキングを適用している場合、新しいシートにもラベルの視覚的なマーキングが適用されるようになりました。

- [既存のカスタム プロパティを使用して Office ドキュメントにラベルを付ける](client-admin-guide-customizations.md#label-an-office-document-by-using-an-existing-custom-property)ためにクライアントの詳細設定を使用する場合、自動ラベル付けは手動ラベル付けをオーバーライドしません。

## <a name="version-127480"></a>バージョン 1.27.48.0

**リリース日**: 2018 年 5 月 30 日

このバージョンには、MSIPC バージョン 1.0.3403.1224 の RMS クライアントが含まれています。

**新機能**: 

- Azure Information Protection スキャナー:
    
    - ファイルの種類のリストを指定して、スキャン対象や除外対象を指定することができます。 このリストを指定するには、[Set-AIPScannerScannedFileType](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes) を使用します。 ファイルの種類のリストを指定した後、新しいファイルの種類をリストに追加するには、[Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes) を使用します。リストからファイルの種類を削除するには、[Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes) を使用します。
    
    - 既定のラベルを適用することで、内容を検査することなく、ファイルにラベル付けすることができます。 [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) コマンドレットを使用し、*MatchPolicy*パラメーターを **Off** に設定します。 
    
    - ラベルを自動分類用に構成しなくても、機密情報の種類のファイルを検出できます。 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットを使用し、*DiscoverInformationTypes* パラメーターを **All** に設定します
    
    - 既定では、Office ドキュメントの種類のみが保護されます。 その他のファイルの種類は、レジストリ内に定義することで保護できます。 詳しくは、開発者ガイダンスの「[ファイル API の構成](../develop/file-api-configuration.md)」をご覧ください。
    
    - 既定では、スキャナーは低整合性レベルで実行されます。これは、特権を持ったアカウントでスキャナーを実行する場合に、セキュリティを高めるためです。 スキャナーを実行するサービス アカウントに、[スキャナーの前提条件](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner)のセクションで説明されている権限だけが付与されている場合、低整合性レベルは必要ありません。これはパフォーマンスに悪影響を及ぼすため、推奨されません。 高度なクライアント設定を使用すると、低整合性レベルを無効にできます。 [詳細情報](client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) 
    
- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/Get-AIPFileStatus) の出力に、Rights Management 所有者、Rights Management 発行者、およびコンテンツが保護された日付が表示されるようになりました。
 
**その他の変更**:

- Azure Information Protection スキャナー: 
    
    - スキャナーの以前のバージョンをインストールした場合は、Azure Information Protection クライアントをアップグレードした後、[Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) でスキャナーのインストール コマンドを再実行します。 スキャナーとリポジトリの構成設定は保持されます。 スキャナーを再インストールすると、スキャナー サービス アカウントに対してスキャナー データベースの削除アクセス許可が付与されます。これはレポートのために必要となります。    
    
    - [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) の *ScanMode* パラメーターの名前が、**Enforce** に変更されました (値は Off と On)。
    
    - 既定のラベルを使用する場合に、既定のラベルをポリシー設定として構成する必要がなくなりました。 代わりに、リポジトリ構成で既定のラベルを指定します。 

- [設定完了] ウェルカム ページと [Azure Information Protection の新機能] ページが削除されました (以前は、Office アプリケーションの初回使用時に表示されていました)。

## <a name="next-steps"></a>次の手順

クライアントのインストールと使用の詳細: 

- ユーザー向け: [クライアントのダウンロードとインストール](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)

