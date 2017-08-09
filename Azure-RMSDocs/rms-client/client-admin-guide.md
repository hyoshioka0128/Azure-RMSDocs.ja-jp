---
title: "Azure Information Protection クライアント管理者ガイド"
description: "Windows 用 Azure Information Protection クライアントのデプロイを担当するエンタープライズ ネットワークの管理者向けの手順および情報です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 275f08ca0ea267c29f5b743300507d66ee1d1118
ms.sourcegitcommit: 7cd6ff39731c7abe990a72a49bc10d104f47764d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2017
---
# <a name="azure-information-protection-client-administrator-guide"></a>Azure Information Protection クライアント管理者ガイド

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

エンタープライズ ネットワークで Azure Information Protection クライアントを担当している場合、または [Azure Information Protection クライアント ユーザー ガイド](client-user-guide.md) に関するページに記載されていない詳細な技術情報が必要な場合は、このガイドの情報をご覧ください。 

たとえば、

- このクライアントのさまざまなコンポーネントについて知り、インストールする必要があるかどうかを理解する

- 前提条件、インストール オプションとパラメーター、検証チェックに関する情報を含む、ユーザー向けにクライアントをインストールする方法

- 通常レジストリの編集が必要なカスタムの構成に対応する方法

- クライアント ファイルと使用状況ログを検索する

- クライアントでサポートされているファイルの種類を識別する

- ユーザー用のドキュメント追跡サイトを構成して使用する

- クライアントで PowerShell を使用したコマンドラインでの制御

**このドキュメントでわからない問題がある場合は**、 [Azure Information Protection についての Yammer サイト](https://www.yammer.com/AskIPTeam)をご覧ください。 

## <a name="technical-overview-of-the-azure-information-protection-client"></a>Azure Information Protection クライアントの技術的概要

Azure Information Protection クライアントには次のものが含まれます。

- Office アドオン。ユーザーが分類ラベルを選択するための Azure Information Protection バーと、追加オプションのためのリボンの **[保護]** ボタンをインストールします。

- エクスプローラー。ユーザーがファイルに分類ラベルと保護を適用するための右クリック オプション。

- ネイティブ アプリケーションで開くことができないときに、保護されたファイルを表示するビューアー。

- ファイルに対して分類ラベルと保護を適用および削除するための PowerShell モジュール。

- Azure Rights Management (Azure RMS) または Active Directory Rights Management サービス (AD RMS) と通信する Rights Management クライアント。

Azure Information Protection クライアントは、Azure サービス (Azure Information Protection とそのデータ保護サービス、Azure Rights Management) と併用すると最適です。 ただし、いくつか制限はありますが、オンプレミス バージョンの Rights Management である AD RMS でも使用できます。 Azure Information Protection と AD RMS でサポートされている機能の包括的な比較については、「[Azure Information Protection と AD RMS の比較](../understand-explore/compare-azure-rms-ad-rms.md)」をご覧ください。 

AD RMS を所有していて、Azure Information Protection に移行する場合は、「[AD RMS から Azure Information Protection に移行する](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」をご覧ください。


## <a name="should-you-deploy-the-azure-information-protection-client"></a>Azure Information Protection クライアントのデプロイが必要な場合

次のいずれかが当てはまる場合は、Azure Information Protection クライアントをデプロイします。

- Office アプリケーション (Word、Excel、PowerPoint、Outlook) 内からラベルを選んで、ドキュメントとメール メッセージを分類 (および必要に応じて保護) したい。

- 追加のファイルの種類、複数選択、およびフォルダーをサポートするエクスプローラーを使って、ドキュメントとメール メッセージを分類 (および必要に応じて保護) したい。

- PowerShell コマンドを使って、ドキュメントを分類 (および必要に応じて保護) するスクリプトを実行したい。

- ファイルを表示するネイティブ アプリケーションがインストールされていないか、ドキュメントを開くことができない場合に、保護されているドキュメントを表示したい。

- エクスプローラーまたは PowerShell コマンドを使って、単にファイルを保護したい。

- ユーザーと管理者が保護されたドキュメントの追跡および取り消しを行えるようにしたい。

- データ回復のために一括してファイルやコンテナーから暗号化を解除 (保護解除) したい。

- Office 2010 を実行していて、Azure Rights Management サービスを使ってドキュメントとメール メッセージを保護したい。

次の例では、Office アプリケーションの Azure Information Protection クライアント アドオン、組織に対する分類ラベル、リボンの新しい **[保護]** ボタンが示されています。

![Azure Information Protection バーと既定のポリシー](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>ユーザー向けに Azure Information Protection クライアントをインストールする方法

クライアントをインストールする前に、「[Azure Information Protection の要件](../get-started/requirements-azure-rms.md)」で Azure Information Protection に必要なオペレーティング システムのバージョンとアプリケーションがコンピューターにインストールされていることを確認してください。 

次に、Azure Information Protection クライアントに必要な追加の前提条件を確認します。

### <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントの追加の前提条件

- Microsoft .NET Framework 4.6.2
    
    Azure Information Protection クライアントを完全にインストールするには、既定では Microsoft .NET Framework 4.6.2 の最小バージョンが必要です。これがない場合、インストーラーでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。 推奨はされていませんが、[カスタム インストール パラメーター](#more-information-about-the-downgradedotnetrequirement-installation-parameter)を使用してこの要件を省略できます。

- Microsoft .NET Framework 4.5.2
    
    Azure Information Protection ビューアーを別にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。これがない場合、インストーラーではダウンロードまたはインストールされません。

- Windows PowerShell バージョン 4.0
    
    クライアント用の PowerShell モジュールには、Windows PowerShell バージョン 4.0 が必要で、以前のオペレーティング システムにインストールする必要がある場合があります。 詳細については、「[How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)」(Windows PowerShell 4.0 のインストール方法) を参照してください。 インストーラーでは、この前提条件のチェックやインストールは行われません。 実行中の Windows PowerShell のバージョンを確認するには、PowerShell セッションで「`$PSVersionTable`」と入力します。

- Microsoft Online Services サインイン アシスタント 7.250.4303.0
    
    Office 2010 を実行するコンピューターには、Microsoft Online Services サインイン アシスタント バージョン 7.250.4303.0 が必要です。 このバージョンは、クライアントのインストールに含まれています。 新しいバージョンのサインイン アシスタントがある場合は、これをアンインストールしてから Azure Information Protection クライアントをインストールしてください。 たとえば、バージョンを確認し、**[コントロール パネル]** > **[プログラムと機能]** > **[プログラムのアンインストールまたは変更]** を使用して、サインイン アシスタントをアンインストールします。

- KB 2533623
    
    Windows 7 Service Pack 1 を実行しているコンピューターには、KB 2533623 が必要です。 この更新プログラムの詳細については、「[マイクロソフト セキュリティ アドバイザリ: 安全でないライブラリの読み込みにより、リモートでコードが実行される](https://support.microsoft.com/en-us/kb/2533623)」を参照してください。 この更新プログラムは直接インストールすることもでき、また、その更新プログラムを包括する別の更新プログラムによって置き換えられることもあります。
    
    この必要な更新プログラムがインストールされていない場合、クライアントのインストールにより、インストールが必要だと警告が表示されます。 クライアントのインストール後にこの更新プログラムをインストールできますが、一部の操作はブロックされ、メッセージが再び表示されます。  

- Office アプリケーションに対して **Microsoft Azure Information Protection** アドインを無効にしないでください
    
    グループ ポリシー設定の **[管理対象アドインの一覧]** を構成した場合は、Microsoft Azure Information Protection の次のプログラム識別子 (ProgID) を指定して、Office アプリケーションの Azure Information Protection アドインを追加し、オプションを **1 (アドインは常に有効)** に設定します。
    
    - Outlook の場合: `MSIP.OutlookAddin`
    
    - Word の場合: `MSIP.WordAddin`
    
    - Excel の場合: `MSIP.ExcelAddin`
    
    - PowerPoint の場合: `MSIP.PowerPointAddin`
    
    この **[管理対象アドインの一覧]** グループ ポリシー設定を構成していなくても、Microsoft Azure Information Protection アドインが無効になることを示すレポートを取得した場合は構成する必要がある場合があります。 このアドインが無効の場合は、Office アプリケーションに Azure Information Protection バーが表示されません。
    
    このグループ ポリシー設定の詳細については、「[No Add-ins loaded due to group policy settings for Office 2013 and Office 2016 programs](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)」 (Office 2013 および Office 2016 プログラムのグループ ポリシー設定によりアドインが読み込まれない) を参照してください。

> [!IMPORTANT]
> Azure Information Protection クライアントのインストールには、ローカル管理者権限が必要です。


### <a name="options-to-install-the-azure-information-protection-client-for-users"></a>ユーザー向けに Azure Information Protection クライアントをインストールするオプション

ユーザー向けにクライアントをインストールするオプションは次の 3 つです。

**Windows Update**: Azure Information Protection クライアントは、Microsoft Update カタログに含まれているため、カタログを使用する任意のソフトウェア更新プログラム サービスを使用して、クライアントをインストールおよび更新することができます。

**実行可能ファイル (.exe) のバージョンのクライアントを実行する**: 対話形式またはサイレント モードで実行できるお勧めのインストール方法です。 この方法ではインストーラーが前提条件の多くを確認し、満たされていない前提条件を自動的にインストールできるため、柔軟性に優れたお勧めの方法です。 [手順](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)

**Windows インストーラー (.msi) バージョンのクライアントを展開する**: グループ ポリシー、構成マネージャー、Microsoft Intune などの一元的な展開メカニズムを使用するサイレント インストールでのみサポートされています。 Intune とモバイル デバイス管理 (MDM) で管理されている Windows 10 PC では、インストールで実行可能ファイルがサポートされていないため、この方法が必要です。 ただし、このインストール方法を使用する場合は、依存関係にあるソフトウェアの確認と、インストールまたはアンインストールを手動で行う必要があります。実行可能ファイルのインストーラーであれば、各コンピューターでインストーラーによってこの作業が実行されます。 [手順](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>実行可能ファイルのインストーラーを使用して Azure Information Protection クライアントをインストールするには

Microsoft Update カタログを使用していない場合、または Intune などの一元的な展開方法を使用して .msi を展開する場合は、次の手順に従ってクライアントをインストールします。

1. 実行可能ファイル バージョンの Azure Information Protection クライアントを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードします。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。 

2. 既定のインストールは、実行可能ファイル (たとえば **AzInfoProtection.exe**) を実行するだけです。 一方、インストール オプションを表示するには、**/help** を付けて実行可能ファイルを実行します。`AzInfoProtection.exe /help`

    サイレント モードでクライアントをインストールする例: `AzInfoProtection.exe /quiet`
    
    PowerShell コマンドレットだけをサイレント インストールする例: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    ヘルプ画面に表示されていない追加のパラメーター:
    
    - Office 2010 を実行するコンピューターにクライアントをインストールするとき、ユーザーがそのコンピューターのローカル管理者ではない場合またはそのユーザーを表示したくない場合は、**ServiceLocation** パラメーターを指定します。 [詳細情報](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: MICROSOFT.NET Framework 4.6.2 のバージョンの要件を省略する場合にこのパラメーターを使用します。 [詳細情報](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry=0**: このパラメーターは、インストール オプション **[Microsoft に利用状況の統計を送信して、Azure Information Protection の改善に協力します]** を無効にするときに使用します。 
    
3. 対話形式でインストールする場合、Office 365 または Azure Active Directory に接続できないが、デモンストレーション用にローカル ポリシーを使って Azure Information Protection のクライアント側を表示し、操作するには、**デモ ポリシー**をインストールするオプションを選択します。 クライアントの Azure Information Protection サービスへの接続時に、このデモ ポリシーは、組織の Azure Information Protection ポリシーに置き換えられます。
    
4. インストールを完了するには: 

    - お使いのコンピューターが Office 2010 を実行する場合は、コンピューターを再起動します。 
        
        ServiceLocation パラメーターを指定してクライアントをインストールしなかった場合は、Azure Information Protection バーを使う Office アプリケーション (Word など) を初めて開くときに、この初回使用時にレジストリを更新するプロンプトを確認する必要があります。 [サービス検索](../rms-client/client-deployment-notes.md#rms-service-discovery)はレジストリ キーの設定に使用されます。 
    
    - その他のバージョンの Office では、Office アプリケーションとエクスプローラーのインスタンスをすべて再起動します。 
        
5. 既定で %temp% フォルダーに作成されるインストール ログ ファイルを確認することで、インストールが成功したか確認できます。 インストール パラメーター **/log** を使用してこの場所を変更できます。 
 
    このファイルの名前は次の形式です: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    例: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    このログ ファイルで、次の文字列を検索します: **製品: Microsoft Azure Information Protection -- インストールを正しく完了しました。** インストールに失敗した場合、このログ ファイルには、問題の特定と解決に役立つ詳細が含まれます。

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>ServiceLocation インストール パラメーターの詳細について

Office 2010 を使っていてローカル管理者権限を持たないユーザーのためにクライアントをインストールするときは、ServiceLocation パラメーターと Azure Rights Management サービスの URL を指定します。 このパラメーターと値により、次のレジストリ キーが作成され、設定されます。

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

次の手順で、ServiceLocation パラメーターに指定する値を特定します。 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>ServiceLocation パラメーターに指定する値を特定するには

1. PowerShell セッションから、最初に [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) を実行し、管理者の資格情報を指定して Azure Rights Management サービスに接続します。 [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration) を実行します。 
 
    Azure Rights Management サービス用の PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

2. 出力から、 **LicensingIntranetDistributionPointUrl** の値を確認します。

    例: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. この値から、**/_wmcs/licensing** 文字列を削除します。 例: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    残りの文字列は、ServiceLocation パラメーターに指定する値です。

Office 2010 と Azure RMS のクライアントのサイレント インストールの例: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>DowngradeDotNetRequirement インストール パラメーターの詳細について

Windows Update を使用して自動アップグレードをサポートし、Office アプリケーションとの信頼性の高い統合のため、Azure Information Protection クライアントは Microsoft .NET Framework バージョン 4.6.2 を使用します。 既定では、インストールのこのバージョンを確認し、ない場合はインストールしようとします。 インストール後はコンピューターの再起動が必要です。

この Microsoft .NET Framework の新しいバージョンのインストールが現実的ではない場合は、**DowngradeDotNetRequirement = True** パラメーターと値を使用してクライアントをインストールすることで、Microsoft .NET Framework バージョン 4.5.1 がインストールされていれば要件を省略できます。

例: `AzInfoProtection.exe DowngradeDotNetRequirement=True`

このパラメーターは、Azure Information Protection クライアントが Microsoft .NET Framework の以前のバージョンと共に使用すると Office アプリケーションがハングする問題が報告されていることを把握したうえで注意して使用することをお勧めします。 ハングすることがある場合は、その他のトラブルシューティングを行う前に推奨されているバージョンにアップグレードしてください。 

Windows Update を使用して Azure Information Protection クライアントを最新の状態に保っている場合は、別のソフトウェアの展開方法でクライアントを新しいバージョンに保つ必要があることにも注意してください。

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>.msi インストーラーを使用して Azure Information Protection クライアントをインストールするには

一元的な展開の場合は、Azure Information Protection クライアントの msi インストール バージョン固有の次の情報をご覧ください。 

ソフトウェアの展開方法に Intune を使用する場合は、次の手順を実行するとともに、「[Microsoft Intune でアプリを追加する](/intune/deploy-use/add-apps)」をご覧ください。

1. Azure Information Protection クライアントの .msi バージョンを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードします。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。 

2. .msi ファイルを実行する各コンピューターで、次のソフトウェアの依存関係が満たされていることを確認する必要があります。 たとえば、.msi バージョンのクライアントとこれらをまとめるか、次の依存関係を満たすコンピューターにのみ展開します。
    
    |Office のバージョン|オペレーティング システム|ソフトウェア|操作|
    |--------------------|--------------|----------------|---------------------|
    |Office 2013|サポートされているすべてのバージョン|[KB 3054941](https://www.microsoft.com/en-us/download/details.aspx?id=49337)<br /><br /> ファイル名に含まれるバージョン番号: v3|インストール|
    |Office 2010|サポートされているすべてのバージョン|[Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> バージョン: 2.1|インストール|
    |Office 2010|Windows 8.1 と Windows Server 2012 R2|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB 2843630 または KB 2919355 がインストールされていない場合はインストールします|
    |Office 2010|Windows 8 と Windows Server 2012|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|インストール|
    |Office 2010|Windows 7|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB 3125574 がインストールされていない場合はインストールします|
    |該当なし|Windows 7|KB 2627273 <br /><br /> ファイル名に含まれるバージョン番号: v4|アンインストール|
    
    Office 2016 のための依存関係の追加はありません。

3. 既定のインストールでは、`AzInfoProtection.msi /quiet` のように、**/quiet** を付けて .msi を実行します。 ただし、[実行可能ファイルのインストーラーの手順](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)に記載されている追加のインストール パラメーターを指定する必要がある場合があります。  

## <a name="additional-checks-and-troubleshooting"></a>追加のチェックとトラブルシューティング

**[ヘルプとフィードバック]** オプションで **[Microsoft Azure Information Protection]** ダイアログ ボックスを開きます。

- Office アプリケーションから、**[ホーム]** タブの **[保護]** グループで、**[保護]**、**[ヘルプとフィードバック]** の順に選択します。

- エクスプローラーから単一ファイル、複数ファイル、またはフォルダーを右クリックで選択し、**[分類して保護する]**、**[ヘルプとフィードバック]** の順に選択します。 

### <a name="help-and-feedback-section"></a>**[ヘルプとフィードバック]** セクション

既定では、**詳細を表示するリンク**から [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) の Web サイトに移動しますが、Azure Information Protection ポリシー内で[ポリシー設定](../deploy-use/configure-policy-settings.md)の 1 つとしてカスタム URL の構成を行えます。

**[フィードバックの送信]** リンクを使って、Information Protection チームに提案または要求を送信します。 テクニカル サポートの場合はこのオプションを使わず、代わりに「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」をご覧ください。 

**ログのエクスポート**は、Azure Information Protection クライアントのログ ファイルの収集と添付を自動的に行うもので、Microsoft サポートから要求された場合にこれらのログ ファイルを送信します。 このオプションは、エンド ユーザーがログ ファイルをヘルプ デスクに送信するために使用することもできます。

診断情報を取得し、クライアントをリセットするには、**[診断の実行]** を選択します。 診断テストが完了したら、**[結果のコピー]** をクリックして情報を電子メールに貼り付け、ヘルプ デスクまたは Microsoft サポートに送信できます。 テストの完了時に、クライアントをリセットすることもできます。

> [!NOTE]
> プレビュー バージョンのクライアントでは、**[診断の実行]** が削除され、**[設定のリセット]** に置き換わります。 さらに、このオプションの動作は[変更されています](#more-information-about-the-reset-option-for-the-current-preview-version-of-the-azure-information-protection-client)。

#### <a name="more-information-about-the-reset-option-for-the-general-availability-ga-version-of-the-azure-information-protection-client"></a>Azure Information Protection クライアントの一般公開 (GA) バージョンのリセット オプションに関する詳細

- このオプションを使用するためにローカル管理者の権限は必要ありません。また、この操作はイベント ビューアーのログに記録されません。 

- ファイルがロックされていない限り、この操作で **%LocalAppData%\Microsoft\MSIPC** 内のすべてのファイルが削除されます。これは、クライアント証明書と Rights Management テンプレートが格納されている場所です。 この操作では、Azure Information Protection ポリシーまたはクライアント ログ ファイルは削除されません。また、ユーザーはサインアウトされません。

- **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC** のレジストリ キーと設定は削除されます。 このレジストリ キーの設定を構成した場合、クライアントをリセットした後に、レジストリ設定を再構成する必要があります。 たとえば、AD RMS から移行しても、内部ネットワーク上にまだサービス接続ポイントがあるため、Azure Information Protection テナントへのリダイレクトの設定を構成する場合があります。

- クライアントをリセットした後は、クライアントの証明書と最新のテンプレートのダウンロードを行い、ユーザー環境を再初期化する必要があります。 再初期化を実行するには、すべての Office インスタンスを終了し、Office アプリケーションを再起動します。 この操作で、最新の Azure Information Protection ポリシーをダウンロードしたことも確認されます。 この確認が完了するまで、診断テストは再実行しないでください。

#### <a name="more-information-about-the-reset-option-for-the-current-preview-version-of-the-azure-information-protection-client"></a>Azure Information Protection クライアントの現在のプレビュー バージョンのリセット オプションに関する詳細

- このオプションを使用するためにローカル管理者の権限は必要ありません。また、この操作はイベント ビューアーのログに記録されません。 

- ファイルがロックされている場合を除き、この操作は、次の場所のすべてのファイルを削除します。 これらのファイルには、クライアント証明書、Rights Management テンプレート、Azure Information Protection ポリシーおよびキャッシュされたユーザーの資格情報が含まれます。 クライアント ログ ファイルは削除されません。
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- 次のレジストリ キーと設定が削除されます。 これらいずれかのレジストリ キーの設定を構成した場合、クライアントをリセットした後に、設定を再構成する必要があります。 たとえば、AD RMS から移行しても、内部ネットワーク上にまだサービス接続ポイントがあるため、Azure Information Protection テナントへのリダイレクトの設定を構成する場合があります。
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- 現在サインインしているユーザーは、サインアウトします。

### <a name="client-status-section"></a>**クライアント ステータス** セクション

**接続**の値を使って、表示されているユーザー名が Azure Information Protection 認証に使用されるアカウントを識別するか確認します。 このユーザー名は、Office 365 または Azure Active Directory に使用しているアカウントに一致する必要があります。 また、アカウントも、Azure Information Protection 用に構成されたテナントに属している必要があります。

表示されているユーザーとは別のユーザーでサインインする必要がある場合は、[別のユーザーでのサインイン](client-admin-guide-customizations.md#sign-in-as-a-different-user)に関するページのカスタマイズをご覧ください。

**[前回の接続]** には、クライアントが組織の Azure Information Protection サービスに前回接続した時刻が表示されます。 この情報と **[<日時> に Information Protection ポリシーがインストールされました]** を使用して、Azure Information Protection ポリシーが最後にインストールまたは更新された日時を確認できます。 クライアントはサービスへの接続時に、現在のポリシーからの変更を見つけると最新のポリシーを自動的にダウンロードし、24 時間ごとに確認を行います。 表示された時刻以降にポリシーを変更している場合は、Office アプリケーションを閉じて再度開きます。

**このクライアントには Office Professional Plus 用のライセンスがありません**というメッセージが表示された場合、Azure Information Protection クライアントはインストールされている Office のエディションが Rights Management による保護の適用をサポートしていないことを検出しています。 この検出が行われると、保護を適用するラベルは Azure Information Protection バーには表示されません。

**[バージョン]** 情報を使用して、どちらのバージョンのクライアントがインストールされているか確認します。 **新機能**のリンクをクリックし、クライアントの[バージョン リリース履歴](client-version-release-history.md)を読むことで、使用しているクライアントが最新のリリースバージョンかどうかや、各バージョンの修正と新しい機能を確認できます。

## <a name="support-for-multiple-languages"></a>複数言語のサポート

Azure Information Protection クライアントでは、Office でサポートされるクライアント言語がすべてサポートされます。 たとえば、メニュー オプション、ダイアログ ボックス、およびメッセージはユーザーの言語で表示されます。 言語を検出するインストーラーが 1 つあるため、他言語のクライアントをインストールするための追加の構成は必要ありません。 

ただし、ユーザーに表示されるラベル名は、[既定のポリシー](../deploy-use/configure-policy-default.md)や指定されたラベル名に応じて自動的には翻訳されません。 ユーザーが他言語でラベルを表示できるようにするには、独自の翻訳を指定し、その翻訳を使用するように Azure Information Protection ポリシーを構成する必要があります。 詳細については、「[Azure Information Protection で他の言語用ラベルを構成する方法](../deploy-use/configure-policy-languages.md)」を参照してください。

## <a name="to-uninstall-the-azure-information-protection-client"></a>Azure Information Protection クライアントをアンインストールするには

次のどの方法も使用できます。

- コントロール パネルを使って、プログラムをアンインストールします。**[Microsoft Azure Information Protection]**  >  **[アンインストール]** をクリックします。

- 実行可能ファイル (例: **AzInfoProtection.exe**) を再実行し、**[セットアップの変更]** ページの **[アンインストール]** をクリックします。 

- **/uninstall** を付けて実行可能ファイルを実行します。 例: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>次のステップ
Azure Information Protection クライアントをインストールしたので、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
