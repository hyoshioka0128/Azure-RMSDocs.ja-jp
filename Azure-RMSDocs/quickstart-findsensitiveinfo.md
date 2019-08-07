---
title: クイック スタート - Azure Information Protection スキャナーを使って機密情報を検索する
description: Azure Information Protection スキャナーを使用して、オンプレミスに格納しているファイル内の機密情報を検索します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 888ddafcea6dd855d970fc959e1bb7447c3d2573
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68790419"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>クイック スタート:オンプレミスに格納しているファイル内の機密情報を検索する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)* "

このクイック スタートでは、Azure Information Protection スキャナーをインストールして構成し、オンプレミスのデータ ストアに格納されているファイル内にある機密情報を検索します。 たとえば、ローカル フォルダー、ネットワーク共有、SharePoint サーバーなどです。

注: このクイックスタートでは現在の一般提供バージョンのスキャナーを使います。これでは、前のバージョンで使われていた PowerShell コマンドレットではなく Azure portal が構成用に使われます。

この構成は 10 分未満で完了します。

## <a name="prerequisites"></a>必要条件

このクイック スタートを完了するには、次の要件があります。

1. Azure Information Protection プラン 1 またはプラン 2 を含むサブスクリプション。
    
    このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

2. Azure Information Protection クライアントがコンピューターにインストールされている。 
    
    クライアントをインストールするには、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)に移動し、Azure Information Protection ページから **AzInfoProtection.exe** をダウンロードします。
    
3. SQL Server Express もコンピューターにインストールされている。
    
    この SQL Server エディションがまだインストールされていない場合は、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express)からダウンロードして、基本インストールを選択できます。

4. 自分のドメイン アカウントが Azure AD に同期されている。

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

## <a name="prepare-a-test-folder-and-file"></a>テスト用のフォルダーとファイルを準備する

スキャナーが動作していることを確認する最初のテスト用に、次の操作を実行します。

1. コンピューターにローカル フォルダーを作成します。 たとえば、ローカルの C ドライブ上の **TestScanner** です。

2. **4242-4242-4242-4242** というテキスト (テスト用の既知のクレジット カード番号) を含む Word ドキュメントを作成して、そのフォルダー内に保存します。

## <a name="configure-a-profile-for-the-scanner"></a>スキャナー用のプロファイルを構成する

スキャナーをインストールする前に、Azure portal でそのためのプロファイルを作成します。 このプロファイルには、スキャナーの設定と、スキャンするデータ リポジトリの場所が含まれます。

1. 新しいブラウザー ウィンドウを開いて、[Azure portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
2. **[スキャナー]** メニュー オプションを見つけて、 **[プロファイル]** を選択します。

3. **[Azure Information Protection - Profiles]\(Azure Information Protection - プロファイル\)** ブレードで、 **[追加]** を選択します。
    
    ![Azure Information Protection スキャナーのプロファイルを追加する](./media/scanner-add-profile.png)

4. **[新しいプロファイルを追加する]** ブレードで、その構成設定とスキャンするデータ リポジトリを識別するために使うスキャナーの名前を指定します。 たとえば、このクイックスタートでは、**Quickstart** を指定できます。 後でスキャナーをインストールするときに、同じプロファイル名を指定する必要があります。
    
    スキャナーのプロファイル名を識別するために、必要に応じて管理目的の説明を指定します。

5. このクイックスタートでは、設定を 1 つだけ選択します。 **[ポリシーの適用]** に対して、 **[オフ]** を選択します。 次に **[保存]** を選択しますが、ブレードは閉じないでください。
    
    この設定では、指定したデータ リポジトリ内にあるすべてのファイルの 1 回限りの探索を実行するようにスキャナーを構成します。 このスキャンでは、機密情報の既知の種類がすべて検索されます。また、最初に Azure Information Protection ラベルやポリシー設定を構成する必要はありません

6. これでプロファイルの作成と保存が完了したので、 **[リポジトリの構成]** オプションに戻って、スキャンするデータ ストアとしてローカル フォルダーを指定する準備が整いました。
    
    引き続き **[新しいプロファイルを追加する]** ブレード上で、 **[リポジトリの構成]** を選択して **[リポジトリ]** ブレードを開きます。
    
    ![Azure Information Protection スキャナーのデータ リポジトリを構成する](./media/scanner-repositories-bar.png)

7. **[リポジトリ]** ブレードで、 **[追加]** を選択します。
    
    ![Azure Information Protection スキャナーのデータ リポジトリを追加する](./media/scanner-repository-add.png)

8. **[リポジトリ]** ブレード上で、一番最初の手順で作成したローカル フォルダーを指定します。 例: `C:\TestScanner`
    
    このブレード上の残りの設定に関しては、変更せずに **[既定のプロファイル]** のままにしておきます。 これは、データ リポジトリがスキャナーのプロファイルから設定を継承することを意味します。 
    
    **[保存]** を選択します。

9. これで **[新しいプロファイルを追加する]** ブレードを閉じることができ、 **[Azure Information Protection - Profiles]\(Azure Information Protection - プロファイル\)** ブレードにご自分のプロファイル名が表示されます。 **[スケジュール]** 列には **[手動]** が表示され、 **[強制]** 列は空白です。

これで、先ほど作成したスキャナーのプロファイルを使ってスキャナーをインストールする準備ができました。

## <a name="install-the-scanner"></a>スキャナーのインストール

1. **[管理者として実行]** オプションを使用して PowerShell セッションを開きます。

2. 次のコマンドを使ってスキャナーをインストールします。自分のコンピューター名と、Azure portal で保存したプロファイル名を指定します。
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS -Profile <profile name>
    
    プロンプトが表示されたら、\<ドメイン\ユーザー名> の形式を使用してスキャナー用の資格情報を独自に指定し、次にパスワードを指定します。 

## <a name="start-the-scan-and-confirm-it-finished"></a>スキャンの開始および完了の確認

1. 再び Azure portal で、Azure Information Protection に戻ってスキャナーを起動します。 **[スキャナー]** メニュー オプションから、 **[ノード]** を選択します。 自分のコンピューター名を選択したら、 **[今すぐスキャン]** オプションを選択します。
    
    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)

2. 調べる対象が小さなファイル 1 つだけなので、この最初のテスト スキャンは非常に高速です。
    
    - **[Azure Information Protection - Nodes]\(Azure Information Protection - ノード\)** ブレードで、 **[状態]** 列の値が **[スキャン]** から **[アイドル]** に変化します。
    
    - または、ローカル Windows イベント ログの **[アプリケーションとサービス]** の **[Azure Information Protection]** を確認します。 **MSIP.Scanner** プロセスの情報イベント ID **911** を確認します。 イベント ログ エントリには、スキャンの結果の概要も含まれています。

## <a name="see-detailed-results"></a>詳細結果を確認する

エクスプローラーを使用して、%*localappdata*%\Microsoft\MSIP\Scanner\Reports にあるスキャナー レポートを見つけます。 .csv ファイル形式の詳細レポート ファイルを開きます。

Excel では、データ ストア リポジトリとファイル名が最初の 2 列に表示されます。 列を調べていくと、 **[Information Type Name]\(情報の種類の名前\)** という名前の列があります。これが最も重要な列です。 最初のテストでは **[クレジット カード番号]** が表示されています。これは、スキャナーが検索できる多くの機密情報の種類の 1 つです。

## <a name="scan-your-own-data"></a>独自のデータをスキャンする

1. 今回は、機密情報をスキャンする独自のオンプレミスのデータ ストアを指定して、スキャナー プロファイルを編集して新しいデータ リポジトリを追加します。 
    
    ローカル フォルダー、ネットワーク共有 (UNC パス)、または SharePoint サイトや SharePoint ライブラリの SharePoint サーバーの URL を指定することができます。 
    
    - ローカル フォルダーについての例:
        
            D:\Data\Finance
    
    - ネットワーク共有についての例
        
            \\NAS\HR
    
    - SharePoint フォルダーについての例:
        
            http://sp2016/Shared Documents

2. もう一度スキャナーを再起動します。 **[スキャナー]** メニュー オプションから、 **[ノード]** を選択し、自分のコンピューター名を選択した後、 **[今すぐスキャン]** オプションを選択します。
    
    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)

3. スキャンが完了すると、新しい結果が表示されます。 
    
    このスキャンにかかる時間は、データ ストア内にあるファイルの数や、それらのファイルの大きさ、およびファイルの種類によって異なります。 

## <a name="clean-up-resources"></a>リソースをクリーンアップする

運用環境では、Azure Information Protection サービスを自動的に認証するサービス アカウントを使用して、Windows Server 上でスキャナーを実行する場合があります。 また、エンタープライズ レベルのバージョンの SQL サーバーを使用して、いくつかのデータ リポジトリを指定する場合もあります。 

その運用環境へのデプロイの準備が整い、PowerShell セッションでリソースをクリーンアップするためには、次のコマンドを実行してスキャナーをアンインストールします。

    Uninstall-AIPScanner

次に、コンピューターを再起動します。

このコマンドでは以下の項目は削除されません。このクイック スタートの後にこれらを削除する場合は、手動で削除する必要があります。

- Azure Information Protection スキャナーをインストールしたときに、Install-AIPScanner コマンドレットを実行することによって作成された **AIPScanner_\<プロファイル>** という名前の SQL Server データベース。 

- %*localappdata*%\Microsoft\MSIP\Scanner\Reports にあるスキャナー レポート。

- ドメイン アカウントがローカル コンピューターに対して付与された、 **[サービスとしてログオン]** ユーザー権限の割り当て。


## <a name="next-steps"></a>次の手順

このクイック スタートには、スキャナーがネットワーク共有内にある機密情報を検索するしくみを簡単に確認するための最小構成が含まれています。 運用環境にスキャナーをインストールする準備が整った場合は、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。

機密情報が含まれているファイルを分類して保護する場合は、自動的な分類と保護のために Azure Information Protection ラベルを構成する必要があります。

- [Azure Information Protection 用の自動および推奨分類の条件を構成する方法](configure-policy-classification.md)

- [Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)
