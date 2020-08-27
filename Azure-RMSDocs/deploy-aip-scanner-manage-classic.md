---
title: Azure Information Protection クラシックスキャナー (AIP) の実行
description: Azure Information Protection クラシックスキャナーを実行して、データストア上のファイルを検出、分類、および保護する方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bb50a25ee406ac6899e15480f0c665f82a7434fd
ms.sourcegitcommit: 2cb5fa2a8758c916da8265ae53dfb35112c41861
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88953101"
---
# <a name="running-the-azure-information-protection-classic-scanner"></a>Azure Information Protection クラシックスキャナーの実行

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE]
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。
>
> 統一されたラベル付けスキャナーを使用している場合は、「 [Azure Information Protection スキャナーの実行](deploy-aip-scanner-manage.md)」を参照してください。

[システム要件](deploy-aip-scanner-prereqs-classic.md)を確認し、スキャナーを[構成してインストールし](deploy-aip-scanner-configure-install-classic.md)たら、[検出スキャンを実行](#run-a-discovery-cycle-and-view-reports-for-the-scanner)して作業を開始します。

次に説明する他の手順に従って、スキャンを管理します。

- [スキャンを停止する](#stopping-a-scan)
- [ファイルの再スキャン](#rescanning-files)
- [停止したスキャンのトラブルシューティング](#troubleshooting-a-stopped-scan)
- [スキャナー診断ツールを使用したトラブルシューティング](#troubleshooting-using-the-scanner-diagnostic-tool)
- [スキャナーイベントログの Id と説明](#event-log-ids-and-descriptions-for-the-scanner)

詳細については、「 [ファイルを自動的に分類して保護するための Azure Information Protection スキャナーの展開](deploy-aip-scanner.md)」を参照してください。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>探索サイクルの実行とスキャナーのレポートの表示

[スキャナーを構成してインストール](deploy-aip-scanner-configure-install.md)した後、次の手順を使用して、コンテンツを最初に理解できるようにします。

コンテンツが変更されたときに、必要に応じてこれらの手順を再度実行します。

1. Azure portal の [ **Azure Information Protection-コンテンツスキャンジョブ** ] ウィンドウで、コンテンツスキャンジョブを選択し、[ **今すぐスキャン** ] オプションを選択します。

    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)

    または、PowerShell セッションで、次のコマンドを実行します。
    
    ```ps
    Start-AIPScan
    ```

1. スキャナーのサイクルが完了するまで待ちます。 スキャナーが、指定されたデータストア内のすべてのファイルを通じてクロールされると、スキャンが完了します。

    スキャナーの進行状況を監視するには、次のいずれかの操作を行います。

    - **スキャンジョブを最新の状態に更新します。**  [ **Azure Information Protection-コンテンツスキャンジョブ** ] ウィンドウで、[最新の情報に **更新**] を選択します。

        [ **最後のスキャン結果** ] 列の値と [最後の **スキャン (終了時刻)** ] 列の値が表示されるまで待ちます。

    - **PowerShell コマンドを使用します。** を実行し `Get-AIPScannerStatus` て、状態の変更を監視します。

    - **Windows イベントログを確認します。** **Azure Information Protection**という名前のローカルの Windows**アプリケーションとサービス**のイベントログを確認します。

        また、このログには、スキャナーのスキャンが完了したこと (結果の概要など) が表示されます。 情報イベント ID **911** を探します。 詳細については、「 [イベントログ id」と「スキャナーの説明](#event-log-ids-and-descriptions-for-the-scanner)」を参照してください。

1. スキャンが完了したら、 ** % *localappdata*% \ Microsoft\MSIP\Scanner\Reports**ディレクトリに格納されているレポートを確認します。

    - .txt の概要ファイルには、スキャンにかかった時間、スキャンされたファイルの数、情報の種類と一致したファイルの数が含まれています。

    - .csv ファイルには各ファイルに関する詳細情報が記載されています。 このフォルダーには、スキャンのサイクルごとに最大 60 のレポートが格納され、必要なディスク領域を最小限に抑えるために最新のもの以外のすべてのレポートが圧縮されます。

[初期構成](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal) では、探索する **情報の種類** を **ポリシーのみ**に設定するように指示されます。 この構成は、自動分類用に構成した条件を満たすファイルのみが詳細レポートに含まれることを意味します。

ラベルが適用されていない場合は、ラベルの構成に [推奨分類] ではなく [自動] が含まれていることを確認するか、[推奨される **ラベルを自動で扱う** (スキャナーバージョン 2.7. x. x 以降で使用可能)] をオンにします。

期待どおりの結果が得られない場合は、ラベルに指定した条件の再構成が必要になることがあります。 その場合は、必要に応じて条件を再構成し、結果が得られるまでこの手順を繰り返します。 次に、構成を自動的に更新し、必要に応じて保護を行います。

### <a name="viewing-updates-in-the-azure-portal"></a>Azure portal での更新プログラムの表示

スキャナーは、この情報を5分ごとに Azure Information Protection に送信し、Azure portal からほぼリアルタイムで結果を表示できるようにします。 詳細については、[Azure Information Protection のレポート作成](reports-aip.md)に関するページを参照してください。

Azure portal には、最後のスキャンに関する情報のみが表示されます。 前のスキャンの結果を確認する必要がある場合は、スキャナー コンピューターの %*localappdata*%\Microsoft\MSIP\Scanner\Reports フォルダーに格納されているレポートに戻ります。

### <a name="changing-log-levels-or-locations"></a>ログレベルまたは場所の変更

*Reportlevel*パラメーターを[設定](/powershell/module/azureinformationprotection/set-aipscannerconfiguration)して、ログ記録のレベルを変更します。

レポートフォルダーの場所または名前を変更することはできません。 レポートを別の場所に保存する場合は、フォルダーに対してディレクトリの接合を使用することを検討してください。

たとえば、 [Mklink](/windows-server/administration/windows-commands/mklink) コマンドを使用します。 `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`

初期構成とインストール後にこれらの手順を実行したことがある場合は、「 [分類と保護を適用するようにスキャナーを構成](deploy-aip-scanner-configure-install.md#configure-the-scanner-to-apply-classification-and-protection)する」に進んでください。

## <a name="stopping-a-scan"></a>スキャンを停止する

現在実行中のスキャンが完了する前に停止するには、次のいずれかの方法を使用します。

- **Azure portal。** [ **スキャンの停止**] を選択します。

    ![Azure Information Protection スキャナーのスキャンを停止する](./media/scanner-stop-scan.png)

- **PowerShell コマンドを実行します。** 次のコマンドを実行します。
    
    ```ps
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>ファイルの再スキャン

最初の [スキャンサイクル](#run-a-discovery-cycle-and-view-reports-for-the-scanner)では、スキャナーは、構成されたデータストア内のすべてのファイルを検査します。 後続のスキャンでは、新しいファイルまたは変更されたファイルのみが検査されます。

すべてのファイルを再検査することは、通常、レポートにすべてのファイルを含め、スキャナーを検出モードで実行する場合に便利です。

次のいずれかの方法を使用して、すべてのファイルの新しいスキャンを実行します。

- [完全な再スキャンを手動で実行する](#manually-run-a-full-rescan)
- [ポリシーを更新して完全な再スキャンをトリガーする](#trigger-a-full-rescan-by-refreshing-the-policy)

### <a name="manually-run-a-full-rescan"></a>完全な再スキャンを手動で実行する

必要に応じて、Azure portal の [ **Azure Information Protection コンテンツスキャンジョブ** ] ウィンドウで、スキャナーがすべてのファイルを再検査するように強制します。

一覧からコンテンツスキャンジョブを選択し、[ **すべてのファイルを再スキャン** ] オプションを選択します。

![Azure Information Protection スキャナーの再スキャンを開始する](./media/scanner-rescan-files.png)

フルスキャンが完了すると、スキャンの種類が自動的に [増分] に変更されます。これにより、以降のスキャンでは、新規または変更されたファイルのみが再度スキャンされるようになります。

### <a name="trigger-a-full-rescan-by-refreshing-the-policy"></a>ポリシーを更新して完全な再スキャンをトリガーする

新しい条件または変更された条件を持つ Azure Information Protection ポリシーをスキャナーがダウンロードするたびに、次のシナリオでもすべてのファイルが検査されます。

スキャナーでは、ポリシーが1時間ごとに自動的に更新されます。また、サービスが開始され、ポリシーが1時間以上経過していることが判明した場合もあります。

テスト中など、ポリシーをすぐに更新するには、 **%LocalAppData%\Microsoft\MSIP**ディレクトリから**Policy.msip**ポリシーファイルを手動で削除し、Azure Information Protection サービスを再起動します。

> [!NOTE]
> ラベルの保護設定を変更した場合は、Azure Information Protection サービスを再起動する前に、更新された保護設定を保存してから15分が経過するのを待ちます。
>

## <a name="troubleshooting-a-stopped-scan"></a>停止したスキャンのトラブルシューティング

スキャナーが途中で突然停止し、リポジトリ内の多数のファイルのスキャンが完了しない場合は、次の設定のいずれかを変更する必要があります。

- **動的ポートの数**。 ファイルをホストしているオペレーティングシステムの動的ポートの数を増やすことが必要になる場合があります。 SharePoint 用にサーバーのセキュリティが強化されている場合、スキャナーが許可されているネットワーク接続の数を超えて、そのために停止する原因の 1 つになる可能性があります。

    これがスキャナーの停止の原因であるかどうかを確認するには、次のエラーメッセージが、そのスキャナーの** % *localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog**ファイルに記録されているかどうかを確認してください。

    **リモートサーバー---に接続できませんでした。ソケットの > 例外: 各ソケットアドレス (プロトコル/ネットワークアドレス/ポート) の使用は、通常、許可されている IP: ポートの1つのみです**

    > [!NOTE]
    > 複数のログがある場合、このファイルは圧縮されます。

    現在のポート範囲を表示し、範囲を拡大する方法について詳しくは、「[ネットワーク パフォーマンスを向上させるために変更可能な設定](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)」をご覧ください。

- **リストビューのしきい値。** 大規模な SharePoint ファームの場合は、リストビューのしきい値を大きくする必要があります。 既定では、リストビューのしきい値は5000に設定されています。

    詳細については、「 [SharePoint での大規模なリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。

## <a name="troubleshooting-using-the-scanner-diagnostic-tool"></a>スキャナー診断ツールを使用したトラブルシューティング

Azure Information Scanner で問題が発生している場合は、次の PowerShell コマンドを使用してデプロイが正常であるかどうかを確認します。

```ps
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
> この **ツールで** は、完全な前提条件の確認は実行されません。 スキャナーで問題が発生している場合は、システムが [スキャナーの要件](deploy-aip-scanner-prereqs.md)を満たしていることと、 [スキャナーの構成とインストール](deploy-aip-scanner-configure-install.md) が完了していることを確認してください。
>

## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>スキャナーのイベント ログ ID と説明

次の AIP スキャナーログイベントは、 **Azure Information Protection**という名前の Windows**アプリケーションおよびサービス**イベントログに格納されます。

|イベント ID  |アクティビティ  |説明  |
|---------|---------|---------|
|**910**     | スキャナーサイクルを開始しました        | スキャナーサービスが開始され、指定したデータリポジトリ内のファイルのスキャンが開始されたときに記録されます。        |
|**911**     |   スキャナーのサイクルが終了しました      | スキャナーが手動スキャンを完了したとき、またはスキャナーが連続スケジュールのサイクルを完了したときに記録されます。       |
| | | |

> [!TIP]
> スキャナーが継続的にではなく手動で実行するように構成されている場合、ファイルを再度スキャンするには、 **スケジュール** を [ **手動** ] または [ **常** にコンテンツスキャンジョブ] に設定してから、サービスを再起動します。 詳細については、「ファイルの再 [スキャン](#rescanning-files)」を参照してください。
>

## <a name="next-steps"></a>次のステップ

- Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

- [Windows Server FCI と Azure Information Protection スキャナーの違いは何ですか](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)。

- また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 これに関する詳細および PowerShell を使用するその他のシナリオについては、「[Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md)」をご覧ください。
