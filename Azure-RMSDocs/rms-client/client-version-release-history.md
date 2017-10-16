---
title: "Azure Information Protection クライアント&colon; バージョン リリース履歴"
description: "Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/09/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ccd6d0cec6a71527fad0303369baad90dd733958
ms.sourcegitcommit: bcc2f69475f811245d2beaf79c67a3d8569c4821
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2017
---
# <a name="azure-information-protection-client-version-release-history"></a>Azure Information Protection クライアント: バージョン リリース履歴

>*適用対象: Azure Information Protection*

Azure Information Protection チームは、Azure Information Protection クライアントの修正点と新機能を定期的に更新しています。 クライアントは Microsoft Update カタログ (カテゴリ: **Azure Information Protection**) に含まれており、いつでも [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)から最新の一般提供 (GA) リリース バージョンと次期バージョン (プレビュー バージョン) をダウンロードできます。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 プレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認および試用にお使いください。 

次の情報を使用して、GA リリースの新機能や変更内容をご確認ください。 最新のリリースは一番上に表示されます。 最新のプレビュー バージョンの変更点については、ダウンロード ページを参照してください。

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、まず最新 GA リリースで同じ問題が起きないかを確認してください。 問題が起きる場合は、最新のプレビュー バージョンを確認します。
>  
> 問題が解決しない場合は、「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="version-110560"></a>バージョン 1.10.56.0

**リリース日**: 2017 年 9 月 18 日

このバージョンには、MSIPC バージョン 1.0.3219.0619 の RMS クライアントが含まれています。

**新機能**:

- ユーザー定義アクションのために作られたラベルに対応。 Outlook の場合、このラベルは [転送不可] オプションに自動的に適用されます。 Word、Excel、PowerPoint、エクスプローラーの場合、このラベルはカスタムのアクセス許可を指定するようにユーザーに求めます。 詳細については、「[Azure Information Protection ラベルを保護するように構成する](../deploy-use/configure-policy-protection.md)」を参照してください。

- 新しい Office 365 DLP 条件に対応。この条件はラベルに設定できます。 詳細については、「[Azure Information Protection ラベルの条件を構成する](../deploy-use/configure-policy-classification.md)」を参照してください。

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

## <a name="version-14210"></a>バージョン 1.4.21.0

**リリース日**: 2017 年 3 月 15 日

**要件の変更**

前のバージョンでは フル クライアント向けに Microsoft .NET Framework 4.6.2 の新しい必須コンポーネントを導入しました。 推奨はされていませんが、カスタム インストール パラメーター **DowngradeDotNetRequirement** を使用してこの要件を省略できます。 詳細については、管理者ガイドの[クライアントのインストールに関するセクション](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users)をご覧ください。

**新機能**:

- Office アプリケーションからカスタム アクセス許可を設定する機能です。ユーザー、外部ユーザー、または別の組織のすべてのユーザーに対してのみ保護を設定します。 詳細については、[ドキュメントのカスタム アクセス許可の設定](client-classify-protect.md#set-custom-permissions-for-a-document)をご覧ください。
    
- PDF ファイルでは現在、分類のみを適用するラベルがサポートされています。

- PDF ファイルの場合、ビューアーでは現在、検索、拡大、回転などのオプションがサポートされています。 これらのオプションを使用するには、ビューアーにファイルが表示された際にファイルを右クリックします。

**修正内容**:

- ファイルを分類して保護するマップされたドライブのサポート。

- Azure Information Protection クライアント ビューアーで大きいファイル (250 MB 超) が使えるようになりました。 

- HYOK が構成されている場合、Outlook は、Azure Rights Management テンプレートまたは AD RMS テンプレートを使用するように構成されたラベルを適用できます。

## <a name="version-131552"></a>バージョン 1.3.155.2

**リリース日**: 2017 年 2 月 8 日

**新しい要件**:

[Microsoft .NET Framework]

- このバージョンの Azure Information Protection クライアントでは、Microsoft .NET Framework 4.6.2 の最小バージョンが必要になります。これがない場合、インストーラーでダウンロードとインストールが試行されます。 Azure Information Protection クライアントのインストールが完了した後に、コンピューターの再起動が必要な場合があります。

- Azure Information Protection ビューアーを別にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。これがない場合、インストーラーではダウンロードまたはインストールされません。

**新機能**:

- Windows 用 Rights Management 共有アプリケーションと Azure Information Protection クライアントの機能を組み合わせた新しい統合クライアント。 主な機能:
    
    - エクスプローラーと統合され、(右クリックで) ラベルと保護を適用できるようになりました。 対応しているファイル形式が追加され、複数のファイルを選択できるようになりました。
    - 保護されたドキュメント (SharePoint の保護された PDF を含む) のビューアー。
    - ローカルまたはネットワーク共有に保存されているファイルのラベルを取得または設定する PowerShell コマンドレット。 これらのコマンドレットと共に、RMS 保護ツール (RMSProtection モジュール) に付属していたコマンドレットもインストールされます。
    - 適用されたラベル、適用方法、適用者などの情報を記録するクライアント使用状況ログ。

このクライアント バージョンは、最初に 2016 年 12 月に発表されたプレビュー クライアントの[一般公開リリース](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/)です。 このバージョンのクライアントの詳細については、次のガイドを参照してください。

- [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)

- [Azure Information Protection ユーザー ガイド](client-user-guide.md)


## <a name="version-1240"></a>バージョン 1.2.4.0

**リリース日**: 2016 年 10 月 27 日

**新機能**:

- Azure Information Protection クライアントがインストールされている場合にユーザーが Office アプリケーションから実行できる診断テストとリセット オプションがあります。この機能を使用するには、**ホーム** タブの **保護** グループで **保護**をクリックし、**ヘルプとフィードバック**、**診断の実行** の順にクリックします。 

    このオプションの詳細については、管理者ガイドの[追加のチェックとトラブルシューティング](client-admin-guide.md#additional-checks-and-troubleshooting)セクションをご覧ください。

**修正内容**:

- Windows Update サービスが無効な場合に、クライアントのインストールが完了するようになりました。

- Office 2016 でドキュメントを保存し、適用されたラベルのヘッダーまたはフッターが構成されている場合、カーソルがヘッダーまたはフッターにジャンプしなくなりました。

- バンドルされているテキスト ボックスのテキストについて、Word の自動分類が動作するようになりました。


## <a name="version-11230"></a>バージョン 1.1.23.0

**リリース日**: 2016 年 10 月 1 日

一般公開。

## <a name="next-steps"></a>次のステップ

クライアントのインストールと使用の詳細:

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]