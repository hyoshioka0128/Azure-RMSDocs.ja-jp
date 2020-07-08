---
title: Azure Information Protection (AIP) の統合ラベル付けスキャナーをインストールして構成する
description: Azure Information Protection 統合されたラベル付けスキャナーをインストールして構成し、データストア上のファイルを検出、分類、および保護する手順について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e786b30075f7a72781dd6cac13af4e14b70fc2db
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86049641"
---
# <a name="configuring-and-installing-the--azure-information-protection-unified-labeling-scanner"></a>Azure Information Protection 統合ラベルスキャナーの構成とインストール

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE] 
> AIP クラシックスキャナーを使用している場合は、「[クラシックスキャナー Azure Information Protection のインストールと構成](deploy-aip-scanner-configure-install-classic.md)」を参照してください。

Azure Information Protection スキャナーの構成とインストールを開始する前に、システムが[必要な前提条件](deploy-aip-scanner-prereqs.md)に準拠していることを確認してください。

準備ができたら、次の手順に進みます。

1. [Azure portal でスキャナーを構成する](#configure-the-scanner-in-the-azure-portal)

1. [スキャナーのインストール](#install-the-scanner)

1. [スキャナー用の Azure AD トークンを取得する](#get-an-azure-ad-token-for-the-scanner)

1. [分類と保護を適用するようにスキャナーを構成する](#configure-the-scanner-to-apply-classification-and-protection)
 
システムで必要に応じて、次の追加の構成手順を実行します。

|手順  |説明  |
|---------|---------|
|[保護するファイルの種類を変更する](#change-which-file-types-to-protect) |既定とは異なる種類のファイルをスキャン、分類、または保護することができます。 詳細については、「 [AIP scanning process](deploy-aip-scanner.md#aip-scanning-process)」を参照してください。 |
|[スキャナーをアップグレードする](#upgrading-your-scanner) | スキャナーをアップグレードして、最新の機能と改善点を活用します。|
|[データリポジトリ設定の一括編集](#editing-data-repository-settings-in-bulk)| インポートとエクスポートのオプションを使用して、複数のデータリポジトリに対して一括変更を行います。|
|[別の構成でスキャナーを使用する](#using-the-scanner-with-alternative-configurations)| 任意の条件でラベルを構成せずにスキャナーを使用する |
|[パフォーマンスを最適化する](#optimizing-scanner-performance)| スキャナーのパフォーマンスを最適化するためのガイダンス|
| | |

詳細については、「[スキャナーのコマンドレットの一覧](#list-of-cmdlets-for-the-scanner)」も参照してください。

## <a name="configure-the-scanner-in-the-azure-portal"></a>Azure portal でスキャナーを構成する

スキャナーをインストールする前、または以前の一般公開バージョンのスキャナーからアップグレードする前に、Azure portal でスキャナー用のクラスターおよびコンテンツスキャンジョブを作成します。 

次に、スキャナーの設定とスキャンするデータリポジトリを使用して、クラスターおよびコンテンツスキャンジョブを構成します。

スキャナーを構成するには: 

1. [Azure portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)し、 **Azure Information Protection** ] ウィンドウに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。
    
1. [**スキャナー** ] メニューオプションを見つけて、[**クラスター**] を選択します。

1. [ **Azure Information Protection クラスター** ] ウィンドウで、[**追加**] を選択します。
    
    :::image type="content" source="media/scanner-add-profile.png" alt-text="Azure Information Protection スキャナーのコンテンツスキャンジョブの追加":::

1. [**新しいクラスターの追加**] ウィンドウで、次のようにします。

    1. スキャナーにわかりやすい名前を指定します。 この名前は、スキャナーの構成設定とスキャンするデータリポジトリを識別するために使用されます。 

        たとえば、スキャナーの対象となるデータ リポジトリの地理的な場所を識別するために、**Europe** を指定する場合があります。 後でスキャナーをインストールまたはアップグレードする場合は、同じクラスター名を指定する必要があります。
   
    2. 必要に応じて、スキャナーのクラスター名を識別しやすいように、管理のための説明を指定します。

    3. **[保存]** を選択します。
1. [**スキャナー** ] メニューオプションを見つけて、[**コンテンツスキャンジョブ**] を選択します。
1. [ **Azure Information Protection-コンテンツスキャンジョブ**] ウィンドウで、[**追加**] を選択します。
 
1. この初期構成では、次の設定を構成してから、[**保存**] を選択しますが、ウィンドウは閉じないでください。
    
    |Section  |設定  |
    |---------|---------|
    |**コンテンツスキャンジョブの設定**     |    - **スケジュール**:**既定のままにし**ておきます。 </br>- **検出される情報の種類**:**ポリシーのみ**に変更 </br>- **リポジトリを構成**する: コンテンツスキャンジョブを最初に保存する必要があるため、現時点では構成しないでください。         |
    |**ポリシーの適用**     | - **強制**: [**オフ**] を選択します。 </br>- **コンテンツに基づいてファイルにラベルを付ける**: の既定値のまま**に**します。 </br>- **既定のラベル**: 既定の**ポリシー**の既定値のままにします。 </br>- **ファイルのラベル**を変更する: 既定値を**オフ**のままにします。        |
    |**ファイル設定の構成**     | - [**更新日]、[最終更新日]、[変更者] を保持し**ます。の既定値のまま**に**します。 </br>- **スキャンするファイルの種類**: [**除外**するファイルの種類を既定のままにする。 </br>- **既定の所有者**: 既定の**スキャナーアカウント**を保持します        |
    | | |


1. コンテンツスキャンジョブの作成と保存が完了したら、[**リポジトリの構成**] オプションに戻り、スキャンするデータストアを指定できます。 

    SharePoint オンプレミスのドキュメントライブラリとフォルダーの UNC パスと SharePoint サーバーの Url を指定します。 
    
    > [!NOTE]
    > Sharepoint では、sharepoint server 2019、SharePoint Server 2016、および SharePoint Server 2013 がサポートされています。 また、SharePoint Server 2010 も、[このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)を受けている場合はサポートされます。
    >     
    最初のデータストアを追加するには、[**新しいコンテンツスキャンジョブの追加**] ウィンドウで [**リポジトリの構成**] を選択し、[**リポジトリ**] ウィンドウを開きます。
    
    :::image type="content" source="media/scanner-repositories-bar.png" alt-text="Azure Information Protection スキャナーのデータ リポジトリを構成する":::

1. **[リポジトリ]** ペインで、 **[追加]** を選択します。
    
    :::image type="content" source="media/scanner-repository-add.png" alt-text="Azure Information Protection スキャナーのデータ リポジトリを追加する":::

1. [**リポジトリ**] ウィンドウで、データリポジトリのパスを指定し、[**保存**] を選択します。

    次に例を示します。 

    - ネットワーク共有の場合は、を使用 `\\Server\Folder` します。 
    - SharePoint ライブラリの場合は、を使用 `http://sharepoint.contoso.com/Shared%20Documents/Folder` します。

    > [!NOTE]
    > ワイルドカードはサポートされていません。また、WebDav の場所はサポートされていません。
    >     

    SharePoint パスを追加するときは、次の構文を使用します。
    
    |パス  |構文  |
    |---------|---------|
    |**ルートパス**     | `http://<SharePoint server name>` </br></br>スキャナーユーザーに許可されているサイトコレクションも含め、すべてのサイトをスキャンします。 </br>ルートコンテンツを自動的に検出するには、[追加のアクセス許可](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories)が必要です        |
    |**特定の SharePoint サブサイトまたはコレクション**     | 次のいずれか: </br>- `http://<SharePoint server name>/<subsite name>` </br>- `http://SharePoint server name>/<site collection name>/<site name>` </br></br>サイトコレクションのコンテンツを自動的に検出するには、[追加のアクセス許可](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories)が必要です         |
    |**特定の SharePoint ライブラリ**     | 次のいずれか: </br>- `http://<SharePoint server name>/<library name>` </br>- `http://SharePoint server name>/.../<library name>`       |
    |**特定の SharePoint フォルダー**     | `http://<SharePoint server name>/.../<folder name>`        |
    | | |

    このウィンドウの残りの設定については、この初期構成では変更せず、[**コンテンツスキャンジョブ] の既定値**のままにしておきます。 既定の設定は、データリポジトリがコンテンツスキャンジョブから設定を継承することを意味します。

    <!--
        > [!IMPORTANT]
        > While the local file system can be scanned, this configuration is not recommended for production deployments and can **only** be used in single node clusters.
        >
        > Scanning of local folders by multi-node clusters is not supported. If you need to scan a folder on the local file system, we recommend creating a share, and scanning it using a network URL.
    -->

1. 別のデータリポジトリを追加する場合は、手順 8. と 9. を繰り返します。 

1. [**リポジトリ**] ウィンドウと [**コンテンツスキャンジョブ**] ウィンドウを閉じます。 

[ **Azure Information Protection-コンテンツスキャンジョブ**] ウィンドウに戻り、[**スケジュール**] 列に [**手動**] が表示され、[**適用**] 列が空白になっている場合は、コンテンツスキャン名が表示されます。

これで、作成したコンテンツスキャナージョブを使用して、スキャナーをインストールする準備ができました。 [スキャナーのインストール](#install-the-scanner)を続行します。

## <a name="install-the-scanner"></a>スキャナーのインストール

[Azure portal で Azure Information Protection スキャナーを構成](#configure-the-scanner-in-the-azure-portal)したら、次の手順を実行してスキャナーをインストールします。

1. スキャナーを実行する Windows Server コンピューターにサインインします。 ローカル管理者権限と SQL Server マスター データベースに書き込むためのアクセス許可を持つアカウントを使用します。

    > [!IMPORTANT]
    > 詳細については、「 [Azure Information Protection スキャナーをインストールおよび展開するための前提条件](deploy-aip-scanner-prereqs.md)」を参照してください。
    >
 
1. **[管理者として実行]** オプションを使用して Windows PowerShell セッションを開きます。

1. [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)コマンドレットを実行して、Azure Information Protection スキャナー用のデータベースを作成する SQL Server インスタンスと、前のセクションで指定したスキャナークラスター名を指定します。 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <cluster name>
    ```
    
    プロファイル名 **Europe** を使った例:
    
    - 既定のインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - 名前付きインスタンスの場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - SQL Server Express の場合: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    プロンプトが表示されたら、スキャナーサービスアカウントの資格情報 ( \<domain\user name> ) とパスワードを入力します。

1. **管理ツール**サービスを使用して、サービスがインストールされていることを確認し  >  **Services**ます。 
    
    インストールされているサービスの名前は **Azure Information Protection スキャナー**で、作成したスキャナー サービス アカウントを使用して実行するように構成されます。

スキャナーをインストールしたので、スキャナーを無人で実行できるように、スキャナーサービスアカウント[の Azure AD トークンを取得](#get-an-azure-ad-token-for-the-scanner)して認証する必要があります。 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>スキャナー用の Azure AD トークンを取得する

Azure AD トークンを使用すると、スキャナーは Azure Information Protection サービスに対して認証を行うことができます。

Azure AD トークンを取得するには:

1. Azure portal に戻り、認証用のアクセストークンを指定する Azure AD アプリケーションを作成します。 このトークンを使用すると、スキャナーを非対話形式で実行できます。 詳細については、「 [Azure Information Protection のために非対話形式でファイルにラベルを付ける方法](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」を参照してください。

2. Windows Server コンピューターから、スキャナーサービスアカウントにインストールの**ローカルログオン**権限が付与されている場合は、このアカウントでサインインし、PowerShell セッションを開始します。 

    前の手順でコピーした値を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行します。
    
    ```ps
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
        
    次に例を示します。

    ```ps
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
    Acquired application access token on behalf of CONTOSO\scanner.
    ```

> [!TIP]
> スキャナーサービスアカウントにインストールの**ローカルログオン**権限が付与されていない場合は、「 [Azure Information Protection のために非対話形式でファイルにラベルを付ける方法](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」で説明されているように、 [Set-aipauthentication](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipauthentication)で*OnBehalfOf*パラメーターを使用します。

スキャナーには Azure AD に対して認証するためのトークンが用意されています。これは、Azure AD の**Web アプリ/API**クライアントシークレットの構成に従って、1年間、2年間、またはそれ以上に有効です。 

トークンの有効期限が切れると、この手順を繰り返す必要があります。

これで、最初のスキャンを検索モードで実行する準備ができました。 詳細については、「[検出サイクルの実行とスキャナーのレポートの表示](deploy-aip-scanner-manage.md#run-a-discovery-cycle-and-view-reports-for-the-scanner)」を参照してください。

検出スキャンを既に実行している場合は、引き続き[分類と保護を適用するようにスキャナーを構成](#configure-the-scanner-to-apply-classification-and-protection)します。

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>スキャナーを構成して分類と保護を適用する

既定の設定では、スキャナーが1回だけ実行され、レポート専用モードで実行されるように構成されています。

これらの設定を変更するには、コンテンツスキャンジョブを編集します。

1. Azure portal の [ **Azure Information Protection-コンテンツスキャンジョブ**] ウィンドウで、クラスターとコンテンツスキャンジョブを選択して編集します。

2. [コンテンツスキャンジョブ] ウィンドウで、次のように変更し、[**保存**] を選択します。
    
   - **コンテンツスキャンジョブ**セクション:**スケジュール**を**常**に変更する
   - [**ポリシーの適用**] セクションから: [**適用**先] を **[オン**] に変更します。
    
    > [!TIP]
    > ファイルの属性を変更するかどうかや、スキャナーがファイルのラベルを変更できるかどうかなど、このウィンドウの他の設定を変更することもできます。 情報のポップアップ ヘルプを使って、各構成設定について詳しく学習してください。

3. 現在の時刻をメモし、[ **Azure Information Protection-コンテンツスキャンジョブ**] ウィンドウからもう一度スキャナーを起動します。

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Azure Information Protection スキャナーのスキャンを開始する":::
    
    または、PowerShell セッションで次のコマンドを実行します。
    
    ```ps
    Start-AIPScan
    ```

これで、スキャナーが継続的に実行されるようにスケジュールされました。 スキャナーは、構成されたすべてのファイルを介して動作するときに、新しいファイルと変更されたファイルが検出されるように、新しいサイクルを自動的に開始します。

## <a name="change-which-file-types-to-protect"></a>保護するファイルの種類を変更する

既定では、AIP スキャナーは Office ファイルの種類と PDF ファイルのみを保護します。

PowerShell コマンドを使用して、必要に応じてこの動作を変更します。たとえば、すべてのファイルの種類を保護するようにスキャナーを構成したり、クライアントと同様に、またはその他の特定のファイルの種類を保護したりします。 

スキャナーのラベルをダウンロードするユーザーアカウントに適用されるラベルポリシーについては、 **PFileSupportedExtensions**という名前の PowerShell の詳細設定を指定します。 

インターネットにアクセスできるスキャナーの場合、このユーザーアカウントは、 *DelegatedUser*パラメーターに指定するアカウントで、Set-AIPAuthentication コマンドを使用します。

**例 1:** ラベルポリシーが "Scanner" という名前のすべてのファイルの種類を保護するためのスキャナーの PowerShell コマンド:

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

**例 2:** Office ファイルと PDF ファイルに加えて .xml ファイルと tiff ファイルを保護するためのスキャナー用の PowerShell コマンド。ラベルポリシーには "Scanner" という名前が付けられています。

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}
```

詳細については、「[保護するファイルの種類を変更](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)する」を参照してください。

## <a name="upgrading-your-scanner"></a>スキャナーをアップグレードする
 
以前にスキャナーをインストールし、アップグレードする場合は、 [Azure Information Protection スキャナーのアップグレード](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)に関するページに記載されている手順に従ってください。

次に、スキャナーを通常どおりに[構成](deploy-aip-scanner-configure-install.md)して[使用](deploy-aip-scanner-manage.md)し、スキャナーをインストールする手順をスキップします。

## <a name="editing-data-repository-settings-in-bulk"></a>データリポジトリ設定の一括編集

複数のリポジトリでスキャナーを変更するには、[**エクスポート**] ボタンと [**インポート**] ボタンを使用します。 

このようにして、Azure portal で同じ変更を何度も手動で行う必要はありません。

たとえば、複数の SharePoint データリポジトリに新しいファイルの種類がある場合は、それらのリポジトリの設定を一括で更新することができます。

リポジトリ間で一括変更を行うには、次のようにします。

1. [**リポジトリ**] ウィンドウの Azure portal で、[**エクスポート**] オプションを選択します。 次に例を示します。

    :::image type="content" source="media/export-scanner-repositories.png" alt-text="Azure Information Protection スキャナーのデータリポジトリ設定をエクスポートしています":::

1. エクスポートしたファイルを手動で編集して変更を行います。 

1. 同じページの [**インポート**] オプションを使用して、リポジトリ間で更新を再びインポートします。

## <a name="using-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーの使用

通常、Azure Information Protection スキャナーは、必要に応じてコンテンツを分類して保護するために、ラベルに指定された条件を検索します。

次のシナリオでは、Azure Information Protection スキャナーがコンテンツをスキャンしてラベルを管理することもできます。条件を構成する必要はありません。

- [データリポジトリ内のすべてのファイルに既定のラベルを適用する](#apply-a-default-label-to-all-files-in-a-data-repository)
- [データリポジトリ内のすべてのファイルから既存のラベルを削除する](#remove-existing-labels-from-all-files-in-a-data-repository)
- [すべてのカスタム条件と既知の機密情報の種類を識別する](#identify-all-custom-conditions-and-known-sensitive-information-types)
### <a name="apply-a-default-label-to-all-files-in-a-data-repository"></a>データリポジトリ内のすべてのファイルに既定のラベルを適用する

この構成では、リポジトリ内のラベルのないすべてのファイルに、リポジトリまたはコンテンツスキャンジョブに指定された既定のラベルが付けられます。 ファイルには検査なしでラベルが付けられます。 

次の設定を構成します。 

|設定  |[説明]  |
|---------|---------|
|**コンテンツに基づいてファイルにラベルを付ける**    |**Off**に設定         |
|**既定のラベル**     | [**カスタム**] に設定し、使用するラベルを選択します。       |
|**既定のラベルを適用する**     | 既定のラベルが既にラベル付けされている場合でも、すべてのファイルに適用されるようにする場合に選択します。        |
| | |

### <a name="remove-existing-labels-from-all-files-in-a-data-repository"></a>データリポジトリ内のすべてのファイルから既存のラベルを削除する

この構成では、保護がラベルと共に適用された場合、既存のすべてのラベルが保護を含めて削除されます。 ラベルとは無関係に適用される保護が保持されます。

次の設定を構成します。 

|設定  |[説明]  |
|---------|---------|
|**コンテンツに基づいてファイルにラベルを付ける**    |**Off**に設定         |
|**既定のラベル**     | **[なし**] に設定  |
|**ファイルのラベルを再付けする** | [**既定のラベルを強制**する] チェックボックスをオンにして、 **[オン**] に設定します。|
| | |

### <a name="identify-all-custom-conditions-and-known-sensitive-information-types"></a>すべてのカスタム条件と既知の機密情報の種類を識別する

この構成を使用すると、スキャナーのスキャンレートが低下した場合に気付いていない機密情報を見つけることができます。 

[**探索する情報の種類**] を [**すべて**] に設定します。 

ラベル付けの条件と情報の種類を識別するために、スキャナーは、指定されたカスタムの機密情報の種類と、ラベル付け管理センターで定義されている、選択できる組み込みの機密情報の種類の一覧を使用します。

## <a name="optimizing-scanner-performance"></a>スキャナーのパフォーマンスの最適化

> [!NOTE]
> スキャナーのパフォーマンスではなく、スキャナーコンピューターの応答性を向上させる場合は、高度なクライアント設定を使用し[て、スキャナーが使用するスレッドの数を制限](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)します。
> 

スキャナーのパフォーマンスを最適化するには、次のオプションとガイダンスを参考にしてください。

|オプション  |説明  |
|---------|---------|
|**スキャナー コンピューターとスキャンされたデータ ストア間のネットワーク接続を高速かつ信頼性の高い接続にする**     |  たとえば、スキャナーコンピューターを同じ LAN、または可能であれば、スキャンしたデータストアと同じネットワークセグメントに配置します。 </br></br>ネットワーク接続の品質はスキャナーのパフォーマンスに影響します。これは、ファイルを検査するために、スキャナーがファイルの内容をスキャナーサービスを実行しているコンピューターに転送するためです。 </br></br>データの移動に必要なネットワークホップを減らしたり、削除したりすると、ネットワークの負荷も軽減されます。      |
|**スキャナー コンピューターに利用可能なプロセッサ リソースがあることを確認する**     | ファイルの内容の検査とファイルの暗号化と復号化は、プロセッサを集中的に処理する操作です。 </br></br>指定されたデータストアの一般的なスキャンサイクルを監視し、プロセッサリソースの不足がスキャナーのパフォーマンスに悪影響を与えていないかどうかを特定します。        |
|**スキャナーの複数のインスタンスをインストールする** | スキャナーにカスタムクラスター (プロファイル) 名を指定した場合、Azure Information Protection スキャナーは、同じ SQL server インスタンス上の複数の構成データベースをサポートします。 </br></br>複数のスキャナーで同じクラスター (プロファイル) を共有することもでき、その結果、スキャン時間が短縮されます。|
|**別の構成の使用方法を確認する** |[代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのファイルに既定のラベルを適用すると、ファイル内容の検査がスキップされるため、スキャナーの実行速度が速くなります。 <br/></br>[代替構成](#using-the-scanner-with-alternative-configurations)を使ってすべてのカスタム条件と既知の機密情報の種類を特定すると、スキャナーの実行速度が遅くなりなります。|
| | |

<!-- removed when removing local folders
|**Do not scan local folders on the computer running the scanner service**     | If you have folders to scan on a Windows server, install the scanner on a different computer and configure those folders as network shares to scan. </br></br>Separating the two functions of hosting files and scanning files means that the computing resources for these services are not competing with one another.        |
-->

### <a name="additional-factors-that-affect-performance"></a>パフォーマンスに影響するその他の要因

スキャナーのパフォーマンスに影響するその他の要因は次のとおりです。

|要素  |説明  |
|---------|---------|
|**読み込み/応答時間**     |スキャンするファイルが含まれているデータストアの現在の負荷と応答時間は、スキャナーのパフォーマンスにも影響します。         |
|**スキャナーモード**(検出/強制)    | 通常、検出モードは、強制モードよりも高いスキャンレートを持ちます。 </br></br>検出には1つのファイル読み取り操作が必要ですが、強制モードでは読み取りと書き込みの操作が必要です。        |
|**ポリシーの変更**     |ラベルポリシーで autolabeling を変更した場合、スキャナーのパフォーマンスが影響を受ける可能性があります。 </br></br>最初のスキャンサイクルでは、スキャナーがすべてのファイルを検査する必要があるときに、既定では、新しいファイルと変更されたファイルのみを検査する後続のスキャンサイクルよりも時間がかかります。 </br></br>条件または autolabeling の設定を変更すると、すべてのファイルが再度スキャンされます。 詳細については、「ファイルの再[スキャン](deploy-aip-scanner-manage.md#rescanning-files)」を参照してください。|
|**Regex の構造**    | スキャナーのパフォーマンスは、カスタム条件の regex 式がどのように構築されるかによって影響を受けます。 </br></br> メモリの大量消費とタイムアウト (1 ファイルあたり 15 分) のリスクを回避するには、ご利用の正規表現式を確認して効率的なパターン マッチングが行われているかを確認してください。 </br></br>次に例を示します。 </br>-[最長一致の量指定子](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)を避けます。 </br>-の代わりに、のような非キャプチャグループを使用し `(?:expression)` ます。`(expression)`    |
|**ログ レベル**     |  ログレベルのオプションには、スキャナーレポートの [**デバッグ**]、[**情報**]、[**エラー** ]、[**オフ**] があります。</br></br>- **オフ**にすると最適なパフォーマンスが得られる </br>- **デバッグ**によってスキャナーの速度が大幅に低下するため、トラブルシューティングにのみ使用してください。 </br></br>詳細については、[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) コマンドレットの *ReportLevel* パラメーターを参照してください。       |
|**スキャンされるファイル**     |-Excel ファイルを除き、Office ファイルは PDF ファイルよりもすばやくスキャンされます。 </br></br>-保護されていないファイルは、保護されたファイルよりもスキャンが高速です。 </br></br>-大きなファイルは、小さいファイルよりもスキャンに時間がかかることが明らかです。         |
| | |

## <a name="list-of-cmdlets-for-the-scanner"></a>スキャナーのコマンドレットの一覧

このセクションでは、Azure Information Protection スキャナーでサポートされている PowerShell コマンドレットの一覧を示します。

> [!NOTE]
> Azure Information Protection スキャナーは、Azure portal から構成されます。 このため、以前のバージョンで使用されていた、データリポジトリとスキャンされたファイルの種類の一覧を構成するコマンドレットは非推奨となりました。
> 

スキャナーでサポートされているコマンドレットは次のとおりです。

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Export-Ai: Gs](/powershell/module/azureinformationprotection/Export-AIPLogs)

- [インポート-Aipscanの構成](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [開始-AIPScanDiagnostics](/powershell/module/azureinformationprotection/Start-AIPScanDiagnostics)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [停止-AIPScan](/powershell/module/azureinformationprotection/Stop-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)

## <a name="next-steps"></a>次のステップ

スキャナーのインストールと構成が完了したら、[ファイルのスキャン](deploy-aip-scanner-manage.md)を開始します。

「[ファイルを自動的に分類して保護するための Azure Information Protection スキャナーの展開](deploy-aip-scanner.md)」も参照してください。

**詳細情報:**

- Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

- [Windows Server FCI と Azure Information Protection スキャナーの違いは何ですか](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)。

- PowerShell を使用して、デスクトップコンピューターから対話形式でファイルを分類および保護します。 PowerShell を使用するその他のシナリオの詳細については、「 [Azure Information Protection の統合ラベル付けクライアントでの powershell の使用](./rms-client/clientv2-admin-guide-powershell.md)」を参照してください。
