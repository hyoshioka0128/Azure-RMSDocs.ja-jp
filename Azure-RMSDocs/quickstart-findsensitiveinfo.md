---
title: クイック スタート - Azure Information Protection スキャナーを使ってファイル内の機密情報を検索する - AIP
description: Azure Information Protection スキャナーを使用して、オンプレミスに格納しているファイル内の機密情報を検索します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/15/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 5a051967ad9f3b572eecd5214cf411dd4a4a01d6
ms.sourcegitcommit: d716d3345a6a5adc63814dee28f7c01b55b96770
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57828993"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>クイック スタート:オンプレミスに格納しているファイル内の機密情報を検索する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

このクイック スタートでは、Azure Information Protection スキャナーをインストールして構成し、オンプレミスのデータ ストアに格納されているファイル内にある機密情報を検索します。 たとえば、ローカル フォルダー、ネットワーク共有、SharePoint サーバーなどです。

注: このクイックスタートでは、Azure portal を使用して構成するプレビュー バージョンのスキャナーではなく、現在の一般公開バージョンのスキャナーを使用します。

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

## <a name="install-the-scanner"></a>スキャナーのインストール

1. **[管理者として実行]** オプションを使用して PowerShell セッションを開きます。

2. 自分のコンピューター名を指定しながら次のコマンドを使用して、スキャナーをインストールします。
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS
    
    プロンプトが表示されたら、\<ドメイン\ユーザー名> の形式を使用してスキャナー用の資格情報を独自に指定し、次にパスワードを指定します。 

## <a name="specify-your-test-data-store"></a>テスト用のデータ ストアを指定する

PowerShell セッションで、次のコマンドを入力します。

    Add-AIPScannerRepository -Path C:\TestScanner

## <a name="configure-the-scanner-to-discover-all-information-types"></a>すべての情報の種類を探索するようにスキャナーを構成する

PowerShell セッションで、次のコマンドを入力します。

    Set-AIPScannerConfiguration -Enforce Off -Schedule Manual -DiscoverInformationTypes All

このコマンドでは、指定したデータ リポジトリ内にあるすべてのファイルの 1 回限りの探索を実行するようにスキャナーを構成します。 このスキャンでは、機密情報の既知の種類がすべて検索されます。また、最初に Azure Information Protection ラベルやポリシー設定を構成する必要はありません。

## <a name="start-the-scan-and-confirm-it-finished"></a>スキャンの開始および完了の確認

1. PowerShell セッションで、次のコマンドを入力してスキャナーを起動します。
    
        Start-AIPScan
    
    調べる対象が小さなファイル 1 つだけなので、この最初のテスト スキャンは非常に高速です。 

2. Windows の **[イベント ビューアー]** > **[アプリケーションとサービス]** > **[Azure Information Protection]** イベント ログに移動します。 
    
    Azure Information Protection で **MSIP.Scanner** プロセスに対して情報イベント ID **911** が表示されていることを確認します。 イベント ログ エントリには、スキャンの結果の概要も含まれています。

## <a name="see-detailed-results"></a>詳細結果を確認する

エクスプローラーを使用して、%*localappdata*%\Microsoft\MSIP\Scanner\Reports にあるスキャナー レポートを見つけます。 .csv ファイル形式の詳細レポート ファイルを開きます。

Excel では、データ ストア リポジトリとファイル名が最初の 2 列に表示されます。 列を調べていくと、**[Information Type Name]\(情報の種類の名前\)** という名前の列があります。これが最も重要な列です。 最初のテストでは **[クレジット カード番号]** が表示されています。これは、スキャナーが検索できる多くの機密情報の種類の 1 つです。

## <a name="scan-your-own-data"></a>独自のデータをスキャンする

1. 今回は、機密情報をスキャンする独自のオンプレミスのデータ ストアを指定して、もう一度 Add-AIPScannerRepository を実行します。 
    
    ローカル フォルダー、ネットワーク共有 (UNC パス)、または SharePoint サイトや SharePoint ライブラリの SharePoint サーバーの URL を指定することができます。 
    
    - ローカル フォルダーについての例:
        
            Add-AIPScannerRepository -Path D:\Data\Finance
    
    - ネットワーク共有についての例
        
            Add-AIPScannerRepository -Path \\NAS\HR
    
    - SharePoint フォルダーについての例:
        
            Add-AIPScannerRepository -Path "http://sp2016/Shared Documents"

2. スキャナーを再起動します。
    
        Start-AIPScan

3. スキャンが完了すると、新しい結果が表示されます。 
    
    このスキャンにかかる時間は、データ ストア内にあるファイルの数や、それらのファイルの大きさ、およびファイルの種類によって異なります。 

## <a name="clean-up-resources"></a>リソースをクリーンアップする

運用環境では、Azure Information Protection サービスを自動的に認証するサービス アカウントを使用して、Windows Server 上でスキャナーを実行する場合があります。 また、エンタープライズ レベルのバージョンの SQL サーバーを使用して、いくつかのデータ リポジトリを指定する場合もあります。 

その運用環境へのデプロイの準備が整い、PowerShell セッションでリソースをクリーンアップするためには、次のコマンドを実行してスキャナーをアンインストールします。

    Uninstall-AIPScanner

次に、コンピューターを再起動します。

このコマンドでは以下の項目は削除されません。このクイック スタートの後にこれらを削除する場合は、手動で削除する必要があります。

- Azure Information Protection スキャナーをインストールしたときに、Install-AIPScanner コマンドレットを実行することによって作成された **AzInfoProtection** という名前の SQL サーバー データベース。 

- %*localappdata*%\Microsoft\MSIP\Scanner\Reports にあるスキャナー レポート。

- ドメイン アカウントがローカル コンピューターに対して付与された、**[サービスとしてログオン]** ユーザー権限の割り当て。


## <a name="next-steps"></a>次の手順

このクイック スタートには、スキャナーがネットワーク共有内にある機密情報を検索するしくみを簡単に確認するための最小構成が含まれています。 運用環境にスキャナーをインストールする準備が整った場合は、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。

機密情報が含まれているファイルを分類して保護する場合は、自動的な分類と保護のために Azure Information Protection ラベルを構成する必要があります。

- [Azure Information Protection 用の自動および推奨分類の条件を構成する方法](configure-policy-classification.md)

- [Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)
