---
title: Azure Information Protection の統合されたラベル付けクライアントのカスタム構成
description: Windows 用 Azure Information Protection の統合されたラベル付けクライアントのカスタマイズに関する情報。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: c565c025b6ae3001984141a691ed37a057203f38
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181091"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>管理者ガイド: Azure Information Protection の統合されたラベル付けクライアントのカスタム構成

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> "*手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統合されたラベル付けクライアントを管理するときに、特定のシナリオまたはユーザーのサブセットは必要な高度な構成の次の情報を使用します。

これらの設定では、レジストリの編集が必要です。  

## <a name="sign-in-as-a-different-user"></a>別のユーザーでのサイン イン

運用環境でユーザーは、通常、統合されたクライアントのラベル付けを Azure Information Protection を使用しているときに、別のユーザーにサインインする必要はありません。 ただし管理者の場合は、テスト段階のときに別ユーザーとしてサインインする必要がある場合があります。 

**Microsoft Azure Information Protection** ダイアログ ボックスを使用して、現在サインインしているアカウントを確認することができます。Office アプリケーションを開くと、**ホーム** タブで、、**感度**ボタンをクリックし、**ヘルプとフィードバック**。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

表示されるサインイン アカウントのドメイン名も必ず確認してください。 正しいアカウントでサインインしていてもドメインが間違っている、という状況は気付きにくいものです。 症状の間違ったアカウントを使用してダウンロードが失敗、ラベル、ラベルまたは予測される動作が表示されない場合またはします。

別のユーザーでサイン インする方法は以下の通りです。

1. **%localappdata%\Microsoft\MSIP** に移動し、**TokenCache** ファイルを削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするには、Office アプリケーションで、プロンプトが表示されない場合に戻って、 **Microsoft Azure Information Protection**  ダイアログ ボックスを選択します**サインイン**から、更新**クライアント ステータス**セクション。

補足:

- Azure Information Protection の統合されたラベル付けクライアントがサインインしたまま、古いアカウントこれらの手順が完了したら、Internet Explorer から、すべての cookie を削除し、手順 1. および 2. を繰り返します。

- シングル サインオンを使用する場合は、トークン ファイルを削除した後に Windows からサインアウトし、別のユーザー アカウントでサインインする必要があります。 Azure Information Protection の統合されたラベル付けクライアントし、自動的に認証し、現在サインインしてを使用してユーザー アカウントにします。

- このソリューションでは、同じテナントから別ユーザーとしてサインインする操作がサポートされています。 別のテナントから別のユーザーとしてサインインする操作はサポートされていません。 複数のテナントがある Azure Information Protection をテストするには、異なるコンピューターを使用します。

- 使用することができます、**設定にリセット**オプションを**ヘルプとフィードバック**サインアウトしてから、Office 365 セキュリティ/コンプライアンス センターでは、現在ダウンロードされているラベルとポリシーの設定を削除しますMicrosoft 365 セキュリティ センター、または Microsoft 365 コンプライアンス センター。


## <a name="change-the-local-logging-level"></a>ローカルのログ記録レベルを変更する

既定では、Azure Information Protection にユニファイド ラベル付けクライアント書き込みクライアント ログ ファイルを **%localappdata%\Microsoft\MSIP**フォルダー。 これらのファイルは、Microsoft サポートによるトラブルシューティングを目的としています。
 
これらのファイルのログ記録レベルを変更するには、レジストリ内で、次の値の名前を検索し、値のデータを必要なログ記録レベルに設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

ログ記録レベルに次の値のいずれかを設定します。

- **Off**: ローカルのログ記録なし。

- **Error**: エラーのみ。

- **[情報]**:最小のログ記録 (イベント ID は含まれません)。

- **[デバッグ]**:完全な情報。

- **[トレース]**:詳細なログ記録 (クライアントの既定の設定)。

このレジストリ設定では、Azure Information Protection に送信される情報は変更されません[中央 reporting](../reports-aip.md)します。


## <a name="next-steps"></a>次の手順
これで、Azure Information Protection の統一されたラベル付けクライアントをカスタマイズして、このクライアントをサポートする必要があります追加情報については、次のリソースを参照してください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)
