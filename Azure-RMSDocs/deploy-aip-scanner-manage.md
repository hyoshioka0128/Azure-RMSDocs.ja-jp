---
title: Azure Information Protection 統合されたラベル付けスキャナーの実行 (AIP)
description: Azure Information Protection 統合されたラベル付けスキャナーを実行して、データストア上のファイルを検出、分類、および保護する方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/25/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9815969701e1dee352d2b2ad5d2874de6c8df204
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809577"
---
# <a name="running-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの実行

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***関連**: [AIP 統合ラベルクライアントのみ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 クラシックスキャナーについては、「 [クラシックスキャナー Azure Information Protection を実行](deploy-aip-scanner-manage-classic.md)する」を参照してください。

[システム要件](deploy-aip-scanner-prereqs.md)を確認し、スキャナーを[構成してインストールし](deploy-aip-scanner-configure-install.md)たら、[検出スキャンを実行](#run-a-discovery-cycle-and-view-reports-for-the-scanner)して作業を開始します。

次に説明する他の手順に従って、スキャンを管理します。

- [スキャンを停止する](#stopping-a-scan)
- [ファイルの再スキャン](#rescanning-files)

詳細については、「 [ファイルを自動的に分類して保護するための Azure Information Protection スキャナーの展開](deploy-aip-scanner.md)」を参照してください。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>探索サイクルの実行とスキャナーのレポートの表示

[スキャナーを構成してインストール](deploy-aip-scanner-configure-install.md)した後、次の手順を使用して、コンテンツを最初に理解できるようにします。

コンテンツが変更されたときに、必要に応じてこれらの手順を再度実行します。

1. Azure portal の [ **Azure Information Protection-コンテンツスキャンジョブ** ] ウィンドウで、コンテンツスキャンジョブを選択し、[ **今すぐスキャン** ] オプションを選択します。

    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)

    または、PowerShell セッションで、次のコマンドを実行します。

    ```PowerShell
    Start-AIPScan
    ```

1. スキャナーのサイクルが完了するまで待ちます。 スキャナーが、指定されたデータストア内のすべてのファイルを通じてクロールされると、スキャンが完了します。

    スキャナーの進行状況を監視するには、次のいずれかの操作を行います。

    - **スキャンジョブを最新の状態に更新します。**  [ **Azure Information Protection-コンテンツスキャンジョブ** ] ウィンドウで、[最新の情報に **更新**] を選択します。

        [ **最後のスキャン結果** ] 列の値と [最後の **スキャン (終了時刻)** ] 列の値が表示されるまで待ちます。

    - **PowerShell コマンドを使用します。** を実行し `Get-AIPScannerStatus` て、状態の変更を監視します。

1. スキャンが完了したら、 **% *localappdata*% \ Microsoft\MSIP\Scanner\Reports** ディレクトリに格納されているレポートを確認します。

    - .txt の概要ファイルには、スキャンにかかった時間、スキャンされたファイルの数、情報の種類と一致したファイルの数が含まれています。

    - .csv ファイルには各ファイルに関する詳細情報が記載されています。 このフォルダーには、スキャンのサイクルごとに最大 60 のレポートが格納され、必要なディスク領域を最小限に抑えるために最新のもの以外のすべてのレポートが圧縮されます。

[初期構成](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal) では、探索する **情報の種類** を **ポリシーのみ** に設定するように指示されます。 この構成は、自動分類用に構成した条件を満たすファイルのみが詳細レポートに含まれることを意味します。

ラベルが適用されていない場合は、ラベルの構成に [推奨分類] ではなく [自動] が含まれていることを確認するか、[推奨される **ラベルを自動で扱う** (スキャナーバージョン 2.7. x. x 以降で使用可能)] をオンにします。

期待どおりの結果が得られない場合は、ラベルに指定した条件の再構成が必要になることがあります。 その場合は、必要に応じて条件を再構成し、結果が得られるまでこの手順を繰り返します。 次に、構成を自動的に更新し、必要に応じて保護を行います。

### <a name="viewing-updates-in-the-azure-portal"></a>Azure portal での更新プログラムの表示

スキャナーは、この情報を5分ごとに Azure Information Protection に送信し、Azure portal からほぼリアルタイムで結果を表示できるようにします。 詳細については、[Azure Information Protection のレポート作成](reports-aip.md)に関するページを参照してください。

Azure portal には、最後のスキャンに関する情報のみが表示されます。 前のスキャンの結果を確認する必要がある場合は、スキャナー コンピューターの %*localappdata*%\Microsoft\MSIP\Scanner\Reports フォルダーに格納されているレポートに戻ります。

### <a name="changing-log-levels-or-locations"></a>ログレベルまたは場所の変更

*Reportlevel* パラメーターを [設定](/powershell/module/azureinformationprotection/set-aipscannerconfiguration)して、ログ記録のレベルを変更します。

レポートフォルダーの場所または名前を変更することはできません。 レポートを別の場所に保存する場合は、フォルダーに対してディレクトリの接合を使用することを検討してください。

たとえば、 [Mklink](/windows-server/administration/windows-commands/mklink) コマンドを使用します。 `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`

初期構成とインストール後にこれらの手順を実行したことがある場合は、「 [分類と保護を適用するようにスキャナーを構成](deploy-aip-scanner-configure-install.md#configure-the-scanner-to-apply-classification-and-protection)する」に進んでください。

## <a name="stopping-a-scan"></a>スキャンを停止する

現在実行中のスキャンが完了する前に停止するには、次のいずれかの方法を使用します。

- **Azure portal。** [ **スキャンの停止**] を選択します。

    ![Azure Information Protection スキャナーのスキャンを停止する](./media/scanner-stop-scan.png)

- **PowerShell コマンドを実行します。** 次のコマンドを実行します。

    ```PowerShell
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>ファイルの再スキャン

最初の [スキャンサイクル](#run-a-discovery-cycle-and-view-reports-for-the-scanner)では、スキャナーは、構成されたデータストア内のすべてのファイルを検査します。 後続のスキャンでは、新しいファイルまたは変更されたファイルのみが検査されます。

すべてのファイルを再検査することは、通常、すべてのファイルをレポートに含める場合、すべてのファイルに適用する変更がある場合、およびスキャナーを検出モードで実行する場合に便利です。

**完全な再スキャンを手動で実行するに** は:

1. Azure portal の [ **Azure Information Protection-コンテンツスキャンジョブ** ] ウィンドウに移動します。

1. 一覧からコンテンツスキャンジョブを選択し、[ **すべてのファイルを再スキャン** ] オプションを選択します。

    ![Azure Information Protection スキャナーの再スキャンを開始する](./media/scanner-rescan-files.png)

フルスキャンが完了すると、スキャンの種類が自動的に [増分] に変更されます。これにより、以降のスキャンでは、新規または変更されたファイルのみが再度スキャンされるようになります。

> [!TIP]
> AIP [コンテンツスキャンジョブ](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)を変更した場合、Azure portal によって、完全な再スキャンをスキップするように求められます。 再スキャンが確実に行われるようにするには、表示されるプロンプトで [ **いいえ** ] を選択してください。
> 
### <a name="trigger-a-full-rescan-by-modifying-your-settings-versions-271010-and-lower"></a>設定を変更して完全な再スキャンをトリガーします (バージョン2.7.101.0 およびそれ以降)

スキャナーバージョン [2.7.101.0](rms-client/unifiedlabelingclient-version-release-history.md#version-271010) およびそれ以降では、スキャナーが自動および推奨のラベル設定の新しい設定または変更された設定を検出するたびに、すべてのファイルがスキャンされます。 スキャナーは、4時間ごとにポリシーを自動的に更新します。

テスト中など、ポリシーをすぐに更新するには、 **%LocalAppData%\Microsoft\MSIP\mip \<processname>** ディレクトリの内容を手動で削除し、Azure Information Protection サービスを再起動します。

ラベルの保護設定を変更した場合は、Azure Information Protection サービスを再起動する前に、更新された保護設定を保存してから15分が経過するのを待ちます。

> [!IMPORTANT]
> バージョン [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 以降にアップグレードした場合、AIP によって更新された設定の完全な再スキャンがスキップされ、パフォーマンスが一貫して保たれます。 アップグレードした場合は、必要に応じて [手動で完全な再スキャンを実行](#rescanning-files) してください。 
>
> たとえば、 **ポリシー実施** 設定を [ **強制] から** **[強制**] に変更した場合は、フルスキャンを実行して、コンテンツ全体にラベルを適用してください。
> 

## <a name="next-steps"></a>次のステップ

- Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

- また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 PowerShell を使用するその他のシナリオの詳細については、「 [Azure Information Protection の統合ラベル付けクライアントでの powershell の使用](./rms-client/clientv2-admin-guide-powershell.md)」を参照してください。