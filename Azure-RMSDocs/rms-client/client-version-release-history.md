---
title: Azure Information Protection クライアント - バージョン リリース履歴とサポート ポリシー
description: Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点、サポートのライフサイクル ポリシーについて説明します。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4ff64b5bb4f73533352aa5497a98263c86842800
ms.sourcegitcommit: c41490096af48e778947739e320e0dc8511f6c68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2018
ms.locfileid: "34423257"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure Information Protection クライアント: バージョン リリース履歴とサポート ポリシー

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

Azure Information Protection チームは、Azure Information Protection クライアントの修正点と新機能を定期的に更新しています。 

最新の GA リリース バージョンと現在のプレビュー バージョンを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。 これらのバージョンは、WSUS や構成マネージャー、またはその他の Microsoft Update を使用するソフトウェア展開メカニズムを使用してクライアントを展開できるように、Microsoft Update カタログにも含まれます (カテゴリ: **Azure Information Protection**)。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection クライアントの各一般公開 (GA) バージョンは、後続の GA バージョンがリリースされた後も最長で 6 か月間はサポートされます。 サポートされていないクライアント バージョンはこのページに含まれていません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

### <a name="release-history"></a>リリース履歴

Windows 用 Azure Information Protection クライアントのサポートされるリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。 

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、最新の GA リリースで問題が修正されているかどうかを確認することをお勧めします。 問題が解決されていない場合は、最新のプレビュー バージョンを確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="versions-later-than-12660"></a>1.26.6.0 以降のバージョン

1.26.6.0 以降のバージョンのクライアントがある場合、それはテストおよび評価目的のプレビュー ビルドです。 
 
**リリース日**: 2018 年 5 月 21 日 

現行のプレビュー バージョンは **1.27.48.0** です。クライアントの現行 GA バージョン以降、次の変更があります。  

**新機能**: 

- Azure Information Protection スキャナー:
    
    - ファイルの種類のリストを指定して、スキャン対象や除外対象を指定することができます。 このリストを指定するには、[Set-AIPScannerScannedFileType](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes) を使用します。 ファイルの種類のリストを指定した後、新しいファイルの種類リストを追加するには、[Add-AIPScannerScannedFileType](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileType) を使用します。リストからファイルの種類を削除するには、[Remove-AIPScannerScannedFileType](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileType) を使用します。
    
    - 既定のラベルを適用することで、内容を検査することなく、ファイルにラベル付けすることができます。 [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) コマンドレットを使用し、*MatchPolicy*パラメーターを **Off** に設定します。 
    
    - ラベルを自動分類用に構成しなくても、機密情報の種類のファイルを検出できます。 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットを使用し、*DiscoverInformationTypes* パラメーターを **All** に設定します
    
    - 既定では、Office ドキュメントの種類のみが保護されます。 その他のファイルの種類は、レジストリ内に定義することで保護できます。 詳しくは、開発者ガイダンスの「[ファイル API の構成](../develop/file-api-configuration.md)」をご覧ください。
    
    - 既定では、スキャナーは低整合性レベルで実行されます。これは、特権を持ったアカウントでスキャナーを実行する場合に、セキュリティを高めるためです。 スキャナーを実行するサービス アカウントに、[スキャナーの前提条件](../deploy-use/deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner)のセクションで説明されている権限だけが付与されている場合、低整合性レベルは必要ありません。これはパフォーマンスに悪影響を及ぼすため、推奨されません。 高度なクライアント設定を使用すると、低整合性レベルを無効にできます。 [詳細情報](../rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) 
    
- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/Get-AIPFileStatus) の出力に、Rights Management 所有者、Rights Management 発行者、およびコンテンツが保護された日付が表示されるようになりました。
 
**その他の変更**:

- Azure Information Protection スキャナー: 
    
    - [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) の *ScanMode* パラメーターの名前が、**Enforce** に変更されました (値は Off と On)。
    
    - 既定のラベルを使用する場合に、既定のラベルをポリシー設定として構成する必要がなくなりました。 代わりに、リポジトリ構成で既定のラベルを指定します。 

- [設定完了] ウェルカム ページと [Azure Information Protection の新機能] ページが削除されました (以前は、Office アプリケーションの初回使用時に表示されていました)。

## <a name="version-12660"></a>バージョン 1.26.6.0

**リリース日**: 2018 年 4 月 17 日

このバージョンには、MSIPC バージョン 1.0.3403.1224 の RMS クライアントが含まれています。

**新機能**:

- Azure Information Protection スキャナー: クライアントに付属する PowerShell モジュールには、オンプレミス データ ソース上のファイルを検出、分類、保護できるよう、スキャナーをインストールし、構成するための新しいコマンドレットが含まれています。 インストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](../deploy-use/deploy-aip-scanner.md)」を参照してください。 

- テキスト文字列に "If.App" 変数ステートメントを使用し、Word、Excel、PowerPoint、Outlook にさまざまな視覚的マーキングを設定し、アプリケーションの種類を識別できるようになりました。 [詳細情報](../deploy-use/configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)

- [ポリシー設定](../deploy-use/configure-policy-settings.md)の **[Display the Information Protection bar in Office apps]\(Office アプリで Information Protection バーを表示する\)** 対応になりました。 この設定をオフにすると、リボンの **[保護]** ボタンからラベルを選択します。

- バックグラウンドで分類の継続的な実行を有効にする新しい高度なクライアント設定 (プレビュー段階)。 この設定が有効になっている場合、Office アプリでは、推奨されている自動分類が、文書が保存されたときに実行されるのではなく、バックグラウンドで継続的に実行されます。 このように動作が変更されたことで、SharePoint Online に格納されている文書に自動 (推奨) 分類を適用できるようになりました。 [詳細情報](client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)

- クライアント設定が新しくなりました。Outlook では、Azure Information Protection ポリシーで構成した既定のラベルが適用されません。 別の既定のラベルを適用できるか、ラベルがありません。 [詳細情報](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook) 

- Office アプリでは、カスタムのアクセス許可を指定するとき、アドレス帳アイコンからユーザーを参照し、選択できるようになりました。 エクスプローラーでカスタムのアクセス許可を指定するとき、同じような操作性が与えられます。

- PowerShell を使用するが、**ローカルでログオンする**権限を付与できないサービス アカウントに完全に非対話式の認証方法を与えます。 この認証方法では、[Set-AIPAuthentication](/powershell/module/azureinformationprotection/Set-AIPAuthentication) と共に新しい *Token* パラメーターを使用し、タスクとして PowerShell スクリプトを実行する必要があります。 [詳細情報](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)

- [Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication) に新しいパラメーター、*IntegratedAuth* が追加されました。 このパラメーターは AD RMS のサーバー モードをサポートします。このモードは AD RMS で Windows Server FCI をサポートするために必要になります。


**修正内容**:

以下を含む、安定性の問題と特定のシナリオの問題が修正されました。

- Office バージョン 16.0.8628.2010 以降 (クイック実行) の場合、Azure Information Protection バーに最新のモニター ディスプレイ オプションが表示されます。以前は Office アプリケーションの外部にバーが表示されることがありました。

- Azure Information Protection を利用する 2 つの組織がラベル付きの文書とメールを共有しているとき、独自のラベルの保持されます。他の組織のラベルで置換されることはありません。

- Excel の場合:
        
    - Office テーマや Windows テーマを変更できるようになりました。以前は Excel では、テーマの変更後、データが表示されませんでした。
        
    - 相互参照を含むセルに対応しました。以前は、そのようなセルではテキストが壊れてしまいました。
    
    - 日本語、中国語、韓国語の文字の入力に対応しました。以前は、ウィンドウが閉じてしまい、これらの文字を選択できませんでした。
    
    - コメントに対応しました。以前は、入力中にコメントが閉じてしまいました。

- PowerPoint の場合: 共同作成に対応しました。以前は、データの損失が発生する可能性がありました。

- 推奨分類または自動分類で、ファイル名に .xml 拡張子が付くファイルを調べることができるようになりました。

- 20 MB を超えるテキスト ベースの保護ファイル (.ptxt と .pxml) を開けるようになりました。 
- Outlook リマインダーの利用時の Outlook の停止を回避します。

- Office 64 ビットでブートストラップできます。文書やメールを保護できます。

- Word、Excel、PowerPoint、エクスプローラーのユーザー定義アクセス許可にラベルを設定できるようになりました。また、クライアント詳細設定を利用し、カスタムのアクセス許可オプションを非表示にできます。 [詳細情報](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users) 

- クライアントにインストールされていないフォント名について、Azure Information Protection ポリシーの視覚的マーカーが設定されている場合、Calibri フォントが使用されます。

- Azure Information Protection クライアントのアップグレード後に Office がクラッシュする事態を回避できるようになりました。

- Office アプリでパフォーマンスとメモリ消費が改善されました。

- ユーザー定義アクセス許可と HYOK (AD RMS) 保護にラベルを設定するとき、保護で Azure Rights Management サービスが不適切に使用されることがなくなりました。

- 一貫性の高い管理作業を可能にするため、下位ラベルが上位ラベルから視覚的マーキングや保護設定を継承することがなくなりました。


## <a name="version-110560"></a>バージョン 1.10.56.0

**リリース日**: 2017 年 9 月 18 日

このバージョンには、MSIPC バージョン 1.0.3219.0619 の RMS クライアントが含まれています。

**新機能**:

- 新しい Office 365 DLP 条件に対応。この条件はラベルに設定できます。 詳細については、「[Azure Information Protection ラベルの条件を構成する](../deploy-use/configure-policy-classification.md)」を参照してください。

- ユーザー定義アクションのために作られたラベルに対応。 Outlook の場合、このラベルは [転送不可] オプションに自動的に適用されます。 Word、Excel、PowerPoint、エクスプローラーの場合、このラベルはカスタムのアクセス許可を指定するようにユーザーに求めます。 詳細については、「[Azure Information Protection ラベルを保護するように構成する](../deploy-use/configure-policy-protection.md)」を参照してください。

- ラベルでは、複数言語をサポートします。 2017 年 8 月 30 日以降、[既定のポリシー](../deploy-use/configure-policy-default.md)では、このバージョンのクライアントがユーザーに表示する言語が複数サポートされています。 この日付より前にユーザーに既定のポリシーから希望する言語でラベルが表示されるようにする方法、および構成するラベルについては、[Azure Information Protection でさまざまな言語のラベルを構成する方法](../deploy-use/configure-policy-languages.md)に関するページを参照してください。

- ラベルは [Information Protection] バーに表示されるほか、Office リボンの **[保護]** ボタンをクリックしたときに表示されます。 

- 次の Visio ファイルの種類のネイティブ保護: .vsdm、.vsdx、.vssm、.vssx、.vstm、.vstx

- Azure Portal で設定する詳細なクライアント構成に対応。 この構成には次のものが含まれます。
    
    - [Outlook の [転送不可] ボタンを表示または非表示にする](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [ユーザーに対してカスタムのアクセス許可オプションを利用可能または利用不可にする](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [Azure Information Protection バーを完全に非表示にする](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
    - [Outlook で推奨分類を有効にする](../rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- PowerShell の場合、新しい PowerShell コマンドレットの [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) と [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication) を利用し、非対話式にファイルにラベルを付けることができます。 このコマンドレットについては、管理者ガイドの [PowerShell セクション](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)をご覧ください。

- PowerShell コマンドレットの [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) と [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) には、**Owner** と **PreserveFileDetails** という新しいパラメーターがあります。 このパラメーターを利用すれば、Owner カスタム プロパティに電子メール アドレスを指定したり、ラベルを付ける文書の日付を変更せずに残したりできます。

**修正内容**:

以下を含む、安定性の問題と特定のシナリオの問題が修正されました。

- 以前は 1 GB を超える大きなファイルが破損することがありましたが、そのような大きなファイルが通常は保護されるようになりました。 ファイル サイズの上限は、ハード ディスクの空き領域と使用可能なメモリで決まります。 ファイル サイズの上限については、管理者ガイドの「[保護がサポートされているファイルのサイズ](client-admin-guide-file-types.md#file-sizes-supported-for-protection)」を参照してください。

- Azure Information Protection クライアント ビューアーは、保護されている PDF (.ppdf) ファイルを閲覧限定で開きます。

- SharePoint Server に保存されているファイルにラベルを付け、保護できるようになりました。

- 複数の行に透かしを付けることができるようになりました。 また、視覚的なマーキングが、文書が保存されるたびにではなく、[最初に保存したときだけ](../deploy-use/configure-policy-markings.md#when-visual-markings-are-applied)文書に適用されるようになりました。

- **[ヘルプとフィードバック]** ダイアログ ボックスの **[診断の実行]** オプションが **[設定のリセット]** になりました。 このアクションの動作が変更され、ユーザーのサインアウトと Azure Information Protection ポリシーの削除が追加されました。 詳細については、管理者ガイドの「[More information about the Reset Settings option](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option)」 ([設定のリセット] オプションの詳細) を参照してください。

- プロキシ認証対応になりました。

ユーザー エクスペリエンス改善のため、次のような修正がありました。

- カスタムのアクセス許可を指定するときの電子メール検証。 また、Enter を押し、複数の電子メール アドレスを指定できるようになりました。

- すべての下位ラベルの保護を設定するとき、親ラベルが表示されません。クライアントには、保護対応の Office エディションが与えられません。 

## <a name="next-steps"></a>次の手順

クライアントのインストールと使用の詳細: 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
