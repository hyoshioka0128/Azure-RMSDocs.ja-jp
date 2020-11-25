---
title: チュートリアル - Azure Information Protection (AIP) スキャナーを使用して機密コンテンツを検出する
description: Azure Information Protection (AIP) スキャナーを使用して、危険にさらされるおそれのあるリポジトリを見つけます。 次に、ドリルダウンして、それらのファイル共有をスキャンし、機密コンテンツを探します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 432004443bf684967849b5b91acd9052cbf07eec
ms.sourcegitcommit: 72694afc0e74fd51662e40db2844cdb322632428
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94924977"
---
# <a name="tutorial-discovering-your-sensitive-content-with-the-azure-information-protection-aip-scanner"></a>チュートリアル: Azure Information Protection (AIP) スキャナーを使用して機密コンテンツを検出する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順: [Windows 用の Azure Information Protection 統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection クライアントには、システム管理者がオンプレミスのファイル リポジトリをスキャンして機密コンテンツを検出できるようにするためのオンプレミスのスキャナーが用意されています。 

このチュートリアルで学習する内容は次のとおりです。

> [!div class="checklist"]
> * ネットワーク スキャン ジョブを作成し、危険なリポジトリ探してスキャンする
> * 危険なリポジトリが見つかったら、コンテンツ スキャン ジョブに追加する
> * コンテンツ共有をスキャンして機密コンテンツを探し、検出された結果を理解する

> [!NOTE]
> ネットワーク探索は、統合ラベル付けクライアントのバージョン [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 以降でのみ使用することができ、現在プレビュー段階にあります。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。
>
> このバージョンのクライアントおよびスキャナーがインストールされていない場合は、[チュートリアルの前提条件](#tutorial-prerequisites)を確認してから、「[コンテンツ スキャン ジョブを定義して実行する](#define-and-run-your-content-scan-job)」に進んでください。


**必要な時間:** この構成は 15 分で完了します。

## <a name="tutorial-prerequisites"></a>チュートリアルの前提条件

|要件  |説明  |
|---------|---------|
|**サポート サブスクリプション**     |  [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/) を含む Azure サブスクリプションが必要です。 <br /><br />このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。       |
|**Azure portal への管理者アクセス** |サポートされている管理者アカウントで [Azure portal](https://portal.azure.com/) にサインインできること、保護が有効になっていることを確認してください。 サポートされている管理者アカウントは次のとおりです。 <br /><br />- **コンプライアンス管理者**<br />- **コンプライアンス データ管理者**<br />- **セキュリティ管理者**<br />- **グローバル管理者**   |
|**AIP クライアント、スキャナー、およびネットワーク探索サービス**   |   このチュートリアルを完全に完了するには、Azure Information Protection 統合ラベル付けクライアントおよびスキャナーと、ネットワーク探索サービス (パブリック プレビュー) をインストールしておく必要があります。 <br /><br />詳細については、次を参照してください。 <br /><br />- [クイックスタート: Azure Information Protection (AIP) 統合ラベル付けクライアントのデプロイ](quickstart-deploy-client.md) <br />- [チュートリアル: Azure Information Protection (AIP) 統合ラベル付けスキャナーのインストール](tutorial-install-scanner.md) |
|**コンテンツ スキャン ジョブ** | テストに使用できる基本的なコンテンツ スキャン ジョブがあることを確認します。 [スキャナーのインストール](tutorial-install-scanner.md)時に作成済みである可能性があります。<br /><br />ここで作成する必要がある場合は、「[Azure portal で Azure Information Protection を構成する](tutorial-install-scanner.md#configure-azure-information-protection-in-the-azure-portal)」に記載の手順を参照してください。 基本的なコンテンツ スキャン ジョブがある場合は、ここに戻り、このチュートリアルを完了してください。 |
|**SQL Server**     | スキャナーを実行するには、スキャナー コンピューター上に SQL Server がインストールされている必要があります。 <br /><br /> インストールするには、[SQL Server のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-downloads)に移動し、インストールするインストール オプションの下にある **[今すぐダウンロード]** を選択します。 インストーラーで、 **[基本]** をインストールの種類に選択します。 <br /><br />**注**:SQL Server Enterprise は運用環境に、そして Express はテスト専用にインストールすることをお勧めします。    |
|**Azure Active Directory アカウント**     |  標準的なクラウド接続で作業する場合は、使用するドメイン アカウントを [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)に同期させる必要があります。 これは、オフラインで作業する場合には必要ありません。 <br /><br />ご自身のアカウントについて不明な場合は、いずれかのシステム管理者に問い合わせて同期の状態を確認してください。 詳細については、「[代替構成でのスキャナーのデプロイ](deploy-aip-scanner-prereqs.md#deploying-the-scanner-with-alternative-configurations)」を参照してください。  |
|**秘密度ラベルと公開されたポリシー** |スキャナー サービス アカウント用に、秘密度ラベルを作成し、少なくとも 1 つのラベルが付いたポリシーをラベル付け管理センターに公開している必要があります。 <br /><br />Microsoft 365 コンプライアンス センター、Microsoft 365 セキュリティ センター、または Microsoft 365 セキュリティ/コンプライアンス センターを含む、ご利用のラベル付け管理センター内で秘密度ラベルを構成します。 詳細については、[Microsoft 365 のドキュメント](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)を参照してください。 |
| | | 


準備ができたら、「[ネットワーク スキャン ジョブを作成する](#create-a-network-scan-job)」に進んでください。

## <a name="create-a-network-scan-job"></a>ネットワーク スキャン ジョブを作成する

指定した IP アドレスまたは IP 範囲をスキャンして危険なリポジトリを探すネットワーク スキャン ジョブを作成します。

> [!NOTE]
> この機能は、バージョン [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 以降でのみ使用することができ、現在プレビュー段階にあります。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。
> 

**ネットワーク スキャン ジョブを作成するには:**

1. [サポートされている管理者](#tutorial-prerequisites)として [Azure portal](https://portal.azure.com/) にサインインし、 **[Azure Information Protection]** 領域に移動します。
        
1. 左側の **[スキャナー]** メニューで、:::image type="icon" source="media/qs-tutor/i-network-scan-jobs.png" border="false"::: **[ネットワーク スキャン ジョブ (プレビュー)]** を選択します。

1. :::image type="icon" source="media/i-add.PNG" border="false"::: **[追加]** を選択して、新しいジョブを追加します。 **[新しいネットワーク スキャン ジョブを追加する]** ウィンドウで、次の詳細を入力します。
    
    |オプション  |説明  |
    |---------|---------|
    |**ネットワーク スキャン ジョブ名** と **説明**     |わかりやすい名前 (`Quickstart` など) を入力し、必要に応じて説明を入力します。         |
    |**クラスターを選択します**     | ドロップダウン リストからご利用のクラスター名を選択します。<br /><br /> たとえば、「[チュートリアル: Azure Information Protection (AIP) 統合ラベル付けスキャナーのインストール](tutorial-install-scanner.md)」を終了してから、そのクラスターを引き続き使用できるようにするには、 **[クイックスタート]** を選択します。       |
    |**検出する IP 範囲を構成する**     | 行を選択して **[Choose IP ranges]\(IP 範囲の選択\)** ウィンドウを開きます。 ここで、スキャンする IP アドレスまたは IP 範囲を入力します。 <br /><br />**注**: 必ずスキャナーのコンピューターからアクセス可能な IP アドレスを入力してください。      |
    |**スケジュールを設定する**     | 既定値の **[1 回限り]** をそのまま使用します。        |
    |**開始時刻 (UTC) を設定する**     |  現在のタイムゾーンを考慮して現在の UTC 時刻を計算し、今から 5 分以内に実行されるように開始時刻を設定します。     |
    |     |         |

    次に例を示します。 

    :::image type="content" source="media/qs-tutor/network-scan-job.png" alt-text="ネットワーク スキャン ジョブの詳細を入力する":::

1. ページの最上部で :::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **[保存]** を選択します。

1. :::image type="icon" source="media/qs-tutor/i-network-scan-jobs.png" border="false"::: **[ネットワーク スキャン ジョブ (プレビュー)]** グリッドに戻り、スキャンの実行が開始されるまで待ちます。

スキャンが完了すると、グリッド データが更新されます。 次に例を示します。

:::image type="content" source="media/qs-tutor/scanned-network.png" alt-text="更新されたネットワーク スキャン ジョブ":::

> [!TIP]
> ネットワーク スキャン ジョブが実行されない場合は、スキャナー コンピューター上に[ネットワーク探索サービスが正しくインストールされている](tutorial-install-scanner.md#install-the-network-discovery-service)ことを確認してください。

「[危険なリポジトリをコンテンツ スキャン ジョブに追加する](#add-risky-repositories-to-a-content-scan-job)」に進みます。

## <a name="add-risky-repositories-to-a-content-scan-job"></a>危険なリポジトリをコンテンツ スキャン ジョブに追加する

ネットワークス キャンジョブが完了したら、危険なリポジトリが検出されたかどうかを確認できます。 

たとえば、読み取りと書き込みのパブリック アクセスが両方とも行われるリポジトリが見つかった場合は、さらにスキャンし、そこに機密データが保存されていないことを確認することをお勧めします。

> [!NOTE]
> この機能は、バージョン [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 以降でのみ使用することができ、現在プレビュー段階にあります。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。
> 

**危険なリポジトリをコンテンツ スキャン ジョブに追加するには**:

1. [サポートされている管理者](#tutorial-prerequisites)として [Azure portal](https://portal.azure.com/) にサインインし、 **[Azure Information Protection]** ウィンドウに移動します。
        
1. 左側の **[スキャナー]** メニューで、:::image type="icon" source="media/qs-tutor/i-repos.png" border="false"::: **[リポジトリ (プレビュー)]** を選択します。

    :::image type="content" source="media/small/risky-repos-small.png" alt-text="ネットワーク スキャン ジョブによって検出されたリポジトリを表示する" lightbox="media/qs-tutor/risky-repos.png":::

1. グラフの下にあるグリッドで、スキャナーによってまだ管理されていないリポジトリを見つけます。 スキャナーによって管理されていないとは、それらがコンテンツ スキャン ジョブに含まれていなくて、機密コンテンツを探してスキャンが行われていないことを意味します。

    > [!TIP]
    > たとえば、**有効なパブリック アクセス** が **R** (読み取り) または **RW** (読み取り/書き込み) であることが判明したリポジトリは、一般に公開されており、その機密コンテンツが危険にさらされるおそれがあります。
    > 

1. その行を選択し、グリッドの上にある :::image type="icon" source="media/i-add.PNG" border="false"::: **[Assign Selected Items]\(選択された項目の割り当て\)** を選択します。 

1. 右側に表示される **[Assign to Content Scan Job]\(コンテンツ スキャン ジョブに割り当て\)** ウィンドウで、ドロップダウン リストから自分のコンテンツ スキャン ジョブを選択して、:::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **[保存]** を選択します。

    次に例を示します。

    :::image type="content" source="media/qs-tutor/assign-content-scan-job.png" alt-text="危険なリポジトリをコンテンツ スキャン ジョブに割り当てる":::

ご利用のコンテンツ スキャン ジョブが次に実行されると、この新しく検出されたリポジトリが取り込まれ、さらにポリシーで構成されているように機密コンテンツの特定、ラベル付け、分類、および保護が行われます。

「[コンテンツ スキャン ジョブを定義して実行する](#define-and-run-your-content-scan-job)」に進みます。

## <a name="define-and-run-your-content-scan-job"></a>コンテンツ スキャン ジョブを定義して実行する

[チュートリアルの前提条件](#tutorial-prerequisites)で準備したコンテンツ スキャン ジョブを使用して、コンテンツをスキャンします。 

コンテンツ スキャン ジョブをまだ用意していない場合は、[Azure portal での初期設定の構成](tutorial-install-scanner.md#configure-initial-scanner-settings-in-the-azure-portal)を実行してから、ここに戻って続行します。


1. [サポートされている管理者](#tutorial-prerequisites)として [Azure portal](https://portal.azure.com/) にサインインし、 **[Azure Information Protection]** ウィンドウに移動します。
        
1. 左側の **[スキャナー]** メニューで、:::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **[コンテンツ スキャン ジョブ]** を選択してから、ご利用のコンテンツ スキャン ジョブを選択します。
 
1. わかりやすい名前を付けし、必要に応じて説明を加えるように、コンテンツ スキャン ジョブの設定を編集します。 

    次の変更を除き、ほとんどの設定については既定値をそのまま使用します。

    -  **推奨されるラベル付けを自動として処理します**。 **[オン]** に設定します。
    
    - **リポジトリの構成**。 少なくとも 1 つのリポジトリを定義します。 
    
        > [!TIP]
        > 「[危険なリポジトリをコンテンツ スキャン ジョブに追加する](#add-risky-repositories-to-a-content-scan-job)」に従って、ご利用のネットワークをスキャンした後でコンテンツ スキャン ジョブにさらにリポジトリを加えた場合は、今ここにリストされたそれらを表示することを選択できます。 

    - **強制**: **[オン]** に設定します
    
1. :::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **[保存]** を選択してから、:::image type="icon" source="media/i-content-scan-jobs.PNG" border="false"::: **[コンテンツ スキャン ジョブ]** グリッドに戻ります。

1. コンテンツをスキャンするには、:::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **[コンテンツ スキャン ジョブ]** 領域に戻り、目的のコンテンツ スキャン ジョブを選択します。

    グリッドの上にあるツールバーで、:::image type="icon" source="media/i-scan-now.PNG" border="false"::: **[今すぐスキャン]** を選択してスキャンを開始します。

    スキャンが完了したら、「[スキャンの結果を表示する](#view-scan-results)」に進みます。

### <a name="view-scan-results"></a>スキャンの結果を表示する

スキャンが完了したら、Azure portal の **[Azure Information Protection] > [分析]** 領域でレポートを確認します。

次に例を示します。

:::image type="content" source="media/qs-tutor/content-scan-job-data-discovery.PNG" alt-text="スキャナーの結果の分析データ検出レポート":::
    
> [!TIP]
> 結果が空である場合に、意味のあるスキャンを実行したいときは、コンテンツ スキャン ジョブに含まれているリポジトリの 1 つに **支払い情報** という名前のファイルを作成します。 次の内容を含むファイルを保存します。
> 
> **クレジット カード:** 2384 2328 5436 3489
>
> スキャンをもう一度実行して、結果の違いを確認します。
> 

詳細については、「[Azure Information Protection の中央レポート機能 (パブリック レビュー)](reports-aip.md)」を参照してください。

#### <a name="local-scanner-reports"></a>ローカル スキャナー レポート

ログはまた、スキャナー コンピューター上の **%localappdata%\Microsoft\MSIP\Scanner\Reports ディレクトリ** にローカルにも保存され、その内容は次のとおりです。

|Type  |説明  |
|---------|---------|
|**.txt 概要ファイル**     |  スキャンにかかった時間、スキャンされたファイルの数、情報の種類と一致したファイルの数が含まれています。       |
|**.csv 詳細ファイル。**     | スキャンされた各ファイルの詳細な説明が含まれます。 ディレクトリには、スキャン サイクルごとに最大で 60 のレポートを保持できます。         |
|     |         |

## <a name="next-steps"></a>次のステップ

その他のチュートリアルについては、以下を参照してください。

- [チュートリアル: Azure Information Protection (AIP) を使用した過剰共有の防止](tutorial-preventing-oversharing.md)
- [チュートリアル: Azure Information Protection (AIP) クラシック クライアントから統合ラベル付けクライアントへの移行](tutorial-migrating-to-ul.md)

**関連項目:**

- [Azure Information Protection 統合ラベル付けスキャナーとは](deploy-aip-scanner.md)
- [Azure Information Protection 統合ラベル付けスキャナーをインストールおよびデプロイするための前提条件](deploy-aip-scanner-prereqs.md)
- [Azure Information Protection 統合ラベル付けスキャナーの構成とインストール](deploy-aip-scanner-configure-install.md)
- [Azure Information Protection スキャナーの実行](deploy-aip-scanner-manage.md)
