---
title: Azure Information Protection 統合されたラベル付けスキャナーについて-AIP
description: Azure Information Protection 統合されたラベル付けスキャナーの現在のバージョンをインストール、構成、および実行して、データストア上のファイルを検出、分類、および保護する方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a8c0d8ae4989a31029979c819ac6c59c390a8f3c
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382549"
---
# <a name="what-is-the-azure-information-protection-unified-labeling-scanner"></a>Azure Information Protection 統合ラベル付けスキャナーとは

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***関連**: [AIP 統合ラベルクライアントのみ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 クラシッククライアントについては、「 [Azure Information Protection クラシックスキャナーとは](deploy-aip-scanner-classic.md)」を参照してください。*

>[!NOTE] 
> クラウド リポジトリ上のファイルをスキャンおよびラベル付けするには、スキャナーの代わりに [Cloud App Security](/cloud-app-security/) を使用します。

このセクションの情報を使用して、Azure Information Protection 統合されたラベル付けスキャナーについて説明し、正常にインストール、構成、実行、必要に応じてトラブルシューティングを行う方法について説明します。

AIP スキャナーは、Windows Server 上のサービスとして実行され、次のデータストア上のファイルを検出、分類、および保護することができます。

- SMB または NFS (プレビュー) プロトコルを使用するネットワーク共有の **UNC パス**。

- Sharepoint server 2013 2019 の sharepoint **ドキュメントライブラリおよびフォルダー** 。 [SharePoint 2010 の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)をご利用のお客様向けに、このバージョンの SharePoint もサポートされています。

ファイルを分類して保護するために、スキャナーでは、管理センター (Microsoft 365 Security Center、Microsoft 365 コンプライアンスセンター、Microsoft 365 のセキュリティとコンプライアンスセンターなど) にラベルを付けるために、管理センターにラベルを付ける Microsoft 365 の1つで構成された [機密ラベル](/microsoft-365/compliance/sensitivity-labels) を使用します。 

## <a name="azure-information-protection-unified-labeling-scanner-overview"></a>Azure Information Protection 統合されたラベル付けスキャナーの概要

AIP スキャナーは、Windows がインデックスを作成できるすべてのファイルを検査できます。 自動分類を適用するように感度ラベルを構成した場合は、検出されたファイルにラベルを付けてその分類を適用し、必要に応じて保護を適用または削除することができます。 

次の図は、スキャナーがオンプレミスと SharePoint サーバーの間でファイルを検出する AIP スキャナーアーキテクチャを示しています。

:::image type="content" source="media/ul-scanner-arch.png" alt-text="Azure Information Protection 統合されたラベル付けスキャナーのアーキテクチャ":::

ファイルを検査するために、スキャナーはコンピューターにインストールされている IFilters を使用します。 ファイルにラベルを付ける必要があるかどうかを判断するために、スキャナーは Microsoft 365 組み込みのデータ損失防止 (DLP) の機密情報の種類とパターンの検出、または正規表現パターンの Microsoft 365 を使用します。

スキャナーは Azure Information Protection クライアントを使用し、クライアントと同じ種類のファイルを分類して保護することができます。 詳細については、「 [Azure Information Protection の統合ラベル付けクライアントでサポートされるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md)」を参照してください。

次のいずれかの操作を行って、必要に応じてスキャンを構成します。

- **検索モードでスキャナーを実行** するのは、ファイルにラベルが付けられたときに何が起こるかを確認するレポートを作成する場合のみにしてください。
- 自動分類を適用するラベルを構成せず **に、スキャナーを実行して機密情報を含むファイルを検出** します。
- 構成に従ってラベルを適用するに **は、スキャナーを自動的に実行** します。 
- スキャンまたは除外する特定のファイルを指定する **ファイルの種類の一覧を定義** します。

> [!NOTE]
> スキャナーはリアルタイムで検出してラベルを付けません。 指定したデータストア上のファイルを体系的にクロールします。 このサイクルを1回または繰り返し実行するように構成します。

> [!TIP]
> 統一されたラベル付けスキャナーでは、複数のノードを持つスキャナークラスターがサポートされます。これにより、組織のスケールアウトが可能になり、スキャン時間が短縮され、範囲が広くなります。 
> 
> 開始時から複数のノードを直接デプロイするか、または1ノードクラスターから開始して、後で拡張するときにノードを追加します。 **Install AIPScanner** コマンドレットに同じクラスター名とデータベースを使用して、複数のノードを展開します。
> 

## <a name="aip-scanning-process"></a>AIP のスキャンプロセス

AIP スキャナーは、ファイルをスキャンするときに、次の手順に従って実行されます。

[1. スキャンのためにファイルが含まれるか除外されるかを決定します。](#1-determine-whether-files-are-included-or-excluded-for-scanning)

[2. ファイルを検査してラベルを付ける](#2-inspect-and-label-files)

[3. 検査できないファイルにラベルを付ける](#3-label-files-that-cant-be-inspected) 

詳細については、「 [スキャナーによってラベル付けされていないファイル](#files-not-labeled-by-the-scanner)」を参照してください。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. スキャンのためにファイルが含まれるか除外されるかを決定します。 

スキャナーでは、実行可能ファイルやシステム ファイルなど、分類と保護から除外されているファイルは自動的にスキップされます。 詳細については、「 [分類と保護から除外されるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)」を参照してください。

また、スキャナーは、明示的に定義されたすべてのファイルリストをスキャンするか、スキャンから除外するかを検討します。 ファイルの一覧は、既定ですべてのデータリポジトリに適用されます。また、特定のリポジトリに対してのみ定義できます。

スキャンまたは除外するファイルの種類を定義するには、コンテンツスキャンジョブの [ **スキャンするファイルの種類** ] を使用します。 次に例を示します。

![Azure Information Protection スキャナー用にスキャンするファイルの種類を構成する](./media/scanner-file-types.png)

詳細については、「 [ファイルを自動的に分類して保護するための Azure Information Protection スキャナーの展開](deploy-aip-scanner-configure-install.md)」を参照してください。

### <a name="2-inspect-and-label-files"></a>2. ファイルを検査してラベルを付ける

除外されたファイルを特定した後、スキャナーはもう一度フィルターを使用して検査がサポートされているファイルを特定します。

これらの追加のフィルターは、Windows Search およびインデックス作成用にオペレーティングシステムで使用されるものと同じであり、追加の構成は必要ありません。 Windows IFilter は、Word、Excel、PowerPoint で使用されるファイルの種類、および PDF ドキュメントやテキストファイルのスキャンにも使用されます。

検査がサポートされているファイルの種類の完全な一覧と、.zip ファイルと tiff ファイルを含めるようにフィルターを構成するための追加の手順については、「 [検査でサポートされるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection)」を参照してください。

検査後、サポートされているファイルの種類は、ラベルに指定された条件を使用してラベル付けされます。 探索モードを使用している場合、これらのファイルには、ラベルに指定された条件を含むようにレポートされるか、既知の機密情報の種類が含まれていることを報告できます。

#### <a name="stopped-scanner-processes"></a>スキャナープロセスを停止しました

スキャナーが停止し、リポジトリ内の多数のファイルのスキャンが完了していない場合は、ファイルをホストしているオペレーティングシステムの動的ポートの数を増やすことが必要になる場合があります。

たとえば、SharePoint のサーバーのセキュリティ強化は、スキャナーが許可されているネットワーク接続の数を超過して停止する理由の1つです。

これがスキャナーの停止の原因であるかどうかを確認するには、 **%localappdata%\Microsoft\MSIP\Logs\MSIPScanner.iplog** のスキャナーログに次のエラーメッセージがないかを確認します (複数のログは zip ファイルに圧縮されます)。

`Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port`

現在のポート範囲を表示し、必要に応じて増やす方法の詳細については、「 [ネットワークパフォーマンスを向上させるために変更できる設定](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)」を参照してください。

> [!TIP]
> 大規模な SharePoint ファームの場合は、リストビューのしきい値を大きくする必要があります。既定値は **5000** です。
>
> 詳細については、「 [SharePoint での大きなリストとライブラリの管理](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)」を参照してください。
>

### <a name="3-label-files-that-cant-be-inspected"></a>3. 検査できないファイルにラベルを付ける

検査できないファイルの種類については、AIP スキャナーによって、Azure Information Protection ポリシーの既定のラベル、またはスキャナー用に構成された既定のラベルが適用されます。

### <a name="files-not-labeled-by-the-scanner"></a>スキャナーによってラベル付けされていないファイル
AIP スキャナーは、次の状況でファイルにラベルを付けることはできません。

- ラベルに分類が適用され、保護は適用されず、ファイルの種類がクライアントによる分類のみをサポートしていない場合。 詳細については、「 [クライアントファイルの種類の統合](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only)」を参照してください。

- ラベルに分類と保護が適用されていても、スキャナーがファイルの種類をサポートしていない場合。
  
    既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 

    保護 [するファイルの種類を変更](deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect)すると、保護のために他の種類のファイルを追加できます。

**例**: .txt ファイルを検査した後、スキャナーは分類のみに構成されたラベルを適用できません。これは、.txt ファイルの種類では分類のみがサポートされていないためです。 

ただし、ラベルが分類と保護の両方に構成されていて、保護するスキャナーに .txt ファイルの種類が含まれている場合は、スキャナーでファイルにラベルを付けることができます。

## <a name="next-steps"></a>次のステップ

スキャナーの展開の詳細については、次の記事を参照してください。

- [AIP スキャナーの展開の前提条件](deploy-aip-scanner-prereqs.md)
- [AIP スキャナーの構成とインストール](deploy-aip-scanner-configure-install.md)
- [AIP スキャナーを使用したスキャンの実行](deploy-aip-scanner-manage.md)

**詳細情報**:

- 統合されたラベル付けスキャナーのベストプラクティスに関するブログをご覧ください: [AIP UL スキャナーをデプロイおよび使用するためのベストプラクティス](https://aka.ms/AIPScannerBestPractices)

- Microsoft の Core Services Engineering と Operations チームがどのようにこのスキャナーを実装したかについて関心をお持ちですか。  テクニカル ケース スタディ「[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)」(Azure Information Protection スキャナーを使用したデータ保護の自動化) をご覧ください。

- また、PowerShell を使用して、デスクトップ コンピューターからファイルを対話的に分類し、保護することができます。 PowerShell を使用するその他のシナリオの詳細については、「 [Azure Information Protection の統合ラベル付けクライアントでの powershell の使用](./rms-client/clientv2-admin-guide-powershell.md)」を参照してください。
