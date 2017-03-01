---
title: "Azure Information Protection クライアント&colon; バージョン リリース履歴"
description: "Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: fec4ca2541b28fd9d91286fceaee0466fc445364
ms.lasthandoff: 02/24/2017


---

# <a name="azure-information-protection-client-version-release-history"></a>Azure Information Protection クライアント: バージョン リリース履歴

>*適用対象: Azure Information Protection*

Azure Information Protection チームは、Azure Information Protection クライアントの修正点と新機能を定期的に更新しています。 Azure Information Protection クライアントは Microsoft Update カタログ (カテゴリ: **Azure Information Protection**) に含まれており、いつでも [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)から最新バージョンをダウンロードできます。

次の情報を使用して、リリースの新機能や変更内容をご確認ください。 最新のリリースは一番上に表示されます。 一般公開前のバージョンは記載されていません。

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、まず最新リリースで問題が起きないかを確認してください。
>  
> 問題が解決しない場合は、「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

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

    このオプションの詳細については、クライアントのインストールに関するドキュメントで「[To verify installation, connection status, or send feedback](client-admin-guide.md#to-verify-installation-connection-status-or-send-feedback)」(インストール、接続状態を確認するには、または問題を報告するには) を参照してください。

## <a name="version-11230"></a>バージョン 1.1.23.0

**リリース日**: 2016 年 10 月 1 日

一般公開。

## <a name="next-steps"></a>次のステップ

クライアントのインストールの詳細:

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
