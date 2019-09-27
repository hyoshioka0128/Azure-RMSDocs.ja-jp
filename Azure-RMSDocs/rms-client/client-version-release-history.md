---
title: Azure Information Protection クライアント-バージョン履歴 & サポートポリシー
description: Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点、サポートのライフサイクル ポリシーについて説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b64e10f93abd89299405e8b4df8e20ca2393616d
ms.sourcegitcommit: a091cabd5ad24b4534b5f69f029843037c7872d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314060"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure Information Protection クライアント:バージョン リリース履歴とサポート ポリシー

>*適用対象:Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、WINDOWS 7 SP1、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *手順:[Windows 用 Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection チームは、Azure Information Protection クライアントの修正点と新機能を定期的に更新しています。 

最新の一般公開リリース バージョンと現在のプレビュー バージョン (利用できる場合) を [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。 

通常は数週間後に、一般公開されている最新バージョンが、 **Microsoft Azure Information Protection** > Microsoft Azure 情報の製品名と共に Microsoft Update カタログにも含まれるようになります。**保護クライアント**および**更新プログラム**の分類。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、「[Azure Information Protection クライアントのアップグレードと保守](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)」をご覧ください。

> [!TIP]
> ラベルが Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、または Microsoft 365 コンプライアンスセンターから公開されているため、Azure Information Protection 統合ラベルクライアントの使用に関心がある場合は、 Microsoft ダウンロードセンターから、統合されたラベル付けクライアントをダウンロードしてインストールすると、Azure Information Protection クライアントをこの統一された[ラベル付けクライアント](unifiedlabelingclient-version-release-history.md)にアップグレードできます。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection クライアントの各一般公開 (GA) バージョンは、後続の GA バージョンがリリースされた後も最長で 6 か月間はサポートされます。 このセクションを除き、ドキュメントにはサポートされていないバージョンのクライアントに関する情報は含まれていません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン:

|クライアントのバージョン|リリース日|
|--------------|-------------|
|1.37.19.0|2018 年 9 月 17 日|
|1.29.5.0|2018 年 6 月 26 日|
|1.27.48.0|2018 年 5 月 30 日|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|03/15/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|10/27/2016|
|1.1.23.0|10/01/2016|

このページで使用される日付形式は、*月/日/年*です。

6/2/2019 以降、Azure Information Protection のラベル付けサービスには、TLS 1.2 を使用する接続が必要です。

1\.4.21.0 リリース03/15/2017 のすべてのクライアントバージョンが TLS 1.2 をサポートしています。 クライアントバージョン**1.3.155.2**、 **1.2.4.0**、および**1.1.23.0**は TLS 1.2 を使用しないため、Azure Information Protection ポリシーをダウンロードできなくなります。

### <a name="release-history"></a>リリース履歴

Windows 用 Azure Information Protection クライアントのサポートされるリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、最新の GA リリースで問題が修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="version-153100"></a>バージョン1.53.10.0

**リリース日**: 07/15/2019

このバージョンには、RMS クライアントの MSIPC バージョン1.0.3889.0419 が含まれています。

**新機能:**

- ポリシー設定から Outlook メッセージを除外する新しい高度なクライアント設定**すべてのドキュメントと電子メールにラベルを付ける必要があり**ます。 [詳細情報](client-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)

- 新しい高度なクライアント設定。 Outlook でポップアップメッセージを実装する設定をカスタマイズして、送信される電子メールを警告、ブロック、またはブロックします。 この新しい詳細設定では、添付ファイルのない電子メールメッセージに対して別のアクションを設定できます。 [詳細情報](client-admin-guide-customizations.md#to-specify-a-different-action-for-email-messages-without-attachments)

**修正内容**:

- エクスプローラーを使用する場合、右クリックすると、保護がラベルとは別に適用されているファイルにラベルを付けることができます。 たとえば、ユーザーがファイルにカスタムアクセス許可を適用したとします。

- 電子メールスレッドの [転送不可] オプションを、ユーザー定義のアクセス許可用に構成され、転送しないラベルに置き換えると、元の受信者は引き続き電子メールメッセージを開くことができます。

- 次のシナリオでは、ラベルが自動的に設定されたことを示すラベルのツールヒントにユーザーが表示されなくなりました。ユーザーは、ラベルが付けられているが自動的に保護されていないドキュメントが添付された保護された電子メールを受信します。 差出人と同じ組織のユーザーがドキュメントを開くと、保護設定の対応するラベルがドキュメントに適用されます。

- [Protect-rmsfile](/powershell/module/azureinformationprotection/unprotect-rmsfile)コマンドレットを実行するための最小[使用権限](../configure-usage-rights.md#usage-rights-and-descriptions)は、**コピー** (EXTRACT) ではなく **、名前を付けて保存、エクスポート**(エクスポート) されるようになりました。

## <a name="version-1482040"></a>バージョン1.48.204.0

**リリース日**: 04/16/2019

01/15/2020 までサポート

このバージョンには、MSIPC バージョン 1.0.3592.627 の RMS クライアントが含まれています。

**新機能:**

- Azure Information Protection スキャナーは、PowerShell を使用するのではなく、Azure portal から構成されるようになりました。
    
    一般公開バージョンのスキャナーからアップグレードする場合は、アップグレード プロセスが以前のバージョンとは異なるため、「[Azure Information Protection スキャナーのアップグレード](client-admin-guide.md#upgrading-the-azure-information-protection-scanner)」を必ずお読みください。

- スキャナーは、プロファイル名を指定するときに、同じ SQL server インスタンス上の複数の構成データベースをサポートするようになりました。

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

- エンドポイント探索による[Azure Information Protection analytics](../reports-aip.md)のサポート: ユーザーが最初に Office ドキュメントを保存したときに検出された機密情報を報告する (Word、Excel、PowerPoint 用のデスクトップアプリを使用):
    - この情報を見つけるには、ドキュメントにラベルを付ける必要はありません。
    - 機密情報は、定義済みおよびカスタムの情報の種類によって識別されます。
    - 機密情報の種類が Azure Information Protection analytics に送信されないようにする場合は、[クライアントの詳細設定](client-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)を使用してエンドポイントの検出を無効にすることができます。

- Outlook で送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する、新しいクライアント詳細設定。 [詳細情報](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    
    プレビューバージョンの OutlookCollaborationTrustedDomains のアドバンストクライアントプロパティを構成した場合、この設定は3つの新しい設定に置き換えられるため、ドメインがアクションごとに除外されるようになりました。OutlookWarnTrustedDomains、Outlookジャスト Ifytrusteddomains、および OutlookBlockTrustedDomains。

- [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) コマンドレットを使ってファイルにラベルを付けて保護する場合、*EnableTracking* パラメーターを使ってドキュメント追跡サイトにファイルを登録できます。 [詳細情報](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- Azure portal のチェックボックスをオンにして、機密データをより深く分析できるようにするための、 [Azure Information Protection analytics](../reports-aip.md)の新しいクライアント設定の1つ。 この設定は、クライアントとスキャナーに適用されます。 [詳細情報](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)

- カスタム アクセス許可を表示しないようポリシー設定を構成する場合にのみ適用される、新しいクライアント詳細設定。カスタム アクセス許可で保護されているファイルがある場合に、ユーザーが (保護設定を変更するアクセス許可を持っていれば) 表示および変更できるように、ファイル エクスプローラーにカスタム アクセス許可オプションが表示されます。 [詳細情報](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)


**修正内容**:

- Azure Information Protection 分析で、送信元オペレーティング システムのロケールが英語の場合に、パスおよびファイル名に含まれる非 ASCII 文字が疑問符 ( **?** ) で表示されません。

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

- 次の機密情報の種類は、推奨または自動分類用に構成するラベルでは[サポートされなくなり](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client)ました。
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

- [ポリシー設定](../configure-policy-settings.md) **[分類ラベルを低くする、ラベルを削除する、保護を削除する場合、ユーザーは理由を提供する必要があります]** がスキャナーに適用されなくなりました。 スキャナーのプロファイルで [**ファイル**のラベルを **[オン**] に設定する] を構成し、[**ラベルダウングレードを許可**する] チェックボックスをオンにすると、これらの操作が実行されます。

## <a name="version-141510"></a>バージョン 1.41.51.0

**リリース日**: 2018 年 11 月 27 日

10/16/2019 までサポート

このバージョンには、MSIPC バージョン 1.0.3592.627 の RMS クライアントが含まれています。

**新機能:**

- Azure Information Protection により、既定で PDF 暗号化の ISO 標準を使用して PDF ファイルが保護されるようになりました。 以前は、クライアントの詳細設定を使ってこのサポートを有効にする必要がありました。
    
    クライアントを元に戻して、ファイル名拡張子 .ppdf を使って PDF ファイルを保護させるようにするには、同じ[クライアントの詳細設定](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)を使いますが、ここでは **False** を指定します。

- Azure Information Protection analytics を使用した、[中央レポート](../reports-aip.md)のデータサポートの監査。 この情報には、ラベルの使用状況を監視したり、ラベル付きドキュメントや電子メールにユーザーがアクセスしたりするためのラベルの使用方法が含まれています。

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
    
    - Excel 2010: スプレッドシートが共同作成者の[アクセス許可レベル](../configure-usage-rights.md#rights-included-in-permissions-levels)を使って保護されている場合、ファイルを右クリックして **[分類して保護する]** を選択したときに、 **[ラベルの削除]** ボタンを使用できるようになりました。

- [他のラベル付けソリューションからヘッダーとフッターを削除する](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)ことができるクライアントの詳細設定で、カスタム レイアウトがサポートされるようになりました。

**その他の変更:**

- スキャナーのスケジュールを **[常時]** に設定した場合、スキャンの間に 30 秒の遅延が追加されるようになりました。

- スキャナーで、ファイルが既に保護されていた場合にそれがラベル付けする、ファイルの Rights Management 所有者が変更されなくなりました。

## <a name="next-steps"></a>次の手順

クライアントのインストールと使用の詳細: 

- ユーザー向け: [クライアントのダウンロードとインストール](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)
