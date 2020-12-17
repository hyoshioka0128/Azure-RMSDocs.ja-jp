---
title: チュートリアル - Azure Information Protection (AIP) 統合ラベル付けスキャナーをインストールする
description: Azure Information Protection (AIP) 統合ラベル付けスキャナーをインストールして、オンプレミスのネットワーク共有に格納されている機密データを検出します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 73bcb5e636b8a5e4456ad80f8435a27dfc898339
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384776"
---
# <a name="tutorial-installing-the-azure-information-protection-aip-unified-labeling-scanner"></a>チュートリアル:Azure Information Protection (AIP) 統合ラベル付けスキャナーのインストール

>***適用対象**:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***関連する内容**:[Windows 用の Azure Information Protection 統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

このチュートリアルでは、Azure Information Protection (AIP) オンプレミス スキャナーをインストールする方法について説明します。 このスキャナーを使用すると、AIP 管理者は、自分たちのネットワークやコンテンツ共有をスキャンして機密データがないかを調べ、自分の組織のポリシーで構成されているように分類および保護のラベルを適用することができます。

**必要な時間**:このチュートリアルは 30 分で完了できます。

## <a name="tutorial-prerequisites"></a>チュートリアルの前提条件

統合ラベル付けスキャナーをインストールしてこのチュートリアルを完了するには、次のものが必要です。

|要件  |説明  |
|---------|---------|
|**サポート サブスクリプション**     |  [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/) を含む Azure サブスクリプションが必要です。 <br /><br />これらのサブスクリプションのいずれかがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成してください。       |
|**Azure portal への管理者アクセス** |次のいずれかの管理者アカウントを使用して [Azure portal](https://portal.azure.com/) にサインインできることを確認します。 <br /><br />- **コンプライアンス管理者**<br />- **コンプライアンス データ管理者**<br />- **セキュリティ管理者**<br />- **グローバル管理者** |
|**クライアントのインストール**    |   スキャナーのインストールにアクセスするには、ご利用のコンピューター上に AIP 統合ラベル付けクライアントをインストールします。 <br /><br />[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=53018)から **AzInfoProtection_UL.exe** をダウンロードして実行します。 <br /><br />インストールが完了すると、コンピューターまたは Office ソフトウェアの再起動を求めるメッセージが表示される場合があります。 必要に応じて再起動して続行します。 <br /><br />詳細については、「[クイック スタート: Azure Information Protection (AIP) 統合ラベル付けクライアントのデプロイ](quickstart-deploy-client.md)」を参照してください。|
|**SQL Server**     | スキャナーを実行するには、スキャナー コンピューター上に SQL Server がインストールされている必要があります。 <br /><br /> インストールするには、[SQL Server のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-downloads)に移動し、インストールするインストール オプションの下にある **[今すぐダウンロード]** を選択します。 インストーラーで、 **[基本]** をインストールの種類に選択します。 <br /><br />**注**:SQL Server Enterprise は運用環境に、そして Express はテスト環境のみにインストールすることをお勧めします。       |
|**Azure Active Directory アカウント**     |  標準的なクラウド接続環境で作業する場合は、スキャナーに使用するドメインサービス アカウントを [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) に同期させる必要があります。 これは、オフラインで作業する場合には必要ありません。 <br /><br />ご自身のアカウントについて不明な場合は、いずれかのシステム管理者に問い合わせて同期の状態を確認してください。   |
|**秘密度ラベルと公開されたポリシー** |スキャナー サービス アカウント用に、秘密度ラベルを作成し、少なくとも 1 つのラベルが付いたポリシーをラベル付け管理センターに公開している必要があります。 <br /><br />Microsoft 365 コンプライアンス センター、Microsoft 365 セキュリティ センター、または Microsoft 365 セキュリティ/コンプライアンス センターを含む、ご利用のラベル付け管理センター内で秘密度ラベルを構成します。 詳細については、[Microsoft 365 のドキュメント](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)を参照してください。 |
| | |

前提条件を確認したら、[Azure portal で Azure Information Protection を構成](#configure-azure-information-protection-in-the-azure-portal)します。

## <a name="configure-azure-information-protection-in-the-azure-portal"></a>Azure portal で Azure Information Protection を構成する

Azure Information Protection が Azure portal で使用できないこともあれば、保護が現在アクティブになっていないこともあります。 

必要に応じて、次の手順のいずれか、または両方を実行します。

- [Azure portal に Azure Information Protection を追加する](#add-azure-information-protection-to-the-azure-portal)
- [保護がアクティブになっていることを確認する](#confirm-that-protection-is-activated)

次に、「[Azure portal でスキャナーの初期設定を構成する](#configure-initial-scanner-settings-in-the-azure-portal)」に進んでください。

### <a name="add-azure-information-protection-to-the-azure-portal"></a>Azure portal に Azure Information Protection を追加する

1. [サポートしている管理アカウント](#tutorial-prerequisites)を使用して、[Azure portal](https://portal.azure.com) にサインインします。

1. **[+ リソースの作成]** を選択します。 検索ボックスで、**Azure Information Protection** を検索して選択します。 [Azure Information Protection] ページで、 **[作成]** を選択し、もう一度 **[作成]** を選択します。

    :::image type="content" source="media/gifs/quickstart-add-aip-to-portal.gif" alt-text="Azure portal に Azure Information Protection を追加する":::

    > [!TIP]
    > この手順を初めて実行する場合は、ペインの名前の横に **[ダッシュボードにピン留めする]** ![[ダッシュボードにピン留めする] アイコン](media/qs-tutor/pin-to-dashboard.png "ダッシュボードにピン留めするアイコン") アイコンが表示されます。 ピン アイコンを選択して、ダッシュボード上にタイルを作成すると、次回からここに直接移動できるようになります。

「[保護がアクティブになっていることを確認する](#confirm-that-protection-is-activated)」に進んでください。

### <a name="confirm-that-protection-is-activated"></a>保護がアクティブになっていることを確認する

使用可能な Azure Information Protection が既にある場合は、保護がアクティブになっていることを確認します。

1. Azure Information Protection 領域の左側にある **[管理]** の下で、 **[保護のアクティブ化]** を選択します。

1. テナントの保護がアクティブになっているかどうかを確認します。 次に例を示します。

    :::image type="content" source="media/qs-tutor/confirm-activation.PNG" alt-text="AIP のアクティブ化を確認する":::

保護がアクティブになっていない場合は、![[AIP のアクティブ化]](media/qs-tutor/activate.png "AIP のアクティブ化") **[アクティブ化]** を選択します。 アクティブ化が完了すると、情報バーに **[Activation finished successfully]\(アクティブ化が正常に完了しました\)** と表示されます。

「[Azure portal でスキャナーの初期設定を構成する](#configure-initial-scanner-settings-in-the-azure-portal)」に進んでください。

### <a name="configure-initial-scanner-settings-in-the-azure-portal"></a>Azure portal でスキャナーの初期設定を構成する

ご利用のコンピューターにスキャナーをインストールする前に、Azure portal でスキャナーの初期設定を作成します。

1. Azure Information Protection 領域の左側にある **[スキャナー]** の下で、:::image type="icon" source="media/i-clusters.png" border="false":::  **[クラスター]** を選択します。

1. クラスター ページ上で、:::image type="icon" source="media/i-add.PNG" border="false"::: **[追加]** を選択して、スキャナーを管理するための新しいクラスターを作成します。

1. 右側に開いている **[新しいクラスターの追加]** ウィンドウで、わかりやすいクラスター名と必要に応じて説明を入力します。

    > [!IMPORTANT]
    > このクラスター名は、スキャナーをインストールするときに必要となります。
    > 
    
    次に例を示します。

    :::image type="content" source="media/qs-tutor/qs-add-new-cluster.png" alt-text="チュートリアル用に新しいクラスターを追加する":::

1. 最初のコンテンツ スキャン ジョブを作成します。 左側の **[スキャナー]** メニューで、:::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **[コンテンツ スキャン ジョブ]** を選択してから、:::image type="icon" source="media/i-add.PNG" border="false"::: **[追加]** を選択します。

1. **[Add a new content scan job]\(新しいコンテンツ スキャン ジョブの追加\)** ウィンドウで、コンテンツ スキャン ジョブに付けるわかりやすい名前と、必要に応じて説明を入力します。

    次に、 **[ポリシーの適用]** までページを下方にスクロールし、 **[オフ]** を選択します。

    完了したら、変更内容を保存します。 

    この既定のスキャン ジョブでは、既知の機密情報の種類がすべてスキャンの対象となります。

1. コンテンツ スキャン ジョブの詳細ウィンドウを閉じ、:::image type="icon" source="media/i-content-scan-jobs.png" border="false":::  **[コンテンツ スキャン ジョブ]** グリッドに戻ります。 

    コンテンツ スキャン ジョブに対して表示される新しい行の **[クラスター名]** 列で、 **[+ クラスターへの割り当て]** を選択します。 次に、右側に表示される **[クラスターへの割り当て]** ウィンドウで、目的のクラスターを選択します。 

    :::image type="content" source="media/qs-tutor/assign-cluster-all.png" alt-text="クラスターへの割り当て":::

これで、[AIP 統合ラベル付けスキャナーをインストールする](#install-the-aip-unified-labeling-scanner)準備ができました。

## <a name="install-the-aip-unified-labeling-scanner"></a>AIP 統合ラベル付けスキャナーをインストールする

[Azure portal で基本的なスキャナーを構成](#configure-azure-information-protection-in-the-azure-portal)したら、ご利用の AIP クライアント コンピューターに統合ラベル付けスキャナーをインストールします。

1. クライアント コンピューター上で、 **[管理者として実行]** オプションを使用して PowerShell セッションを開きます。

1. 次のコマンドを使用してスキャナーをインストールします。 このコマンドでは、スキャナーをインストールする場所と、[Azure portal で作成したクラスター](#configure-initial-scanner-settings-in-the-azure-portal)の名前を指定します。

    ```PowerShell
    Install-AIPScanner -SqlServerInstance <your SQL installation location>\SQLEXPRESS -Cluster <cluster name>
    ```
    次に例を示します。

    ```powershell
    Install-AIPScanner -SqlServerInstance localhost\SQLEXPRESS -Cluster Quickstart
    ```

    資格情報を入力するように PowerShell から求められたら、ユーザー名とパスワードを入力します。 

    **[ユーザー名]** フィールドについては、次の構文を使用します: `<domain\user name>`。 (例: `emea\contososcanner`)。

1. Azure portal に戻ります。 左側の **[スキャナー]** メニューで、:::image type="icon" source="media/qs-tutor/i-nodes.png" border="false"::: **[ノード]** を選択します。 

    ここで、ご自分のスキャナーがグリッドに追加されているのがわかります。 次に例を示します。

    :::image type="content" source="media/qs-tutor/qs-post-install-scanner.png" alt-text="新しくインストールしたスキャナーが [ノード] グリッド上に表示されている":::

「[スキャナー用の Azure Active Directory トークンを取得する](#get-an-azure-active-directory-token-for-the-scanner)」に進み、スキャナー サービス アカウントを非対話形式で実行できるようにします。

## <a name="get-an-azure-active-directory-token-for-the-scanner"></a>スキャナー用の Azure Active Directory トークンを取得する

標準的なクラウド接続環境で作業している場合にこの手順を行うと、スキャナーで AIP サービスへの認証を実行できるようになり、その結果サービスを非対話形式で実行することが可能になります。

オフラインのみで作業している場合、この手順は必要ありません。

「[非対話形式でファイルに Azure Information Protection のラベル付けをする方法](rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」を参照してください。

**スキャナー用の Azure AD トークンを取得するには**:

1. Azure portal で、認証用のアクセス トークンを指定するための Azure AD アプリケーションを作成します。

1. スキャナー コンピューター上で、**ローカル ログオン** 権限が付与されているスキャナー サービス アカウントでサインインし、PowerShell セッションを開始します。

1. PowerShell セッションを開始し、そして Azure AD アプリケーションからコピーした値を使用して次のコマンドを実行します。

    ```PowerShell
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```

    次に例を示します。

    ```PowerShell
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds

    Acquired application access token on behalf of CONTOSO\scanner.
    ``` 

    > [!TIP]
    > インストールのための **ローカル ログオン** 権限をスキャナー サービス アカウントに付与できない場合は、**Set-AIPAuthentication** に対して、**DelegatedUser** パラメーターではなく、**OnBehalfOf** パラメーターを使用してください。

これで、Azure AD への認証を行うためのトークンがスキャナーに与えられました。 このトークンは、Azure Active Directory 内で構成されている限り有効です。 トークンの有効期限が切れた場合は、この手順を繰り返す必要があります。

[オプションのネットワーク探索サービスのインストール](#install-the-network-discovery-service)に関するセクションに進みます。それに従えば、ネットワーク リポジトリをスキャンして危険にさらされるおそれがあるコンテンツがないかを調べてから、それらのリポジトリをコンテンツ スキャン ジョブに追加することができます。

## <a name="install-the-network-discovery-service"></a>ネットワーク探索サービスをインストールする

AIP 統合ラベル付けクライアントのバージョン [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 以降、管理者は AIP スキャナーを使用してネットワーク リポジトリをスキャンして、危険にさらされるおそれがあると考えられるリポジトリをコンテンツ スキャン ジョブに追加することができます。

ネットワーク スキャン ジョブを使用すれば、管理者とパブリック ユーザーの両方で、構成されたリポジトリへのアクセスを試みることによって、コンテンツが危険にさらされるおそれがある "*場所*" を容易に把握することができます。

たとえば、読み取りと書き込みのパブリック アクセスが両方とも行われるリポジトリが見つかった場合は、さらにスキャンし、そこに機密データが保存されていないことを確認することをお勧めします。

> [!NOTE]
> 現在、この機能はプレビュー段階にあります。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。

**ネットワーク探索サービスをインストールするには**:

1. スキャナー コンピューター上で、管理者として PowerShell セッションを開きます。

1. ネットワーク探索サービスを実行するとき、管理者およびパブリック ユーザーのアクセスをシミュレートするときに、AIP で使用する資格情報を定義します。 

    プロンプトが表示されたら、次の構文を使用して、コマンドごとに資格情報を入力します: `domain\user`。 例: `emea\msanchez`

    次を実行します。 

    **ネットワーク探索サービスを実行するための資格情報**:

    ``` PowerShell 
    $serviceacct= Get-Credential 
    ``` 

    **管理者アクセスをシミュレートするための資格情報**:

    ``` PowerShell 
    $shareadminacct= Get-Credential 
    ``` 

    **パブリック ユーザー アクセスをシミュレートするための資格情報**:

    ``` PowerShell  
    $publicaccount= Get-Credential 
    ``` 

1. ネットワーク探索サービスをインストールするには、次のようにします。

    ```PowerShell
    Install-MIPNetworkDiscovery [-ServiceUserCredentials] <PSCredential> [[-StandardDomainsUserAccount] <PSCredential>] [[-ShareAdminUserAccount] <PSCredential>] [-SqlServerInstance] <String> -Cluster <String> [-WhatIf] [-Confirm] [<CommonParameters>]

    For example:

    ```PowerShell
    Install-MIPNetworkDiscovery -SqlServerInstance SQLSERVER1\SQLEXPRESS -Cluster Quickstart -ServiceUserCredentials $serviceacct  -ShareAdminUserAccount $shareadminacct -StandardDomainsUserAccount $publicaccount
 
    ```

インストールが完了すると、システムに確認メッセージが表示されます。

## <a name="next-steps"></a>次のステップ

スキャナーとネットワーク探索サービスのインストールが完了したら、いつでもスキャンを開始することができます。 

詳細については、「[チュートリアル: Azure Information Protection (AIP) スキャナーを使用して機密コンテンツを検出する](tutorial-scan-networks-and-content.md)」を参照してください。

> [!TIP]
> [バージョン 2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) のインストールが完了したら、ネットワークをスキャンして、危険にさらされているコンテンツが含まれている可能性があるリポジトリを検出することをお勧めします。 
>
>危険性の高いリポジトリをスキャンして機密データがないかを調べてから、そのデータを分類して外部ユーザーから保護を行うには、検出されたリポジトリの詳細でコンテンツ スキャン ジョブを更新します。
>

**関連項目**:

- [Azure Information Protection 統合ラベル付けスキャナーとは](deploy-aip-scanner.md)
- [Azure Information Protection 統合ラベル付けスキャナーをインストールおよびデプロイするための前提条件](deploy-aip-scanner-prereqs.md)
- [チュートリアル: Azure Information Protection (AIP) を使用した過剰共有の防止](tutorial-preventing-oversharing.md)
- [チュートリアル: Azure Information Protection (AIP) クラシック クライアントから統合ラベル付けクライアントへの移行](tutorial-migrating-to-ul.md)
