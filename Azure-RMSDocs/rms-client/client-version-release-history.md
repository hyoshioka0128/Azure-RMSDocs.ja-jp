---
title: "Azure Information Protection クライアント&colon; バージョン リリース履歴とサポート ポリシー"
description: "Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点、サポートのライフサイクル ポリシーについて説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e107d796ebda1b1942e19ede8c794f79defbf64e
ms.sourcegitcommit: fd3932ab19a00229b56efc3e301abaf9cff3f70b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2017
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure Information Protection クライアント: バージョン リリース履歴とサポート ポリシー

>*適用対象: Azure Information Protection*

Azure Information Protection チームは、Azure Information Protection クライアントの修正点と新機能を定期的に更新しています。 

最新の GA リリース バージョンと現在のプレビュー バージョンを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。 これらのバージョンは、WSUS や構成マネージャー、またはその他の Microsoft Update を使用するソフトウェア展開メカニズムを使用してクライアントを展開できるように、Microsoft Update カタログにも含まれます (カテゴリ: **Azure Information Protection**)。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection クライアントの一般提供 (GA) バージョンは、リリース日から 6 か月間サポートされます。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

### <a name="release-history"></a>リリース履歴

Windows 用 Azure Information Protection クライアントのサポートされるリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。 


> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、最新の GA リリースで問題が修正されているかどうかを確認することをお勧めします。 問題が解決されていない場合は、最新のプレビュー バージョンを確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="versions-later-than-110560"></a>1.10.56.0 以降のバージョン

1.10.56.0 以降のバージョンのクライアントがある場合、それはテストおよび評価目的のプレビュー ビルドです。 

クライアントの最後の GA バージョン以降の最新のプレビュー バージョンでの新機能または変更については、[ダウンロード ページ](https://www.microsoft.com/en-us/download/details.aspx?id=53018)の**詳細**セクションを参照してください。 

## <a name="version-110560"></a>バージョン 1.10.56.0

**リリース日**: 2017 年 9 月 18 日

このバージョンには、MSIPC バージョン 1.0.3219.0619 の RMS クライアントが含まれています。

**新機能**:

- 新しい Office 365 DLP 条件に対応。この条件はラベルに設定できます。 詳細については、「[Azure Information Protection ラベルの条件を構成する](../deploy-use/configure-policy-classification.md)」を参照してください。

- ユーザー定義アクションのために作られたラベルに対応。 Outlook の場合、このラベルは [転送不可] オプションに自動的に適用されます。 Word、Excel、PowerPoint、エクスプローラーの場合、このラベルはカスタムのアクセス許可を指定するようにユーザーに求めます。 詳細については、「[Azure Information Protection ラベルを保護するように構成する](../deploy-use/configure-policy-protection.md)」を参照してください。

- ラベルは [Information Protection] バーに表示されるほか、Office リボンの **[保護]** ボタンをクリックしたときに表示されます。 

- 次の Visio ファイルの種類のネイティブ保護: .vsdm、.vsdx、.vssm、.vssx、.vstm、.vstx

- Azure Portal で設定する詳細なクライアント構成に対応。 この構成には次のものが含まれます。
    
    - [Outlook の [転送不可] ボタンを非表示にする](../rms-client/client-admin-guide-customizations.md#hide-the-do-not-forward-button-in-outlook)
    
    - [ユーザーがカスタムのアクセス許可オプションを使用できなくする](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-unavailable-to-users)
    
    - [Azure Information Protection バーを完全に非表示にする](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-unavailable-to-users)
    
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

- 下位ラベルの保護を設定するとき、親ラベルが表示されません。クライアントには、保護対応の Office エディションが与えられません。 

## <a name="version-172100"></a>バージョン 1.7.210.0

**リリース日**: 2017 年 6 月 6 日

このバージョンには、MSIPC バージョン 1.0.2217.1 の RMS クライアントが含まれています。

**新機能**:

- 新しい PowerShell コマンドレット: [Set-AIPFileClassification](/powershell/module/azureinformationprotection/Set-AIPFileClassification)。 このコマンドレットを実行すると、Azure Information Protection ポリシーで指定した条件に従って、ファイルの内容を検査し、ラベル付けされていないファイルに自動でラベルを付与します。

**修正内容**:

- 現在、ラベル付けと分類を行うすべてのコマンドレットは、インターネットに接続されておらず、Azure Information Protection ポリシーが有効になっているコンピューターでサポートされます。

- 整合性を保つため、[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) コマンドレットの出力パラメーターは、英語 (英国) (**IsLabelled**) から英語 (米国) (**IsLabeled**) に変更されます。 このパラメーターを検索するスクリプトまたは自動プロセスを使用している場合は、このパラメーターのスペルを更新してください。

- 安定性を改善するための一般的な修正は次のとおりです。

    - Outlook: クラッシュ、高いメモリ消費量、メニューの表示に関する問題を修正。
    
    - Word、Excel、PowerPoint: 高い CPU 使用率、サイズの大きい Excel ファイルを保存する際の表示に関する問題、またはアプリケーションが応答を停止する問題を修正。 
    
    また、これらのアプリケーションに関して、SharePoint Online での Office 2016 と OneDrive for Business のパフォーマンスを改善するため、ファイルを保存するとき (自動保存、またはユーザーが保存を選択したとき) ではなくファイルを閉じるときに、推奨のラベル付けを自動で行います。 同様に、**[All documents and email must have a label]\(すべてのドキュメントと電子メール アドレスにラベルが必要\)** の設定が有効になっている場合は、ファイルを閉じるとき以外にラベルを選択するように求めるメッセージが表示されることはありません。 Word 2016 と Excel 2016 で、ユーザーが **[名前を付けて保存]** オプションを選択するときは例外です。 そのときに、これらが構成されている場合は、この操作によってラベル付け動作がトリガーされます。 

## <a name="next-steps"></a>次のステップ

クライアントのインストールと使用の詳細: 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
