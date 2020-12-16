---
title: ユーザー用の Azure Information Protection クラシッククライアントをインストールする
description: 企業ネットワーク上の Windows 用 Azure Information Protection クラシッククライアントを展開するための管理者向けの手順と情報です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c14750bd4cbdbbc160b711640fc87d16ecce56f7
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583389"
---
# <a name="admin-guide-install-the-azure-information-protection-classic-client-for-users"></a>管理者ガイド: ユーザー用の Azure Information Protection クラシッククライアントをインストールする

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>***関連**: [Azure Information Protection Classic client for Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。
>
> **AIP クラシッククライアントをデプロイするに** は、サポートチケットを開いてダウンロードアクセスを取得します。

企業ネットワークに Azure Information Protection クライアントをインストールする前に、「[Azure Information Protection の要件](../requirements.md)」で Azure Information Protection に必要なオペレーティング システムのバージョンとアプリケーションがコンピューターにインストールされていることを確認してください。

次に、次のセクションに記載されている、Azure Information Protection クライアントに必要な追加の前提条件を確認します。 インストール プログラムでは、一部の前提条件が確認されません。

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントの追加の前提条件

- **Microsoft .NET Framework 4.6.2**

    Azure Information Protection クライアントを完全にインストールするには、既定では Microsoft .NET Framework 4.6.2 の最小バージョンが必要です。これがない場合、実行可能インストーラーのセットアップ ウィザードでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。 推奨はされていませんが、この要件は、セットアップ ウィザードを使用する際に、[カスタム インストール パラメーター](#more-information-about-the-downgradedotnetrequirement-installation-parameter)を使用することで省略できます。

    この前提条件は、実行可能インストーラー、Windows Update、または Windows インストーラーを使用してクライアントをサイレント モードでインストールする場合には、自動的にはインストールされていません。 これらのシナリオでは、必要に応じてこの前提条件をインストールしてください。そうしないと、インストールが失敗します。 Microsoft .NET Framework 4.6.2 (オフライン インストーラー) は、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=53344)からダウンロードできます。

- **Microsoft .NET Framework 4.5.2**

    Azure Information Protection ビューアーを別にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。これがない場合、実行可能インストーラーではダウンロードまたはインストールされません。

- **Windows PowerShell の最小バージョン4.0**

    クライアントの PowerShell モジュールには、Windows PowerShell 用の4.0 の最小バージョンが必要です。これは、以前のオペレーティングシステムにインストールする必要がある場合があります。 詳細については、「[How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)」(Windows PowerShell 4.0 のインストール方法) を参照してください。 インストーラーでは、この前提条件のチェックやインストールは行われません。 実行中の Windows PowerShell のバージョンを確認するには、PowerShell セッションで「`$PSVersionTable`」と入力します。

- **800 x 600 より大きい画面の解像度**

    解像度が 800 x 600 以下だと、エクスプローラーでファイルやフォルダーを右クリックしても、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスを完全に表示できません。

- **Microsoft Online Services サインイン アシスタント 7.250.4303.0**

    Office 2010 を実行するコンピューターには、Microsoft Online Services サインイン アシスタント バージョン 7.250.4303.0 が必要です。 このバージョンは、クライアントのインストールに含まれています。 

    新しいバージョンのサインイン アシスタントがある場合は、これをアンインストールしてから Azure Information Protection クライアントをインストールしてください。 たとえば、バージョンを確認し、[**コントロールパネル]** プログラムを使用してサインインアシスタントをアンインストールし、[  >    >  **プログラムのアンインストールまたは変更**] を使用します。

    詳細については、「 [AIP For Windows And Office versions in extended support](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。


- **KB 4482887**

    Windows 10 バージョン 1809 の場合のみ、17763.348 より前のオペレーティング システム ビルドでは、Office アプリケーションに正しい Information Protection バーが確実に表示されるように、[2019 年 3 月 1 日—KB4482887 (OS ビルド 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) がインストールされます。 Office 365 1902 以降をお持ちの場合、この更新プログラムは必要ありません。

- **グループ ポリシーを構成して Azure Information Protection アドインが無効にならないようにする**

    Office 2013 およびそれ以降のバージョンの場合、グループ ポリシーを構成して、Office アプリケーション用の **Microsoft Azure Information Protection** アドインが常に有効になるようにします。 この構成を行わないと、Microsoft Azure Information Protection アドインが無効にされる場合があり、ユーザーが Office アプリケーションで自分のドキュメントや電子メールにラベル付けできなくなります。

    - **Outlook の場合:** Office ドキュメントの「 [システム管理者](/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins) によるアドインの制御」に記載されているグループポリシー設定を使用します。

    - **Word、Excel、PowerPoint の場合:** 「サポート記事」に記載されている **管理対象アドインの** グループポリシー設定の一覧を使用して、 [Office 2013 および office 2016 プログラムのグループポリシー設定によってアドインが読み込まれていないことを](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)示します。

        Azure Information Protection に次のプログラム識別子 (ProgID) を指定して、オプションを **[1: アドインを常に有効にする]** に設定します。

        **Word の場合:**`MSIP.WordAddin`

        **Excel の場合:**`MSIP.ExcelAddin`

        **PowerPoint の場合:**`MSIP.PowerPointAddin`

- **悪用防止。** 

    AIP クライアントは、 [Exploit protection](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) が有効になっている .net バージョン2または3のコンピューターではサポートされていません。 上記の .NET 4.x バージョンに加えて、コンピューターに .NET version 2 または3がある場合は、AIP クライアントをインストールする前に、 [Exploit protection を無効](../known-issues.md#known-issues-for-aip-and-exploit-protection) にしてください。  

> [!IMPORTANT]
> Azure Information Protection クライアントのインストールには、ローカル管理者権限が必要です。

## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>ユーザー向けに Azure Information Protection クライアントをインストールするオプション

次のいずれかのオプションを使用して、ユーザーのクライアントをインストールします。

|インストール オプション  |説明  |
|---------|---------|
|**クライアント実行可能ファイル (.exe) を実行します。**  <br><br> [手順](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)      | インストールを対話形式またはサイレントモードで実行するには、クライアントの .exe バージョンを実行することをお勧めします。<br><br> .Exe ファイルを実行すると、最も柔軟性が高くなります。また、前提条件の多くをチェックし、不足している必須コンポーネントをインストールすることもできるため、このファイルを使用することをお勧めします。 |
|**クライアントの Windows インストーラー (.msi) を展開する** <br><br> [手順](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)    | Azure Information Protection クライアントの Windows インストーラーは、中央の展開メカニズムを使用するサイレントインストールでのみサポートされています。<br><br> たとえば、グループポリシー、Configuration Manager、Microsoft Intune と共に展開する場合は、.msi ファイルを使用します。<br><br> この方法は、Intune で管理されている Windows 10 Pc に対して使用する必要があります。また、これらのコンピューターでは、.exe ファイルとしてのモバイルデバイス管理 (MDM) はサポートされていません。<br><br>**注**: .msi のインストールを使用する場合は、前提条件を手動で確認し、必要な依存ソフトウェアをインストールまたはアンインストールする必要があります。 |

クライアントをインストールした後、同じインストール方法を繰り返して更新を実行するか、Windows Update を使用してクライアントを自動的に更新します。 新しいバージョンをインストールする前に、レガシバージョンのクライアントをアンインストールする必要はありません。

詳細については、「[Azure Information Protection クライアントのアップグレードと保守](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)」をご覧ください。

> [!NOTE]
> クライアントをアンインストールするには、 [windows のコントロールパネル](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs)などの [**プログラムの追加と削除**] オプションを使用します。

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>実行可能ファイルのインストーラーを使用して Azure Information Protection クライアントをインストールするには

Microsoft Update カタログを使用していない場合、または Intune などの一元的な展開方法を使用して .msi を展開する場合は、次の手順に従ってクライアントをインストールします。

1. 既定のインストールは、実行可能ファイル (たとえば **AzInfoProtection.exe**) を実行するだけです。 

    その他のインストールオプションを表示するには、まず、 **/help** を使用して実行可能ファイルを実行します。 `AzInfoProtection.exe /help`

    サイレント モードでクライアントをインストールする例: `AzInfoProtection.exe /quiet`

    PowerShell コマンドレットだけをサイレント インストールする例: `AzInfoProtection.exe  PowerShellOnly=true /quiet`

    ヘルプ画面に表示されていない追加のパラメーター:

    - Office 2010 を実行するコンピューターにクライアントをインストールするとき、ユーザーがそのコンピューターのローカル管理者ではない場合またはそのユーザーを表示したくない場合は、**ServiceLocation** パラメーターを指定します。 
    
        詳細については、「 [ServiceLocation インストールパラメーターの詳細](#more-information-about-the-servicelocation-installation-parameter) 」と「 [拡張サポートでの Windows および Office バージョンの AIP](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。

    - **DowngradeDotNetRequirement**: MICROSOFT.NET Framework 4.6.2 のバージョンの要件を省略する場合にこのパラメーターを使用します。 [詳細情報](#more-information-about-the-downgradedotnetrequirement-installation-parameter)

    - **AllowTelemetry=0**: このパラメーターは、インストール オプション **[Microsoft に利用状況の統計を送信して、Azure Information Protection の改善に協力します]** を無効にするときに使用します。

1. 対話形式でインストールする場合は、Microsoft 365 または Azure Active Directory に接続できなくても、デモンストレーション目的でローカルポリシーを使用して Azure Information Protection のクライアント側を表示して操作する場合は、 **デモポリシー** をインストールするオプションを選択します。 クライアントの Azure Information Protection サービスへの接続時に、このデモ ポリシーは、組織の Azure Information Protection ポリシーに置き換えられます。

1. インストールを完了するには:

    - **コンピューターが Office 2010 を実行している場合は**、コンピューターを再起動します。

        クライアントが **Servicelocation** パラメーターを使用してインストールされていない場合、Azure Information Protection バーを使用するいずれかの Office アプリケーションを初めて開くとき (Word など) は、この初回使用時にレジストリを更新するように求めるプロンプトを確認する必要があります。 [サービス検索](client-deployment-notes.md#rms-service-discovery)はレジストリ キーの設定に使用されます。

        詳細については、「 [AIP For Windows And Office versions in extended support](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。


    - **他のバージョンの office** の場合は、すべての office アプリケーションとエクスプローラーのすべてのインスタンスを再起動します。

1. 既定で %temp% フォルダーに作成されるインストール ログ ファイルを確認することで、インストールが成功したか確認できます。 インストール パラメーター **/log** を使用してこの場所を変更できます。

    このファイルの名前は次の形式です: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`

    例: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**

    このログ ファイルで、次の文字列を検索します: **製品: Microsoft Azure Information Protection -- インストールを正しく完了しました。** インストールに失敗した場合、このログ ファイルには、問題の特定と解決に役立つ詳細が含まれます。

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>ServiceLocation インストール パラメーターの詳細について

Office 2010 を使用していて、ローカルの管理アクセス許可を持たないユーザーのクライアントをインストールする場合は、 **Servicelocation** パラメーターと Azure Rights Management サービスの URL を指定します。 このパラメーターと値により、次のレジストリ キーが作成され、設定されます。

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation`

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation`

**Servicelocation** パラメーターに指定する値を特定するには、[次の手順](#to-identify-the-value-to-specify-for-the-servicelocation-parameter)に従います。

詳細については、「 [AIP For Windows And Office versions in extended support](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>ServiceLocation パラメーターに指定する値を特定するには

1. PowerShell セッションから、まず [connect-AipService](/powershell/module/aipservice/connect-aipservice) を実行し、Azure Rights Management サービスに接続するための管理者の資格情報を指定します。 次 [に、AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)を実行します。

    Azure Rights Management サービス用の PowerShell モジュールをまだインストールしていない場合は、「 [AIPService powershell モジュールのインストール](../install-powershell.md)」を参照してください。

2. 出力から、**LicensingIntranetDistributionPointUrl** の値を確認します。

    例: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. この値から、**/_wmcs/licensing** 文字列を削除します。 例: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    残りの文字列は、 **Servicelocation** パラメーターに指定する値です。

[Office 2010](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)および Azure RMS 用にクライアントをサイレントインストールする例を次に示します。 

`AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`

#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>DowngradeDotNetRequirement インストール パラメーターの詳細について

Windows Update を使用して自動アップグレードをサポートし、Office アプリケーションとの信頼性の高い統合のため、Azure Information Protection クライアントは Microsoft .NET Framework バージョン 4.6.2 を使用します。 既定では、実行可能ファイルによる対話型インストールによってこのバージョンが確認され、ない場合はインストールが試行されます。 インストール後はコンピューターの再起動が必要です。

この Microsoft .NET Framework の新しいバージョンのインストールが現実的ではない場合は、**DowngradeDotNetRequirement = True** パラメーターと値を使用してクライアントをインストールすることで、Microsoft .NET Framework バージョン 4.5.1 がインストールされていれば要件を省略できます。

例: `AzInfoProtection.exe DowngradeDotNetRequirement=True`

このパラメーターは、Azure Information Protection クライアントが Microsoft .NET Framework の以前のバージョンと共に使用すると Office アプリケーションがハングする問題が報告されていることを把握したうえで注意して使用することをお勧めします。 ハングすることがある場合は、その他のトラブルシューティングを行う前に推奨されているバージョンにアップグレードしてください。 

Windows Update を使用して Azure Information Protection クライアントを最新の状態に保っている場合は、別のソフトウェアの展開方法でクライアントを新しいバージョンに保つ必要があることにも注意してください。

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>.msi インストーラーを使用して Azure Information Protection クライアントをインストールするには

一元的な展開の場合は、Azure Information Protection クライアントの msi インストール バージョン固有の次の情報をご覧ください。 

ソフトウェアの展開方法に Intune を使用する場合は、次の手順を実行するとともに、「[Microsoft Intune でアプリを追加する](/intune/apps/apps-add)」をご覧ください。

1. **.Msi** ファイルを実行するコンピューターごとに、次のソフトウェアの依存関係が配置されていることを確認する必要があります。 たとえば、 **.msi** バージョンのクライアントを使用してパッケージ化するか、次の依存関係を満たすコンピューターにのみ展開します。
    
    |Office のバージョン|オペレーティング システム|ソフトウェア|アクション|
    |--------------------|--------------|----------------|---------------------|
    |**Office 365 1902 以降を除くすべてのバージョン**|Windows 10 バージョン 1809 のみ、17763.348 より前のオペレーティング システム ビルド|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|インストール|
    |**Office 2013**|サポートされているすべてのバージョン|64 ビット: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 ビット: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />バージョン: 1.0|インストール|
    |**Office 2010**|サポートされているすべてのバージョン|[Microsoft Online Services サインインアシスタント](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> バージョン: 2.1|インストール|
    |**Office 2016**|サポートされているすべてのバージョン|64 ビット: [KB317866](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 ビット: [KB317866](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> バージョン: 1.0|インストール|
    |**Office 2010**|サポートされているすべてのバージョン|[Microsoft Online Services サインインアシスタント](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> バージョン: 2.1|インストール|
    |**Office 2010**|Windows 8.1 および Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB2843630 または KB2919355 がインストールされていない場合はインストールします|
    |**Office 2010**|Windows 8 と Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|インストール|
    | | | | |

    AIP と Office 2010 の詳細については、「 [AIP For Windows」および「office バージョン (拡張サポート](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support))」を参照してください。

1. 既定のインストールでは、`AzInfoProtection.msi /quiet` のように、**/quiet** を付けて .msi を実行します。 ただし、[実行可能ファイルのインストーラーの手順](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)に記載されている追加のインストール パラメーターを指定する必要がある場合があります。

    > [!NOTE]
    > 既定では、[ **使用状況の統計情報を Microsoft インストールに送信して Azure Information Protection を向上させる** ] オプションが有効になっています。 このオプションを無効にするには、次のいずれかを実行してください。
    >
    >- インストール中に、 **Allowtelemetry = 0** を指定します。
    >- インストール後、レジストリキーを次のように更新します: **EnableTelemetry = 0**。
    >

## <a name="how-to-install-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーをインストールする方法

Azure Information Protection クライアントに含まれている PowerShell モジュールには、スキャナーをインストールし、構成するためのコマンドレットがあります。 ただし、スキャナーを使用するには、クライアントのフル バージョンをインストールする必要があります。PowerShell モジュールのみをインストールすることはできません。

このクライアントに付属するスキャナーをインストールするには、前のセクションの同じ手順に従います。 これで、スキャナーを構成してからインストールする準備が整いました。 詳細については、「 [Azure Information Protection クラシックスキャナーとは](../deploy-aip-scanner-classic.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

Azure Information Protection クライアントをインストールしたので、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [クライアントのファイルと使用状況ログ](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)