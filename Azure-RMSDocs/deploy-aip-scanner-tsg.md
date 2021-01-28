---
title: オンプレミスのスキャナーデプロイのトラブルシューティング
description: 統合されたオンプレミスのスキャナー展開のトラブルシューティングの手順
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/26/2021
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 46a994c5191e82d68f318e4900e0a5d45c1e176b
ms.sourcegitcommit: 3136ce04e185b93503585466b7ab4b5bb1df6827
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "98958076"
---
# <a name="troubleshooting-your-unified-labeling-on-premises-scanner-deployment"></a>統合されたオンプレミスのスキャナー展開のトラブルシューティング

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***関連**: [AIP のラベル付けクライアントのみ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 *

この記事の内容は、オンプレミスのスキャナーの展開のトラブルシューティングに役立ちます。

## <a name="troubleshooting-using-the-scanner-diagnostic-tool"></a>スキャナー診断ツールを使用したトラブルシューティング

Azure Information Scanner で問題が発生した場合は、次のように、 [Start-Aipscanの診断](/powershell/module/azureinformationprotection/start-aipscannerdiagnostics) PowerShell コマンドを使用して、デプロイが正常であるかどうかを確認します。

```powershell
Start-AIPScannerDiagnostics
```

診断ツールは、次の詳細を確認し、結果と共にログファイルをエクスポートします。

- データベースが最新かどうか
- ネットワーク Url にアクセスできるかどうか
- 有効な認証トークンがあるかどうか、およびポリシーを取得できるかどうか
- プロファイルが Azure portal で定義されているかどうか
- オフライン/オンライン構成が存在し、取得できるかどうか
- 構成されている規則が有効かどうか

> [!TIP]
> スキャナーユーザーではないユーザーでコマンドを実行している場合は、必ず **-onbehalf** パラメーターを追加してください。 
>

> [!NOTE]
> **Start-Aipscanは**、完全な前提条件の確認を実行しません。 スキャナーで問題が発生している場合は、システムが [スキャナーの要件](deploy-aip-scanner-prereqs.md)を満たしていることと、 [スキャナーの構成とインストール](deploy-aip-scanner-configure-install.md) が完了していることを確認してください。
>

## <a name="troubleshooting-a-scan-that-timed-out"></a>タイムアウトしたスキャンのトラブルシューティング

スキャナーが途中で停止し、リポジトリ内の多数のファイルのスキャンが完了しない場合は、次の設定のいずれかを変更する必要があります。

- **動的ポートの数**。 ファイルをホストしているオペレーティングシステムの動的ポートの数を増やすことが必要になる場合があります。 SharePoint 用にサーバーのセキュリティが強化されている場合、スキャナーが許可されているネットワーク接続の数を超えて、そのために停止する原因の 1 つになる可能性があります。

    現在のポート範囲を表示し、範囲を拡大する方法について詳しくは、「[ネットワーク パフォーマンスを向上させるために変更可能な設定](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)」をご覧ください。

- **リストビューのしきい値**。 大規模な SharePoint ファームの場合は、リストビューのしきい値を大きくする必要があります。 既定では、リストビューのしきい値は **5000** に設定されています。

    詳細については、「 [SharePoint での大規模なリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。


## <a name="scanner-error-reference"></a>スキャナーエラーのリファレンス

スキャナーによって生成される特定のエラーメッセージと、問題を解決するためのトラブルシューティングまたは解決策を理解するには、次のセクションを使用します。

|エラーの種類 |トラブルシューティング  |
|---------|---------|
|**認証エラー**     |  - [認証トークンが受け入れられません](#authentication-token-not-accepted) <br>  - [認証トークンがありません](#authentication-token-missing)|
|**ポリシー エラー**     |  - [ポリシーがありません](#policy-missing) <br>- [ポリシーに自動ラベル付け条件が含まれていません](#policy-doesnt-include-any-automatic-labeling-condition)      |
|**DB/スキーマエラー**     |  - [データベースエラー](#database-errors) <br> - [不一致または古いスキーマ](#mismatched-or-outdated-schema)  |
|**その他のエラー**     |  - [基になる接続が閉じられました](#underlying-connection-was-closed) <br> - [スキャナープロセスをスタックする](#stuck-scanner-processes) <br>- [リモートサーバーに接続できません](#unable-to-connect-to-remote-server) <br>- [要求の送信中にエラーが発生しました](#error-occurred-while-sending-the-request) <br>- [コンテンツスキャンジョブまたはプロファイルがありません](#missing-content-scan-job-or-profile) <br>- [リポジトリが構成されていません](#no-repositories-configured) <br>- [クラスターが見つかりませんでした](#no-cluster-found)   |
|     |         |


<!--Authentication errors-->

### <a name="authentication-token-not-accepted"></a>認証トークンが受け入れられません

**エラー メッセージ**

`Microsoft.InformationProtection.Exceptions.AccessDeniedException: The service didn't accept the auth token.`

**ソリューション**

[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)コマンドが失敗した場合は、Azure portal で権限を正しく定義していることを確認してください。

詳細については、「 [Set-AIPAuthentication の Azure AD アプリケーションの作成と構成](rms-client/clientv2-admin-guide-powershell.md#create-and-configure-azure-ad-applications-for-set-aipauthentication)」を参照してください。

### <a name="authentication-token-missing"></a>認証トークンがありません

**エラー メッセージ**

次のいずれか:

- `NoAuthTokenException: Client application failed to provide authentication token for HTTP request`

- `Microsoft.InformationProtection.Exceptions.NoAuthTokenException: Client application failed to provide authentication token for HTTP request. Failed with: System.AggregateException: One or more errors occurred. ---> Microsoft.IdentityModel.Clients.ActiveDirectory.AdalException: user_interaction_required: One of two conditions was encountered: 1. The PromptBehavior.Never flag was passed, but the constraint could not be honored, because user interaction was required. 2. An error occurred during a silent web authentication that prevented the http authentication flow from completing in a short enough time frame`

- `Failed to acquire a token using windows integrated authentication (No SSO)`

- [ **ノード** ] ページの Azure portal から、次のようにします。 `Policy does not include any automatic labeling condition`

**ソリューション**

スキャナーが非対話形式で実行されるようにするには、トークンを使用して認証を行う必要があります。 

[Set AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)コマンドを実行するときは、スキャナーユーザーの代わりに token パラメーターを使用してください。

例:

```powershell
$pscreds = Get-Credential CONTOSO\scanner
Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
Acquired application access token on behalf of CONTOSO\scanner.
```

詳細については、「 [スキャナーの Azure AD トークンを取得する](deploy-aip-scanner-configure-install.md#get-an-azure-ad-token-for-the-scanner)」を参照してください。

<!--Policy errors-->

### <a name="policy-missing"></a>ポリシーがありません

**エラー メッセージ**

`Policy is missing`

**説明**

スキャナーが Microsoft Information Protection (MIP) ポリシーファイルを見つけることができません。

**ソリューション**

ポリシーファイルが想定どおりに存在することを確認するには、次の場所を確認してください: **% localappdata% \Microsoft\MSIP\mip\MSIP.Scanner.exe \mip\mip.policies.sqlite3**

MIP ラベルとラベルポリシーの詳細については、Microsoft 365 のドキュメントの「 [感度ラベルとそのポリシーを作成して構成する](/microsoft-365/compliance/create-sensitivity-labels) 」を参照してください。

### <a name="policy-doesnt-include-any-automatic-labeling-condition"></a>ポリシーに自動ラベル付け条件が含まれていません

**Error**

ラベル付けポリシーに自動ラベル付け条件がないことを示すエラーが表示される

**ソリューション**

次のいずれかまたはすべての問題を確認します。

|解決策  |詳細  |
|---------|---------|
|**コンテンツスキャンジョブの設定を確認する**     | Azure Portal で、次の操作を行います。 <br> <br>- [[**探索する情報の種類**] を [**すべて**] に設定します。](deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types)  <br>- [スキャン時に適用される既定のラベルを定義する](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository)      |
|**ラベル付けポリシーの設定を確認する**     |  Microsoft 365 セキュリティ & コンプライアンスセンターなどのラベル付け管理センターで、次の操作を行います。 <br> <br>- [既定の秘密度ラベルを定義する](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)  <br> - [自動/推奨のラベル付け規則を定義する](/microsoft-365/compliance/apply-sensitivity-label-automatically)       |
|**ポリシーがアクセス可能であることを確認する**     | 設定が想定どおりに定義されている場合、ポリシーファイル自体が見つからないか、アクセスできない可能性があります。たとえば、Microsoft 365 セキュリティ & コンプライアンスセンターからタイムアウトが発生した場合などです。 <br>  <br>ポリシーファイルを確認するには、次のファイルが存在することを確認してください: **% localappdata% \Microsoft\MSIP\mip\MSIP.Scanner.exe \mip\mip.policies.sqlite3**        |
| | |

詳細については、「 [Azure Information Protection 統合ラベル付けスキャナーとは](deploy-aip-scanner.md)」を[参照してください。](/microsoft-365/compliance/sensitivity-labels)

<!--DB / Schema errors-->

### <a name="database-errors"></a>データベース エラー

**エラー メッセージ**

`DB error`

**説明**

スキャナーがデータベースに接続できない可能性があります。

**ソリューション**

スキャナーコンピューターとデータベースの間のネットワーク接続を確認します。 

また、スキャナープロセスの実行に使用されているサービスアカウントに、データベースにアクセスするために必要なアクセス許可があることを確認します。

### <a name="mismatched-or-outdated-schema"></a>不一致または古いスキーマ

**エラー メッセージ**

次のいずれか:

- `SchemaMismatchException`

- Azure portal の [ **ノード** ] ページ: `DB schema is not up to date. Run Update-AIPScanner command to update the DB schema` または `Error: DB schema is not up to date`

**ソリューション**

[更新プログラム AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)コマンドを実行して、スキーマを再同期し、最新の変更内容があるかどうかを確認します。


<!--Other errors-->

### <a name="underlying-connection-was-closed"></a>基になる接続が閉じられました

**エラー メッセージ**

`System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a send. ---> System.IO.IOException: Authentication failed because the remote party has closed the transport stream.`

**ソリューション**

このエラーは、通常、TLS 1.2 が有効になっていないことを示します。

詳細については、「 [ファイアウォールとネットワークインフラストラクチャ](requirements.md#firewalls-and-network-infrastructure)」を参照してください。 

TLS 1.2 を有効にする方法については、Enterprise Mobility + Security のドキュメントの「 [tls 1.2 を有効にする方法](/mem/configmgr/core/plan-design/security/enable-tls-1-2-client) 」を参照してください。

### <a name="stuck-scanner-processes"></a>スキャナープロセスをスタックする

**エラー メッセージ**

スキャナーが、予想より長い1つのファイルを処理しています。 プロセスがスタックしている可能性があります。

**ソリューション**

詳細レポートで、ファイルがまだ拡大しているかどうかを確認します。 

ファイルのサイズが増加し続ける場合は、スキャナーが引き続きデータを処理しているため、完了するまで待機する必要があります。

ただし、ファイルが大きくなっていない場合は、次の手順を実行します。

1. 次のいずれかまたは両方の操作を行います。

    - [スタートアップ](/powershell/module/azureinformationprotection/start-aipscannerdiagnostics)コマンドレットを実行して、スキャナーで診断チェックを実行し、検出されたエラーについては、ログファイルをエクスポートおよび zip ログに記録します。
    - [Export-Ai%localappdata%\Microsoft\MSIP\Logs gs](/powershell/module/azureinformationprotection/export-aiplogs)コマンドレットを実行して、ファイルをエクスポートし 、ログファイルを zip 形式でエクスポートします。

1. MSIP スキャナーサービスのダンプファイルを作成します。 Windows タスクマネージャーで、[ **Msip スキャナー] サービス** を右クリックし、[ **ダンプファイルの作成**] を選択します。

1. Azure portal で、スキャンを停止します。 

1. スキャナーコンピューターで、サービスを再起動します。

1. サポートチケットを開き、スキャナープロセスからダンプファイルを添付します。

詳細については、「 [タイムアウトしたスキャンのトラブルシューティング](#troubleshooting-a-scan-that-timed-out)」を参照してください。 

### <a name="unable-to-connect-to-remote-server"></a>リモートサーバーに接続できません

**Error**

**% *Localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog** ファイルで、`Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port`    

> [!NOTE]
> 複数のログがある場合、このファイルは圧縮されます。

**説明**

スキャナーが、許可されているネットワーク接続の数を超えています。

**ソリューション**

ファイルをホストしているオペレーティングシステムの動的ポートの数を増やします。

現在のポート範囲を表示し、範囲を拡大する方法について詳しくは、「[ネットワーク パフォーマンスを向上させるために変更可能な設定](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)」をご覧ください。


「タイムアウトし [たスキャンのトラブルシューティング](#troubleshooting-a-scan-that-timed-out)」も参照してください。
### <a name="error-occurred-while-sending-the-request"></a>要求の送信中にエラーが発生しました

**エラー メッセージ**

`[System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a send. ---> System.IO.IOException: Unable to read data from the transport connection: An existing connection was forcibly closed by the remote host. ---> System.Net.Sockets.SocketException: An existing connection was forcibly closed by the remote host`

**ソリューション**

このエラーは、通常、TLS 1.2 が有効になっていないことを示します。

詳細については、「 [ファイアウォールとネットワークインフラストラクチャ](requirements.md#firewalls-and-network-infrastructure)」を参照してください。 

TLS 1.2 を有効にする方法については、Enterprise Mobility + Security のドキュメントの「 [tls 1.2 を有効にする方法](/mem/configmgr/core/plan-design/security/enable-tls-1-2-client) 」を参照してください。


### <a name="missing-content-scan-job-or-profile"></a>コンテンツスキャンジョブまたはプロファイルがありません

**Error**

エラーは、コンテンツスキャンジョブまたはプロファイルが見つからないことを示します。

たとえば、[ **ノード** ] ページの Azure portal に次のエラーがあります。 `No content scan job found`

**ソリューション**

Azure portal でスキャナーの構成を確認します。

詳細については、「 [Azure Information Protection 統合ラベル付けスキャナーの構成とインストール](deploy-aip-scanner-configure-install.md)」を参照してください。 

> [!NOTE]
> *プロファイル* とは、新しいバージョンのスキャナーで、スキャナークラスターおよびコンテンツスキャンジョブによって置き換えられた従来のスキャナー用語です。
> 
### <a name="no-repositories-configured"></a>リポジトリが構成されていません

**エラー メッセージ**

Azure portal の [ **ノード** ] ページで次のようにします。 `No repositories are configured`

**説明**

リポジトリが構成されていないコンテンツスキャンジョブがある可能性があります。 

**ソリューション**

コンテンツスキャンジョブの設定を確認し、少なくとも1つのリポジトリを追加します。 

詳細については、「 [コンテンツスキャンジョブの作成](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)」を参照してください。

### <a name="no-cluster-found"></a>クラスターが見つかりませんでした

**エラー メッセージ**

Azure portal の [ **ノード** ] ページで次のようにします。 `No cluster found`

**説明**

定義したスキャナークラスターの1つに対して、実際の一致は見つかりませんでした。

**ソリューション**

クラスター構成を確認し、入力ミスやエラーがないかどうか、システムの詳細を確認します。

詳細については、「 [スキャナークラスターを作成する](deploy-aip-scanner-configure-install.md#create-a-scanner-cluster)」を参照してください。

## <a name="next-steps"></a>次のステップ

詳細については、 [AIP UL スキャナーをデプロイして使用するためのベストプラクティス](https://techcommunity.microsoft.com/t5/microsoft-security-and/best-practices-for-deploying-and-using-the-aip-ul-scanner/ba-p/1878168)に関するブログを参照してください。