---
title: Azure Information Protection クライアントのバージョンの履歴とサポート ポリシー
description: Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点、サポートのライフサイクル ポリシーについて説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 43f7f685cfa1567084ebdc0877215229b0ae592b
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64768342"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure Information Protection クライアント:バージョン リリース履歴とサポート ポリシー

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> *手順:[Windows 用 Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection チームは、Azure Information Protection クライアントの修正点と新機能を定期的に更新しています。 

最新の一般公開リリース バージョンと現在のプレビュー バージョン (利用できる場合) を [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。 通常数週間の短い遅延の後で、最新の一般公開バージョンもまた Microsoft Update カタログに含められます (カテゴリ:**Azure Information Protection**)。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、「[Azure Information Protection クライアントのアップグレードと保守](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)」をご覧ください。

> [!TIP]
> ラベルが Office 365 セキュリティとコンプライアンス センター、Microsoft 365 セキュリティ センター、または Microsoft 365 コンプライアンス センターからパブリッシュされるので、Azure Information Protection 統合ラベル付けのクライアントに興味があるでしょうか。 これを Azure Information Protection クライアントをアップグレードするにはダウンロードして、Microsoft ダウンロード センターから、統一されたラベル付けクライアントをインストールすると、[統合型のラベル付けクライアント](unifiedlabelingclient-version-release-history.md)します。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection クライアントの各一般公開 (GA) バージョンは、後続の GA バージョンがリリースされた後も最長で 6 か月間はサポートされます。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

### <a name="release-history"></a>リリース履歴

Windows 用 Azure Information Protection クライアントのサポートされるリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。 

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、最新の GA リリースで問題が修正されているかどうかを確認することをお勧めします。 問題が解決しない場合は、(該当する場合)、現在のプレビュー バージョンを確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="version-1482040"></a>バージョン 1.48.204.0

**リリース日**: 04/16/2019

このバージョンには、MSIPC バージョン 1.0.3592.627 の RMS クライアントが含まれています。

**新機能:**

- PowerShell を使用してではなく、Azure portal から Azure Information Protection スキャナーが構成されます。
    
    一般公開バージョンのスキャナーからアップグレードする場合は、アップグレード プロセスが以前のバージョンとは異なるため、「[Azure Information Protection スキャナーのアップグレード](client-admin-guide.md#upgrading-the-azure-information-protection-scanner)」を必ずお読みください。

- スキャナーは、プロファイル名を指定するときにようになりました複数の構成データベースと同じ SQL server インスタンスでサポートします。

- ドキュメントおよび電子メール内の資格情報を識別するのに役立つ、次の機密情報の種類のサポート。
    - Azure Service Bus の接続文字列
    - Azure IoT の接続文字列
    - Azure ストレージ アカウント
    - Azure IAAS データベースの接続文字列および Azure SQL の接続文字列
    - Azure Redis Cache の接続文字列
    - Azure SAS
    - SQL Server の接続文字列
    - Azure DocumentDB の認証キー
    - Azure 発行設定のパスワード
    - Azure Storage のアカウント キー (汎用)

- Outlook で送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する、新しいクライアント詳細設定。 [詳細情報](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    
    ドメインはアクションごとに除外できるように OutlookCollaborationTrustedDomains のプレビュー バージョンのクライアントの詳細プロパティを構成した場合は、この設定は、次の 3 つの新しい設定によっては置き換えられます今すぐに注意してください。OutlookWarnTrustedDomains、OutlookJustifyTrustedDomains、および OutlookBlockTrustedDomains です。

- [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) コマンドレットを使ってファイルにラベルを付けて保護する場合、*EnableTracking* パラメーターを使ってドキュメント追跡サイトにファイルを登録できます。 [詳細情報](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- カスタム アクセス許可を表示しないようポリシー設定を構成する場合にのみ適用される、新しいクライアント詳細設定。カスタム アクセス許可で保護されているファイルがある場合に、ユーザーが (保護設定を変更するアクセス許可を持っていれば) 表示および変更できるように、ファイル エクスプローラーにカスタム アクセス許可オプションが表示されます。 [詳細情報](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)

- エンドポイントの検出の[Azure Information Protection analytics](../reports-aip.md)します。
    
- 2 つの新しいアドバンスト、クライアントは、次のシナリオの analytics の設定。
    
    - Azure portal でコンテンツ一致を収集するチェック ボックスをオンにしてあるときに、ユーザーのサブセットについて情報の種類の一致が送信されないようにします。 [詳細情報](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - **データ検出**レポートをファイルには、機密情報が含まれるかどうかを表示します。 [詳細情報](client-admin-guide-customizations.md#enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents)

**修正内容**:

- Azure Information Protection 分析で、送信元オペレーティング システムのロケールが英語の場合に、パスおよびファイル名に含まれる非 ASCII 文字が疑問符 (**?**) で表示されません。

- ユーザーがWord 文書に新しいセクションを追加した後で再度ラベルを付ける場合、新しい視覚的なマーキングが一貫して適用されます。

- Azure Information Protection クライアントで、Rights Management 共有アプリケーションによって保護されていた PDF 文書の保護が正しく解除されます。

- ユーザー定義のアクセス許可に対して親ラベルが構成されている場合、PowerShell およびスキャナーによってサブラベルが正しく適用されます。

- Azure Information Protection クライアントで、[統合ラベル付けをサポートしているクライアント](../configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)によって適用されているラベルが正しく表示されます。

- エクスプローラーと右クリック、PowerShell、およびスキャナーによって保護が解除された後に、ドキュメントが Office で回復メッセージなしで正しく開きます。

- クライアント詳細設定を使用して [Outlook の既定のラベル](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook)を設定すると、ユーザーに対してすべてのサブラベルが無効化されている場合でも、これらのサブラベルを含む親ラベルを適用できます。

- [ポリシー設定](../configure-policy-settings.md)の **[添付ファイルのあるメール メッセージの場合、それらの添付ファイルの最上位の分類に一致するラベルを適用します]** を使用し、ユーザー定義のアクセス許可で最上位の分類のラベルが構成されている場合、以前はそのラベルが電子メールに適用されましたが、保護は適用されませんでした。 現在の動作は次のとおりです。
    - ラベルのユーザー定義のアクセス許可に Outlook (転送不可) が含まれる場合: そのラベルとその転送不可保護を電子メールに適用します。
    - ラベルのユーザー定義のアクセス許可が Word、Excel、PowerPoint、およびファイル エクスプローラーのみを対象とする場合: 電子メールにラベルが適用されず、保護も適用されません。

**その他の変更:**

- 推奨または自動の分類に対して構成するラベルで、次の機密情報の種類がサポートされなくなりました。
    - EU の電話番号
    - EU の GPS 座標

- Azure Information Protections スキャナーは Azure portal を使用して構成されるため、次のコマンドレットが非推奨になり、データ リポジトリまたはファイルの種類一覧の構成に使用できなくなりました。
    - Add-AIPScannerRepository
    - Add-AIPScannerScannedFileTypes
    - Get-AIPScannerRepository
    - Remove-AIPScannerRepository
    - Remove-AIPScannerScannedFileTypes
    - Set-AIPScannerRepository
    - Set-AIPScannerScannedFileTypes

- Azure Information Protection スキャナーが Azure portal から構成をダウンロードできないシナリオに対処するための新しい PowerShell コマンドレット [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)。

- Azure Information Protection スキャナーで、.zip ファイルが既定で除外されなくなりました。 .zip ファイルの検査およびラベル付けの方法については、管理ガイドの「[.zip ファイルを検査するには](client-admin-guide-file-types.md#to-inspect-zip-files)」セクションをご覧ください。

- [ポリシー設定](../configure-policy-settings.md) **[分類ラベルを低くする、ラベルを削除する、保護を削除する場合、ユーザーは理由を提供する必要があります]** がスキャナーに適用されなくなりました。 スキャナーのプロファイルで **[ファイルのラベルを書き換える]** 設定を **[オン]** に構成すると、スキャナーでこれらのアクションが実行されます。

## <a name="version-141510"></a>バージョン 1.41.51.0

**リリース日**: 2018 年 11 月 27 日

このバージョンには、MSIPC バージョン 1.0.3592.627 の RMS クライアントが含まれています。

**新機能:**

- Azure Information Protection により、既定で PDF 暗号化の ISO 標準を使用して PDF ファイルが保護されるようになりました。 以前は、クライアントの詳細設定を使ってこのサポートを有効にする必要がありました。
    
    クライアントを元に戻して、ファイル名拡張子 .ppdf を使って PDF ファイルを保護させるようにするには、同じ[クライアントの詳細設定](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)を使いますが、ここでは **False** を指定します。

- データのサポートを監査[中央レポート機能](../reports-aip.md)Microsoft Ignite 2018 で発表された、Azure Information Protection の analytics を使用しています。

- Excel で異なる色の[視覚的なマーキング](../configure-policy-markings.md)もサポートされるようになりました。

- 既存の S/MIME の展開について、Outlook で S/MIME の保護を自動的に適用するようにラベルを構成する、新しいクライアントの詳細設定。 [詳細情報](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- [切断されたコンピューター](client-admin-guide-customizations.md#support-for-disconnected-computers)に対して Azure Information Protection サービスのサインイン プロンプトが表示されないようにするためのレジストリの編集に代わる、新しいクライアントの詳細設定。

- 以下のポリシー設定を使う際に[サブラベルの順序をサポートする](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)ための、新しいクライアントの詳細設定。
    - **添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します**

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

- ユーザーに Azure Rights Management (別名: Azure Information Protection for Office 365) のライセンスが割り当てられている場合は、Office 365 Business または Microsoft 365 Business の Office 365 アプリ内で、保護を適用するラベルが表示されるようになりました。

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


## <a name="next-steps"></a>次の手順

クライアントのインストールと使用の詳細: 

- ユーザー向け: [クライアントのダウンロードとインストール](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)
