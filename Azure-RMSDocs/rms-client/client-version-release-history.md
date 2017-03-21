---
title: "Azure Information Protection クライアント&colon; バージョン リリース履歴"
description: "Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 70c358954a39b02610a77ec81074379dc574158b
ms.sourcegitcommit: d5ce1bce5e63b3e510033ff9d4d246dd3511ed7c
translationtype: HT
---
# <a name="azure-information-protection-client-version-release-history"></a>Azure Information Protection クライアント: バージョン リリース履歴

>*適用対象: Azure Information Protection*

Azure Information Protection チームは、Azure Information Protection クライアントの修正点と新機能を定期的に更新しています。 クライアントは Microsoft Update カタログ (カテゴリ: **Azure Information Protection**) に含まれており、いつでも [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)から最新の一般提供 (GA) リリース バージョンおよび次期バージョン (プレビュー バージョン) をダウンロードできます。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 プレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認および試用にお使いください。 

次の情報を使用して、GA リリースの新機能や変更内容をご確認ください。 最新のリリースは一番上に表示されます。 最新のプレビュー バージョンに関する情報は、ダウンロード ページを参照してください。

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、まず最新 GA リリースで同じ問題が起きないかを確認してください。 問題が起きる場合は、最新のプレビュー バージョンを確認します。
>  
> 問題が解決しない場合は、「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="version-14210"></a>バージョン 1.4.21.0

**リリース日**: 2017 年 3 月 15 日

**要件の変更**

前のバージョンでは フル クライアント向けに Microsoft .NET Framework 4.6.2 の新し必須コンポーネントを導入しました。 推奨はされていませんが、カスタム インストール パラメーター **DowngradeDotNetRequirement** を使用してこの要件を省略できます。 詳細については、管理者ガイドの[クライアントのインストールに関するセクション](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users)をご覧ください。


**修正内容**:

- ファイルを分類して保護するマップされたドライブのサポート。

- ビューアーでサイズの大きいファイル (>&250; MB) のサポート。 

- HYOK が構成されている場合、Outlook は、Azure Rights Management テンプレートまたは AD RMS テンプレートを使用するように構成されたラベルを適用できます。


**新機能**:

- Office アプリケーションからカスタム アクセス許可を設定する機能です。ユーザー、外部ユーザー、または別の組織のすべてのユーザーに対してのみ保護を設定します。 詳細については、[ドキュメントのカスタム アクセス許可の設定](client-classify-protect.md#set-custom-permissions-for-a-document)をご覧ください。
    
- PDF ファイルでは現在、分類のみを適用するラベルがサポートされています。

- PDF ファイルの場合、ビューアーでは現在、検索、拡大、回転などのオプションがサポートされています。 これらのオプションを使用するには、ビューアーにファイルが表示された際にファイルを右クリックします。


## <a name="version-131552"></a>バージョン 1.3.155.2

**リリース日**: 2017 年 2 月 8 日

**新しい要件**:

[Microsoft .NET Framework]

- このバージョンの Azure Information Protection クライアントでは、Microsoft .NET Framework 4.6.2 の最小バージョンが必要になります。これがない場合、インストーラーでダウンロードとインストールが試行されます。 Azure Information Protection クライアントのインストールが完了した後に、コンピューターの再起動が必要な場合があります。

- Azure Information Protection ビューアーを別にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。これがない場合、インストーラーではダウンロードまたはインストールされません。

**新機能**:

- Windows 用 Rights Management 共有アプリケーションと Azure Information Protection クライアントの機能を組み合わせた新しい統合クライアント。 主な機能:
    
    - エクスプローラーと統合され、(右クリックで) ラベルと保護を適用できるようになりました。 サポートされるファイル形式が追加され、複数ファイルを選択できるようになりました。
    - 保護されたドキュメント (SharePoint の保護された PDF を含む) のビューアー。
    - ローカルまたはネットワーク共有に保存されているファイルのラベルを取得または設定する PowerShell コマンドレット。 これらのコマンドレットと共に、RMS 保護ツール (RMSProtection モジュール) に付属していたコマンドレットもインストールされます。
    - 適用されたラベル、適用方法、適用者などの情報を記録するクライアント使用状況ログ。

このクライアント バージョンは、最初に 2016 年 12 月に発表されたプレビュー クライアントの[一般公開リリース](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/)です。 このバージョンのクライアントの詳細については、次のガイドを参照してください。

- [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)

- [Azure Information Protection ユーザー ガイド](client-user-guide.md)


## <a name="version-1240"></a>バージョン 1.2.4.0

**リリース日**: 2016 年 10 月 27 日

**修正内容**:

- Windows Update サービスが無効な場合に、クライアントのインストールが完了するようになりました。

- Office 2016 でドキュメントを保存し、適用されたラベルのヘッダーまたはフッターが構成されている場合、カーソルがヘッダーまたはフッターにジャンプしなくなりました。

- バンドルされているテキスト ボックスのテキストについて、Word の自動分類が動作するようになりました。

**新機能**:

- Azure Information Protection クライアントがインストールされている場合にユーザーが Office アプリケーションから実行できる診断テストとリセット オプションがあります。この機能を使用するには、[**ホーム**] タブの [**保護**] グループで [**保護**] をクリックし、[**ヘルプとフィードバック**]、[**診断の実行**] の順にクリックします。 

    このオプションの詳細については、管理者ガイドの[追加のチェックとトラブルシューティング](client-admin-guide.md#additional-checks-and-troubleshooting)セクションをご覧ください。

## <a name="version-11230"></a>バージョン 1.1.23.0

**リリース日**: 2016 年 10 月 1 日

一般公開。

## <a name="next-steps"></a>次のステップ

クライアントのインストールの詳細:

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]