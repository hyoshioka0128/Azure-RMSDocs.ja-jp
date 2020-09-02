---
title: Azure Information Protection のクライアント
description: Microsoft Azure Information Protection は、組織のデータを保護するクライアント/サーバー型のソリューションです。 クライアント (Azure Information Protection クライアントまたは Rights Management クライアント) は、コンピューターおよびモバイル デバイスで実行するアプリケーションに統合されます。
author: mlottner
ms.author: bagol
manager: rkarlin
ms.date: 07/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 8b72c0b8efe31ad570bed684dbe63283c5f79b47
ms.sourcegitcommit: 129370798e7d1b5baa110b2d7b2f24abd3cad5c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89316639"
---
# <a name="the-client-side-of-azure-information-protection"></a>クライアント側での Azure Information Protection

>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。


Azure Information Protection は、組織の文書や電子メールを保護するクライアント/サーバー型のソリューションです。

- クライアントには、Office 用の組み込みのラベル付けクライアント、Windows 用の Azure Information Protection 統合ラベルクライアント、Windows 用 Azure Information Protection クライアント (クラシック)、または Rights Management クライアントを使用できます。
    
    これらのクライアントは、多くの場合、 **Office 組み込みラベルクライアント**、統一された **ラベル付けクライアント**、 **従来のクライアント**、および **RMS クライアント**と呼ばれます。 どちらのクライアントを使用するかは、コンピューターやモバイルデバイスで実行するアプリケーションと統合されます。

- このサービスはクラウドまたはオンプレミスに存在します。 クラウドサービスは Azure Information Protection であり、データ保護に Azure Rights Management サービスを使用します。 オンプレミスのサービスは Active Directory Rights Management サービスであり、より一般的に AD RMS と呼ばれています。 

これらのクライアントはすべて Office アプリケーションと統合されますが、統一されたラベル付けクライアントとクラシッククライアントは個別にインストールし、追加の機能とコンポーネントをサポートする必要があります。 たとえば、これらのクライアントにはエクスプローラーのサポートが含まれているので、Office 以外でファイルを分類して保護することができます。 追加のコンポーネントには、保護された PDF ドキュメントと保護されたイメージのビューアー、およびオンプレミスのデータストアのスキャナーが含まれます。

RMS クライアントは保護のみを提供します。 このクライアントは、Office アプリケーション、Azure Information Protection クライアント、ソフトウェアベンダーからの RMS 対応アプリケーションなど、一部のアプリケーションと共に自動的にインストールされます。 ただし、IRM で保護され[たライブラリや OneDrive からのファイルの同期](https://docs.microsoft.com/onedrive/deploy-on-windows)、および rights management による保護を基幹業務アプリケーションに統合する開発者のために、[単独でインストール](https://www.microsoft.com/download/details.aspx?id=38396)することもできます。

## <a name="choose-which-labeling-client-to-use-for-windows-computers"></a>Windows コンピューターに使用するラベル付けクライアントを選択する

可能な場合は、ラベル付けクライアントのいずれかを使用します。ラベルはユーザーの保護の適用の複雑さを抽象化し、ラベルも分類を提供してデータの追跡と管理を行うことができるためです。

Windows コンピューターのクライアントにラベルを付ける方法は、使用する管理ポータルの影響を受ける可能性があります。

- Office に組み込まれているラベル付けクライアントと Azure Information Protection は、次の管理センターのラベルとポリシー設定をクライアントにダウンロードします。 
    - Office 365 セキュリティ/コンプアライアンス センター
    - Microsoft 365 セキュリティ センター
    - Microsoft 365 コンプライアンス センター

- Azure Information Protection クライアント (クラシック) は、Azure portal からラベルとポリシー設定をダウンロードします。

統一されたラベル付けクライアントと従来のクライアントは Office に個別にインストールする必要があるため、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)からこれらのクライアントをダウンロードしてインストールする必要があります。 

組織に最適なクライアントを判断するには、次のセクションを参考にしてください。

- [組み込みの Office ラベル付けクライアント](#built-in-office-labeling-client)
- [Azure Information Protection 統合されたラベル付けクライアント](#azure-information-protection-unified-labeling-client)
- [クラシッククライアントを Azure Information Protection する](#azure-information-protection-classic-client)
- [同じ環境での複数のクライアントの使用](#using-multiple-clients-in-the-same-environment)

詳細については、「AIP のクライアントと[機能](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client)[の詳細な比較](#detailed-comparisons-for-the-azure-information-protection-clients)」を参照してください。

> [!NOTE]
> 最新バージョンのラベル付けクライアントでは、従来のクライアントを使用して機能のパリティを閉じることができます。 このギャップが閉じられると、新しい機能は、統合されたラベル付けクライアントにのみ追加されることを期待できます。 
>
> 現在の機能セットと機能がビジネス要件を満たしている場合は、統一されたラベル付けクライアントを展開することをお勧めします。
> 

### <a name="built-in-office-labeling-client"></a>組み込みの Office ラベル付けクライアント

Microsoft Office するために組み込まれているラベル付けクライアント:

- Office 365 アプリケーションを搭載した Windows コンピューター、最小バージョン1910が必要です。
- MacOS、iOS、および Android でも使用できるラベルとポリシー設定を共有できます。
- アカウントの切り替えをサポートする
- Office アプリケーションのパフォーマンスを向上させる
- 個別のインストールとメンテナンスを必要としない
- この機能は無効にできません。

クラシックまたは統合されたラベル付けクライアント (リボンの下の Information Protection バーなど) によってのみ提供される機能が必要な場合は、組み込みの Office ラベル付けクライアントを**使用しない**でください。 このバーは、ラベルの選択と表示を容易にします。

### <a name="azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアント

統一されたラベル付けクライアントには Windows コンピューターが必要であり、macOS、iOS、および Android でも使用できるラベルとポリシー設定を共有できます。

現在の統一されたラベル付け機能がビジネス要件を満たしていない場合、または[統合ラベルストアにまだ移行](../configure-policy-migrate-labels.md)していない Azure portal でラベルを構成している場合は、統一されたラベル付けクライアントを**使用しない**でください。

### <a name="azure-information-protection-classic-client"></a>クラシッククライアントを Azure Information Protection する

クラシック クライアント: 

- Windows コンピューターが必要です
- オンプレミスのキー (HYOK) を保持するなど、統合されたラベル付けクライアントでまだ使用できない機能へのアクセスを提供します。また、オンプレミスのデータストアのスキャナーの一般公開バージョンも利用できます。 
- MacOS、iOS、および Android でラベルを共有できるようになります。

ただし、従来のクライアントには、macOS、iOS、および Android 用のさまざまなポリシー設定があります。 そのため、追加機能を使用する必要がある場合でも、オペレーティングシステム間でコンテンツを保護するために、別の管理ポータルとユーザーエクスペリエンスを操作する必要があります。

統一されたラベル付けクライアントでのみ新しい機能を使用できるようにする場合や、一元化された統合ユーザーエクスペリエンスを提供する場合は、従来のクライアントを**使用しない**でください。

### <a name="using-multiple-clients-in-the-same-environment"></a>同じ環境での複数のクライアントの使用

次の展開例に示すように、同じ環境で異なるクライアントを使用して、さまざまなビジネス要件をサポートできます。 混合クライアント環境では、管理を容易にするためにクライアントが同じラベルのセットを共有できるように、統一されたラベルを使用することをお勧めします。 新しい顧客は、テナントが統一されたラベル付けプラットフォーム上にあるため、既定では統合ラベルを持ちます。 詳細については、「[テナントが統一されたラベル付けプラットフォームにあるかどうかを確認する方法](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)」を参照してください。

Office 365 アプリを実行している Windows コンピューターに最小バージョン1910がインストールされており、いずれかの Azure Information Protection クライアントがインストールされている場合、既定では、組み込みのラベル付けクライアントは Office アプリで無効になっています。 ただし、この動作を変更して、Office アプリ専用のラベル付けクライアントを使用することができます。 この構成では、Azure Information Protection クライアント (クラシックまたは統合されたラベル付け) は、ファイルエクスプローラー、PowerShell、およびスキャナーでラベル付けできます。 Office 365 アプリで Azure Information Protection クライアントを無効にする手順については、Microsoft 365 のコンプライアンスドキュメントの「 [office 組み込みラベルクライアントと Azure Information Protection クライアント](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#office-built-in-labeling-client-and-the-azure-information-protection-client) 」を参照してください。

##### <a name="example-deployment-strategy"></a>展開方法の例:

- 多くのユーザーにとっては、このクライアントがこれらのユーザーのビジネスニーズを満たしているため、Azure Information Protection 統合されたラベル付けクライアントを展開します。 
    
    これらのユーザーについては、Windows、Mac、iOS、および Android ではラベル付けエクスペリエンスが似ています。これらのユーザーには同じラベルが発行され、同じポリシー設定が使用されているためです。 管理者は、これらのラベルとポリシー設定を同じ管理センターで管理します。

- また、自分用に統一されたラベル付けクライアントをインストールし、Azure Information Protection スキャナーをテストします。

- ユーザーのサブセットでは、従来のクライアントを展開します。これらのユーザーには、独自のキーの保持 (HYOK) 保護を適用するラベルが必要なためです。
    
    このようなユーザーの場合、このクライアントを使用すると、ラベル付けエクスペリエンスが若干異なります。 たとえば、Office アプリの [**秘密度**] ボタンではなく、[**保護**] ボタンが表示されます。 管理者は、別の管理センターにある HYOK の設定とポリシー設定のラベルを、他のクライアントプラットフォームのラベルと設定に管理する必要があります。

- 機密情報のスキャンや分類、保護が必要なドキュメントを含むオンプレミスのデータストアがある。 実稼働環境で使用する場合は、クラシッククライアントをサーバーに展開して Azure Information Protection スキャナーを実行します。

## <a name="compare-the-labeling-clients-for-windows-computers"></a>Windows コンピューターのラベル付けクライアントの比較

次の表を使用して、Windows コンピューターの3つのラベル付けクライアントでサポートされている機能を比較してください。

さまざまなオペレーティングシステムプラットフォーム (Windows、macOS、iOS、Android) における Office の組み込みの機密ラベル付け機能を比較するには、Microsoft 365 のコンプライアンスドキュメント、 [アプリでの機密ラベル機能のサポート](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)を参照してください。 このドキュメントには、サポートされている機能の Office ビルド番号または Office 更新チャネルに関する情報も含まれています。

|特徴量|従来のクライアント|統合ラベル付けクライアント|Office 組み込みラベルクライアント|
|:------|:------------:|:---------------------:|:-----------------------------:|
|手動によるラベル付け:| **はい** | **はい** |**はい** |
|既定のラベル:| **はい** | **はい** | **はい** |
|推奨または自動ラベル付け: <br />-Word、Excel、PowerPoint の場合| **はい** | **はい** | **はい** |
|推奨または自動ラベル付け:<br />-Outlook の場合| **はい** | **はい** | いいえ |
|必須ラベル:| **はい** | **はい** | いいえ |
|ラベルに対するユーザー定義のアクセス許可: <br />-メールの転送不可| **はい** | **はい** | **はい** |
|ラベルに対するユーザー定義のアクセス許可: <br />-Word、Excel、PowerPoint のカスタムアクセス許可| **はい** | **はい** | **はい** |
|ラベルの多言語サポート:| **はい** | **はい** |**はい** |
|メールの添付ファイルからのラベル継承:| **はい** | **はい**  |いいえ |
|以下を含むカスタマイズ:<br />- メールの既定のラベル<br />-Outlook でメッセージをポップアップ表示する <br />- S/MIME のサポート<br />- [問題の報告] オプション| **はい** <sup>1</sup> | **はい** <sup>2</sup> | いいえ |
|オンプレミスのデータ ストア用のスキャナー:| **はい** | **うん <br />** | いいえ |
|中央レポート機能 (分析):| **はい** | **はい** | いいえ |
|ラベルとは別に設定するカスタムのアクセス許可:| **はい** | **はい** <sup>3</sup>| いいえ |
|Office アプリの Information Protection バー: | **はい** | **はい**| いいえ |
|ラベルアクションとしての視覚的なマーキング (ヘッダー、フッター、透かし):| **はい** | **はい** | **はい**|
|アプリごとの視覚的マーキング:| **はい** | **はい** | いいえ |
|変数を使用した動的な視覚的マーキング:| **はい** | **はい** | いいえ |
|ファイルエクスプローラーでラベルを付ける:| **はい** | **はい** | いいえ |
|保護されたファイルのビューアー (テキスト、画像、PDF、pfile):| **はい** | **はい** | いいえ|
|ラベルを適用するための PPDF のサポート:| **はい** | いいえ | いいえ |
|PowerShell のラベル付けコマンドレット:| **はい** | **はい** <sup>4</sup> | いいえ |
|保護アクションに対するオフライン サポート:| **はい** | **はい** <sup>5</sup> | **はい** |
|切断されたコンピューターの手動ポリシーファイル管理:| **はい** |**はい**| いいえ |
|HYOK のサポート:| **はい** | いいえ | いいえ |
|イベントビューアーの使用状況ログ:| **はい** | いいえ |いいえ |
|Outlook の [転送不可] ボタンを表示します。| **はい** | いいえ | いいえ |
|保護されたトラックの文書化:| **はい** | **はい** <sup>6</sup> | いいえ |
|保護されたドキュメントの取り消し:| **はい** | いいえ | いいえ |
|保護のみモード (ラベルなし):| **はい** | いいえ | いいえ |
|アカウントの切り替えのサポート:| いいえ | いいえ | **はい** |
|リモートデスクトップサービスのサポート:| **はい** | **はい** | **はい** |
|AD RMS のサポート:| **はい** | いいえ <sup>7</sup> | いいえ |
|アプリで外部コンテンツのマークを削除する:| **はい**| **はい**| いいえ|


脚注:

<sup>1</sup> これらの設定は、 [Azure portal で構成するアドバンストクライアント設定](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal)としてサポートされています。

<sup>2</sup> これらの設定とその他の多くは、 [PowerShell で構成する詳細設定](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)としてサポートされています。

<sup>3</sup> ファイルエクスプローラーと PowerShell でサポートされます。 Office アプリでは、ユーザーは**ファイル情報**[ドキュメントの保護] [アクセスの制限] を選択でき  >  **Protect Document**  >  **Restrict Access**ます。

<sup>4</sup> コンテナーファイル (zip) からの保護の削除はサポートされていません。

<sup>5</sup> ファイルエクスプローラーと PowerShell コマンドの場合、ユーザーはファイルを保護するためにインターネットに接続されている必要があります。

<sup>6</sup> クラシッククライアントでサポートされているドキュメント追跡サイトは、統合ラベル付けクライアントでサポートされていません。 ただし、ドキュメントを追跡するために最初に登録する必要がない場合は、 [中央レポート](../reports-aip.md) を使用して、Windows コンピューターから文書化されている保護されているかどうか、およびアクセスが許可または拒否されたかどうかを識別できます。 

<sup>7</sup> ラベル付けおよび保護操作はサポートされていません。 ただし、AD RMS 展開の場合、 [Active Directory Rights Management サービスモバイルデバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))を使用すると、ビューアーは保護されたドキュメントを開くことができます。


### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Azure Information Protection クライアントの詳細な比較

Azure Information Protection クライアント (クラシック) と Azure Information Protection の統一されたラベル付けクライアントの両方で同じ機能がサポートされている場合は、次の表を使用して、2つのクライアントの機能上の違いを特定してください。

|機能 |従来のクライアント|統合ラベル付けクライアント|
|--------------|-----------------------------------|-----------------------------------------------------------|
|セットアップ:| ローカルのデモ ポリシーをインストールするオプション | ローカルのデモ ポリシーなし|
|Office アプリで適用した場合のラベルの選択と表示:|リボン上の **[保護]** ボタンから <br /><br /> Information Protection バーから (リボンの下の水平バー)|リボン上の **[秘密度]** ボタンから<br /><br /> Information Protection バーから (リボンの下の水平バー)|
|Office アプリの Information Protection バーを管理する:|ユーザー向け:  <br /><br />- リボン上の **[保護]** ボタンからバーを表示または非表示にするオプション<br /><br />- ユーザーがバーを非表示にするよう選択した場合、既定では、バーはそのアプリ内で非表示になりますが、新しく開いたアプリでは自動的に表示され続けます <br /><br /> 管理者向け:  <br /><br />- アプリを最初に開いたときにバーを自動的に表示または非表示にする、および、ユーザーがバーの非表示を選択した後に新しく開いたアプリに対してバーを自動的に非表示のままにするかどうかを制御するポリシー設定|ユーザー向け:  <br /><br />- リボン上の **[秘密度]** ボタンからバーを表示または非表示にするオプション<br /><br />- ユーザーがバーを非表示にするよう選択すると、バーはそのアプリ内でも新しく開いたアプリ内でも非表示になります <br /><br />管理者向け:  <br /><br />-バーを管理するための PowerShell 設定 |
|ラベルの色:  | Azure portal で構成する | ラベルの移行後に保持され、 [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)で構成可能|
|ラベルは、さまざまな言語をサポートします。| Azure portal で構成する | [Office 365 セキュリティ & コンプライアンス PowerShell](/microsoft-365/compliance/create-sensitivity-labels#additional-label-settings-with-office-365-security--compliance-center-powershell)を使用して構成する|
|ポリシーの更新: | Office アプリを開いたとき <br /><br /> 右クリックしてファイルまたはフォルダーを分類して保護したとき <br /><br />ラベル付けと保護のために PowerShell コマンドレット を実行したとき<br /><br />24 時間ごと <br /><br />スキャナーの場合: 1 時間ごと、およびサービスが開始され、ポリシーが1時間を経過した場合| Office アプリを開いたとき <br /><br /> 右クリックしてファイルまたはフォルダーを分類して保護したとき <br /><br />ラベル付けと保護のために PowerShell コマンドレット を実行したとき<br /><br />4 時間ごと <br /><br />スキャナーの場合: 4 時間ごと|
|サポートされている PDF 形式:| 保護: <br /><br /> - PDF の暗号化における ISO 標準 (既定) <br /><br /> - .ppdf <br /><br /> 消費:  <br /><br /> - PDF の暗号化における ISO 標準 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保護| 保護: <br /><br /> - PDF の暗号化における ISO 標準 <br /><br /> <br /><br /> 消費:  <br /><br /> - PDF の暗号化における ISO 標準 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保護|
|ビューアーで開かれた一般的な保護されたファイル (pfile):| ファイルは元のアプリで開き、保護なしで表示、変更、および保存できます。 | ファイルは元のアプリで開くことができ、それを表示して変更することはできますが、保存することはできません。|
|サポートされているコマンドレット:| ラベル付けのためのコマンドレットと保護のみのコマンドレット | ラベル付け用のコマンドレット:<br /><br /> Set-aipfileclassification と Set-aipfilelabel は *Owner* パラメーターをサポートしていません <br /><br /> さらに、ラベルが適用されないすべてのシナリオに対して、"No label to apply" (適用するラベルがありません) というコメントが 1 つ付きます <br /><br /> Set-aipfileclassification は *WhatIf* パラメーターをサポートするため、検出モードで実行できます。 <br /><br /> Set-AIPFileLabel は *EnableTracking* パラメーターをサポートしていません <br /><br /> Get-AIPFileStatus は他のテナントからのラベル情報を返しません。また、*RMSIssuedTime* パラメーターを表示しません<br /><br />また、Get-AIPFileStatus の*Labelingmethod*パラメーターには、**手動**または**自動**ではなく**Privileged**または**Standard**が表示されます。 詳細については、[オンライン ドキュメント](/powershell/module/azureinformationprotection/get-aipfilestatus)をご覧ください。|
|Office でのアクションごとの理由プロンプト (構成している場合): | 頻度: ファイルあたり <br /><br /> 秘密度レベルを下げる <br /><br /> ラベルの削除<br /><br /> 保護の削除 | 頻度: セッションごと <br /><br /> 秘密度レベルを下げる<br /><br /> ラベルの削除|
|適用されたラベルのアクションを削除する: | ユーザーは確認するよう求められます <br /><br />既定のラベルや自動ラベル (構成している場合) は、Office アプリで次にファイルを開いたときに自動的に適用されません  <br /><br />| ユーザーは確認するよう求められません<br /><br /> 既定のラベルや自動ラベル (構成している場合) は、Office アプリで次にファイルを開いたときに自動的に適用されます|
|自動および推奨ラベル: | 組み込みの情報の種類と、語句や正規表現を使ったカスタム条件を使って、Azure portal で[ラベル条件](../configure-policy-classification.md)として構成されます <br /><br />構成のオプションには、次のようなものがあります。 <br /><br />- 一意の / 一意でない数 <br /><br /> - 最小数| 組み込みの機密情報の種類と[カスタムの情報の種類](https://docs.microsoft.com/microsoft-365/compliance/create-a-custom-sensitive-information-type)を使用して、管理センターで構成されます<br /><br />構成のオプションには、次のようなものがあります。  <br /><br />- 一意の数のみ <br /><br />- 最小および最大数 <br /><br />- 情報の種類での AND と OR のサポート <br /><br />- キーワード ディクショナリ<br /><br />- カスタマイズ可能な信頼度レベルと文字の近接|
|添付ファイルのサブラベルのサポートを注文します。 | [クライアントの詳細設定](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)で有効 | 既定で有効になっています。構成は必要ありません|
|ファイルの種類の既定の保護動作を変更します。 | [レジストリの編集](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)を使用して、ネイティブ保護と汎用保護の既定値を上書きすることができます。 | [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)を使用して、保護するファイルの種類を変更できます。|
|自動再スキャン | スキャナーがポリシーまたはラベル設定の変更を検出するたびに、フルスキャンが自動的に実行されます。 | バージョン [2.8.85](unifiedlabelingclient-version-release-history.md#version-2885-public-preview)以降では、ポリシーまたはコンテンツスキャンジョブの設定を変更した後、完全な再スキャンをスキップするように管理者が選択できます。 |
|ネットワーク検出 |クラシックスキャナーではネットワーク探索機能を使用できません | 管理者は、指定された IP アドレスまたは範囲をスキャンすることで、他の危険なリポジトリを検出できます。|
| | | |

特定の保護設定の動作の違いの詳細な比較については、「 [ラベルの保護設定の動作の比較](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label)」を参照してください。

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合されたラベル付けクライアントに含まれていない機能

Azure Information Protection 統合されたラベル付けクライアントはまだ開発中ですが、従来のクライアントとの次の機能と動作の違いは、現在、統合されたラベル付けクライアントの今後のリリースで使用できるとは想定されていません。 

- [Office アプリでユーザーが選択できる別のオプション](client-classify-protect.md#set-custom-permissions-for-a-document)としてのカスタムアクセス許可: Word、Excel、PowerPoint

- Office アプリとエクスプローラーのオプションを[追跡および取り消す](client-track-revoke.md)

- Information Protection バーのタイトルとヒント

- テンプレートを使用した[保護のみのモード](client-protection-only-mode.md)(ラベルなし)

- ドキュメントを ppdf として保護する [(古い形式)](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)

- Outlook の [ **転送不可** ] ボタンを表示する

- デモ ポリシー

- 確認プロンプト **[このラベルを削除しますか?]** ポリシー設定を使用しない場合、ユーザーに対してこのラベルを削除します。

- Rights Management サービスに接続するために PowerShell コマンドレットを分離させる

- ラベルを適用したユーザー id の表示


### <a name="parent-labels-and-their-sublabels"></a>親ラベルとそのサブラベル 

Azure Information Protection クライアント (クラシック) では、サブラベルを持つ親ラベルを指定する構成はサポートされていません。 これらの構成には、既定のラベルと、推奨または自動分類のラベルの指定が含まれます。 ラベルにサブラベルがある場合は、親ラベルではなく、サブラベルのいずれかを指定できます。

パリティについて、Azure Information Protection 統合ラベル付けクライアントでも、管理センターでこれらのラベルを選択できる場合でも、サブラベルのある親ラベルの適用はサポートされていません。 このシナリオでは、Azure Information Protection 統合ラベル付けクライアントで親ラベルが適用されません。

## <a name="next-steps"></a>次の手順

Azure Information Protection クライアントをインストールして構成するには、次のドキュメントを参照してください。

- [Azure Information Protection クライアント](AIP-client.md)

- [Azure Information Protection 統合されたラベル付けクライアント](unifiedlabelingclient-version-release-history.md)

Office 365 アプリ用の組み込みのラベル付けクライアントの使用の詳細については、「 [office アプリの感度ラベル](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)」を参照してください。
