---
title: クイック スタート - Azure Information Protection スキャナーを使って機密情報を検索する
description: Azure Information Protection スキャナーを使用して、オンプレミスに格納しているファイル内の機密情報を検索します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 04e114e6b719288a26663bd5534af4b1f1b73ac8
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91587883"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>クイック スタート:オンプレミスに格納しているファイル内の機密情報を検索する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用の Azure Information Protection クラシック クライアントまたは統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

このクイックスタートでは、SharePoint によるスキャンの許可を有効にし、また Azure Information Protection スキャナーのインストールと構成を行って、オンプレミスのデータ ストアに格納している機密情報を検索します。

**必要な時間:** この構成は 15 分未満で完了します。

## <a name="prerequisites"></a>前提条件

このクイック スタートを完了するには、次のものが必要です。

|要件  |説明  |
|---------|---------|
|**サポート サブスクリプション**     |  [**Azure Information Protection プラン 1 またはプラン 2**](https://azure.microsoft.com/pricing/details/information-protection/) を含むサブスクリプションが必要です。 </br></br>このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。       |
|**クライアントのインストール**    |   使用するコンピューターにクラシック クライアントか統合ラベル付けクライアントをインストールする必要があります。 </br></br>- 統合ラベル付けクライアントをインストールするには、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=53018)に移動し、Azure Information Protection ページから **AzInfoProtection_UL.exe** をダウンロードします。 </br>- AIP クラシック クライアントをデプロイするには、サポート チケットを作成してダウンロード アクセスを取得します。       |
|**SQL Server Express**     | 使用するコンピューターに SQL Server Express をインストールする必要があります。 </br></br> インストールするには、[Microsoft ダウンロード センター](https://www.microsoft.com/sql-server/sql-server-editions-express)に移動し、Express オプションの下にある **[今すぐダウンロード]** を選択します。 インストーラーで、 **[基本]** をインストールの種類に選択します。        |
|**Azure AD**     |  ご自身のドメイン アカウントが Azure AD に同期されている必要があります。 </br></br>ご自身のアカウントについて不明な場合は、いずれかのシステム管理者にお問い合わせください。      |
|**SharePoint へのアクセス**     | SharePoint のスキャンを有効にするには、SharePoint ポリシーへのアクセスと権限が必要です。 |
| | |

## <a name="prepare-a-test-folder-and-file"></a>テスト用のフォルダーとファイルを準備する

スキャナーが動作していることを確認する最初のテスト用に、次の操作を実行します。

1. アクセス可能なネットワーク共有に新しいフォルダーを作成します。 たとえば、このフォルダーに **TestScanner** という名前を付けます。

1. **Credit card: 4242-4242-4242-4242** というテキストを含む Word 文書を作成して、そのフォルダー内に保存します。

## <a name="permission-users-to-scan-sharepoint-repositories"></a>ユーザーに SharePoint リポジトリのスキャンを許可する

SharePoint リポジトリ間でスキャナーを使用するには、Azure Information Protection に対してサイトの URL を指定し、その URL の下にあるすべてのサイトを検出してスキャンします。

リポジトリ間でのスキャンを有効にするには、スキャンに使用するユーザーに対して次の SharePoint アクセス許可を追加します。

1. SharePoint を開き、 **[アクセス許可ポリシー]** を選択し、 **[アクセス許可ポリシー レベルの追加]** を選択します。

    ![特定のユーザーに対して新しいアクセス許可ポリシー レベルを作成する](./media/aip-quick-set-sp-permissions.png)

1. **[サイト コレクションの権限]** で **[Site Collector Auditor]\(サイト コレクター監査人\)** オプションを選択します。

1. **[アクセス許可]** の **[アプリケーション ページの表示]** オプションに **[許可]** を選択して、変更を**保存**します。  

    ![特定のユーザーに対して [Site Collector Auditor]\(サイトコレクターの監査人\) とアクセス許可のオプションを選択する](./media/aip-quick-set-site-permissions.png)

1. 変更を確認すると、 **[Web アプリケーションのポリシー]** メッセージが開くので、 **[OK]** をクリックします。

1. **[ユーザーの追加]** ページの **[ユーザーの選択]** フィールドで、スキャンに使用するユーザーを追加します。 **[権限の選択]** で **[サイト コレクション]** オプションを選択し、 **[完了]** をクリックして、作成したアクセス許可を追加または選択したユーザーに適用します。

    ![新しいアクセス許可のオプションにユーザーを追加する](./media/aip-quick-set-user-permissions.png)

## <a name="configure-a-profile-for-the-scanner"></a>スキャナー用のプロファイルを構成する

スキャナーをインストールする前に、Azure portal でそのためのプロファイルを作成します。 このプロファイルには、スキャナーの設定と、スキャンするデータ リポジトリの場所が含まれます。

1. 新しいブラウザー ウィンドウを開いて、[Azure portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。

    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

1. 左側のペインで **[スキャナー]** オプションを見つけて、 **[プロファイル]** を選択します。

1. **[Azure Information Protection] - [プロファイル]** ペインで、 **[追加]** を選択します。

    :::image type="content" source="media/scanner-add-profile.png" alt-text="Azure Information Protection スキャナーのプロファイルを追加する":::

1. **[新しいプロファイルを追加する]** ペインで、その構成設定とスキャンするデータ リポジトリを識別するために使うスキャナーの名前を指定します。 たとえば、このクイックスタートでは、**Quickstart** を指定できます。 後でスキャナーをインストールするときに、同じプロファイル名を指定する必要があります。

    スキャナーのプロファイル名を識別するために、必要に応じて管理目的の説明を指定します。

1. **[ポリシーの適用]** セクションを探します。このクイックスタートでは、このセクションで 1 つの設定のみを選択します。 **[強制]** で **[オフ]** を選択します。 次に **[保存]** を選択しますが、ペインは閉じないでください。

    この設定では、指定したデータ リポジトリ内にあるすべてのファイルの 1 回限りの探索を実行するようにスキャナーを構成します。 このスキャンでは、機密情報の既知の種類がすべて検索されます。また、最初に Azure Information Protection ラベルやポリシー設定を構成する必要はありません。

1. これでプロファイルの作成と保存が完了したので、 **[リポジトリの構成]** オプションに戻って、スキャンするデータ ストアとしてネットワーク フォルダーを指定する準備が整いました。

    引き続き **[新しいプロファイルを追加する]** ペインで、 **[リポジトリの構成]** を選択して **[リポジトリ]** ペインを開きます。

    :::image type="content" source="./media/scanner-repositories-bar.png" alt-text="Azure Information Protection スキャナーのプロファイルを追加する":::

1. **[リポジトリ]** ペインで、 **[追加]** を選択します。

    :::image type="content" source="media/scanner-repository-add.png" alt-text="Azure Information Protection スキャナーのプロファイルを追加する":::

1. **[リポジトリ]** ペインで、前に作成したフォルダーを指定します。 例: `\\server\TestScanner`

    このペインの残りの設定については、変更せずに **[既定のプロファイル]** のままにしておきます。これは、スキャナーのプロファイルからデータ リポジトリに設定が継承されることを意味します。

    **[保存]** を選択します。

1. **[Azure Information Protection] - [プロファイル]** ペインに戻ると、自分のプロファイルが表示されています。 **[スケジュール]** 列には **[手動]** が表示され、 **[強制]** 列は空白です。

    このプロファイル用のスキャナーをまだインストールしていないので、 **[ノード]** 列には **0** が表示されます。

これで、作成したスキャナーのプロファイルを使ってスキャナーをインストールする準備ができました。

## <a name="install-the-scanner"></a>スキャナーのインストール

1. **[管理者として実行]** オプションを使用して PowerShell セッションを開きます。

1. 次のコマンドを使ってスキャナーをインストールします。ネットワーク共有の名前と、Azure portal で保存したプロファイル名を指定します。

    ```ps
    Install-AIPScanner -SqlServerInstance <your network share name>\SQLEXPRESS -Profile <profile name>
    ```

    プロンプトが表示されたら、\<domain\user name> の形式でご自分のスキャナー用の資格情報をに指定し、次にご自分のパスワードを指定します。

## <a name="start-the-scan-and-confirm-it-finished"></a>スキャンの開始および完了の確認

1. Azure portal に戻り、 **[Azure Information Protection] - [プロファイル]** ペインを最新の情報に更新すると、 **[ノード]** 列に **1** と表示されるようになります。

1. ご自身のプロファイル名を選択してから、 **[今すぐスキャン]** オプションを選択します。

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Azure Information Protection スキャナーのプロファイルを追加する":::

    プロファイルを選択した後にこのオプションを使用できない場合は、スキャナーが Azure Information Protection に接続されていません。 構成とインターネット接続を確認します。

1. 調べる対象が小さなファイル 1 つだけなので、この最初のテスト スキャンはすぐに完了します。

    **[前回のスキャン結果]** 列と **[前回のスキャン (終了時刻)]** 列に値が表示されるまで待ちます。

> [!TIP]
> または、クラシック クライアントのスキャナーの場合のみ:
>
> ローカル Windows イベント ログの **[アプリケーションとサービス]** の **[Azure Information Protection]** を確認します。 **MSIP.Scanner** プロセスの情報イベント ID **911** を確認します。 イベント ログ エントリには、スキャンの結果の概要も含まれています。
>
## <a name="see-detailed-results"></a>詳細結果を確認する

エクスプローラーを使用して、 **%*localappdata*%\Microsoft\MSIP\Scanner\Reports** にあるスキャナー レポートを見つけます。 **.csv** ファイル形式の詳細レポート ファイルを開きます。

Excel の場合:

- データ ストア リポジトリとファイル名が最初の 2 列に表示されます。
- 列を調べていくと、 **[Information Type Name]\(情報の種類の名前\)** という名前の列があります。これが最も重要な列です。

    最初のテストでは **[クレジット カード番号]** が表示されています。これは、スキャナーが検索できる多くの機密情報の種類の 1 つです。

## <a name="scan-your-own-data"></a>独自のデータをスキャンする

1. 今回は、機密情報をスキャンする独自のオンプレミスのデータ ストアを指定して、スキャナー プロファイルを編集して新しいデータ リポジトリを追加します。

    ネットワーク共有 (UNC パス)、または SharePoint サイトや SharePoint ライブラリの SharePoint Server の URL を指定します。

    次に例を示します。

    - **ネットワーク共有の場合**: `\\NAS\HR`
    - **SharePoint フォルダーの場合**: `http://sp2016/Shared Documents`

1. もう一度スキャナーを再起動します。

    **[Azure Information Protection] - [プロファイル]** ペインで、プロファイルが選択されていることを確認し、 **[今すぐスキャン]** オプションを選択します。

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Azure Information Protection スキャナーのプロファイルを追加する":::

1. スキャンが完了すると、新しい結果が表示されます。

    このスキャンにかかる時間は、データ ストア内にあるファイルの数や、それらのファイルの大きさ、およびファイルの種類によって異なります。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

運用環境では、Azure Information Protection サービスを自動的に認証するサービス アカウントを使用して、Windows Server 上でスキャナーを実行する場合があります。 また、エンタープライズ レベルのバージョンの SQL サーバーを使用して、いくつかのデータ リポジトリを指定する場合もあります。

リソースをクリーンアップし、システムによる運用環境デプロイの準備を整えるには、PowerShell セッションで次のコマンドを実行して、スキャナーをアンインストールします。

```ps
Uninstall-AIPScanner
```

次に、コンピューターを再起動します。

このコマンドでは以下の項目は削除されません。このクイック スタートの後にこれらを削除する場合は、手動で削除する必要があります。

- Azure Information Protection スキャナーをインストールしたときに、Install-AIPScanner コマンドレットを実行することによって作成された SQL Server データベース:

    - クラシック クライアントの場合: **AIPScanner_\<profile>**
    - 統合ラベル付けクライアントの場合: **AIPScannerUL_\<profile_name>**

- **%*localappdata*%\Microsoft\MSIP\Scanner\Reports** にあるスキャナー レポート。

- ドメイン アカウントがローカル コンピューターに対して付与された、 **[サービスとしてログオン]** ユーザー権限の割り当て。

## <a name="next-steps"></a>次のステップ

このクイックスタートには、オンプレミスのデータ ストア内にある機密情報がスキャナーによって検索されるしくみを簡単に確認するための最小構成が含まれています。 運用環境にスキャナーをインストールする準備が整った場合は、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。

機密情報が含まれているファイルを分類して保護する場合は、自動的な分類と保護のためにラベルを構成する必要があります。

**クラシック クライアントの場合:**

- [Azure Information Protection 用の自動および推奨分類の条件を構成する方法](configure-policy-classification.md)
- [Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)

**統合ラベル付けクライアントの場合:**

- [機密ラベルをコンテンツに自動的に適用する](/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [機密ラベルの暗号化を使用してコンテンツへのアクセスを制限する](/microsoft-365/compliance/encryption-sensitivity-labels)