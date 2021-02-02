---
title: Azure Information Protection のクライアント
description: Microsoft Azure Information Protection は、組織のデータを保護するクライアント/サーバー型のソリューションです。 クライアント (Azure Information Protection クライアントまたは Rights Management クライアント) は、コンピューターおよびモバイル デバイスで実行するアプリケーションに統合されます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/20/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: fd76ce1c8efa79050869a93a311f0ae80d59d0b4
ms.sourcegitcommit: d3548610fbfee6006e12acd5471e085edf2da483
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99473040"
---
# <a name="the-client-side-of-azure-information-protection"></a>クライアント側での Azure Information Protection

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows Server 2016、Windows server 2012 R2、windows server 2012 *
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP and Legacy Windows And office versions](../known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。*
>
>***関連する内容**:[AIP の統合ラベル付けクライアントとクラシック クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。


Azure Information Protection の統一されたラベル付けクライアントは、組織のドキュメントや電子メールを保護するのに役立つクライアントサーバーソリューションを提供します。これは、 [Microsoft Office 用の組み込みのラベル付けソリューション](/microsoft-365/compliance/sensitivity-labels)の代替手段です。 

Office アプリケーションと直接統合するだけでなく、統合されたラベル付けクライアントには、ファイルエクスプローラーと PowerShell のサポートが含まれているため、Office の外部でファイルを分類して保護することができます。 追加のコンポーネントには、保護された Pdf とイメージのビューアー、およびオンプレミスのデータストアのスキャナーが含まれます。

統一されたラベル付けクライアントは、Office アプリに個別にインストールする必要があります。

このサービスは、クラウドまたはオンプレミスに存在します。

- クラウドサービスは **Azure Information Protection** し、Azure Rights Managements サービスを使用してデータを保護します。
- オンプレミスのサービスが **Active Directory Rights Management サービス** (AD RMS)

## <a name="choose-your-windows-labeling-solution"></a>Windows のラベル付けソリューションを選択する

ラベルを使用すると、ユーザーが保護を簡単に適用できるようになります。また、データを追跡して管理できるように分類を提供することもできます。 

Windows ラベル付けソリューションを選択する場合は、次の基本的な相違点を考慮してください。

- **ラベルとラベルポリシーのダウンロード元** 

    組み込みのラベル付けソリューションと AIP のラベル付けクライアントは、次のいずれかの管理センターを使用します。 
    
    - Office 365 セキュリティ/コンプアライアンス センター 
    - Microsoft 365 セキュリティ センター 
    - Microsoft 365 コンプライアンス センター
      
    従来の AIP クラシッククライアントを使用している場合は、ラベルとラベルのポリシーが Azure portal でダウンロードおよび管理されます。 

- **インストール要件**

    組み込みのラベル付けソリューションでは、個別にインストールする必要はありません。

    AIP の統一されたラベル付けクライアントと従来の従来のクライアントは、どちらも Office に個別にインストールする必要があります。 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)から、統一されたラベル付けクライアントをダウンロードしてインストールします。  

    従来のクラシッククライアントをダウンロードしてインストールする必要がある場合は、サポートに連絡して、インストールファイルにアクセスするチケットを開いてください。 

組織に最適なクライアントを判断するには、次のセクションを参考にしてください。

- [組み込みの Office ラベル付けソリューション](#built-in-office-labeling-solution)
- [Azure Information Protection 統合ラベル付けクライアント](#azure-information-protection-unified-labeling-client)
- [Azure Information Protection クラシック クライアント](#azure-information-protection-classic-client)
- [同じ環境での複数のクライアントの使用](#using-multiple-clients-in-the-same-environment)

詳細については、「AIP のクライアントと[機能](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client)[の詳細な比較](#detailed-comparisons-for-the-azure-information-protection-clients)」を参照してください。

> [!NOTE]
> 最新バージョンのラベル付けクライアントでは、従来のクライアントを使用して機能のパリティを閉じることができます。 このギャップが閉じられると、新しい機能は、統合されたラベル付けクライアントにのみ追加されることを期待できます。 
>
> 現在の機能セットと機能がビジネス要件を満たしている場合は、統一されたラベル付けクライアントを展開することをお勧めします。
> 

### <a name="built-in-office-labeling-solution"></a>組み込みの Office ラベル付けソリューション

Microsoft Office に組み込まれているラベル付けソリューション:

- Microsoft 365 アプリケーションが適用される Windows コンピューター、最小バージョン1910が必要です。
- MacOS、iOS、および Android でも使用できるラベルとポリシー設定を共有できます。
- アカウントの切り替えをサポートする
- Office アプリケーションのパフォーマンスを向上させる
- 個別のインストールとメンテナンスを必要としない
- この機能は無効にできません。

リボンの下にある Information Protection バーなどの Azure Information Protection クライアントのみを提供する機能が必要な場合は、組み込みの Office ラベル付けクライアントを **使用しない** でください。 このバーは、ラベルの選択と表示を容易にします。

### <a name="azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアント

統一されたラベル付けクライアントには Windows コンピューターが必要であり、macOS、iOS、および Android でも使用できるラベルとポリシー設定を共有できます。

統一されたラベル [付けストアにまだ移行](../configure-policy-migrate-labels.md)していない Azure portal でラベルを構成している場合は、統一されたラベル付けクライアントを **使用しない** でください。

### <a name="azure-information-protection-classic-client"></a>Azure Information Protection クラシック クライアント

従来のクライアントは AIP のレガシクライアントであり、統一されたラベル付けクライアントと同様の機能をサポートします。また、Office アプリに対して個別にインストールする必要があります。 

従来のクライアントは [2021 年3月に非推奨](https://aka.ms/aipclassicsunset)とされます。

統合ラベルに移行していない場合にのみ、クラシッククライアントを使用します。 詳細については、「[チュートリアル:  Azure Information Protection (AIP) クラシック クライアントから、統合ラベル付けクライアントへの移行](../tutorial-migrating-to-ul.md)」を参照してください。

クラシッククライアントには、macOS、iOS、および Android 用のさまざまなポリシー設定があります。 そのため、追加機能を使用する必要がある場合でも、オペレーティングシステム間でコンテンツを保護するために、別の管理ポータルとユーザーエクスペリエンスを操作する必要があります。

可能であれば、従来のクライアントではなく、統合されたラベル付けクライアントを使用することをお勧めします。

### <a name="using-multiple-clients-in-the-same-environment"></a>同じ環境での複数のクライアントの使用

次の展開例に示すように、同じ環境で異なるクライアントを使用して、さまざまなビジネス要件をサポートできます。 混合クライアント環境では、管理を容易にするためにクライアントが同じラベルのセットを共有できるように、統一されたラベルを使用することをお勧めします。 新しい顧客は、テナントが統一されたラベル付けプラットフォーム上にあるため、既定では統合ラベルを持ちます。 詳細については、「[テナントが統一されたラベル付けプラットフォームにあるかどうかを確認する方法](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)」を参照してください。

インストールされている Windows コンピューターで、最小バージョン1910と Azure Information Protection クライアントのいずれかがインストールされている Microsoft 365、既定では、組み込みのラベル付けソリューションは Office アプリで無効になっています。 ただし、この動作を変更して、Office アプリ専用のラベル付けソリューションを使用することができます。 この構成では、Azure Information Protection クライアントは、エクスプローラー、PowerShell、およびスキャナーでラベルを付けることができます。 Microsoft 365 アプリで Azure Information Protection クライアントを無効にする手順については、Microsoft 365 の準拠に関するドキュメントの「 [Office 組み込みのラベル付けソリューション」と「Azure Information Protection クライアント](/microsoft-365/compliance/sensitivity-labels-office-apps#office-built-in-labeling-client-and-the-azure-information-protection-client) 」を参照してください。

##### <a name="sample-deployment-strategy"></a>展開方法の例

- 多くのユーザーにとっては、このクライアントがこれらのユーザーのビジネスニーズを満たしているため、Azure Information Protection 統合されたラベル付けクライアントを展開します。 
    
    これらのユーザーについては、Windows、Mac、iOS、および Android ではラベル付けエクスペリエンスが似ています。これらのユーザーには同じラベルが発行され、同じポリシー設定が使用されているためです。 管理者は、これらのラベルとポリシー設定を同じ管理センターで管理します。

- また、自分用に統一されたラベル付けクライアントをインストールし、Azure Information Protection スキャナーをテストします。

- ユーザーのサブセットでは、従来のクライアントを展開します。これらのユーザーには、独自のキーの保持 ([HYOK](../configure-adrms-restrictions.md)) 保護を適用するラベルが必要なためです。
    
    このようなユーザーの場合、このクライアントを使用すると、ラベル付けエクスペリエンスが若干異なります。 たとえば、Office アプリの [**秘密度**] ボタンではなく、[**保護**] ボタンが表示されます。 管理者は、別の管理センターにある HYOK の設定とポリシー設定のラベルを、他のクライアントプラットフォームのラベルと設定に管理する必要があります。

- 機密情報のスキャンや分類、保護が必要なドキュメントを含むオンプレミスのデータストアがある。 運用環境で使用する場合は、 [Azure Information Protection スキャナー](../deploy-aip-scanner.md)を実行するサーバーに、統合されたラベル付けクライアントを展開します。

#### <a name="rights-management-client"></a>Rights Management クライアント

RMS クライアントは保護のみを提供し、Office アプリケーション、AIP に統合されたラベル付けと従来のクライアント、および他のソフトウェアベンダーからの RMS 対応アプリケーションを含む一部のアプリケーションと共に自動的にインストールされます。 

また、 [RMS クライアントを自分でインストール](https://www.microsoft.com/download/details.aspx?id=38396)して、 [IRM で保護されたライブラリと OneDrive からのファイルの同期](/onedrive/deploy-on-windows)、および rights management 保護を基幹業務アプリケーションに統合する開発者をサポートすることもできます。

## <a name="compare-the-labeling-solutions-for-windows-computers"></a>Windows コンピューターのラベル付けソリューションを比較する

Windows コンピューターの3つのラベル付けソリューションでサポートされている機能を比較するには、次の表を参考にしてください。

さまざまなオペレーティングシステムプラットフォーム (Windows、macOS、iOS、Android) における Office の組み込みの機密ラベル付け機能を比較するには、Microsoft 365 のコンプライアンスドキュメント、 [アプリでの機密ラベル機能のサポート](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)を参照してください。 このドキュメントには、サポートされている機能の Office ビルド番号または Office 更新チャネルに関する情報も含まれています。

詳細については、「」も参照してください。
- [Azure Information Protection クライアントの詳細な比較](#detailed-comparisons-for-the-azure-information-protection-clients)
- [Azure Information Protection 統合されたラベル付けクライアントに含まれていない機能](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client)

|機能|従来のクライアント|統一されたラベル付けクライアント|Office 組み込みラベル付けソリューション|
|:------|:------------:|:---------------------:|:-----------------------------:|
|**手動によるラベル付け**| ![はい](../media/yes-icon.png)   | ![はい](../media/yes-icon.png)   |![はい](../media/yes-icon.png) |
|**既定のラベル**| ![はい](../media/yes-icon.png)| ![はい](../media/yes-icon.png)| ![はい](../media/yes-icon.png)|
|**推奨または自動ラベル付け** <br />Word、Excel、PowerPoint、Outlook の場合|![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |
|**必須のラベル付け**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |  ![はい](../media/yes-icon.png)|
|**ラベルに対するユーザー定義のアクセス許可**: <br />メールに転送しない| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |
|**ラベルに対するユーザー定義のアクセス許可**: <br />Word、Excel、PowerPoint のカスタムアクセス許可| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |
|**複数言語によるラベルのサポート**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |![はい](../media/yes-icon.png) |
|**電子メールの添付ファイルからのラベルの継承**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png)  | ![no](../media/no-icon.png)|
|次 **のようなカスタマイズが含ま** れます。<br />- メールの既定のラベル<br />-Outlook でメッセージをポップアップ表示する <br />- S/MIME のサポート<br />- [問題の報告] オプション| ![はい ](../media/yes-icon.png) <sup>1</sup> | ![はい ](../media/yes-icon.png) <sup>2</sup> |  ![no](../media/no-icon.png)|
|**オンプレミスのデータストアのスキャナー**| ![はい](../media/yes-icon.png) |  ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**中央レポート (分析)**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**ラベルとは別に設定するカスタムアクセス許可**| ![yes](../media/yes-icon.png) | ![はい ](../media/yes-icon.png) <sup>3</sup>|  ![no](../media/no-icon.png)|
|**Office アプリの Information Protection バー**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png)|  ![no](../media/no-icon.png)|
|**ラベルアクションとしての視覚的なマーキング**<br> (ヘッダー、フッター、透かし)| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png)|
|**アプリごとの視覚的マーキング**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![はい ](../media/yes-icon.png) <sup>9</sup>|
|**変数を使用した動的な視覚的マーキング**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![はい ](../media/yes-icon.png) <sup>9</sup>|
|**アプリ内の外部コンテンツマークの削除**| ![はい](../media/yes-icon.png)| ![はい](../media/yes-icon.png)| ![no](../media/no-icon.png)|
|**ファイルエクスプローラーでラベルを付ける**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**保護されたファイルのビューアー** <br> (テキスト、画像、PDF、. pfile)| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![no](../media/no-icon.png)|
|**ラベルを適用するための PPDF のサポート**| ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)|
|**PowerShell のラベル付けコマンドレット**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png)  |  ![no](../media/no-icon.png)|
|**保護アクションのオフラインサポート**| ![yes](../media/yes-icon.png) | ![はい ](../media/yes-icon.png) <sup>4</sup> | ![yes](../media/yes-icon.png) |
|**切断されたコンピューターのポリシーファイルの手動管理**| ![はい](../media/yes-icon.png) |![はい](../media/yes-icon.png)|  ![no](../media/no-icon.png)|
|**HYOK のサポート**| ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)|
|**イベントビューアーの使用状況ログ**| ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)| ![no](../media/no-icon.png)|
|**Outlook の [転送不可] ボタンを表示する**| ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)|
|**保護されたドキュメントの追跡**| ![可 ](../media/yes-icon.png) <sup>5</sup> | ![可 ](../media/yes-icon.png) <sup>5</sup> |  ![no](../media/no-icon.png)|
|**保護されたドキュメントの取り消し**| ![可 ](../media/yes-icon.png) <sup>5</sup> |  ![可 ](../media/yes-icon.png) <sup>5</sup>|  ![no](../media/no-icon.png)|
|**保護のみモード** (ラベルなし)| ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)|
|**アカウントの切り替えのサポート**|  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)| ![はい](../media/yes-icon.png) |
|**リモートデスクトップサービスのサポート**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |
|**AD RMS のサポート**| ![yes](../media/yes-icon.png) |  ![× ](../media/no-icon.png) <sup>6</sup> |  ![no](../media/no-icon.png)|
|**Microsoft Office 97-2003 形式のサポート**| ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) |  ![](../media/no-icon.png) <sup>8</sup>なし|
|**二重キーの暗号化**|  ![no](../media/no-icon.png)| ![はい](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**政府機関向けコミュニティクラウド** | ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png) | ![はい](../media/yes-icon.png)|
| | | | |

**脚注**:

<sup>1</sup> これらの設定は、 [Azure portal で構成するアドバンストクライアント設定](client-admin-guide-customizations.md#how-to-configure-advanced-classic-client-configuration-settings-in-the-portal)としてサポートされています。

<sup>2</sup> これらの設定とその他の多くは、 [PowerShell で構成する詳細設定](clientv2-admin-guide-customizations.md#configuring-advanced-settings-for-the-client-via-powershell)としてサポートされています。

<sup>3</sup> ファイルエクスプローラーと PowerShell でサポートされます。 Office アプリでは、ユーザーは **ファイル情報**[ドキュメントの保護] [アクセスの制限] を選択でき  >    >  ます。

<sup>4</sup> ファイルエクスプローラーと PowerShell コマンドについては、ユーザーがファイルを保護するためにインターネットに接続されている必要があります。

<sup>5</sup>詳細については、「**統合ラベル付けクライアント**:[管理者ガイド (パブリック](track-and-revoke-admin.md)プレビュー)  |   [ユーザーガイド (パブリックプレビュー)](revoke-access-user.md)」を参照してください。 追跡は、グローバル管理者のみがサポートしています。 **従来のクライアント**:[管理者ガイド](client-admin-guide-document-tracking.md)  |  [ユーザーガイド](client-track-revoke.md)。 管理者は、 [中央レポート](../reports-aip.md) を使用して、Windows コンピューターから保護されたドキュメントにアクセスするかどうか、およびアクセスを許可または拒否するかどうかを指定することもできます。

<sup>6</sup> ラベル付けおよび保護操作はサポートされていません。 ただし、AD RMS 展開の場合、 [Active Directory Rights Management サービスモバイルデバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))を使用すると、ビューアーは保護されたドキュメントを開くことができます。

<sup>8</sup> AIP クライアントは、 **.doc** などの Microsoft Office 97-2003 ファイル形式と Office Open xml 形式 ( **.docx** など) の両方をサポートしていますが、組み込みのラベル付けでは open xml 形式のみがサポートされています。

<sup>9</sup> 組み込みラベル付けソリューションの動的コンテンツマーキングとアプリごとのコンテンツマーキングのサポートの詳細については、 [Microsoft 365 のドキュメント](/microsoft-365/compliance/sensitivity-labels-office-apps#dynamic-markings-with-variables)を参照してください。

### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Azure Information Protection クライアントの詳細な比較

Azure Information Protection クラシッククライアントと Azure Information Protection 統一されたラベル付けクライアントの両方で同じ機能がサポートされている場合は、次の一覧を使用して、2つのクライアントの機能上の違いを特定します。


|機能 |従来のクライアント|統一されたラベル付けクライアント|
|--------------|-----------------------------------|-----------------------------------------------------------|
|**セットアップ**| ローカルのデモ ポリシーをインストールするオプション | ローカルのデモ ポリシーなし|
|**Office アプリで適用したときのラベルの選択と表示**|リボン上の **[保護]** ボタンから <br /><br /> Information Protection バーから (リボンの下の水平バー)|リボン上の **[秘密度]** ボタンから<br /><br /> Information Protection バーから (リボンの下の水平バー)|
|**Office アプリの Information Protection バーを管理する**|**ユーザーの場合**:<br />リボンの [ **保護** ] ボタンのバーを表示または非表示にするオプション<br /><br>ユーザーがバーを非表示にすることを選択した場合、既定では、バーはそのアプリで非表示になりますが、新しく開いたアプリには引き続き自動的に表示されます。 <br /><br /> **管理者の場合**: <br />アプリが初めて開いたときにバーを自動的に表示または非表示にしたり、ユーザーがバーを選択した後に新しく開いたアプリのバーを自動的に非表示にするかどうかを制御するためのポリシー設定|**ユーザーの場合**: <br />リボンの [ **感度** ] ボタンのバーを表示または非表示にするオプション。 <br><br />ユーザーがバーを非表示にすることを選択すると、そのアプリと新しく開いたアプリでバーが非表示になります。 <br /><br />**管理者の場合**: <br />バーを管理するための PowerShell 設定 |
|**ラベルの色**| Azure portal で構成する | ラベルの移行後に保持され、 [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)で構成可能|
|**ラベルが異なる言語をサポートする**| Azure portal で構成する | [Office 365 セキュリティ & コンプライアンス PowerShell](/microsoft-365/compliance/create-sensitivity-labels#additional-label-settings-with-office-365-security--compliance-center-powershell)を使用して構成する|
|**ポリシーの更新**| -Office アプリが開いたとき <br /> -ファイルまたはフォルダーを分類して保護するために右クリックしたとき <br />-ラベル付けと保護のために PowerShell コマンドレットを実行する場合<br />-24 時間ごと <br />-スキャナーの場合: 1 時間ごと、およびサービスが開始され、ポリシーが1時間を経過した場合| -Office アプリが開いたとき <br />-ファイルまたはフォルダーを分類して保護するために右クリックしたとき <br />-ラベル付けと保護のために PowerShell コマンドレットを実行する場合<br />-4 時間ごと <br />-スキャナーの場合: 4 時間ごと|
|**サポートされている PDF 形式**| **保護**: <br /> - PDF の暗号化における ISO 標準 (既定) <br /> - .ppdf <br /><br> 使用 **量**: <br /> - PDF の暗号化における ISO 標準 <br />- .ppdf<br />- SharePoint IRM 保護| **保護**: <br /> - PDF の暗号化における ISO 標準 <br /> <br /> 使用 **量**: <br /> - PDF の暗号化における ISO 標準 <br />- .ppdf<br />- SharePoint IRM 保護|
|**ビューアーで開かれた一般的な保護されたファイル (pfile)**| ファイルは元のアプリで開き、保護なしで表示、変更、および保存できます。 | ファイルは元のアプリで開くことができ、それを表示して変更することはできますが、保存することはできません。|
|**サポートされているコマンドレット**| -ラベル付け用のコマンドレット <br> -保護専用のコマンドレット | **ラベル付け用のコマンドレット**:<br /> [Set-aipfileclassification](/powershell/module/azureinformationprotection/get-aipfileclassification) と [set-aipfilelabel](/powershell/module/azureinformationprotection/get-aipfilelabel) は **Owner** パラメーターをサポートしていません <br /> さらに、ラベルが適用されないすべてのシナリオに対して、"No label to apply" (適用するラベルがありません) というコメントが 1 つ付きます <br /><br /> [Set-aipfileclassification](/powershell/module/azureinformationprotection/get-aipfileclassification) は **WhatIf** パラメーターをサポートするため、検出モードで実行できます。 <br /><br /> [Set-aipfilelabel](/powershell/module/azureinformationprotection/get-aipfilelabel) は *enabletracking* パラメーターをサポートしていません <br /><br /> [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) は他のテナントからラベル情報を返さず、 **RMSIssuedTime** パラメーターを表示しません。<br />また、 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)の **labelingmethod** パラメーターには、**手動** または **自動** ではなく **Privileged** または **Standard** が表示されます。|
|**Office のアクションごとの理由プロンプト (構成されている場合)** | -頻度: ファイルあたり <br /> -感度レベルを下げます。 <br /> -ラベルの削除<br /> -保護を削除しています | -頻度: セッションごと <br /> -感度レベルを下げます。<br />-ラベルの削除|
|**適用されたラベルアクションの削除** | ユーザーは確認するよう求められます <br /><br />既定のラベルまたは自動ラベル (構成されている場合) は、Office アプリがファイルを開いたときに自動的に適用されません。  | ユーザーに確認を求めるメッセージが表示されない<br /><br /> 既定のラベルまたは自動ラベル (構成されている場合) は、次に Office アプリがファイルを開いたときに自動的に適用されます。|
|**自動および推奨ラベル** | 組み込みの情報の種類と、語句や正規表現を使ったカスタム条件を使って、Azure portal で[ラベル条件](../configure-policy-classification.md)として構成されます <br /><br />構成のオプションには、次のようなものがあります。 <br />- 一意の / 一意でない数 <br /> - 最小数| 組み込みの機密情報の種類と[カスタムの情報の種類](/microsoft-365/compliance/create-a-custom-sensitive-information-type)を使用して、管理センターで構成されます<br /><br />構成のオプションには、次のようなものがあります。  <br />- 一意の数のみ <br />- 最小および最大数 <br />- 情報の種類での AND と OR のサポート <br />- キーワード ディクショナリ<br />- カスタマイズ可能な信頼度レベルと文字の近接|
|**添付ファイルに対するサブラベルのサポートの注文** | [クライアントの詳細設定](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)で有効 | 既定で有効になっています。構成は必要ありません|
|**ファイルの種類の既定の保護動作を変更する**| [レジストリの編集](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)を使用して、ネイティブ保護と汎用保護の既定値を上書きする | [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)を使用して保護するファイルの種類を変更する|
|**自動再スキャン** | スキャナーがポリシーまたはラベル設定の変更を検出するたびに、フルスキャンが自動的に実行されます。 | バージョン [2.8.85.0](unifiedlabelingclient-version-release-history.md#version-28850)以降では、ポリシーまたはコンテンツスキャンジョブの設定を変更した後、完全な再スキャンをスキップするように管理者が選択できます。 |
|**ネットワーク探索** (パブリックプレビュー) |クラシックスキャナーではネットワーク探索機能を使用できません | 管理者は、指定された IP アドレスまたは範囲をスキャンすることで、他の危険なリポジトリを検出できます。|
| | | |

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合されたラベル付けクライアントに含まれていない機能

Azure Information Protection 統合されたラベル付けクライアントはまだ開発中ですが、従来のクライアントとの次の機能と動作の違いは、現在、統合されたラベル付けクライアントの今後のリリースで使用できるとは想定されていません。 

- [Office アプリでユーザーが選択できる別のオプション](client-classify-protect.md#set-custom-permissions-for-a-document)としてのカスタムアクセス許可: Word、Excel、PowerPoint

- [感度] ツールバーには、 **秘密度** のタイトルやタイトルのヒントは表示されません。 バー自体は、統合されたラベル付けクライアントに表示されます。

- テンプレートを使用した[保護のみのモード](client-protection-only-mode.md)(ラベルなし)

- ドキュメントを ppdf として保護する [(古い形式)](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)

- Outlook の [ **転送不可** ] ボタンを表示する

- デモ ポリシー

- Rights Management サービスに接続するために PowerShell コマンドレットを分離させる

- ラベルを適用したユーザー id の表示


### <a name="parent-labels-and-their-sublabels"></a>親ラベルとそのサブラベル 

Azure Information Protection classic クライアントは、サブラベルを持つ親ラベルを指定する構成をサポートしていません。 これらの構成には、既定のラベルと、推奨または自動分類のラベルの指定が含まれます。 ラベルにサブラベルがある場合は、親ラベルではなく、サブラベルのいずれかを指定できます。

パリティについて、Azure Information Protection 統合ラベル付けクライアントでも、管理センターでこれらのラベルを選択できる場合でも、サブラベルのある親ラベルの適用はサポートされていません。 このシナリオでは、Azure Information Protection 統合ラベル付けクライアントで親ラベルが適用されません。

## <a name="next-steps"></a>次のステップ

Azure Information Protection 統合ラベル付けクライアントをインストールして構成するには、次を参照してください。

- [Azure Information Protection 統合ラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)
- [Azure Information Protection 統合されたラベル付けユーザーガイド](clientv2-user-guide.md)

組み込みのラベル付けソリューションを Microsoft 365 アプリに使用する方法の詳細については、「 [Office アプリの秘密度ラベル](/microsoft-365/compliance/sensitivity-labels-office-apps)」を参照してください。
