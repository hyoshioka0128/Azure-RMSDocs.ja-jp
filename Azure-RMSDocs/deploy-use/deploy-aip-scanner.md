---
title: "Azure Information Protection スキャナーのデプロイ"
description: "Azure Information Protection スキャナーをインストール、構成、実行して、データ ストア上のファイルを検出、分類、および保護する手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/16/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: bfe4074710bd93c92e383056f587994ec805b6c2
ms.sourcegitcommit: 4234de57201411cd9b292492fddc683df0e6b4cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2018
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する

>*適用対象: Azure Information Protection、Windows Server 2016、Windows Server 2012 R2*

この情報を使用して、Azure Information Protection スキャナーについて説明し、正常にインストール、構成、および実行する方法について説明します。 

このスキャナーは、Windows Server でサービスとして実行され、次のデータ ストア上のファイルを検出、分類、および保護することができます。

- スキャナーを実行する Windows Server コンピューター上のローカル フォルダー。

- Common Internet File System (CIFS) プロトコルを使用するネットワーク共有の UNC パス。

- SharePoint Server 2016 および SharePoint Server 2013 のサイトとライブラリ。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの概要

自動分類を適用するラベルに [Azure Information Protection ポリシー](configure-policy.md)を構成している場合、このスキャナーで検出されたファイルにラベルを付けることができます。 ラベルは分類を適用し、必要に応じて、保護を適用または保護を解除します。

![Azure Information Protection スキャナーの概要](../media/infoprotect-scanner.png)

スキャナーは、コンピューターにインストールされている iFilter を使用して Windows でインデックス化できるすべてのファイルを検証することができます。 そして、ファイルでラベル付けが必要かどうかを判断するため、スキャナーで Office 365 に組み込まれたデータ損失防止 (DLP) の機密情報の種類とパターン検出、または Office 365 の正規表現パターンが使われます。 スキャナーは Azure Information Protection クライアントを使用するため、同じ[ファイルの種類](../rms-client/client-admin-guide-file-types.md)を分類および保護できます。

スキャナーを実行できるのは検索モードでのみです。この場合、レポートを使用して、ファイルがラベル付けされた場合に何が発生するかをチェックします。 またはスキャナーを実行して、自動的にラベルを適用できます。

スキャナーは検出せず、リアルタイムでラベル付けしないことに注意してください。 スキャナーは指定したデータ ストア上のファイルを体系的にクロールします。この実行サイクルは、1 回限りまたは繰り返しに設定することができます。

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの前提条件
Azure Information Protection スキャナーをインストールする前に、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|スキャナー サービスを実行する Windows Server コンピューター:<br /><br />- 4 個のプロセッサ<br /><br />- 4 GB の RAM|Windows Server 2016 または Windows Server 2012 R2。 <br /><br />注: 非運用環境でテストまたは評価を行う場合、[Azure Information Protection クライアントでサポートされている](../get-started/requirements.md#client-devices) Windows クライアント オペレーティング システムを使用できます。<br /><br />このコンピューターは、スキャンするデータ ストアへの高速で信頼性の高いネットワーク接続がある物理コンピューターまたは仮想コンピューターにすることができます。 <br /><br />Azure Information Protection に必要な[インターネット接続](../get-started/requirements.md#firewalls-and-network-infrastructure)がこのコンピューターにあることを確認します。 またはサーバーを[切断されたコンピューター](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)として構成する必要があります。 |
|スキャナーの構成を格納する SQL Server:<br /><br />- ローカルまたはリモート インスタンス<br /><br />- スキャナーをインストールする sysadmin ロール|次のエディションでは、SQL Server 2012 が最小バージョンとなります。<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />スキャナーをインストールするアカウントには、マスター データベースへの書き込みアクセス許可が必要です (db_datawriter ロールのメンバーである必要があります)。 インストール プロセスでは、スキャナーを実行しているサービス アカウントに db-owner ロールを付与します。 代わりに、スキャナーをインストールする前に AzInfoProtectionScanner データベースを手動で作成し、スキャナー サービス アカウントに db-owner ロールを割り当てることもできます。|
|スキャナー サービスを実行するサービス アカウント|このアカウントは、Azure AD と同期された Active Directory アカウントである必要があり、次の追加要件があります。<br /><br />- **ローカル ログオン**権限。 この権限は、スキャナーのインストールと構成に必要ですが、操作には必要ありません。 この権限をサービス アカウントに付与する必要がありますが、スキャナーがファイルを検出、分類、保護できることを確認したら、この権限を削除することができます。 <br /><br />注: 社内の方針によりこの権限をサービス アカウントに許可しないが、**バッチ ジョブとしてログオン**権限を与えることができる場合、追加の構成でこの要件を満たすことができます。 方法については、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」を参照してください。<br /><br />- **サービスとしてログオン**権限。 この権限は、スキャナーのインストール中にサービス アカウントに自動的に付与され、スキャナーのインストール、構成、操作に必要です。 <br /><br />- データ リポジトリへのアクセス許可: ファイルをスキャンして、Azure Information Protection ポリシーの条件を満たすファイルに分類と保護を適用するには、**読み取り**と**書き込み**のアクセス許可を付与する必要があります。 スキャナーを検索モードでのみ実行するには、**読み取り**アクセス許可で十分です。<br /><br />- 再保護または保護を解除するラベル: スキャナーが保護されたファイルに常にアクセスできるようにするには、このアカウントを Azure Rights Management サービスの[スーパー ユーザー](configure-super-users.md)にして、スーパー ユーザー機能が有効になっていることを確認します。 保護を適用するためのアカウント要件の詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](../plan-design/prepare.md)」を参照してください。|
|Azure Information Protection スキャナーが Windows Server コンピューターにインストールされている|現在、Azure Information Protection スキャナーは、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)の **AzInfoProtectionScanner.exe** という名前の個別のダウンロードです。 スキャナーの後続のリリースは、Azure Information Protection クライアントに含められます。|
|自動分類と、必要に応じて保護を適用する構成済みのラベル|条件を構成する方法の詳細については、「[Azure Information Protection 用の自動および推奨分類の条件を構成する方法](configure-policy-classification.md)」を参照してください。<br /><br />ファイルに保護を適用するラベルを構成する方法の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」を参照してください。<br /><br />これらのラベルは、グローバル ポリシーまたは 1 つ以上の[スコープ付きポリシー](configure-policy-scope.md)にあります。|
|1 つ以上のデータ リポジトリ内のすべてのファイルにラベルが必要な場合<br /><br />- ポリシー設定として構成された既定のラベル|既定のラベル設定を構成する方法の詳細については、「[Azure Information Protection のポリシー設定を構成する方法](configure-policy-settings.md)」を参照してください。<br /><br />この既定のラベル設定は、グローバル ポリシーまたはスキャナーのスコープ付きポリシー内にある必要があります。 ただし、この既定のラベル設定は、データ リポジトリ レベルで構成する別の既定のラベルによってオーバーライドされることがあります。|

## <a name="install-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーのインストール

1. スキャナーを実行するために作成したサービス アカウントを使用して、スキャナーを実行する Windows Server コンピューターにサインインします。

2. **[管理者として実行]** オプションを使用して Windows PowerShell セッションを開きます。

3. Azure Information Protection スキャナー用のデータベースを作成する SQL Server インスタンスを指定して、[Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) コマンドレットを実行します。 
    
    ```
    Install-AIPScanner -SqlServerInstance <database name>
    ```
    
    例:
    
    既定のインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    名前付きインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    SQL Server Express の場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`
    
    [詳細な例](/powershell/module/azureinformationprotection/install-aipscanner#examples)が必要な場合は、このコマンドレットのオンライン ヘルプを使用します。
    
    求められたら、スキャナー サービス アカウントの資格情報 (\<ドメイン\ユーザー名>) とパスワードを指定します。

4. **[管理ツール]** > **[サービス]** を使用して、サービスがインストールされたことを確認します。 
    
    インストールされているサービスの名前は **Azure Information Protection スキャナー**で、作成したスキャナー サービス アカウントを使用して実行するように構成されます。

スキャナーをインストールしたら、スキャナーを無人で実行できるように、スキャナー サービス アカウントを認証するための Azure AD トークンを取得する必要があります。 

## <a name="get-an-azure-ad-token-for-the-scanner-service-account-to-authenticate-to-the-azure-information-protection-service"></a>Azure Information Protection サービスを認証するスキャナー サービス アカウントの Azure AD トークンを取得する

1. 同じ Windows Server コンピューター、またはデスクトップから、Azure Portal にサインインして、認証のためのアクセス トークンを指定するために必要な 2 つの Azure AD アプリケーションを作成します。 初めて対話型サインインをした後は、このトークンにより非対話的にスキャナーを実行できます。
    
    これらのアプリケーションを作成するには、管理者ガイドの「[非対話形式でファイルに Azure Information Protection のラベル付けをする方法](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」の指示に従います。

2. スキャナー サービス アカウントでサインインしたまま、Windows Server コンピューターから、前の手順からコピーした値を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行します。
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application>  -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application >
    ```

3. 求められたら、Azure AD のサービス アカウントの資格情報のパスワードを指定し、**[同意する]** をクリックします。

これでスキャナーに Azure AD を認証するためのトークンが取得されました。トークンの有効期間は、Azure AD での **Web アプリ/API** の構成に従って、1 年間、2 年間、または無期限のいずれかになります。 トークンが期限切れになったら、手順 1 から 3 を繰り返す必要があります。

これでスキャンするデータ ストアを指定する準備ができました。 

## <a name="specify-data-stores-for-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーのデータ ストアを指定する

[Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository) コマンドレットを使用して、Azure Information Protection スキャナーでスキャンするデータ ストアを指定します。 SharePoint サイトとライブラリのローカル フォルダー、UNC パス、および SharePoint Server URL を指定できます。 

サポートされている SharePoint のバージョン: SharePoint Server 2016 と SharePoint Server 2013。

1. 同じ Windows Server コンピューターから、PowerShell セッションで次のコマンドを実行して、最初のデータ ストアを追加します。
    
        Add-AIPScannerRepository -Path <path>
    
    例: `Add-AIPScannerRepository -Path \\NAS\Documents`
    
    その他の例については、このコマンドレットの[オンライン ヘルプ](/powershell/module/azureinformationprotection/Add-AIPScannerRepository#examples)を参照してください。

2. スキャンするすべてのデータ ストアに対し、このコマンドを繰り返します。 追加したデータ ストアを削除する必要がある場合は、[Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository) コマンドレットを使用します。

3. [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository) コマンドレットを実行して、すべてのデータ ストアが正しく指定されていることを確認します。
    
        Get-AIPScannerRepository

スキャナーの既定の構成を使用して、最初のスキャンを検索モードで実行できます。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-azure-information-protection-scanner"></a>検索サイクルを実行し、Azure Information Protection スキャナーのレポートを表示する

1. **[管理ツール]** > **[サービス]** を使用して、**Azure Information Protection スキャナー** サービスを開始します。

2. スキャナーのサイクルが完了するまで待ちます。 スキャナーが指定したデータ ストア内のすべてのファイルをクロールすると、サービスが停止します。 サービスが停止したときに、ローカルの Windows **アプリケーションとサービス**のイベント ログ、**Azure Information Protection** を使用して確認できます。 情報イベント ID **911** を探します。

3. %*localappdata*%\Microsoft\MSIP\Scanner\Reports に格納され、.csv ファイル形式を持つレポートを確認します。 スキャナーの既定の構成では、自動分類の条件に一致するファイルのみがこれらのレポートに含まれます。
    
    結果が期待どおりにならない場合は、Azure Information Protection ポリシーに指定した条件を微調整する必要がある場合があります。 その場合は、構成を変更して分類、および必要に応じて保護を適用する準備ができるまで、手順 1 から 3 を繰り返します。 これらの手順を繰り返すたびに、最初に Windows Server コンピューターで次の PowerShell コマンドを実行します。
    
        Set-AIPScannerConfiguration -Schedule OneTime

スキャナーが検出したファイルに自動的にラベル付けする準備ができたら、次の手順に進みます。 

## <a name="configure-the-azure-information-protection-scanner-to-apply-classification-and-protection-to-discovered-files"></a>Azure Information Protection スキャナーを構成して、検出されたファイルに分類および保護を適用する

既定の設定では、スキャナーは、レポートのみモードで 1 回だけ実行されます。 これらの設定を変更するには、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットを実行します。

1. Windows Server コンピューターの PowerShell セッションで、次のコマンドを実行します。
    
        Set-AIPScannerConfiguration -ScanMode Enforce -Schedule Continuous
    
    変更する可能性があるその他の構成があります。 たとえば、ファイル属性を変更するかどうか、およびレポートに記録する項目などがあります。 さらに、Azure Information Protection ポリシーに分類レベルを下げる、または保護を解除する理由メッセージを必要とする設定が含まれている場合、このコマンドレットを使用してそのメッセージを指定します。 各構成設定に関する詳細については、[オンライン ヘルプ](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#parameters)を参照してください。 

2. **[管理ツール]** > **[サービス]** を使用して、**Azure Information Protection スキャナー** サービスを再開します。

3. 以前と同じく、イベント ログとレポートを監視して、ラベル付けされたファイル、適用された分類、保護が適用されたかどうかを確認します。

継続的に実行するスケジュールを構成したため、スキャナーはすべてのファイルを完了すると、新しいファイルと変更されたファイルが検出されるように、新しいサイクルを開始します。


## <a name="how-files-are-scanned-by-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーでファイルをスキャンする方法

このスキャナーは、実行可能ファイルやシステム ファイルなど、[分類と保護から除外されている](../rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-client)ファイルを自動的にスキップします。

その後、Windows iFilter を利用し、次の種類のファイルをスキャンします。 このような種類のファイルでは、ラベルに指定した条件によって文書にラベルが付けられます。

|アプリケーションの種類|ファイルの種類|
|--------------------------------|-------------------------------------|
|Word|.docx; .docm; .dotm; .dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|Project|.mpp; .mpt|
|PDF|.pdf|
|テキスト|.txt; .xml; .csv|


最後に、残りの種類のファイルについて、スキャナーは Azure Information Protection ポリシーの既定のラベルを適用します。

|アプリケーションの種類|ファイルの種類|
|--------------------------------|-------------------------------------|
|Project|.mpp; .mpt|
|発行者|.pub|
|Visio|.vsd; .vdw; .vst; .vss; .vsdx; .vsdm; .vssx; .vssm; .vstx; .vstm|
|XPS|.xps; .oxps; .dwfx|
|Solidworks|.sldprt; .slddrw; .sldasm|
|Jpeg |.jpg; .jpeg; .jpe; .jif; .jfif; .jfi|
|Png |.png|
|Gif|.gif|
|ビットマップ|.bmp; .giff|
|Tiff|.tif; .tiff|
|Photoshop|.psdv|
|DigitalNegative|.dng|
|Pfile|.pfile|

ラベルで文書に汎用的保護を適用するとき、ファイル名の拡張子が .pfile に変わります。 また、権限が与えられたユーザーが開き、そのネイティブ形式で保存されるまで、ファイルは読み取り専用になります。 テキスト ファイルと画像ファイルでは、そのファイル名の拡張子を変更し、読み取り専用にすることもできます。 この動作を望まない場合、特定の種類のファイルが保護されることを回避できます。 たとえば、PDF ファイルが保護付き PDF (.ppdf) ファイルにならないようにしたり、.txt ファイルが保護付きテキスト (.ptxt) ファイルにならないようにできます。

ファイルの種類によって異なる保護レベルと保護動作の制御方法については、管理者ガイドの「[保護がサポートされているファイルの種類](../rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)」を参照してください。


## <a name="when-files-are-rescanned-by-the-azure-information-protection-scanner"></a>ファイルが Azure Information Protection スキャナーで再スキャンされる場合

最初のスキャン サイクルではスキャナーは構成されているデータ ストアのすべてのファイルを検査し、後続のスキャンでは、新しいファイルまたは変更されたファイルのみが検査されます。 

[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) の実行時に `-Type` パラメーターを **[Full]** に設定すると、スキャナーにすべてのファイルの検査を強制することができます。 この構成は、レポートにすべてのファイルを含める必要がある場合に役立ち、通常は検索モードでスキャナーが実行されるときに使用されます。 フル スキャンが完了すると、後続のスキャンで新しいファイルまたは変更されたファイルのみがスキャンされるように、スキャンの種類が自動的に [増分] に変更されます。

さらに、新しいまたは変更された条件を含む Azure Information Protection ポリシーをスキャナーがダウンロードした場合も、すべてのファイルが検査されます。 スキャナーは、1 時間ごと、およびサービスの開始時にポリシーを更新します。

## <a name="optimizing-the-performance-of-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーのパフォーマンスの最適化

スキャナーのパフォーマンスを最大化するには

- **スキャナー コンピューターとスキャンされたデータ ストア間のネットワーク接続を高速かつ信頼性の高い接続にする**
    
    たとえば、同じ LAN 内か、スキャンされたデータ ストアと同じネットワーク セグメント内 (推奨) にスキャナー コンピューターを配置します。
    
    ネットワーク接続の品質は、スキャナーがスキャナー サービスを実行しているコンピューターにファイルのコンテンツを転送してファイルを検査するため、スキャナーのパフォーマンスに影響します。 このデータを移動する必要があるネットワークのホップ数を減らす (削除する) と、ネットワークの負荷も軽減されます。 

- **スキャナー コンピューターに利用可能なプロセッサ リソースがあることを確認する**
    
    ファイル コンテンツが構成した条件に一致するかの検査、およびファイルの暗号化と複合化は、プロセッサ負荷の高いアクションです。 プロセッサ リソースの不足がスキャナー パフォーマンスを低下させるかどうかを識別するには、指定したデータ ストアの標準のスキャン サイクルを監視します。
    
- **スキャナー サービスを実行しているコンピューター上のローカル フォルダーをスキャンしない**
    
    Windows Server 上にスキャンするフォルダーがある場合は、別のコンピューター上にスキャナーをインストールし、これらのフォルダーをネットワーク共有として構成してスキャンします。 ファイルをホストする機能とファイルをスキャンする機能の 2 つの機能を分離させると、これらのサービス用のリソースの計算が相互に競合していないことを意味します。

スキャナーのパフォーマンスに影響するその他の要因

- スキャンするファイルを含むデータ ストアの現在の負荷と応答時間

- スキャナーが検索モードまたは強制モードのどちらで実行されているか
    
    通常、検索モードでは、強制モードよりもスキャン速度が速くなります。これは、発見には単一ファイルの読み取りアクションが必要なのに対して、強制モードでは読み取り/書き込みアクションが必要なためです。

- Azure Information Protection の条件を変更する
    
    スキャナーがすべてのファイルを検査する必要があるときの最初のスキャン サイクルでは、既定では、新規および変更されたファイルのみを検査する後続のスキャン サイクルよりも明らかに長く時間がかかります。 ただし、Azure Information Protection ポリシーの条件を変更した場合、[上記のセクション](#when-files-are-rescanned-by-the-azure-information-protection-scanner)に示されているように、すべてのファイルがもう一度スキャンされます。

- 選択したログ レベル
    
    スキャナー レポートに対して **[デバッグ]**、**[情報]**、**[エラー]**、**[オフ]** から選択できます。 **[オフ]** を選択すると、最適なパフォーマンスになります。**[デバッグ]** は大幅にスキャナーのスピードを低下させるので、トラブルシューティング時にのみ使用してください。 詳細については、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットの *ReportLevel* パラメーターを参照してください。

- ファイル自体
    
    - Office ファイルは PDF ファイルよりもすばやくスキャンされます。
    
    - 保護されていないファイルは、保護されたファイルよりもすばやくスキャンされます。
    
    - 大きいファイルは明らかに小さいファイルよりも時間がかかります。

## <a name="list-of-cmdlets-for-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーのコマンドレットのリスト 

スキャナーの他のコマンドレットを使用して、サービス アカウントとスキャナーのデータベースを変更したり、スキャナーの現在の設定を取得したり、スキャナー サービスをアンインストールしたりすることができます。 スキャナーは、次のコマンドレットを使用します。

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)


## <a name="event-log-ids-and-descriptions"></a>イベント ログ ID と説明

次のセクションを使用して、スキャナーの可能性のあるイベント ID と説明を特定できます。 これらのイベントは、Windows の**アプリケーションとサービス**のイベント ログ、**Azure Information Protection** でスキャナー サービスを実行しているサーバーにログオンします。

-----

情報 **910**

**スキャナーのサイクルが開始しました。**

スキャナー サービスが開始され、指定したデータ リポジトリ内のファイルのスキャンが開始されたときに、このイベントがログに記録されます。

----

情報 **911**

**スキャナーのサイクルが完了しました。**

サーバーを起動してからスキャナーが 1 回限りのスキャンを完了するか、スキャナーが連続的なスケジュールのサイクルを完了したときに、このイベントがログに記録されます。

----

情報 **913**

**スキャナーが [Never\(常に不可\)] に設定されているため、スキャナーが停止しました。**

スキャナーが継続的ではなく 1 回限りに構成されていて、コンピューターが起動されてから Azure Information Protection スキャナー サービスが手動で再起動されている場合に、このイベントがログに記録されます。  

ファイルをもう一度スキャンするには、**[OneTime\(1 回限り\)]** または **[Continuous\(連続\)]** にスケジュールを設定してから、サービスを手動で再起動する必要があります。 スケジュールを変更するには、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットと **[スケジュール]** パラメーターを使用します。

----

エラー **912**

**不明なエラーが発生しました。**

詳細レポートには、より詳細な情報がログ記録されます。このレポートは、%localappdata%\Microsoft\MSIP\Scanner\Reports\DetailedReport_YYYY_MM_DD_HH_MM.csv に格納されます。

このイベントが継続的にログに記録される場合は、[Microsoft サポート](../get-started/information-support.md#to-contact-microsoft-support)にお問い合わせください。 

----

エラー **914**

**無効な構成によりサービスが自動的に停止しました: ポリシー ファイルが見つからないか破損しています。**

Azure Information Protection クライアントに、スキャナーを実行するための有効なポリシー ファイルがない場合に、このイベントがログに記録されます。

Azure Information Protection ポリシーは %localappdata%\Microsoft\MSIP に格納され、自動分類を適用する条件があるラベルを使用して構成する必要があります。 または、既定のラベルにポリシーを構成する必要があります。

ファイアウォールが、インターネットへの必要な接続をブロックしていないことを確認します。 詳細については、Azure Information Protection の[ファイアウォールとネットワーク インフラストラクチャ](../get-started/requirements.md#firewalls-and-network-infrastructure)の要件を参照してください。 インターネット接続が不可能な場合は、[切断されたコンピューター](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)のサポートの指示に従います。


## <a name="next-steps"></a>次の手順

[Windows Server FCI と Azure Information Protection スキャナーの違い](../get-started/faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)についてご説明します。

また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 これに関する詳細および PowerShell を使用するその他のシナリオについては、「[Azure Information Protection クライアントでの PowerShell の使用](../rms-client/client-admin-guide-powershell.md)」をご覧ください。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
