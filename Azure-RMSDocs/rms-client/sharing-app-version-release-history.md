---
title: "Rights Management 共有アプリケーション&colon; バージョン リリース履歴 | Azure Information Protection"
description: "Windows 用 Rights Management 共有アプリケーションのリリースにおける新機能や変更点について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: aded487e9d7f7bc8341c7f6e1d6ac4e673b55c56


---

# <a name="rights-management-sharing-application-version-release-history"></a>Rights Management 共有アプリケーション: バージョン リリース履歴

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

Azure Information Protection チームは、Rights Management 共有アプリケーションの修正プログラムと新機能を定期的に更新しています。 次の情報を使用して、リリースの新機能や変更内容をご確認ください。 最新のリリースは一番上に表示されます。

2015 年 1 月 1 日より前のバージョンは表示されません。

> [!NOTE]
> RMS 共有アプリケーションに関するフィードバックまたはご質問については、 [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question)まで電子メール メッセージをお送りください。

## <a name="version-1022170"></a>バージョン 1.0.2217.0

**リリース日**: 2016 年 7 月 13 日

**修正内容**:

- フェデレーションと多要素認証を使用している場合、コンテンツを保護するときにエラー 0x800704DC が発生しなくなりました。



## <a name="version-1021910"></a>バージョン 1.0.2191.0
**リリース日**: 2016 年 6 月 16 日

**修正内容**:

- ドキュメント追跡サイトに、追跡対象の各ドキュメントの正確なビューの数が表示されるようになりました。

- すべてのロケールのテンプレートがユーザーに表示されるようになりました。

- PowerPoint ファイルで [保護ファイルの共有] を使用した後、ファイルのローカル バージョンの変更が正しく保存されるようになりました。

- いくつかの軽微なバグと、エラー メッセージが改善されました。


## <a name="version-1020040"></a>バージョン 1.0.2004.0
**リリース日**: 2015 年 12 月 11 日

**修正内容**:

-   ファイルの所有者と "**共同所有者**" アクセス許可レベルが付与されているユーザーのみがファイルの保護を解除できます。 以前は、ファイルの所有者と "**共同作成者**" および "**共同所有者**" アクセス許可レベルが付与されているユーザーのみがファイルの保護を解除できました。

-   RMS で保護された読み取り専用 **.ptif** ファイルを生成するための、**.tif** ファイル (および .tiff ファイル) のネイティブ保護。

-   エラー メッセージの改善 (正確さと明確さ)。

-   コンテンツの暗号化と暗号化解除に関するパフォーマンスの向上。

**新機能**:

-   管理者以外によるインストールのサポート。これにより、標準ユーザーは RMS 共有アプリケーションをインストールできます。

    Office 2010 を実行している標準ユーザーの場合は、いくつか制限があります。 詳細については、「[Rights Management 共有アプリケーションをダウンロードしてインストールする](install-sharing-app.md)」の「[ローカル管理者ではなく、かつ Office 2010 を使用している場合](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010)」セクションを参照してください。

## <a name="version-1019080"></a>バージョン 1.0.1908.0
**リリース日**: 2015 年 9 月 16 日

**修正内容**:

-   Azure RMS 用の多要素認証 (MFA) をサポートするようになりました。それにより、最新の認証を利用するアプリケーションの Microsoft サインイン アシスタントへの依存関係が削除されました。

    詳細については、「[Azure Information Protection の Azure Active Directory の要件](../get-started/requirements-azure-ad.md)」の「[多要素認証 (MFA) と Azure Information Protection](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection)」セクションを参照してください。

## <a name="version-1017840"></a>バージョン 1.0.1784.0
**リリース日**: 2015 年 7 月 30 日

**修正内容**:

-   権限ポリシー テンプレートの既定の更新間隔が 7 日から 1 日に短縮されました。

-   少数の回帰とマイナー バグ。

## <a name="version-1017700"></a>バージョン 1.0.1770.0
**リリース日**: 2015 年 4 月 25 日

**修正内容**:

-   所有者と共同所有者のみが保護を削除できるようになりました。 共同作成者は保護を削除できません。

-   ネットワーク共有上のファイルを保護できるようになりました。

**新機能**:

-   ドキュメントの追跡と取り消しをサポートします。 詳細については、「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](sharing-app-track-revoke.md)」を参照してください。

-   **[保護ファイルの共有]**を選んだ場合のテンプレートのサポート:

    -   テンプレートを選べるようになりました。

    -   スライダーの代わりに、テンプレートとカスタム アクセス許可を含むリスト ボックスが表示されます。

    -   **[すべてのデバイスで使用を許可する]** と **[使用制限を強制する]**のオプションが表示されなくなりました。 代わりに、ファイルの種類によって **[一般保護]** が自動的に選択されます。

    詳細については、「[Rights Management 共有アプリケーションのダイアログ ボックス オプション](sharing-app-dialog-box.md)」を参照してください。

## <a name="version-1016670"></a>バージョン 1.0.1667.0
**リリース日**: 2015 年 1 月 19 日

**修正内容**:

-   RMS 共有アプリの PPDF ビューアーで中国語のフォントをサポートするようになりました。

-   エラー処理とメッセージングが向上しました。

-   新しいバージョンのアプリがダウンロード可能になったときの自動更新通知に関する問題が修正されました。

**新機能**:

-   **組織内の複数の電子メール ドメインのサポート**: AD RMS を使用している組織のユーザーが複数の電子メール ドメインを持つ場合、この更新プログラムによって、このユーザーは、他のドメイン内にある自分の組織のユーザーによって保護されているコンテンツを使用できます。 詳細については、「[Rights Management 共有アプリケーション管理者ガイド](sharing-app-admin-guide.md)」の「[AD RMS のみ: 組織内での複数の電子メール ドメインのサポート](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization)」セクションを参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


