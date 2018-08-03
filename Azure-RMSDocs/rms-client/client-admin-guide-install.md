---
title: ユーザー向けに Azure Information Protection クライアントをインストールする
description: 管理者が企業ネットワークに Windows 用 Azure Information Protection クライアントをデプロイするための手順と情報です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/26/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: af9cfca4d328dba7646c1c319744476fe0e6b43f
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474173"
---
# <a name="admin-guide-install-the-azure-information-protection-client-for-users"></a>管理者ガイド: ユーザー向けに Azure Information Protection クライアントをインストールする

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

企業ネットワークに Azure Information Protection クライアントをインストールする前に、「[Azure Information Protection の要件](../requirements.md)」で Azure Information Protection に必要なオペレーティング システムのバージョンとアプリケーションがコンピューターにインストールされていることを確認してください。 

次に、次のセクションに記載されている、Azure Information Protection クライアントに必要な追加の前提条件を確認します。 インストール プログラムでは、一部の前提条件が確認されません。

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントの追加の前提条件

- Microsoft .NET Framework 4.6.2
    
    Azure Information Protection クライアントを完全にインストールするには、既定では Microsoft .NET Framework 4.6.2 の最小バージョンが必要です。これがない場合、実行可能インストーラーのセットアップ ウィザードでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。 推奨はされていませんが、この要件は、セットアップ ウィザードを使用する際に、[カスタム インストール パラメーター](#more-information-about-the-downgradedotnetrequirement-installation-parameter)を使用することで省略できます。
    
    この前提条件は、実行可能インストーラー、Windows Update、または Windows インストーラーを使用してクライアントをサイレント モードでインストールする場合には、自動的にはインストールされていません。 これらのシナリオでは、必要に応じてこの前提条件をインストールしてください。そうしないと、インストールが失敗します。 Microsoft .NET Framework 4.6.2 (オフライン インストーラー) は、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53344)からダウンロードできます。

- Microsoft .NET Framework 4.5.2
    
    Azure Information Protection ビューアーを別にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。これがない場合、実行可能インストーラーではダウンロードまたはインストールされません。

- Windows PowerShell バージョン 4.0
    
    クライアント用の PowerShell モジュールには、Windows PowerShell バージョン 4.0 が必要で、以前のオペレーティング システムにインストールする必要がある場合があります。 詳細については、「[How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)」(Windows PowerShell 4.0 のインストール方法) を参照してください。 インストーラーでは、この前提条件のチェックやインストールは行われません。 実行中の Windows PowerShell のバージョンを確認するには、PowerShell セッションで「`$PSVersionTable`」と入力します。

- Microsoft Online Services サインイン アシスタント 7.250.4303.0
    
    Office 2010 を実行するコンピューターには、Microsoft Online Services サインイン アシスタント バージョン 7.250.4303.0 が必要です。 このバージョンは、クライアントのインストールに含まれています。 新しいバージョンのサインイン アシスタントがある場合は、これをアンインストールしてから Azure Information Protection クライアントをインストールしてください。 たとえば、バージョンを確認し、**[コントロール パネル]** > **[プログラムと機能]** > **[プログラムのアンインストールまたは変更]** を使用して、サインイン アシスタントをアンインストールします。

- KB 2533623
    
    Windows 7 Service Pack 1 を実行しているコンピューターには、KB 2533623 が必要です。 この更新プログラムの詳細については、「[マイクロソフト セキュリティ アドバイザリ: 安全でないライブラリの読み込みにより、リモートでコードが実行される](https://support.microsoft.com/en-us/kb/2533623)」を参照してください。 この更新プログラムは直接インストールすることもでき、また、その更新プログラムを包括する別の更新プログラムによって置き換えられることもあります。
    
    この必要な更新プログラムがインストールされていない場合、クライアントのインストールにより、インストールが必要だと警告が表示されます。 クライアントのインストール後にこの更新プログラムをインストールできますが、一部の操作はブロックされ、メッセージが再び表示されます。  

- Visual Studio 2015 の Visual C++ 再頒布可能パッケージ (32 ビット バージョン)
    
    Windows 7 Service Pack 1 を実行しているコンピューターでは、次のダウンロード ページから **vc_redist.x86.exe** をインストールしてください: [Visual Studio 2015 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
    
    クライアントのインストールでは、この前提条件は確認されませんが、Azure Information Protection クライアントで PDF ファイルを分類し保護する場合は必要になります。

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


## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>ユーザー向けに Azure Information Protection クライアントをインストールするオプション

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
 
    Azure Rights Management サービス用の PowerShell モジュールをまだインストールしていない場合は、「[AADRM PowerShell モジュールのインストール](../deploy-use/install-powershell.md)」を参照してください。

2. 出力から、 **LicensingIntranetDistributionPointUrl** の値を確認します。

    例: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. この値から、**/_wmcs/licensing** 文字列を削除します。 例: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    残りの文字列は、ServiceLocation パラメーターに指定する値です。

Office 2010 と Azure RMS のクライアントのサイレント インストールの例: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>DowngradeDotNetRequirement インストール パラメーターの詳細について

Windows Update を使用して自動アップグレードをサポートし、Office アプリケーションとの信頼性の高い統合のため、Azure Information Protection クライアントは Microsoft .NET Framework バージョン 4.6.2 を使用します。 既定では、実行可能ファイルによる対話型インストールによってこのバージョンが確認され、ない場合はインストールが試行されます。 インストール後はコンピューターの再起動が必要です。

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
    |Office 2016|サポートされているすべてのバージョン|64 ビット: [KB317866](https://www.microsoft.com/en-us/download/details.aspx?id=55007)<br /><br />32 ビット: [KB317866](https://www.microsoft.com/en-us/download/details.aspx?id=54999)<br /><br /> バージョン: 1.0|インストール|
    |Office 2013|サポートされているすべてのバージョン|64 ビット: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 ビット: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />バージョン: 1.0|インストール|
    |Office 2010|サポートされているすべてのバージョン|[Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> バージョン: 2.1|インストール|
    |Office 2010|Windows 8.1 と Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB2843630 または KB2919355 がインストールされていない場合はインストールします|
    |Office 2010|Windows 8 と Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|インストール|
    |Office 2010|Windows 7 および Windows Server 2008 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB3125574 がインストールされていない場合はインストールします|
    |適用できません|Windows 7|[vc_redist.x86.exe](https://www.microsoft.com/en-us/download/details.aspx?id=48145)|インストール|
    |適用できません|Windows 7|KB2627273 <br /><br /> ファイル名に含まれるバージョン番号: v4|アンインストール|

3. 既定のインストールでは、`AzInfoProtection.msi /quiet` のように、**/quiet** を付けて .msi を実行します。 ただし、[実行可能ファイルのインストーラーの手順](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)に記載されている追加のインストール パラメーターを指定する必要がある場合があります。  


## <a name="how-to-install-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーをインストールする方法

Azure Information Protection クライアントに含まれている PowerShell モジュールには、スキャナーをインストールし、構成するためのコマンドレットがあります。 ただし、スキャナーを使用するには、クライアントのフル バージョンをインストールする必要があります。PowerShell モジュールのみをインストールすることはできません。

このクライアントに付属するスキャナーをインストールするには、前のセクションの同じ手順に従います。 これでスキャナーをインストールする準備ができました。 インストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](../deploy-use/deploy-aip-scanner.md)」を参照してください。

## <a name="next-steps"></a>次の手順
Azure Information Protection クライアントをインストールしたので、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


