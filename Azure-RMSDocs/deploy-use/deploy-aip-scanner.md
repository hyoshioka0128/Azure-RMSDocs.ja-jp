---
title: Azure Information Protection スキャナーのデプロイ
description: Azure Information Protection スキャナーをインストール、構成、実行して、データ ストア上のファイルを検出、分類、および保護する手順です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/26/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 862a89dee32c5715d4380eb9e553e06ace3fa5c5
ms.sourcegitcommit: 1f5a5cb650be2b4c302ad4b7a0b109246da3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2018
ms.locfileid: "39295476"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012 R2*

この情報を使用して、Azure Information Protection スキャナーについて説明し、正常にインストール、構成、および実行する方法について説明します。 

このスキャナーは、Windows Server でサービスとして実行され、次のデータ ストア上のファイルを検出、分類、および保護することができます。

- スキャナーを実行する Windows Server コンピューター上のローカル フォルダー。

- サーバー メッセージ ブロック (SMB) プロトコルを使用するネットワーク共有の UNC パス。

- SharePoint Server 2016 および SharePoint Server 2013 のサイトとライブラリ。

クラウド リポジトリのファイルをスキャンおよびラベル付けするには、[Cloud App Security](https://docs.microsoft.com/cloud-app-security/) を使用します。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの概要

自動分類を適用するラベルに [Azure Information Protection ポリシー](configure-policy.md)を構成している場合、このスキャナーで検出されたファイルにラベルを付けることができます。 ラベルは分類を適用し、必要に応じて、保護を適用または保護を解除します。

![Azure Information Protection スキャナーのアーキテクチャの概要](../media/infoprotect-scanner.png)

スキャナーは、コンピューターにインストールされている iFilter を使用して Windows でインデックス化できるすべてのファイルを検証することができます。 そして、ファイルでラベル付けが必要かどうかを判断するため、スキャナーで Office 365 に組み込まれたデータ損失防止 (DLP) の機密情報の種類とパターン検出、または Office 365 の正規表現パターンが使われます。 スキャナーは Azure Information Protection クライアントを使用するため、同じ[ファイルの種類](../rms-client/client-admin-guide-file-types.md)を分類および保護できます。

スキャナーを実行できるのは検索モードでのみです。この場合、レポートを使用して、ファイルがラベル付けされた場合に何が発生するかをチェックします。 またはスキャナーを実行して、自動的にラベルを適用できます。 機密情報の種類を含んだファイルを検出するためにスキャナーを実行することもできます (自動分類を適用する条件用にラベルを構成する必要はありません)。

スキャナーは検出せず、リアルタイムでラベル付けしないことに注意してください。 スキャナーは指定したデータ ストア上のファイルを体系的にクロールします。この実行サイクルは、1 回限りまたは繰り返しに設定することができます。

スキャンするファイルの種類を指定したり、スキャン対象から除外することができます。 スキャナーによって検査されるファイルを制限するには、[Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes) を使用してファイルの種類のリストを定義します。


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの前提条件
Azure Information Protection スキャナーをインストールする前に、次の要件を満たしていることを確認してください。

|要件|説明|
|---------------|--------------------|
|スキャナー サービスを実行する Windows Server コンピューター:<br /><br />- 4 コア プロセッサ<br /><br />- 4 GB の RAM<br /><br />- 一時ファイルのための空き容量 10 GB (平均)|Windows Server 2016 または Windows Server 2012 R2。 <br /><br />注: 非運用環境でテストまたは評価を行う場合、[Azure Information Protection クライアントでサポートされている](../get-started/requirements.md#client-devices) Windows クライアント オペレーティング システムを使用できます。<br /><br />このコンピューターは、スキャンするデータ ストアへの高速で信頼性の高いネットワーク接続がある物理コンピューターまたは仮想コンピューターにすることができます。<br /><br /> スキャナーは、スキャンする各ファイル用に、コアごとに 4 つの一時ファイルを作成するために、十分なディスク領域を必要とします。 推奨される 10 GB のディスク領域を使用すると、4 コア プロセッサで、それぞれのサイズが 625 MB であるファイルを 16 個スキャンできます。 <br /><br />Azure Information Protection に必要な[インターネット接続](../get-started/requirements.md#firewalls-and-network-infrastructure)がこのコンピューターにあることを確認します。 組織のポリシーによってインターネットに接続できない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。|
|スキャナーの構成を格納する SQL Server:<br /><br />- ローカルまたはリモート インスタンス<br /><br />- スキャナーをインストールする sysadmin ロール|次のエディションでは、SQL Server 2012 が最小バージョンとなります。<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Sysadmin ロールを持つアカウントでスキャナーをインストールすると、インストールのプロセスで AzInfoProtectionScanner データベースが自動的に作成され、スキャナーを実行するサービス アカウントに対して必要な db_owner ロールが付与されます。  Sysadmin ロールが付与されない場合や、組織のポリシーがデータベースを手動で作成し構成することを要求している場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」をご覧ください。|
|スキャナー サービスを実行するサービス アカウント|スキャナーのサービスの実行に加えて、このアカウントは Azure AD で認証され、Azure Information Protection ポリシーをダウンロードします。 このアカウントは Active Directory アカウントであり、かつ Azure AD と同期している必要があります。 組織のポリシーによってこのアカウントを同期できない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />このサービス アカウントには次の要件があります。<br /><br />- **ローカル ログオン**権限。 この権限は、スキャナーのインストールと構成に必要ですが、操作には必要ありません。 この権限をサービス アカウントに付与する必要がありますが、スキャナーがファイルを検出、分類、保護できることを確認したら、この権限を削除することができます。 組織のポリシーによって、短時間でもこの権限を付与することができない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />- **サービスとしてログオン**権限。 この権限は、スキャナーのインストール中にサービス アカウントに自動的に付与され、スキャナーのインストール、構成、操作に必要です。 <br /><br />- データ リポジトリへのアクセス許可: ファイルをスキャンして、Azure Information Protection ポリシーの条件を満たすファイルに分類と保護を適用するには、**読み取り**と**書き込み**のアクセス許可を付与する必要があります。 スキャナーを検索モードでのみ実行するには、**読み取り**アクセス許可で十分です。<br /><br />- 再保護または保護を解除するラベル: スキャナーが保護されたファイルに常にアクセスできるようにするには、このアカウントを Azure Rights Management サービスの[スーパー ユーザー](configure-super-users.md)にして、スーパー ユーザー機能が有効になっていることを確認します。 保護を適用するためのアカウント要件の詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](../plan-design/prepare.md)」を参照してください。 さらに、段階的な展開の[オンボーディング制御](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を実装している場合は、このアカウントが構成したオンボーディング制御に含まれていることを確認してください。|
|Azure Information Protection クライアントが Windows Server コンピューターにインストールされる|スキャナーに対する完全なクライアントをインストールする必要があります。 PowerShell モジュールだけで、クライアントをインストールしないでください。<br /><br />クライアントのインストール手順については、[管理者ガイド](../rms-client/client-admin-guide.md)を参照してください。 スキャナーを以前にインストールしていて、今回新しいバージョンにアップグレードする必要がある場合は、[「Azure Information Protection スキャナーのアップグレード](../rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)」をご覧ください。|
|自動分類と、必要に応じて保護を適用する構成済みのラベル|Azure Information Protection ポリシーの条件を構成する方法について詳しくは、「[Azure Information Protection 用の自動および推奨分類の条件を構成する方法](configure-policy-classification.md)」をご覧ください。<br /><br />ファイルに保護を適用するラベルを構成する方法の詳細については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」を参照してください。<br /><br />これらのラベルは、グローバル ポリシーまたは 1 つ以上の[スコープ付きポリシー](configure-policy-scope.md)にあります。<br /><br />注: 自動分類を適用するラベルを構成していない場合でもスキャナーを実行できますが、このシナリオについては、これらのガイドでは説明されていません。 [詳細情報](#using-the-scanner-with-alternative-configurations)|
|スキャンされる Office ドキュメントの場合:<br /><br />- Word、Excel、PowerPoint の 97-2003 ファイル形式および Office Open XML 形式|これらのファイル形式に対してスキャナーがサポートするファイルの種類について詳しくは、「[Azure Information Protection クライアントでサポートされるファイルの種類](../rms-client/client-admin-guide-file-types.md)」をご覧ください。 

組織のポリシーによる禁止のためにテーブルの要件をすべて満たすことができない場合は、代替案として次のセクションをご覧ください。

要件がすべて満たされる場合は、[インストールのセクション](#install-the-azure-information-protection-scanner)に直接移動してください。

### <a name="deploying-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーのデプロイ

テーブルに一覧表示されている前提条件は、スキャナーの既定の要件であり、推奨されます。何故なら、これらはスキャナーをデプロイするための最も簡単な構成であるためです。 これらは、スキャナーの機能を確認するための最初のテスト用に適しています。 ただし、運用環境では、次の制限の 1 つ以上に該当するために組織のポリシーによって既定の要件が禁止される場合があります。

- サーバーのインターネット接続が許可されていない

- Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

- サービス アカウントに**ローカル ログオン**権限を付与できない

- サービス アカウントを Azure Active Directory と同期できないが、サーバーがインターネット接続できる

スキャナーをこれらの制限に対応させることは可能ですが、追加構成が必要です。


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>制限: スキャナー サーバーがインターネット接続できない

[切断されたコンピューター](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)向けの手順に従ってください。 

この構成では、スキャナーは、組織のクラウドベース キーを使用することによる保護 (または保護の削除) を適用できません。 代わりに、スキャナーは、分類にのみ適用されるラベルの使用か、[HYOK](configure-adrms-restrictions.md) を使用する保護に制限されます。 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

スキャナーをインストールするために一時的に Sysadmin ロールが付与される場合、スキャナーのインストールが完了したらこのロールを削除できます。 この構成を使用すると、データベースが自動的に作成され、スキャナー用のサービス アカウントに必要なアクセス許可が自動的に付与されます。 ただし、スキャナーを構成するユーザー アカウントには、AzInfoProtectionScanner データベースの db_owner ロールが必要です。このロールをユーザー アカウントに手動で付与する必要があります。

Sysadmin ロールが一時的にでも付与されない場合は、スキャナーをインストールする前に、AzInfoProtectionScanner という名前のデータベースを手動で作成する必要があります。 この構成を使用する場合、次のロールを割り当てます。
    
|アカウント|データベースレベルのロール|
|--------------------------------|---------------------|
|スキャナーのサービス アカウント|db_owner|
|スキャナーのインストール用のユーザー アカウント|db_owner|
|スキャナーの構成用のユーザー アカウント |db_owner|

通常、スキャナーのインストールと構成には同じユーザー アカウントを使用します。 別々のアカウントを使用する場合は、両方に AzInfoProtectionScanner データベースの db_owner ロールが必要です。

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>制限: スキャナーのサービス アカウントに**ローカル ログオン**権限を付与できない

組織のポリシーで、サービス アカウントに対する**ローカル ログオン**権限の付与が禁止されているが、**バッチ ジョブとしてログオン**権限が許可されている場合は、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」の手順に従います。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>制限: スキャナーのサービス アカウントを Azure Active Directory と同期できないが、サーバーがインターネット接続できる

スキャナーのサービスを実行するために 1 つのアカウントを持ち、Azure Active Directory を認証するために別のアカウントを使用することができます。

- スキャナーのサービス アカウントのためには、ローカルの Windows アカウントか Active Directory アカウントを使用できます。

- Azure Active Directory アカウントの場合は、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」の手順に従ってください。


## <a name="install-the-scanner"></a>スキャナーのインストール

1. スキャナーを実行する Windows Server コンピューターにサインインします。 ローカル管理者権限と SQL Server マスター データベースに書き込むためのアクセス許可を持つアカウントを使用します。

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

## <a name="get-an-azure-ad-token-for-the-scanner"></a>スキャナー用の Azure AD トークンを取得する

Azure AD トークンを使用することで、Azure Information Protection サービスに対してスキャナー サービス アカウントを認証できます。

1. 同じ Windows Server コンピューター、またはデスクトップから、Azure Portal にサインインして、認証のためのアクセス トークンを指定するために必要な 2 つの Azure AD アプリケーションを作成します。 初めて対話型サインインをした後は、このトークンにより非対話的にスキャナーを実行できます。
    
    これらのアプリケーションを作成するには、管理者ガイドの「[非対話形式でファイルに Azure Information Protection のラベル付けをする方法](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」の指示に従います。

2. スキャナーのサービス アカウントにインストール用に**ローカルでログオン**する権限が付与されている場合、Windows Server コンピューターから、このアカウントを使用してサインインし、PowerShell セッションを開始します。 前の手順でコピーした値を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行します。
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application>  -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application >
    ```
    
    求められたら、Azure AD のサービス アカウントの資格情報のパスワードを指定し、**[同意する]** をクリックします。
    
    スキャナーのサービス アカウントにインストールのための**ローカルでログオン**の権限が付与されない場合、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」の手順に従います。 

これでスキャナーに Azure AD を認証するためのトークンが取得されました。トークンの有効期間は、Azure AD での **Web アプリ/API** の構成に従って、1 年間、2 年間、または無期限のいずれかになります。 トークンが期限切れになったら、手順 1 と 2 を繰り返す必要があります。

これでスキャンするデータ ストアを指定する準備ができました。 

## <a name="specify-data-stores-for-the-scanner"></a>スキャナーのデータ ストアの指定

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

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>探索サイクルの実行とスキャナーのレポートの表示

1. **[管理ツール]** > **[サービス]** を使用して、**Azure Information Protection スキャナー** サービスを開始します。

2. スキャナーのサイクルが完了するまで待ちます。 スキャナーが指定したデータ ストア内のすべてのファイルをクロールすると、サービスが停止します。 サービスが停止したときに、ローカルの Windows **アプリケーションとサービス**のイベント ログ、**Azure Information Protection** を使用して確認できます。 情報イベント ID **911** を探します。

3. %*localappdata*%\Microsoft\MSIP\Scanner\Reports に格納され、.csv ファイル形式を持つレポートを確認します。 スキャナーの既定の構成では、自動分類の条件に一致するファイルのみがこれらのレポートに含まれます。
    
    結果が期待どおりにならない場合は、Azure Information Protection ポリシーに指定した条件を微調整する必要がある場合があります。 その場合は、構成を変更して分類、および必要に応じて保護を適用する準備ができるまで、手順 1 から 3 を繰り返します。 これらの手順を繰り返すたびに、最初に Windows Server コンピューターで次の PowerShell コマンドを実行します。
    
        Set-AIPScannerConfiguration -Schedule OneTime

スキャナーが検出したファイルに自動的にラベル付けする準備ができたら、次の手順に進みます。 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>スキャナーを構成して分類と保護を適用する

既定の設定では、スキャナーは、レポートのみモードで 1 回だけ実行されます。 これらの設定を変更するには、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットを実行します。

1. Windows Server コンピューターの PowerShell セッションで、次のコマンドを実行します。
       
        Set-AIPScannerConfiguration -Enforce On -Schedule Continuous
    
    変更する可能性があるその他の構成があります。 たとえば、ファイル属性を変更するかどうか、およびレポートに記録する項目などがあります。 さらに、Azure Information Protection ポリシーに分類レベルを下げる、または保護を解除する理由メッセージを必要とする設定が含まれている場合、このコマンドレットを使用してそのメッセージを指定します。 各構成設定に関する詳細については、[オンライン ヘルプ](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#parameters)を参照してください。 

2. **[管理ツール]** > **[サービス]** を使用して、**Azure Information Protection スキャナー** サービスを再開します。

3. 以前と同じく、イベント ログとレポートを監視して、ラベル付けされたファイル、適用された分類、保護が適用されたかどうかを確認します。

継続的に実行するスケジュールを構成したため、スキャナーはすべてのファイルを完了すると、新しいファイルと変更されたファイルが検出されるように、新しいサイクルを開始します。


## <a name="how-files-are-scanned"></a>ファイルをスキャンする方法

このスキャナーは、実行可能ファイルやシステム ファイルなど、[分類と保護から除外されている](../rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)ファイルを自動的にスキップします。

スキャンする (またはスキャン対象から除外する) ファイルの種類のリストを定義することで、この動作を変更できます。 このリストを指定し、データ リポジトリを指定しなかった場合、そのリストは、独自のリストが指定されていないすべてのデータ リポジトリに適用されます。 このリストを指定するには、[Set-AIPScannerScannedFileType](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes) を使用します。 ファイルの種類のリストを指定した後、新しいファイルの種類をリストに追加するには、[Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes) を使用します。リストからファイルの種類を削除するには、[Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes) を使用します。

その後、Windows iFilter を利用し、次の種類のファイルをスキャンします。 このような種類のファイルでは、ラベルに指定した条件によって文書にラベルが付けられます。

|アプリケーションの種類|ファイルの種類|
|--------------------------------|-------------------------------------|
|Word|.docx; .docm; .dotm; .dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|プロジェクト|.mpp; .mpt|
|PDF|.pdf|
|テキスト|.txt; .xml; .csv|


最後に、残りの種類のファイルについて、スキャナーは Azure Information Protection ポリシーの既定のラベル (またはユーザーがスキャナー用に構成した既定のラベル) を適用します。

|アプリケーションの種類|ファイルの種類|
|--------------------------------|-------------------------------------|
|プロジェクト|.mpp; .mpt|
|発行元|.pub|
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

スキャナーが保護とともにラベルを適用した場合、既定では、Office のファイルの種類のみが保護されます。 他のファイルの種類が保護されるように、この動作を変更できます。 ただし、ラベルがドキュメントに一般保護を適用すると、ファイル名の拡張子が .pfile に変わります。 また、権限が与えられたユーザーが開き、そのネイティブ形式で保存されるまで、ファイルは読み取り専用になります。 テキスト ファイルと画像ファイルでは、そのファイル名の拡張子を変更し、読み取り専用にすることもできます。 

スキャナーの既定の動作を変更する (たとえば、他のファイルの種類も汎用的に保護する) には、レジストリを手動で編集し、保護する他のファイルの種類を指定する必要があります。 詳しくは、開発者ガイダンスの「[ファイル API の構成](../develop/file-api-configuration.md)」をご覧ください。 この開発者向けドキュメントでは、汎用的な保護は "PFile" と呼ばれています。 スキャナーでは、特定のファイル名拡張子を指定する必要があり、`*` ワイルドカードは使用できません。

## <a name="when-files-are-rescanned"></a>ファイルが再スキャンされる場合

最初のスキャン サイクルではスキャナーは構成されているデータ ストアのすべてのファイルを検査し、後続のスキャンでは、新しいファイルまたは変更されたファイルのみが検査されます。 

[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) の実行時に `-Type` パラメーターを **[Full]** に設定すると、スキャナーにすべてのファイルの検査を強制することができます。 この構成は、レポートにすべてのファイルを含める必要がある場合に役立ち、通常は検索モードでスキャナーが実行されるときに使用されます。 フル スキャンが完了すると、後続のスキャンで新しいファイルまたは変更されたファイルのみがスキャンされるように、スキャンの種類が自動的に [増分] に変更されます。

さらに、新しいまたは変更された条件を含む Azure Information Protection ポリシーをスキャナーがダウンロードした場合も、すべてのファイルが検査されます。 スキャナーは、1 時間ごと、およびサービスの開始時にそのポリシーが 1 時間前よりも古い場合にポリシーを更新します。  

> [!TIP]
> テスト期間など、この 1 時間の間隔よりも早くポリシーを更新する必要がある場合は、**%LocalAppData%\Microsoft\MSIP\Policy.msip** と **%LocalAppData%\Microsoft\MSIP\Scanner** の両方からポリシー ファイル **Policy.msip** を手動で削除します。 その後、Azure Information Scanner サービスを再起動します。
> 
> ポリシーの保護設定を変更した場合、保護設定を保存してから 15 分待機した後に、サービスを再起動してください。

スキャナーで自動条件が構成されていないポリシーをダウンロードした場合、スキャナー フォルダーのポリシー ファイルのコピーは更新されません。 このシナリオでは、ラベルが自動条件に対して正しく構成された新たにダウンロードしたポリシー ファイルを使用できるようにするには、その前に **%LocalAppData%\Microsoft\MSIP\Policy.msip** と **%LocalAppData%\Microsoft\MSIP\Scanner** からポリシー ファイル **Policy.msip** を削除する必要があります。

## <a name="using-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーの使用

特定の条件用にラベルを構成する必要がない、次の 2 つの代替シナリオが Azure Information Protection スキャナーでサポートされています。 

- データ リポジトリ内のすべてのファイルに既定のラベルを適用する。
    
    この構成では、[Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) コマンドレットを使用し、*MatchPolicy*パラメーターを **Off** に設定します。 
    
    ファイルの内容は検査されず、データ リポジトリ内のすべてのファイルが、データ リポジトリ用に指定した既定のラベル (*SetDefaultLabel* パラメーター) に従ってラベル付けされます。これが指定されていない場合は、スキャナー アカウントのポリシー設定として指定された既定のラベルが適用されます。
    

- すべてのカスタム条件と、既知の機密情報の種類を特定する。
    
    この構成では、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットを使用し、 *DiscoverInformationTypes* パラメーターを **All** に設定します。
    
    スキャナーでは、Azure Information Protection ポリシー内のラベルに対して指定したカスタム条件と、Azure Information Protection ポリシー内のラベルに指定できる情報の種類のリストが使用されます。 

## <a name="optimizing-the-performance-of-the-scanner"></a>スキャナーのパフォーマンスの最適化

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

- 補足:
    
    - スキャナーを実行するサービス アカウントに、[スキャナーの前提条件](#prerequisites-for-the-azure-information-protection-scanner)のセクションで説明した権限のみが付与されていることを確認し、[高度なクライアント プロパティ](../rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner)を構成して、スキャナーの低整合性レベルを無効してください。
    
    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのファイルに既定のラベルを適用すると、ファイル内容の検査がスキップされるため、スキャナーの実行速度が速くなります。
    
    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのカスタム条件と既知の機密情報の種類を特定すると、スキャナーの実行速度が遅くなりなります。
    

## <a name="list-of-cmdlets-for-the-scanner"></a>スキャナーのコマンドレットの一覧 

スキャナーの他のコマンドレットを使用して、サービス アカウントとスキャナーのデータベースを変更したり、スキャナーの現在の設定を取得したり、スキャナー サービスをアンインストールしたりすることができます。 スキャナーは、次のコマンドレットを使用します。

- [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes)

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes)

- [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>スキャナーのイベント ログ ID と説明

次のセクションを使用して、スキャナーの可能性のあるイベント ID と説明を特定できます。 これらのイベントは、Windows の**アプリケーションとサービス**のイベント ログ、**Azure Information Protection** でスキャナー サービスを実行しているサーバーにログオンします。

-----

情報 **910**

**スキャナーのサイクルが開始しました。**

スキャナー サービスが開始され、指定したデータ リポジトリ内のファイルのスキャンが開始されたときに、このイベントがログに記録されます。

----

情報 **911**

**スキャナーのサイクルが完了しました。**

サーバーを起動してからスキャナーが 1 回限りのスキャンを完了するか、スキャナーが連続的なスケジュールのサイクルを完了したときに、このイベントがログに記録されます。

スキャナーを連続ではなく 1 回のみ実行するように構成している場合、ファイルをもう一度スキャンするには、**[1 回限り]** または **[継続]** にスケジュールを設定してから、サービスを手動で再起動する必要があります。 スケジュールを変更するには、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットと **[スケジュール]** パラメーターを使用します。

----

## <a name="next-steps"></a>次のステップ

[Windows Server FCI と Azure Information Protection スキャナーの違い](../get-started/faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)についてご説明します。

また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 これに関する詳細および PowerShell を使用するその他のシナリオについては、「[Azure Information Protection クライアントでの PowerShell の使用](../rms-client/client-admin-guide-powershell.md)」をご覧ください。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
