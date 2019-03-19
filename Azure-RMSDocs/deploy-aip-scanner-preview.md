---
title: Azure Information Protection スキャナーのデプロイ (プレビュー)
description: 最新のプレビュー バージョンの Azure Information Protection スキャナーをインストール、構成、実行して、データ ストア上のファイルを検出、分類、保護する手順について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/29/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 6aa954a1c111ba20dc890fc9b9b5de4662804379
ms.sourcegitcommit: d716d3345a6a5adc63814dee28f7c01b55b96770
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57828517"
---
# <a name="deploying-the-preview-version-of-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>プレビュー バージョンの Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012 R2*

> [!NOTE]
> この記事は、最新のプレビュー バージョンの Azure Information Protection スキャナーが対象です。 プレビュー バージョンは変更される可能性があります。
> 
> 一般公開バージョンのスキャナーに関するデプロイの手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。
> 
> 一般公開バージョンのスキャナーからプレビュー バージョンにアップグレードする場合は、「[Azure Information Protection スキャナーのアップグレード](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)」をご覧ください。

この情報を利用してプレビュー バージョンの Azure Information Protection スキャナーについて学習した後、これを正しくインストール、構成、および実行する方法を学習してください。 

このスキャナーは、Windows Server でサービスとして実行され、次のデータ ストア上のファイルを検出、分類、および保護することができます。

- スキャナーを実行する Windows Server コンピューター上のローカル フォルダー。

- サーバー メッセージ ブロック (SMB) プロトコルを使用するネットワーク共有の UNC パス。

- SharePoint Server 2016 および SharePoint Server 2013 のサイトとライブラリ。 [このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様向けに SharePoint 2010 もサポートされています。

クラウド リポジトリ上のファイルをスキャンおよびラベル付けするには、スキャナーの代わりに [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) を使用します。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの概要

自動分類を適用するラベルに [Azure Information Protection ポリシー](configure-policy.md)を構成している場合、このスキャナーで検出されたファイルにラベルを付けることができます。 ラベルは分類を適用し、必要に応じて、保護を適用または保護を解除します。

![Azure Information Protection スキャナーのアーキテクチャの概要](./media/infoprotect-scanner.png)

スキャナーは、コンピューターにインストールされている IFilters を使うことで、Windows によってインデックス化できるすべてのファイルを検証できます。 そして、ファイルでラベル付けが必要かどうかを判断するため、スキャナーで Office 365 に組み込まれたデータ損失防止 (DLP) の機密情報の種類とパターン検出、または Office 365 の正規表現パターンが使われます。 スキャナーは Azure Information Protection クライアントを使用するため、同じ[ファイルの種類](./rms-client/client-admin-guide-file-types.md)を分類および保護できます。

スキャナーを実行できるのは検索モードでのみです。この場合、レポートを使用して、ファイルがラベル付けされた場合に何が発生するかをチェックします。 またはスキャナーを実行して、自動的にラベルを適用できます。 機密情報の種類を含んだファイルを検出するためにスキャナーを実行することもできます (自動分類を適用する条件用にラベルを構成する必要はありません)。

スキャナーは検出せず、リアルタイムでラベル付けしないことに注意してください。 スキャナーは指定したデータ ストア上のファイルを体系的にクロールします。この実行サイクルは、1 回限りまたは繰り返しに設定することができます。

スキャナーの構成の一部としてファイルの種類の一覧を定義することで、スキャンするファイルの種類、またはスキャンから除外するファイルの種類を指定できます。


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーの前提条件
Azure Information Protection スキャナーをインストールする前に、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|スキャナー サービスを実行する Windows Server コンピューター:<br /><br />- 4 コア プロセッサ<br /><br />- 8 GB の RAM<br /><br />- 一時ファイルのための空き容量 10 GB (平均)|Windows Server 2016 または Windows Server 2012 R2。 <br /><br />注: 非運用環境でテストまたは評価を行う場合、[Azure Information Protection クライアントでサポートされている](requirements.md#client-devices) Windows クライアント オペレーティング システムを使用できます。<br /><br />このコンピューターは、スキャンするデータ ストアへの高速で信頼性の高いネットワーク接続がある物理コンピューターまたは仮想コンピューターにすることができます。<br /><br /> スキャナーは、スキャンする各ファイル用に、コアごとに 4 つの一時ファイルを作成するために、十分なディスク領域を必要とします。 推奨される 10 GB のディスク領域を使用すると、4 コア プロセッサで、それぞれのサイズが 625 MB であるファイルを 16 個スキャンできます。 <br /><br />組織のポリシーによってインターネットに接続できない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。 それ以外の場合は、HTTPS (ポート 443) 経由で次の URL を許可するインターネット接続がこのコンピューターにあることを確認します。<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|スキャナー サービスを実行するサービス アカウント|Windows Server コンピューター上でのスキャナー サービスの実行に加えて、この Windows アカウントは Azure AD で認証され、Azure Information Protection ポリシーをダウンロードします。 このアカウントは Active Directory アカウントであり、かつ Azure AD と同期している必要があります。 組織のポリシーによってこのアカウントを同期できない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />このサービス アカウントには次の要件があります。<br /><br />- **[Log on locally]\(ローカル ログオン\)** ユーザー権限の割り当て。 この権限は、スキャナーのインストールと構成に必要ですが、操作には必要ありません。 この権限をサービス アカウントに付与する必要がありますが、スキャナーがファイルを検出、分類、保護できることを確認したら、この権限を削除することができます。 組織のポリシーによって、短時間でもこの権限を付与することができない場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」セクションをご覧ください。<br /><br />- **[サービスとしてログオン]** ユーザー権限の割り当て。 この権限は、スキャナーのインストール中にサービス アカウントに自動的に付与され、スキャナーのインストール、構成、操作に必要です。 <br /><br />- データ リポジトリへのアクセス許可: ファイルをスキャンして、Azure Information Protection ポリシーの条件を満たすファイルに分類と保護を適用するには、**読み取り**と**書き込み**のアクセス許可を付与する必要があります。 スキャナーを検索モードでのみ実行するには、**読み取り**アクセス許可で十分です。<br /><br />- 再保護または保護を解除するラベル: スキャナーで保護されたファイルに常に確実にアクセスできるようにするには、このアカウントを Azure Rights Management サービスの[スーパー ユーザー](configure-super-users.md)にして、スーパー ユーザー機能を確実に有効にします。 保護を適用するためのアカウント要件の詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」を参照してください。 さらに、段階的な展開の[オンボーディング制御](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を実装している場合は、このアカウントが構成したオンボーディング制御に含まれていることを確認してください。|
|スキャナーの構成を格納する SQL Server:<br /><br />- ローカルまたはリモート インスタンス<br /><br />- スキャナーをインストールする sysadmin ロール|次のエディションでは、SQL Server 2012 が最小バージョンとなります。<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Azure Information Protection スキャナーでは、スキャナーのカスタム プロファイル名を指定するときに同じ SQL Server インスタンス上の複数の構成データベースがサポートされます。<br /><br />Sysadmin ロールを持つアカウントでスキャナーをインストールすると、インストールのプロセスでスキャナーの構成データベースが自動的に作成され、スキャナーを実行するサービス アカウントに対して必要な db_owner ロールが付与されます。 Sysadmin ロールが付与されない場合や、組織のポリシーがデータベースを手動で作成し構成することを要求している場合は、「[代替構成でのスキャナーのデプロイ](#deploying-the-scanner-with-alternative-configurations)」をご覧ください。<br /><br />構成データベースのサイズはデプロイごとに異なりますが、スキャンしたい 1,000,000 ファイルごとに 500 MB を割り当てることをお勧めします。 |
|プレビュー バージョンの Azure Information Protection クライアントが Windows Server コンピューターにインストールされている|スキャナーに対する完全なクライアントをインストールする必要があります。 PowerShell モジュールだけで、クライアントをインストールしないでください。<br /><br />クライアントのインストール手順については、[管理者ガイド](./rms-client/client-admin-guide.md)を参照してください。 スキャナーを以前にインストールしていて、今回新しいバージョンにアップグレードする必要がある場合は、[「Azure Information Protection スキャナーのアップグレード](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)」をご覧ください。|
|自動分類と、必要に応じて保護を適用する構成済みのラベル|条件用にラベルを構成し、保護を適用する方法について詳しくは、次をご覧ください。<br /> - [自動および推奨分類の条件を構成する方法](configure-policy-classification.md)<br /> - [Rights Management による保護でラベルを構成する方法](configure-policy-protection.md) <br /><br />ヒント[チュートリアル](infoprotect-quick-start-tutorial.md)の手順に従うと、準備した Word 文書内のクレジット カード番号を検索するラベルを使ってスキャナーをテストすることができます。 ただし、オプション **[このラベルの適用方法を選択]** が **[推奨]** ではなく **[自動]** に設定されるように、ラベルの構成を変更する必要があります。 その後、(適用される場合は) ドキュメントからラベルを削除して、スキャナー用のデータ リポジトリにファイルをコピーします。 簡単なテストの場合、これにはスキャナー コンピューター上のローカル フォルダーを使用できます。<br /><br /> 自動分類を適用するラベルを構成していない場合でもスキャナーを実行できますが、このシナリオについては、これらの手順では説明されていません。 [詳細情報](#using-the-scanner-with-alternative-configurations)|
|スキャン対象の SharePoint サイトおよびライブラリの場合:<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|スキャナーでは SharePoint の他のバージョンはサポートされていません。<br /><br />大規模な SharePoint ファームの場合は、スキャナーがすべてのファイルにアクセスするために、リスト ビューのしきい値 (既定では 5,000) を増やす必要があるかどうかを確認します。 詳細については、次の SharePoint のドキュメントを参照してください。[SharePoint で大規模なリストとライブラリを管理する](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|スキャンされる Office ドキュメントの場合:<br /><br />- Word、Excel、PowerPoint の 97-2003 ファイル形式および Office Open XML 形式|これらのファイル形式についてスキャナーでサポートされるファイルの種類について詳しくは、「[Azure Information Protection クライアントでサポートされるファイルの種類](./rms-client/client-admin-guide-file-types.md)」をご覧ください|
|長いパスの場合:<br /><br />- 最大 260 文字 (スキャナーが Windows 2016 にインストールされていて、コンピューターが長いパスをサポートするように構成されているのでない場合)|Windows 10 および Windows Server 2016 では、次の[グループ ポリシー設定](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)により、260 文字を超えるパスの長さがサポートされます。**ローカル コンピューター ポリシー** > **コンピューターの構成** > **管理用テンプレート** > **すべての設定** > **NTFS** > **Win32 の長いパスを有効にする**<br /><br /> 長いファイルのパスのサポートについて詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

組織のポリシーによる禁止のためにテーブルの要件をすべて満たすことができない場合は、代替案として次のセクションをご覧ください。

要件がすべて満たされている場合は、[スキャナーを構成するセクション](#configure-the-scanner-in-the-azure-portal)に直接移動してください。

### <a name="deploying-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーのデプロイ

テーブルに一覧表示されている前提条件は、スキャナーの既定の要件であり、推奨されます。何故なら、これらはスキャナーをデプロイするための最も簡単な構成であるためです。 これらは、スキャナーの機能を確認するための最初のテスト用に適しています。 ただし、運用環境では、次の制限の 1 つ以上に該当するために組織のポリシーによって既定の要件が禁止される場合があります。

- サーバーのインターネット接続が許可されていない

- Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

- サービス アカウントに**ローカル ログオン**権限を付与できない

- サービス アカウントを Azure Active Directory と同期できないが、サーバーがインターネット接続できる

スキャナーをこれらの制限に対応させることは可能ですが、追加構成が必要です。


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>制限: スキャナー サーバーがインターネット接続できない

[切断されたコンピューター](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)向けの手順に従ってください。 その後、次の手順を実行します。

1. スキャナーのプロファイルを作成して、Azure portal でスキャナーを構成します。 この手順に関してサポートが必要な場合は、「[Azure portal でスキャナーを構成する](#configure-the-scanner-in-the-azure-portal)」をご覧ください。

2. **[Azure Information Protection - Profiles (Preview)]\(Azure Information Protection - プロファイル (プレビュー)\)** ブレードから、**[エクスポート]** オプションを使ってスキャナー プロファイルをエクスポートします。

3. 最後に、PowerShell セッションで、[Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) を実行し、エクスポートされた設定を含んでいるファイルを指定します。

この構成では、スキャナーは、組織のクラウドベース キーを使用することによる保護 (または保護の削除) を適用できません。 代わりに、スキャナーは、分類にのみ適用されるラベルの使用か、[HYOK](configure-adrms-restrictions.md) を使用する保護に制限されます。 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

スキャナーをインストールするために一時的に Sysadmin ロールが付与される場合、スキャナーのインストールが完了したらこのロールを削除できます。 この構成を使用すると、データベースが自動的に作成され、スキャナー用のサービス アカウントに必要なアクセス許可が自動的に付与されます。 ただし、スキャナーを構成するユーザー アカウントには、スキャナー構成データベースの db_owner ロールが必要です。このロールをユーザー アカウントに手動で付与する必要があります。

Sysadmin ロールが一時的にでも付与されない場合は、スキャナーをインストールする前にデータベースを手動で作成する必要があります。 この構成を使用する場合、次のロールを割り当てます。
    
|アカウント|データベースレベルのロール|
|--------------------------------|---------------------|
|スキャナーのサービス アカウント|db_owner|
|スキャナーのインストール用のユーザー アカウント|db_owner|
|スキャナーの構成用のユーザー アカウント |db_owner|

通常、スキャナーのインストールと構成には同じユーザー アカウントを使用します。 ただし、別々のアカウントを使用する場合は、両方にスキャナー構成データベースの db_owner ロールが必要です。

- スキャナー用に独自のプロファイル名を指定しない場合、構成データベースには **AIPScanner_\<computer_name>** という名前が付けられます。 

- 独自のプロファイル名を指定すると、構成データベースには **AIPScanner_\<profile_name>** という名前が付けられます。

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>制限: スキャナーのサービス アカウントに**ローカル ログオン**権限を付与できない

組織のポリシーで、サービス アカウントに対する**ローカル ログオン**権限の付与が禁止されているが、**バッチ ジョブとしてログオン**権限が許可されている場合は、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」の手順に従います。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>制限: スキャナーのサービス アカウントを Azure Active Directory と同期できないが、サーバーはインターネット接続できる

スキャナーのサービスを実行するために 1 つのアカウントを持ち、Azure Active Directory を認証するために別のアカウントを使用することができます。

- スキャナーのサービス アカウントのためには、ローカルの Windows アカウントか Active Directory アカウントを使用できます。

- Azure Active Directory アカウントの場合は、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」の手順に従ってください。


## <a name="configure-the-scanner-in-the-azure-portal"></a>Azure portal でスキャナーを構成する

スキャナーをインストールするか、一般公開バージョンのスキャナーからアップグレードする前に、Azure portal でスキャナーのプロファイルを作成します。 スキャナーの設定に関するプロファイルと、スキャンするデータ リポジトリを構成します。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
2. **[スキャナー]** メニュー オプションを見つけて、**[Profiles (Preview)]\(プロファイル (プレビュー)\)** を選択します。
    
    このオプションのテナントへのロールアウトは現在も続いています。そのため、これが表示されない場合は、次のリンクを使って直接ブレードを開くことができます。 https://portal.azure.com/?ScannerConfiguration=true#blade/Microsoft_Azure_InformationProtection/DataClassGroupEditBlade/scannerProfilesBlade

3. **[Azure Information Protection - Profiles (Preview)]\(Azure Information Protection - プロファイル (プレビュー)\)** ブレードで、**[追加]** を選択します。
    
    ![Azure Information Protection スキャナーのプロファイルを追加する](./media/scanner-add-profile.png)

4. **[新しいプロファイルを追加する]** ブレードで、その構成設定とスキャンするデータ リポジトリを識別するために使うスキャナーの名前を指定します。 たとえば、スキャナーの対象となるデータ リポジトリの地理的な場所を識別するために、**Europe** を指定する場合があります。 後でスキャナーをインストールまたはアップグレードするときに、同じプロファイル名を指定する必要があります。
    
    スキャナーのプロファイル名を識別するために、必要に応じて管理目的の説明を指定します。

5. この初期構成では、次の設定を構成して **[保存]** を選択しますが、ブレードは閉じないでください。
    
    - **スケジュール**:既定の **[手動]** のままにしておきます
    - **[検出する情報の種類]**:**[ポリシーのみ]** に変更します
    - **[リポジトリの構成]**:最初にプロファイルを保存する必要があるため、この時点では構成しないでください。
    - **[強制]**:**[オフ]** を選択します
    - **[コンテンツに基づいてファイルにラベルを付ける]**:既定の **[オン]** のままにしておきます
    - **[既定のラベル]**:既定の **[ポリシーの既定値]** のままにしておきます
    - **[ファイルのラベルを書き換える]**:既定の **[オフ]** のままにしておきます
    - **[Preserve "Date modified", "Last modified" and "Modified by"]\("更新日"、"最終変更日時"、"更新者" を保持する\)**:既定の **[オン]** のままにしておきます
    - **[スキャンするファイルの種類]**:既定のファイルの種類を **[対象外]** のままにしておきます
    - **[既定の所有者]**:既定の **[スキャナー アカウント]** のままにしておきます

6. これでプロファイルの作成と保存が完了したので、**[リポジトリの構成]** オプションに戻って、スキャンするデータ ストアを指定する準備が整いました。 オンプレミスの SharePoint サイトとライブラリのローカル フォルダー、UNC パス、および SharePoint Server URL を指定できます。 
    
    SharePoint としては SharePoint Server 2016 と SharePoint Server 2013 がサポートされています。 また、SharePoint Server 2010 も、[このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)を受けている場合はサポートされます。
    
    最初のデータ ストアを追加するには、引き続き **[新しいプロファイルを追加する]** ブレード上で、**[リポジトリの構成]** を選択して **[リポジトリ]** ブレードを開きます。
    
    ![Azure Information Protection スキャナーのデータ リポジトリを構成する](./media/scanner-repositories-bar.png)

7. **[リポジトリ]** ブレードで、**[追加]** を選択します。
    
    ![Azure Information Protection スキャナーのデータ リポジトリを追加する](./media/scanner-repository-add.png)

8. **[リポジトリ]** ブレードで、データ リポジトリのパスを指定します。 
    
    ワイルドカードはサポートされていません。また、WebDav の場所はサポートされていません。
    
    例:
    
    ローカル パスの場合: `C:\Folder`
    
    ネットワーク共有の場合: `C:\Folder\Filename`
    
    UNC パスの場合: `\\Server\Folder`
    
    SharePoint ライブラリの場合: `http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > "共有ドキュメント" の SharePoint パスを追加する場合:
    >
     >- 共有ドキュメントのすべてのドキュメントとすべてのフォルダーをスキャンしたい場合は、パスに **Shared Documents** を指定します。 例: `http://sp2013/Shared Documents`
     >
     >- 共有ドキュメント下のサブフォルダーのすべてのドキュメントとすべてのフォルダーをスキャンしたい場合は、パスに **Documents** を指定します。 例: `http://sp2013/Documents/Sales Reports`
    
    このブレード上の残りの設定に関しては、この初期構成では変更せず、**[既定のプロファイル]** のままにしておきます。 これは、データ リポジトリがスキャナーのプロファイルから設定を継承することを意味します。 
    
    **[保存]** を選択します。

9. 別のデータ リポジトリを追加する場合は、手順 7 と 8 を繰り返します。

10. これで **[新しいプロファイルを追加する]** ブレードを閉じることができ、**[Azure Information Protection - Profiles (Preview)]\(Azure Information Protection - プロファイル (プレビュー)\)** ブレードにご自分のプロファイル名が表示されます。**[スケジュール]** 列には **[手動]** が表示され、**[強制]** 列は空白です。

これで、先ほど作成したスキャナーのプロファイルを使ってスキャナーをインストールする準備ができました。

## <a name="install-the-scanner"></a>スキャナーのインストール

1. スキャナーを実行する Windows Server コンピューターにサインインします。 ローカル管理者権限と SQL Server マスター データベースに書き込むためのアクセス許可を持つアカウントを使用します。

2. **[管理者として実行]** オプションを使用して Windows PowerShell セッションを開きます。

3. Azure Information Protection スキャナー用のデータベースを作成する SQL Server のインスタンスと、前のセクションで指定したスキャナーのプロファイル名を指定して、[Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) コマンドレットを実行します。 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <profile name>
    ```
    
    プロファイル名 **Europe** を使った例:
    
    既定のインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    名前付きインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    SQL Server Express の場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    求められたら、スキャナー サービス アカウントの資格情報 (\<ドメイン\ユーザー名>) とパスワードを指定します。

4. **[管理ツール]** > **[サービス]** を使用して、サービスがインストールされたことを確認します。 
    
    インストールされているサービスの名前は **Azure Information Protection スキャナー**で、作成したスキャナー サービス アカウントを使用して実行するように構成されます。

スキャナーをインストールしたら、スキャナーを無人で実行できるように、スキャナー サービス アカウントを認証するための Azure AD トークンを取得する必要があります。 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>スキャナー用の Azure AD トークンを取得する

Azure AD トークンを使用することで、Azure Information Protection サービスに対してスキャナー サービス アカウントを認証できます。

1. Azure portal に戻り、認証のためのアクセス トークンを指定するために必要な 2 つの Azure AD アプリケーションを作成します。 初めて対話型サインインをした後は、このトークンにより非対話的にスキャナーを実行できます。
    
    これらのアプリケーションを作成するには、管理者ガイドの「[非対話形式でファイルに Azure Information Protection のラベル付けをする方法](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」の指示に従います。

2. スキャナーのサービス アカウントにインストールのための**ローカル ログオン**権限が付与されている場合は、Windows Server コンピューターから、このアカウントを使用してサインインし、PowerShell セッションを開始します。 前の手順でコピーした値を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行します。
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```
    
    求められたら、Azure AD のサービス アカウントの資格情報のパスワードを指定し、**[同意する]** をクリックします。
    
    スキャナーのサービス アカウントにインストールのための**ローカル ログオン**権限を付与できない場合は、管理者ガイドの「[Set-AIPAuthentication の Token パラメーターを指定し、使用する](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)」セクションの手順に従います。 

これでスキャナーに Azure AD を認証するためのトークンが取得されました。トークンの有効期間は、Azure AD での **Web アプリ/API** の構成に従って、1 年間、2 年間、または無期限のいずれかになります。 トークンが期限切れになったら、手順 1 と 2 を繰り返す必要があります。

これで、最初のスキャンを検索モードで実行する準備ができました。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>探索サイクルの実行とスキャナーのレポートの表示

1. Azure portal で Azure Information Protection に戻り、スキャナーを起動します。 **[スキャナー]** メニュー オプションから、**[ノード]** を選択します。 スキャナーのノードを選択したら、**[今すぐスキャン]** オプションを選択します。
    
    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)
    
    または、PowerShell セッションで、次のコマンドを実行します。
    
        Start-AIPScan

2. スキャナーのサイクルが完了するまで待ちます。 スキャナーが指定したデータ ストア内のすべてのファイルをクロールし終わると、スキャナー サービスの動作が続いていてもスキャナーは停止します。
    
    - **[Azure Information Protection - Nodes]\(Azure Information Protection - ノード\)** ブレードで、**[状態]** 列の値が **[スキャン]** から **[アイドル]** に変化します。
    
    - PowerShell を使用すると、`Get-AIPScannerStatus` を実行して状態の変化を監視できます。
    
    - ローカル Windows イベント ログの **[アプリケーションとサービス]** の **[Azure Information Protection]** を確認します。 このログでは、スキャナーがスキャンを完了した時刻も、結果の概要と共に報告されます。 情報イベント ID **911** を探します。

3. %*localappdata*%\Microsoft\MSIP\Scanner\Reports に格納されているレポートを確認します。 .txt の概要ファイルには、スキャンにかかった時間、スキャンされたファイルの数、情報の種類と一致したファイルの数が含まれています。 .csv ファイルには各ファイルに関する詳細情報が記載されています。 このフォルダーには、スキャンのサイクルごとに最大 60 のレポートが格納され、必要なディスク領域を最小限に抑えるために最新のもの以外のすべてのレポートが圧縮されます。
    
    > [!NOTE]
    > [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) と共に *ReportLevel* パラメーターを使って、ログ記録のレベルを変更することができます。ただし、レポート フォルダーの場所または名前を変更することはできません。 別のボリュームまたはパーティションにレポートを保存したい場合は、フォルダーに対するディレクトリのジャンクションの使用を検討してください。
    >
    > たとえば、[Mklink](/windows-server/administration/windows-commands/mklink) コマンドを使います。`mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    **[検出する情報の種類]** に対して **[ポリシーのみ]** を設定しているため、自動分類用に設定した条件を満たすファイルのみが詳細レポートに含まれます。 ラベルが適用されていない場合は、ラベルの構成に推奨される分類ではなく自動分類が含まれていることを確認します。
    
    > [!TIP]
    > スキャナーでは 5 分ごとにこの情報が Azure Information Protection に送信されます。このため、Azure portal から結果をほぼリアルタイムで確認することができます。 詳細については、[Azure Information Protection のレポート作成](reports-aip.md)に関するページを参照してください。 
        
    結果が期待どおりにならない場合は、Azure Information Protection ポリシーでラベルに対して指定した条件を再構成する必要がある場合があります。 その場合は、構成を変更して分類、および必要に応じて保護を適用する準備ができるまで、手順 1 から 3 を繰り返します。 

Azure portal には、最後のスキャンに関する情報のみが表示されます。 前のスキャンの結果を確認する必要がある場合は、スキャナー コンピューターの %*localappdata*%\Microsoft\MSIP\Scanner\Reports フォルダーに格納されているレポートに戻ります。

スキャナーが検出したファイルに自動的にラベル付けする準備ができたら、次の手順に進みます。 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>スキャナーを構成して分類と保護を適用する

これらの手順に従っている場合、スキャナーは、レポートのみモードで 1 回だけ実行されます。 これらの設定を変更するには、スキャナーのプロファイルを編集します。

1. **[[Azure Information Protection - Profiles (Preview)]\(Azure Information Protection - プロファイル (プレビュー)\)](https://portal.azure.com/?ScannerConfiguration=true#blade/Microsoft_Azure_InformationProtection/DataClassGroupEditBlade/scannerProfilesBlade)** ブレードに戻り、スキャナーのプロファイルを選択して編集します。

2. \<**プロファイル名**> ブレード上で、次の 2 つの設定を変更した後、**[保存]** を選択します。
    
   - **スケジュール**:**[常時]** に変更します
   - **[強制]**:**[オン]** を選択します
    
     変更する可能性があるその他の構成があります。 たとえば、ファイル属性を変更するかどうか、またはスキャナーでファイルのラベルを書き換えられるかどうかなどです。 情報のポップアップ ヘルプを使って、各構成設定について詳しく学習してください。

3. 現在の時刻をメモして、**[Azure Information Protection - Nodes]\(Azure Information Protection - ノード\)** ブレードからもう一度スキャナーを起動します。
    
    ![Azure Information Protection スキャナーのスキャンを開始する](./media/scanner-scan-now.png)
    
    または、PowerShell セッションで次のコマンドを実行できます。
    
        Start-AIPScan

4. 情報の種類が **911** で、タイム スタンプが前の手順でスキャンを開始した時刻よりも後のイベント ログを再び監視します。 
    
    次に、レポートをチェックして、ラベル付けされたファイル、各ファイルに適用された分類、それらに保護が適用されたかどうかについての詳細を確認します。 または、Azure portal を使用してより簡単にこの情報を確認します。

スケジュールを継続的に実行するように構成したため、スキャナーはすべてのファイルの作業を完了すると、新しいファイルや変更されたファイルをすべて検出するために新しいサイクルを自動的に開始します。


## <a name="how-files-are-scanned"></a>ファイルをスキャンする方法

スキャナーでは、ファイルをスキャンするとき、次のプロセスが実行されます。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1.ファイルがスキャンに含まれるか、または除外されるかを判断する 
スキャナーでは、実行可能ファイルやシステム ファイルなど、[分類と保護から除外されている](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)ファイルは自動的にスキップされます。

スキャンする (またはスキャン対象から除外する) ファイルの種類のリストを定義することで、この動作を変更できます。 スキャナーに対してこのリストを指定し、既定ですべてのデータ リポジトリに適用させることができます。また、データ リポジトリごとに 1 つのリストを指定することができます。 このリストを指定するには、スキャナーのプロファイルの **[スキャンするファイルの種類]** 設定を使います。

![Azure Information Protection スキャナー用にスキャンするファイルの種類を構成する](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2.ファイルを検査してラベルを付ける

その後、スキャナーでは、フィルターを使用して、サポートされているファイルの種類がスキャンされます。 これらの同じフィルターが、オペレーティング システムによって Windows Search とインデックス作成にも使用されます。 構成を何も追加しなくても、Word、Excel、PowerPoint、PDF ドキュメント、テキスト ファイルに対して使用されるファイルの種類のスキャンに、Windows IFilter が使用されます。

既定でサポートされているファイルの種類の完全な一覧、および .zip ファイルと .tiff ファイルを含む既存のフィルターの構成方法に関する追加情報については、「[検査に対してサポートされているファイルの種類](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)」をご覧ください。

検査が済むと、ユーザーがラベルに対して指定した条件を使用して、これらのファイルの種類にラベルを付けることができます。 または、検出モードを使用している場合は、ユーザーがラベルに対して指定した条件、またはすべての既知の機密情報の種類を含むように、これらのファイルを報告できます。 

ただし、以下の状況では、スキャナーでファイルにラベルを付けることはできません。

- ラベルで分類は適用されるが、保護は適用されず、ファイルの種類で ["分類のみ" がサポート](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)されていない場合。

- ラベルで分類と保護が適用されるが、スキャナーでファイルの種類が保護されていない場合。
    
    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 他のファイルの種類は、次のセクションで説明するように、[レジストリを編集](#editing-the-registry-for-the-scanner)すると保護できます。

たとえば、.txt ファイルの種類では "分類のみ" がサポートされていないため、ファイル名拡張子が .txt であるファイルを検査した後は、分類用にだけ構成されていて保護用には構成されていないラベルを、スキャナーで適用することはできません。 ラベルが分類用と保護用に構成されていて、レジストリが .txt ファイルの種類用に編集されている場合は、スキャナーでファイルにラベルを付けることができます。 

> [!TIP]
> このプロセス中にスキャナーが停止し、リポジトリ内の大量のファイルのスキャンが完了しない場合:
> 
> - ファイルをホストしているオペレーティング システムに対し、動的ポートの数を増やす必要がある場合があります。 SharePoint 用にサーバーのセキュリティが強化されている場合、スキャナーが許可されているネットワーク接続の数を超えて、そのために停止する原因の 1 つになる可能性があります。
>     
>     これがスキャナー停止の原因であるかどうかを確認するには、%*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog にスキャナーに対する以下のエラー メッセージが記録されているかどうかを確認します (複数のログがある場合は zip 形式になっています)。**リモート サーバー 'System.Net.Sockets.SocketException' に接続できません:通常、各ソケット アドレスに対してプロトコル、ネットワーク アドレス、またはポートのどれか 1 つのみを使用できます IP:ポート**
>    
>     現在のポート範囲を表示し、範囲を拡大する方法について詳しくは、「[ネットワーク パフォーマンスを向上させるために変更可能な設定](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)」をご覧ください。
> 
> - 大規模な SharePoint ファームの場合、リスト ビューのしきい値 (既定では 5,000) を増やす必要がある場合があります。 詳細については、次の SharePoint のドキュメントを参照してください。[SharePoint で大規模なリストとライブラリを管理する](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)。

### <a name="3-label-files-that-cant-be-inspected"></a>3.検査できないファイルにラベルを付ける
検査できないファイルの種類に対し、スキャナーでは Azure Information Protection ポリシーの既定のラベル、またはユーザーがスキャナー用に構成した既定のラベルが適用されます。

前のステップと同じように、以下の状況では、スキャナーでファイルにラベルを付けることはできません。

- ラベルで分類は適用されるが、保護は適用されず、ファイルの種類で ["分類のみ" がサポート](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)されていない場合。

- ラベルで分類と保護が適用されるが、スキャナーでファイルの種類が保護されていない場合。
    
    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 他のファイルの種類は、次に説明するように、[レジストリを編集](#editing-the-registry-for-the-scanner)すると保護できます。


### <a name="editing-the-registry-for-the-scanner"></a>スキャナーのレジストリの編集

Office ファイルと PDF 以外のファイルの種類を保護するためにスキャナーの既定の動作を変更するには、レジストリを手動で編集し、保護する他のファイルの種類と、保護の種類 (ネイティブまたは汎用) を指定する必要があります。 詳しくは、開発者ガイダンスの「[ファイル API の構成](develop/file-api-configuration.md)」をご覧ください。 この開発者向けドキュメントでは、汎用的な保護は "PFile" と呼ばれています。 さらに、スキャナーの場合:

- スキャナーには独自の既定の動作があります。既定では、Office ファイル形式と PDF ドキュメントのみが保護されます。 レジストリを変更しない場合、その他のファイル形式は、スキャナーによってラベル付けまたは保護されません。

- すべてのファイルがネイティブのまたは汎用的な保護により自動的に保護される、Azure Information Protection クライアントの同じ既定の保護動作が必要な場合は、`*` ワイルドカードをレジストリ キーとして、`Default` を値データとして指定します。

レジストリを編集するときには、各ファイル名拡張子のキーと共に、**MSIPC** キーと **FileProtection** キーが存在しない場合には手動で作成します。

たとえば、Office ファイルと PDF だけでなく、TIFF イメージも保護するスキャナーの場合、レジストリの編集後は、次の図のようになります。 イメージ ファイルなので、TIFF ファイルではネイティブ保護がサポートされ、結果としてファイル名拡張子は .ptiff になります。

![保護を適用するためのスキャナーのレジストリの編集](./media/editregistry-scanner.png)

同様に、ネイティブ保護はサポートされていても、レジストリで指定する必要があるテキスト ファイルとイメージ ファイルの種類の一覧については、管理者ガイドの「[分類と保護がサポートされているファイルの種類](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)」をご覧ください。

ネイティブ保護がサポートされていないファイルの場合は、新しいキーとしてファイル名拡張子を指定し、汎用的な保護のために **PFile** を指定します。 結果として、保護されるファイルのファイル名拡張子は .pfile になります。


## <a name="when-files-are-rescanned"></a>ファイルが再スキャンされる場合

最初のスキャン サイクルではスキャナーは構成されているデータ ストアのすべてのファイルを検査し、後続のスキャンでは、新しいファイルまたは変更されたファイルのみが検査されます。 

Azure portal の **[Azure Information Protection - Nodes]\(Azure Information Protection - ノード\)** ブレードから、スキャナーに強制的にすべてのファイルをもう一度検査させることができます。 一覧からスキャナーを選択し、**[Rescan all files]\(すべてのファイルを再スキャン\)** オプションを選択します。

![Azure Information Protection スキャナーの再スキャンを開始する](./media/scanner-rescan-files.png)

すべてのファイルの再検査はレポートにすべてのファイルを含める必要がある場合に役立ち、この構成は通常、検索モードでスキャナーが実行されるときに使用されます。 フル スキャンが完了すると、後続のスキャンで新しいファイルまたは変更されたファイルのみがスキャンされるように、スキャンの種類が自動的に [増分] に変更されます。

さらに、新しいまたは変更された条件を含む Azure Information Protection ポリシーをスキャナーがダウンロードした場合も、すべてのファイルが検査されます。 スキャナーは、1 時間ごと、およびサービスの開始時にそのポリシーが 1 時間前よりも古い場合にポリシーを更新します。  

> [!TIP]
> テスト期間など、この 1 時間の間隔よりも早くポリシーを更新する必要がある場合は、**%LocalAppData%\Microsoft\MSIP\Policy.msip** と **%LocalAppData%\Microsoft\MSIP\Scanner** の両方から、ポリシー ファイル **Policy.msip** を手動で削除します。 その後、Azure Information Scanner サービスを再起動します。
> 
> ポリシーの保護設定を変更した場合、保護設定を保存してから 15 分待機した後に、サービスを再起動してください。

スキャナーで自動条件が構成されていないポリシーをダウンロードした場合、スキャナー フォルダーのポリシー ファイルのコピーは更新されません。 このシナリオでは、ラベルが自動条件に対して正しく構成された新たにダウンロードしたポリシー ファイルを使用できるようにするには、その前に **%LocalAppData%\Microsoft\MSIP\Policy.msip** と **%LocalAppData%\Microsoft\MSIP\Scanner** からポリシー ファイル **Policy.msip** を削除する必要があります。

## <a name="editing-in-bulk-for-the-data-repository-settings"></a>データ リポジトリ設定の一括編集

スキャナーのプロファイルに追加したデータ リポジトリに対して、**[エクスポート]** と **[インポート]** オプションを使って簡単に設定を変更することができます。 たとえば、ご自分の SharePoint データ リポジトリに対して、スキャンから除外する新しいファイルの種類を追加したいことがあります。

Azure portal で各データ リポジトリを編集する代わりに、**[リポジトリ]** ブレードの **[エクスポート]** オプションを使います。

![スキャナーのデータ リポジトリの設定をエクスポートする](./media/export-scanner-repositories.png)

手動でファイルを編集して変更を加えたら、同じブレード上で **[インポート]** オプションを使います。

## <a name="using-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーの使用

特定の条件用にラベルを構成する必要がない、次の 2 つの代替シナリオが Azure Information Protection スキャナーでサポートされています。 

- データ リポジトリ内のすべてのファイルに既定のラベルを適用する。
    
    この構成では、**[既定のラベル]** を **[カスタム]** に設定し、使うラベルを選択します。
    
    ファイルの内容は検査されず、データ リポジトリ内にあるすべてのファイルは、データ リポジトリまたはスキャナーのプロファイル用に設定する既定のラベルに従ってラベル付けされます。
    

- すべてのカスタム条件と、既知の機密情報の種類を特定する。
    
    この構成では、**[検出する情報の種類]** を **[すべて]** に設定します。
    
    スキャナーでは、Azure Information Protection ポリシー内のラベルに対して指定したカスタム条件と、Azure Information Protection ポリシー内のラベルに指定できる情報の種類のリストが使用されます。 この設定は、気付かない可能性がある機密情報を発見するのに役立ちますが、スキャナーのスキャン速度が犠牲になります。
    
    次の一般公開バージョンのスキャナーに向けたクイック スタートでは、この構成が使われています。[クイック スタート: 所有している機密情報の検索](quickstart-findsensitiveinfo.md)に関するページで使用されます。

## <a name="optimizing-the-performance-of-the-scanner"></a>スキャナーのパフォーマンスの最適化

スキャナーのパフォーマンスを最適化するには、次のガイダンスを使用します。 ただし、スキャナーのパフォーマンスではなくスキャナー コンピューターの応答性を優先する場合は、クライアントの詳細設定を使ってスキャナーで使用されるスレッドの数を制限することができます。

スキャナーのパフォーマンスを最大化するには

- **スキャナー コンピューターとスキャンされたデータ ストア間のネットワーク接続を高速かつ信頼性の高い接続にする**
    
    たとえば、同じ LAN 内か、スキャンされたデータ ストアと同じネットワーク セグメント内 (推奨) にスキャナー コンピューターを配置します。
    
    ネットワーク接続の品質は、スキャナーがスキャナー サービスを実行しているコンピューターにファイルのコンテンツを転送してファイルを検査するため、スキャナーのパフォーマンスに影響します。 このデータを移動する必要があるネットワークのホップ数を減らす (削除する) と、ネットワークの負荷も軽減されます。 

- **スキャナー コンピューターに利用可能なプロセッサ リソースがあることを確認する**
    
    ファイルの内容の検査、およびファイルの暗号化と複合化は、プロセッサ負荷の高いアクションです。 プロセッサ リソースの不足がスキャナー パフォーマンスを低下させるかどうかを識別するには、指定したデータ ストアの標準のスキャン サイクルを監視します。
    
- **スキャナー サービスを実行しているコンピューター上のローカル フォルダーをスキャンしない**
    
    Windows Server 上にスキャンするフォルダーがある場合は、別のコンピューター上にスキャナーをインストールし、これらのフォルダーをネットワーク共有として構成してスキャンします。 ファイルをホストする機能とファイルをスキャンする機能の 2 つの機能を分離させると、これらのサービス用のリソースの計算が相互に競合していないことを意味します。

必要に応じて、スキャナーの複数のインスタンスをインストールします。 Azure Information Protection スキャナーでは、スキャナーのカスタム プロファイル名を指定するときに同じ SQL Server インスタンス上の複数の構成データベースがサポートされます。

スキャナーのパフォーマンスに影響するその他の要因

- スキャンするファイルを含むデータ ストアの現在の負荷と応答時間

- スキャナーが検索モードまたは強制モードのどちらで実行されているか
    
    通常、検索モードでは、強制モードよりもスキャン速度が速くなります。これは、発見には単一ファイルの読み取りアクションが必要なのに対して、強制モードでは読み取り/書き込みアクションが必要なためです。

- Azure Information Protection の条件を変更する
    
    スキャナーがすべてのファイルを検査する必要がある場合、最初のスキャン サイクルには、既定では新規および変更されたファイルのみを検査する後続のスキャン サイクルよりも、長い時間がかかります。 ただし、Azure Information Protection ポリシーの条件を変更した場合、[上記のセクション](#when-files-are-rescanned)に示されているように、すべてのファイルがもう一度スキャンされます。

- 選択したログ レベル
    
    スキャナー レポートに対して **[デバッグ]**、**[情報]**、**[エラー]**、**[オフ]** から選択できます。 **[オフ]** を選択すると、最適なパフォーマンスになります。**[デバッグ]** は大幅にスキャナーのスピードを低下させるので、トラブルシューティング時にのみ使用してください。 詳細については、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットの *ReportLevel* パラメーターを参照してください。

- ファイル自体
    
    - Office ファイルは PDF ファイルよりもすばやくスキャンされます。
    
    - 保護されていないファイルは、保護されたファイルよりもすばやくスキャンされます。
    
    - 大きいファイルは明らかに小さいファイルよりも時間がかかります。

- 補足:
    
    - スキャナーを実行するサービス アカウントに、[スキャナーの前提条件](#prerequisites-for-the-azure-information-protection-scanner)のセクションで説明した権限のみが付与されていることを確認し、[高度なクライアント プロパティ](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner)を構成して、スキャナーの低整合性レベルを無効してください。
    
    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのファイルに既定のラベルを適用すると、ファイル内容の検査がスキップされるため、スキャナーの実行速度が速くなります。
    
    - [代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのカスタム条件と既知の機密情報の種類を特定すると、スキャナーの実行速度が遅くなりなります。
    

## <a name="list-of-cmdlets-for-the-scanner"></a>スキャナーのコマンドレットの一覧

現在では Azure portal からスキャナーを構成するため、データ リポジトリとスキャンされるファイルの種類のリストを構成する以前のバージョンのコマンドレットは、非推奨になりました。 

残っているコマンドレットには、スキャナーをインストールおよびアップグレードするコマンドレット、スキャナーの構成データベースとプロファイルを変更するコマンドレット、ローカルのレポート レベルを変更するコマンドレット、および切断されたコンピューターの構成設定をインポートするコマンドレットが含まれます。 

以前のバージョンのスキャナーでサポートされているコマンドレットの完全な一覧は、次のとおりです。 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>スキャナーのイベント ログ ID と説明

次のセクションを使用して、スキャナーの可能性のあるイベント ID と説明を特定できます。 これらのイベントは、Windows の**アプリケーションとサービス**のイベント ログ、**Azure Information Protection** でスキャナー サービスを実行しているサーバーにログオンします。

-----

情報 **910**

**スキャナーのサイクルが開始しました。**

スキャナー サービスが開始され、指定したデータ リポジトリ内のファイルのスキャンが開始されたときに、このイベントがログに記録されます。

----

情報 **911**

**スキャナーのサイクルが完了しました。**

スキャナーで手動スキャンまたは継続的スケジュールのサイクルが完了すると、このイベントがログに記録されます。

スキャナーを連続ではなく手動で実行するように構成した場合、ファイルをもう一度スキャンするには、スキャナーのプロファイルで **[スケジュール]** を **[手動]** または **[常時]** に設定して、サービスを再起動します。

----

## <a name="next-steps"></a>次の手順

Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」 (Azure Information Protection スキャナーを使用したデータ保護の自動化) をお読みください。

次に、[Windows Server FCI と Azure Information Protection スキャナーの違い](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)について確認します

また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 これに関する詳細および PowerShell を使用するその他のシナリオについては、「[Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md)」をご覧ください。
