---
title: Azure Information Protection (AIP) 統合スキャナーの前提条件のラベル付け
description: Azure Information Protection 統合されたラベル付けスキャナーをインストールして展開するための前提条件を示します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3f0093e2877ffe15232ed5704dcf2567b8ed99c4
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164183"
---
# <a name="requirements-for-installing-and-deploying-the-azure-information-protection-unified-labeling-scanner"></a>Azure Information Protection 統合ラベルスキャナーをインストールおよび展開するための要件

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***関連**: [AIP 統合ラベルクライアントのみ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 従来のクライアントについては、「[従来のクライアントスキャナーの前提条件](deploy-aip-scanner-prereqs-classic.md)」を参照してください。*

オンプレミスの Azure Information Protection スキャナーをインストールする前に、システムが基本的な [Azure Information Protection の要件](requirements.md)を満たしていることを確認してください。

また、スキャナーに固有の要件は次のとおりです。

- [Windows Server の要件](#windows-server-requirements)
- [サービス アカウントの要件](#service-account-requirements)
- [SQL server の要件](#sql-server-requirements)
- [Azure Information Protection クライアントの要件](#azure-information-protection-client-requirements)
- [構成要件のラベル](#label-configuration-requirements)
- [SharePoint の要件](#sharepoint-requirements)
- [Microsoft Office の要件](#microsoft-office-requirements)
- [ファイルパスの要件](#file-path-requirements)
- [使用状況の統計情報の要件](#usage-statistics-requirements)

組織のポリシーによって禁止されているため、スキャナーに記載されているすべての要件を満たすことができない場合は、「 [代替構成](#deploying-the-scanner-with-alternative-configurations) 」セクションを参照してください。

スキャナーを運用環境にデプロイする場合、または複数のスキャナーのパフォーマンスをテストする場合は、「 [SQL Server のための記憶域の要件と容量計画](#storage-requirements-and-capacity-planning-for-sql-server)」を参照してください。

スキャナーのインストールと展開を開始する準備ができたら、 [Azure Information Protection スキャナーの展開を続けて、ファイルを自動的に分類して保護](deploy-aip-scanner-configure-install.md)します。

## <a name="windows-server-requirements"></a>Windows Server の要件

スキャナーを実行するには、次のシステム仕様の Windows Server コンピューターが必要です。

|仕様  |詳細  |
|---------|---------|
|**プロセッサ**     |4コアプロセッサ         |
|**RAM**     |8 GB         |
|**ディスク領域**     |一時ファイルの 10 GB の空き領域 (平均)。 </br></br>スキャナーは、スキャンする各ファイル用に、コアごとに 4 つの一時ファイルを作成するために、十分なディスク領域を必要とします。 </br></br>推奨される 10 GB のディスク領域を使用すると、4 コア プロセッサで、それぞれのサイズが 625 MB であるファイルを 16 個スキャンできます。
|**オペレーティング システム**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**注**: 非運用環境でテストまたは評価を行う場合は、 [Azure Information Protection クライアントでサポート](requirements.md#client-devices)されている任意の Windows オペレーティングシステムを使用することもできます。
|**ネットワーク接続**     | スキャナーコンピューターは、スキャンするデータストアへの高速で信頼性の高いネットワーク接続がある物理コンピューターまたは仮想コンピューターにすることができます。 </br></br> 組織のポリシーのためにインターネット接続ができない場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」を参照してください。 </br></br>それ以外の場合は、このコンピューターがインターネットに接続されていることを確認し、HTTPS 経由で次の Url を使用できるようにします (ポート 443)。</br><br />-  \*. aadrm.com <br />-  \*. azurerms.com<br />-  \*. informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*. aria.microsoft.com <br />-  \*. protection.outlook.com |
|**NFS 共有** |NFS 共有のスキャンをサポートするには、スキャナーコンピューターに NFS 用サービスを展開する必要があります。 <br><br>コンピューターで、[ **windows の機能] ([windows の機能の有効化または無効化)** の設定] ダイアログボックスに移動し、[ **nfs 用サービス**]  >  **管理ツール** と **nfs クライアント** を選択します。 |
| | |

## <a name="service-account-requirements"></a>サービス アカウントの要件

Windows Server コンピューターでスキャナーサービスを実行するには、サービスアカウントが必要です。また、Azure AD を認証し、Azure Information Protection ポリシーをダウンロードする必要があります。

サービスアカウントは Active Directory アカウントであり、Azure AD に同期されている必要があります。

組織のポリシーのためにこのアカウントを同期できない場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」を参照してください。

このサービス アカウントには次の要件があります。

|要件  |詳細  |
|---------|---------|
|**ローカルログオン** ユーザー権利の割り当て     |スキャナーのインストールと構成に必要ですが、スキャンの実行には必要ありません。  </br></br>スキャナーがファイルを検出、分類、保護できることを確認したら、サービスアカウントからこの権限を削除できます。  </br></br>組織のポリシーにより、この権限を短時間でも付与できない場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」を参照してください。         |
|**[サービスとしてログオン]** ユーザー権限の割り当て。     |  この権限は、スキャナーのインストール中にサービス アカウントに自動的に付与され、スキャナーのインストール、構成、操作に必要です。        |
|**データリポジトリに対するアクセス許可**     |- **ファイル共有またはローカルファイル**: ファイルをスキャンし、構成どおりに分類と保護を適用するための **読み取り**、 **書き込み**、 **変更** のアクセス許可を付与します。  <br /><br />- **SharePoint**: ファイルをスキャンして、Azure Information Protection ポリシーの条件を満たすファイルに分類と保護を適用するには、 **フルコントロール** アクセス許可を付与する必要があります。  <br /><br />- **検出モード**: 検出モードでのみスキャナーを実行するには、 **読み取り** アクセス許可で十分です。         |
|**保護を再保護または削除するラベルの場合**     | スキャナーが常に保護されたファイルにアクセスできるようにするには、このアカウントを Azure Information Protection の [スーパーユーザー](configure-super-users.md) にして、スーパーユーザー機能が有効になっていることを確認します。 </br></br>さらに、段階的展開の [オンボードコントロール](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) を実装している場合は、構成したオンボードコントロールにサービスアカウントが含まれていることを確認してください。|
|**特定の URL レベルのスキャン**: |[特定の URL で](#deploying-the-scanner-with-alternative-configurations)サイトおよびサブサイトをスキャンして検出するには、ファームレベルのスキャナーアカウントに **サイトコレクターの監査** 者権限を付与します。|
| | |

## <a name="sql-server-requirements"></a>SQL server の要件

スキャナー構成データを格納するには、次の要件を持つ SQL server を使用します。

- **ローカルまたはリモートのインスタンス。**

    小規模なデプロイを使用している場合を除き、SQL server とスキャナーサービスを異なるコンピューターでホストすることをお勧めします。 また、スキャナーデータベースのみを提供し、他のアプリケーションと共有されない専用の SQL インスタンスを用意することをお勧めします。

    共有サーバーで作業している場合は、スキャナーデータベースが動作するために、推奨される [コア数](#windows-server-requirements) が無料であることを確認してください。

    SQL Server 2016 は、次のエディションの最小バージョンです。

    - SQL Server Enterprise

    - SQL Server Standard

    - SQL Server Express (テスト環境にのみ推奨)

- **スキャナーをインストールする Sysadmin ロールを持つアカウント。**

    Sysadmin ロールを使用すると、インストールプロセスでスキャナー構成データベースを自動的に作成し、必要な **db_owner** の役割を、スキャナーを実行するサービスアカウントに付与できます。

    Sysadmin ロールが付与されていない場合、または組織のポリシーでデータベースを手動で作成して構成する必要がある場合は、「 [代替構成を使用したスキャナーの展開](#deploying-the-scanner-with-alternative-configurations)」を参照してください。

- **容量。** 容量のガイダンスについては、「 [SQL Server のストレージ要件と容量計画](#storage-requirements-and-capacity-planning-for-sql-server)」を参照してください。

- **[大文字と小文字を区別しない照合順序](/sql/relational-databases/collations/collation-and-unicode-support)。**

> [!NOTE]
> スキャナーにカスタムクラスター名を指定した場合、またはプレビューバージョンのスキャナーを使用している場合は、同じ SQL server 上の複数の構成データベースがサポートされます。
>
### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>SQL Server のストレージ要件と容量計画

スキャナーの構成データベースに必要なディスク領域と、SQL Server を実行しているコンピューターの仕様は環境によって異なる場合があるため、独自のテストを行うことをお勧めします。 次のガイダンスを出発点として使用してください。

詳細については、「 [スキャナーのパフォーマンスの最適化](deploy-aip-scanner-configure-install.md#optimizing-scanner-performance)」を参照してください。

スキャナー構成データベースのディスクサイズは、展開ごとに異なります。 ガイダンスとして、次の式を使用します。

```cli
100 KB + <file count> *(1000 + 4* <average file name length>)
```

たとえば、ファイル名の長さが平均250バイトの100万ファイルをスキャンするには、2 GB のディスク領域を割り当てます。

複数のスキャナーの場合:

- **最大10台のスキャナー** を使用します。

    - 4コアプロセッサ
    - 8 GB の RAM を推奨

- **10 台を超えるスキャナー** (最大 40) を使用します。
    - 8コアプロセス
    - 16 GB の RAM を推奨

## <a name="azure-information-protection-client-requirements"></a>Azure Information Protection クライアントの要件

Azure Information Protection クライアントの現在の [一般公開バージョン](./rms-client/unifiedlabelingclient-version-release-history.md) が Windows Server コンピューターにインストールされている必要があります。

詳細については、「 [クライアント管理者向けの統合ガイド](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner)」を参照してください。

> [!IMPORTANT]
> スキャナーに対する完全なクライアントをインストールする必要があります。 PowerShell モジュールだけで、クライアントをインストールしないでください。
>

## <a name="label-configuration-requirements"></a>構成要件のラベル

スキャナーアカウントの管理センターにラベルを付け、分類を適用し、必要に応じて保護を適用するには、少なくとも1つの秘密度ラベルを Microsoft 365 構成する必要があります。

管理センターにラベルを付ける Microsoft 365 には、Microsoft 365 Security Center、Microsoft 365 コンプライアンスセンター、Microsoft 365 セキュリティとコンプライアンスセンターが含まれます。 

*スキャナーアカウント* は、DelegatedUser [コマンドレットの](/powershell/module/azureinformationprotection/set-aipauthentication) パラメーターで指定するアカウントで、スキャナーの構成時に実行されます。 

ラベルに自動ラベル付けの条件がない場合は、以下 [の代替構成の手順](#restriction-your-labels-do-not-have-auto-labeling-conditions) を参照してください。

詳細については、次を参照してください。

- [秘密度ラベルについて](/microsoft-365/compliance/sensitivity-labels)
- [機密ラベルをコンテンツに自動的に適用する](/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [機密ラベルの暗号化を使用してコンテンツへのアクセスを制限する](/microsoft-365/compliance/encryption-sensitivity-labels)
- [Azure Information Protection 統合ラベルスキャナーの構成とインストール](deploy-aip-scanner-configure-install.md)

## <a name="sharepoint-requirements"></a>SharePoint の要件

SharePoint ドキュメントライブラリおよびフォルダーをスキャンするには、SharePoint サーバーが次の要件を満たしていることを確認します。

|要件  |説明  |
|---------|---------|
|**サポートされているバージョン** | サポートされているバージョンは、SharePoint 2019、SharePoint 2016、および SharePoint 2013 です。 <br> スキャナーでは SharePoint の他のバージョンはサポートされていません。     |
|**バージョン管理**     |  [バージョン管理](/sharepoint/governance/versioning-content-approval-and-check-out-planning)を使用すると、スキャナーは最後に発行されたバージョンを検査してラベルを付けます。 <br><br>スキャナーがファイルと [コンテンツの承認](/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) を必要とする場合は、そのラベルの付いたファイルをユーザーが使用できるように承認する必要があります。       |
|**大規模な SharePoint ファーム** |大規模な SharePoint ファームの場合は、スキャナーがすべてのファイルにアクセスするために、リスト ビューのしきい値 (既定では 5,000) を増やす必要があるかどうかを確認します。 <br><br>詳細については、「 [SharePoint での大規模なリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。 |
|**長いファイルパス**  |SharePoint に長いファイルパスがある場合は、SharePoint サーバーの HttpRuntime の [maxUrlLength](/dotnet/api/system.web.configuration.httpruntimesection.maxurllength) 値が既定の260文字より大きいことを確認します。 <br><br>詳細については、「 [SharePoint でのスキャナータイムアウトの回避](rms-client/clientv2-admin-guide-customizations.md#avoid-scanner-timeouts-in-sharepoint)」を参照してください。 | 
| | |

## <a name="microsoft-office-requirements"></a>Microsoft Office の要件

Office ドキュメントをスキャンするには、ドキュメントは次のいずれかの形式である必要があります。

- Microsoft Office 97-2003
- Word、Excel、PowerPoint 用の Office Open XML 形式

詳細については、「 [Azure Information Protection の統合ラベル付けクライアントでサポートされるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md)」を参照してください。

## <a name="file-path-requirements"></a>ファイルパスの要件

既定では、ファイルをスキャンするには、ファイルパスの最大文字数が260文字である必要があります。

260文字を超えるファイルパスを使用してファイルをスキャンするには、次のいずれかのバージョンの Windows がインストールされているコンピューターにスキャナーをインストールし、必要に応じてコンピューターを構成します。

|Windows Version  |説明  |
|---------|---------|
|**Windows 2016 以降**     |   長いパスをサポートするようにコンピューターを構成する      |
|**Windows 10 または Windows Server 2016**     | 次の [グループポリシー設定](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)を定義します。**ローカルコンピューターポリシー**  >  **コンピューターの構成**  >  **管理用テンプレート**  >  **すべての設定** で、  >  **Win32 の長いパスを有効に** します。    </br></br>これらのバージョンでのファイルパスのサポートの詳細については、Windows 10 開発者ドキュメントの「 [パスの最大長の制限](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) 」セクションを参照してください。    |
|**Windows 10 バージョン 1607 以降**     |  更新された **MAX_PATH** 機能を選択します。 詳細については、「 [Windows 10 バージョン1607以降での長いパスの有効化](/windows/win32/fileio/naming-a-file#enable-long-paths-in-windows-10-version-1607-and-later)」を参照してください。      |
| | |

## <a name="usage-statistics-requirements"></a>使用状況の統計情報の要件

次のいずれかの方法を使用して使用状況の統計を無効にします。

- [Allowtelemetry](./rms-client/client-admin-guide-install.md#to-install-the-azure-information-protection-client-by-using-the-executable-installer)パラメーターを0に設定しています

- スキャナーのインストールプロセス中に、[ **使用状況の統計を Microsoft に送信して Azure Information Protection を改善** する] オプションが選択されていないことを確認します。

## <a name="deploying-the-scanner-with-alternative-configurations"></a>代替構成でのスキャナーのデプロイ

上記の前提条件は、スキャナー展開の既定の要件であり、最も単純なスキャナー構成をサポートしているため推奨されています。

既定の要件は、初期テストに適しているため、スキャナーの機能を確認できます。

ただし、運用環境では、組織のポリシーが既定の要件と異なる場合があります。 スキャナーでは、追加の構成によって次の変更を行うことができます。

- [特定の URL の下にあるすべてのサイトとサブサイトを検出してスキャンする](#discover-and-scan-all-sharepoint-sites-and-subsites-under-a-specific-url)

- [制限: スキャナーサーバーはインターネットに接続できません](#restriction-the-scanner-server-cannot-have-internet-connectivity)

- [制限: スキャナーサービスアカウントを Azure Active Directory に同期することはできませんが、サーバーがインターネットに接続しています](#restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity)

- [制限: スキャナーのサービスアカウントに **ローカルログオン** 権限を付与することはできません](#restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right)

- [制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある](#restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually)

- [制限: ラベルにオートラベルの条件がありません](#restriction-your-labels-do-not-have-auto-labeling-conditions)

### <a name="discover-and-scan-all-sharepoint-sites-and-subsites-under-a-specific-url"></a>特定の URL の下にある Sharepoint サイトとサブサイトをすべて検出してスキャンする

スキャナーは、次の構成を使用して、特定の URL の下にあるすべての Sharepoint サイトおよびサブサイトを検出し、スキャンできます。

1. **SharePoint サーバーの全体管理** を開始します。

1. **SharePoint サーバーの全体管理** web サイトの [**アプリケーション管理**] セクションで、[ **web アプリケーションの管理**] をクリックします。

1. 管理するアクセス許可ポリシーレベルを持つ web アプリケーションをクリックして強調表示します。

1. 関連するファームを選択し、[ **アクセス許可ポリシーレベルの管理**] を選択します。

1. サイトコレクションの **アクセス許可** のオプションで [**サイトコレクションの監査** 者] を選択し、[アクセス許可] の一覧で [**アプリケーションページの表示**] を許可します。最後に、新しいポリシーレベルとして「 **AIP scanner Site Collection 監査者とビューアー**」という名前を指定します。

1. 新しいポリシーにスキャナーユーザーを追加し、アクセス許可の一覧に **サイトコレクション** を付与します。   

1. スキャンする必要があるサイトまたはサブサイトをホストする SharePoint の URL を追加します。 詳細については、「 [Azure portal でのスキャナーの構成](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal)」を参照してください。

SharePoint ポリシーレベルを管理する方法の詳細については、「 [web アプリケーションのアクセス許可ポリシーを管理](/sharepoint/administration/manage-permission-policies-for-a-web-application)する」を参照してください。

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>制限: スキャナーサーバーはインターネットに接続できません

統一されたラベル付けクライアントは、インターネット接続を使用せずに保護を適用できませんが、インポートされたポリシーに基づいてラベルを適用することはできます。

切断されたコンピューターをサポートするには、次のいずれかの方法を使用します。

- [Azure portal を使用](#use-the-azure-portal-with-a-disconnected-computer) する (可能な場合は推奨)

- [PowerShell の使用](#use-powershell-with-a-disconnected-computer)

#### <a name="use-the-azure-portal-with-a-disconnected-computer"></a>切断されたコンピューターで Azure portal を使用する

Azure portal から切断されたコンピューターをサポートするには、次の手順を実行します。

1.  ポリシーのラベルを構成し、切断された [コンピューターをサポートする手順](rms-client/clientv2-admin-guide-customizations.md#support-for-disconnected-computers) を使用して、オフラインでの分類とラベル付けを有効にします。

1. 次のように、コンテンツおよびネットワークスキャンジョブのオフライン管理を有効にします。

    **コンテンツスキャンジョブのオフライン管理を有効にする**:

    1. スキャナーを **オフライン** モードで機能するように設定するには、 [Set-Aipscanの configuration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) コマンドレットを使用します。

    1. スキャナークラスターを作成して、Azure portal でスキャナーを構成します。 詳細については、「 [Azure portal でのスキャナーの構成](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal)」を参照してください。

    1. [**エクスポート**] オプションを使用して、[ **Azure Information Protection コンテンツスキャンジョブ**] ウィンドウからコンテンツジョブをエクスポートします。
    
    1. [インポート](/powershell/module/azureinformationprotection/import-aipscannerconfiguration)コマンドレットを使用して、ポリシーをインポートします。 
    
    オフラインコンテンツスキャンジョブの結果は次の場所にあります: **%localappdata%\Microsoft\MSIP\Scanner\Reports**
    
    **ネットワークスキャンジョブのオフライン管理を有効にする**:

    1. ネットワーク探索サービスをオフラインモードで機能するように設定するには、 [MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/set-mipnetworkdiscoveryconfiguration) コマンドレットを使用します。

    1. Azure portal でネットワークスキャンジョブを構成します。 詳細については、「 [ネットワークスキャンジョブの作成](deploy-aip-scanner-configure-install.md#creating-a-network-scan-job)」を参照してください。
    
    1. [**エクスポート**] オプションを使用して、[ **Azure Information Protection-ネットワークスキャンジョブ (プレビュー)** ] ウィンドウからネットワークスキャンジョブをエクスポートします。 
    
    1.  [MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/import-mipnetworkdiscoveryconfiguration)コマンドレットを使用して、クラスター名と一致するファイルを使用してネットワークスキャンジョブをインポートします。  
    
    オフラインのネットワークスキャンジョブの結果は次の場所にあります: **%localappdata%\Microsoft\MSIP\Scanner\Reports**

#### <a name="use-powershell-with-a-disconnected-computer"></a>接続されていないコンピューターで PowerShell を使用する

切断されたコンピューターを PowerShell を使用してのみサポートするには、次の手順を実行します。

> [!IMPORTANT]
> [Azure 中国の 21vianet](/microsoft-365/admin/services-in-china/parity-between-azure-information-protection#manage-azure-information-protection-content-scan-jobs)の管理者は、コンテンツのスキャンジョブを管理するために、この手順を使用する *必要があり* ます。
> 

**PowerShell のみを使用してコンテンツスキャンジョブを管理し** ます。

1. スキャナーを **オフライン** モードで機能するように設定するには、 [Set-Aipscanの configuration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) コマンドレットを使用します。

1. [AIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-aipscannercontentscanjob)コマンドレットを使用して新しいコンテンツスキャンジョブを作成し、必ず必須パラメーターを使用し `-Enforce On` ます。

1. 追加するリポジトリのパスと共に、 [Add Aipscanを](/powershell/module/azureinformationprotection/add-aipscannerrepository) 使用してリポジトリを追加します。

    > [!TIP]
    > リポジトリがコンテンツスキャンジョブから設定を継承しないようにするには、 `OverrideContentScanJob On` パラメーターと追加設定の値を追加します。
    >
    > 既存のリポジトリの詳細を編集するには、 [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository) コマンドを使用します。
    >
 
1. [AIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-aipscannercontentscanjob)および[Get-aipscan](/powershell/module/azureinformationprotection/get-aipscannerrepository)コマンドレットを使用して、コンテンツスキャンジョブの現在の設定に関する情報を返します。 

1. 既存のリポジトリの詳細を更新するには、 [Set-Aipscanを](/powershell/module/azureinformationprotection/set-aipscannerrepository) 使用します。

1. 必要に応じて、 [Start-AIPScan](/powershell/module/azureinformationprotection/start-aipscan) コマンドレットを使用して、コンテンツスキャンジョブを直ちに実行します。 

    オフラインコンテンツスキャンジョブの結果は次の場所にあります: **%localappdata%\Microsoft\MSIP\Scanner\Reports**

1. リポジトリまたはコンテンツスキャンジョブ全体を削除する必要がある場合は、次のコマンドレットを使用します。

    - [AIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-aipscannercontentscanjob)
    - [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/remove-aipscannerrepository)

### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>制限: Sysadmin の付与が認められない、または手動でデータベースを作成し構成する必要がある

データベースを手動で作成し、必要に応じて **db_owner** ロールを付与するには、次の手順に従います。

- [スキャナーデータベースの手順](#manually-create-a-database-and-user-for-the-scanner-and-grant-db_owner-rights)
- [ネットワーク探索データベースの手順](#manually-create-a-database-and-user-for-the-network-discovery-service-and-grant-db_owner-rights)

スキャナーをインストールするために Sysadmin の役割を *一時的* に付与できる場合は、スキャナーのインストールが完了したらこの役割を削除できます。

組織の要件に応じて、次のいずれかの操作を行います。

|Restriction  |説明  |
|---------|---------|
|**Sysadmin ロールを一時的に持つことができます。**     |  Sysadmin ロールを一時的に持っている場合は、データベースが自動的に作成され、スキャナーのサービスアカウントに必要なアクセス許可が自動的に付与されます。 <br><br>ただし、スキャナーを構成するユーザーアカウントには、スキャナー構成データベースの **db_owner** ロールが必要です。 スキャナーのインストールが完了するまで Sysadmin の役割しかない場合は、ユーザーアカウントに **db_owner** の役割を手動で付与します。       |
|**Sysadmin ロールをまったく持つことはできません。**     |  Sysadmin ロールが一時的に付与されていない場合は、スキャナーをインストールする前に、データベースを手動で作成するための Sysadmin 権限をユーザーに要求する必要があります。 <br><br>この構成では、 **db_owner** ロールが次のアカウントに割り当てられている必要があります。 <br>-スキャナーのサービスアカウント<br>-スキャナーインストール用のユーザーアカウント<br>-スキャナー構成のユーザーアカウント <br><br>通常、スキャナーのインストールと構成には同じユーザー アカウントを使用します。 異なるアカウントを使用する場合は、どちらもスキャナー構成データベースの **db_owner** ロールが必要です。 必要に応じて、このユーザーと権限を作成します。 独自のクラスター名を指定した場合、構成データベースの名前は **cluster_name>AIPScannerUL_<** になります。  |
| | |

追加として:

- スキャナーを実行するサーバーのローカル管理者である必要があります。
- スキャナーを実行するサービスアカウントには、次のレジストリキーに対するフルコントロールのアクセス許可が付与されている必要があります。

    - `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server`
    - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server`

これらのアクセス許可を構成した後、スキャナーをインストールするときにエラーが表示される場合は、エラーを無視して、スキャナーサービスを手動で開始することができます。

#### <a name="manually-create-a-database-and-user-for-the-scanner-and-grant-db_owner-rights"></a>スキャナー用のデータベースとユーザーを手動で作成し、db_owner 権限を付与する

手動でスキャナーデータベースを作成したり、ユーザーを作成してデータベースに **db_owner** 権限を付与したりする必要がある場合は、次の手順を実行するように Sysadmin に依頼してください。

1. スキャナー用のデータベースを作成します。

    ```sql
    **CREATE DATABASE AIPScannerUL_[clustername]**

    **ALTER DATABASE AIPScannerUL_[clustername] SET TRUSTWORTHY ON**
    ```

2. インストールコマンドを実行するユーザーに権限を付与し、スキャナー管理コマンドを実行するために使用します。 次のスクリプトを実行します。

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. スキャナーサービスアカウントに権限を付与します。 次のスクリプトを実行します。

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```

#### <a name="manually-create-a-database-and-user-for-the-network-discovery-service-and-grant-db_owner-rights"></a>ネットワーク探索サービスのデータベースとユーザーを手動で作成し、db_owner 権限を付与する

[ネットワーク探索](deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview)データベースを手動で作成する必要がある場合、またはユーザーを作成してデータベースに **db_owner** 権限を付与する必要がある場合は、次の手順を実行するように Sysadmin に依頼してください。

1. ネットワーク探索サービスのデータベースを作成します。

    ```sql
    **CREATE DATABASE AIPNetworkDiscovery_[clustername]**

    **ALTER DATABASE AIPNetworkDiscovery_[clustername] SET TRUSTWORTHY ON**
    ```

2. インストールコマンドを実行するユーザーに権限を付与し、スキャナー管理コマンドを実行するために使用します。 次のスクリプトを実行します。

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. スキャナーサービスアカウントに権限を付与します。 次のスクリプトを実行します。

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```
### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>制限: スキャナーのサービス アカウントに **ローカル ログオン** 権限を付与できない

組織のポリシーでサービスアカウントに **ローカルでログオン** する権限が禁止されている場合は、Set-AIPAuthentication で *OnBehalfOf* パラメーターを使用します。

「[非対話形式でファイルに Azure Information Protection のラベル付けをする方法](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」を参照してください。

### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>制限: スキャナーサービスアカウントを Azure Active Directory に同期することはできませんが、サーバーがインターネットに接続しています

スキャナーのサービスを実行するために 1 つのアカウントを持ち、Azure Active Directory を認証するために別のアカウントを使用することができます。

- **スキャナーサービスアカウントの** 場合は、ローカルの Windows アカウントまたは Active Directory アカウントを使用します。

- **Azure Active Directory アカウントの** 場合は、Set-AIPAuthentication を使用して、 *OnBehalfOf* パラメーターのローカルアカウントを指定します。 「[非対話形式でファイルに Azure Information Protection のラベル付けをする方法](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」を参照してください。

### <a name="restriction-your-labels-do-not-have-auto-labeling-conditions"></a>制限: ラベルにオートラベルの条件がありません

ラベルに自動ラベルの条件がない場合は、スキャナーを構成するときに、次のいずれかのオプションを使用することを計画します。

|オプション  |説明  |
|---------|---------|
|**すべての情報の種類を検出**     |  [コンテンツスキャンジョブ](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)で、[情報の **種類**] を [検出済み]**に設定します。** </br></br>このオプションは、すべての機密情報の種類についてコンテンツをスキャンするようにコンテンツスキャンジョブを設定します。      |
|**推奨ラベルの使用**     |  [コンテンツスキャンジョブ](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)で、[**推奨ラベルを自動的** に処理する] オプションを **[オン**] に設定します。</br></br> この設定により、推奨されるすべてのラベルがコンテンツに自動的に適用されるようにスキャナーが構成されます。      |
|**既定のラベルを定義する**     |   [ポリシー](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do)、[コンテンツスキャンジョブ](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)、または[リポジトリ](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository)で既定のラベルを定義します。 </br></br>この場合、スキャナーは、見つかったすべてのファイルに既定のラベルを適用します。       |
| | |

## <a name="next-steps"></a>次のステップ

システムがスキャナーの前提条件に準拠していることを確認したら、 [Azure Information Protection スキャナーの展開を続けて、ファイルを自動的に分類して保護](deploy-aip-scanner-configure-install.md)します。

スキャナーの概要については、「 [ファイルを自動的に分類して保護するための Azure Information Protection スキャナーの展開](deploy-aip-scanner.md)」を参照してください。

**詳細情報**:

- Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

- また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 PowerShell を使用するその他のシナリオの詳細については、「 [Azure Information Protection の統合ラベル付けクライアントでの powershell の使用](./rms-client/clientv2-admin-guide-powershell.md)」を参照してください。