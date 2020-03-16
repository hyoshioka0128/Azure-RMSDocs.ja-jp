---
title: Azure Information Protection 統合されたラベル付けクライアントをユーザーにインストールする
description: Azure Information Protection 統合された Windows 用のラベル付けクライアントを企業ネットワークに展開するための管理者向けの手順と情報です。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f50db0279d5611e3e62698a6a4ca7f871f00dd04
ms.sourcegitcommit: 2917e822a5d1b21bf465f2cb93cfe46937b1faa7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2020
ms.locfileid: "79403656"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>管理者ガイド: Azure Information Protection 統合されたユーザー用ラベル付けクライアントのインストール

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection 統合されたラベル付けクライアントをエンタープライズネットワークにインストールする前に、コンピューターに必要なオペレーティングシステムのバージョンとアプリケーションがあることを確認してください。 Azure Information Protection: [Azure Information Protection の要件](../requirements.md)を確認してください。 

次に、次のセクションで説明するように、Azure Information Protection 統合されたラベル付けクライアントに必要な追加の前提条件を確認します。 インストール プログラムでは、一部の前提条件が確認されません。

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection の統合ラベル付けクライアントの追加の前提条件

- Microsoft .NET Framework 4.6.2
    
    既定では Azure Information Protection 統合されたラベル付けクライアントの完全インストールには Microsoft .NET Framework 4.6.2 の最小バージョンが必要です。これがない場合は、実行可能ファイルインストーラーのセットアップウィザードによって、このファイルをダウンロードしてインストールしようとします。要件. この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。 推奨はされていませんが、この要件は、セットアップ ウィザードを使用する際に、[カスタム インストール パラメーター](#more-information-about-the-downgradedotnetrequirement-installation-parameter)を使用することで省略できます。
    
    この前提条件は、実行可能インストーラー、Windows Update、または Windows インストーラーを使用してクライアントをサイレント モードでインストールする場合には、自動的にはインストールされていません。 これらのシナリオでは、必要に応じてこの前提条件をインストールしてください。そうしないと、インストールが失敗します。 Microsoft .NET Framework 4.6.2 (オフライン インストーラー) は、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53344)からダウンロードできます。

- Microsoft .NET Framework 4.5.2
    
    Azure Information Protection ビューアーを別にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。これがない場合、実行可能インストーラーではダウンロードまたはインストールされません。

- Windows PowerShell の最小バージョン4.0
    
    クライアントの PowerShell モジュールには、Windows PowerShell 用の4.0 の最小バージョンが必要です。これは、以前のオペレーティングシステムにインストールする必要がある場合があります。 詳細については、「[How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)」(Windows PowerShell 4.0 のインストール方法) を参照してください。 インストーラーでは、この前提条件のチェックやインストールは行われません。 実行中の Windows PowerShell のバージョンを確認するには、PowerShell セッションで「`$PSVersionTable`」と入力します。

- 800 x 600 より大きい画面の解像度
    
    解像度が 800 x 600 以下だと、エクスプローラーでファイルやフォルダーを右クリックしても、 **[分類と保護 - Azure Information Protection]** ダイアログ ボックスを完全に表示できません。


- Microsoft Online Services サインイン アシスタント 7.250.4303.0
    
    Office 2010 を実行するコンピューターには、Microsoft Online Services サインイン アシスタント バージョン 7.250.4303.0 が必要です。 このバージョンは、クライアントのインストールに含まれています。 新しいバージョンのサインインアシスタントがある場合は、Azure Information Protection 統合ラベル付けクライアントをインストールする前にアンインストールしてください。 たとえば、バージョンを確認し、 **[コントロール パネル]**  >  **[プログラムと機能]**  >  **[プログラムのアンインストールまたは変更]** を使用して、サインイン アシスタントをアンインストールします。

- KB 4482887
    
    Windows 10 バージョン 1809 の場合のみ、17763.348 より前のオペレーティング システム ビルドでは、Office アプリケーションに正しい Information Protection バーが確実に表示されるように、[2019 年 3 月 1 日—KB4482887 (OS ビルド 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) がインストールされます。 Office 365 1902 以降をお持ちの場合、この更新プログラムは必要ありません。

- KB 2533623
    
    Windows 7 Service Pack 1 を実行しているコンピューターには、KB 2533623 が必要です。 この更新プログラムの詳細については、「[マイクロソフト セキュリティ アドバイザリ: 安全でないライブラリの読み込みにより、リモートでコードが実行される](https://support.microsoft.com/en-us/kb/2533623)」を参照してください。 この更新プログラムは直接インストールすることもでき、また、その更新プログラムを包括する別の更新プログラムによって置き換えられることもあります。
    
    この必要な更新プログラムがインストールされていない場合、クライアントのインストールにより、インストールが必要だと警告が表示されます。 クライアントのインストール後にこの更新プログラムをインストールできますが、一部の操作はブロックされ、メッセージが再び表示されます。  

- Visual Studio 2015 の Visual C++ 再頒布可能パッケージ (32 ビット バージョン)
    
    Windows 7 Service Pack 1 を実行しているコンピューターでは、次のダウンロード ページから **vc_redist.x86.exe** をインストールしてください: [Visual Studio 2015 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
    
    クライアントインストールでは、この前提条件は確認されませんが、Azure Information Protection 統合されたラベル付けクライアントが PDF ファイルを分類して保護するために必要です。

- グループ ポリシーを構成して Azure Information Protection アドインが無効にならないようにする
    
    Office 2013 およびそれ以降のバージョンの場合、グループ ポリシーを構成して、Office アプリケーション用の **Microsoft Azure Information Protection** アドインが常に有効になるようにします。 この構成を行わないと、Microsoft Azure Information Protection アドインが無効にされる場合があり、ユーザーが Office アプリケーションで自分のドキュメントや電子メールにラベル付けできなくなります。
    
    - Outlook の場合、Office ドキュメントの「[システム管理者によるアドインの制御](https://docs.microsoft.com/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins)」に記載されているグループ ポリシー設定を使用します。
    
    - Word、Excel、および PowerPoint の場合、サポート記事「**No Add-ins loaded due to group policy settings for Office 2013 and Office 2016 programs**」 (Office 2013 および Office 2016 プログラムのグループ ポリシー設定によりアドインが読み込まれない) に記載されているグループ ポリシー設定 [[管理対象アドインの一覧]](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off) を使用します。 
        
        Azure Information Protection に次のプログラム識別子 (ProgID) を指定して、オプションを **[1: アドインを常に有効にする]** に設定します。
        
        Word の場合: `MSIP.WordAddin`
        
        Excel の場合: `MSIP.ExcelAddin`
        
        PowerPoint の場合: `MSIP.PowerPointAddin`

> [!IMPORTANT]
> Azure Information Protection の統合ラベル付けクライアントをインストールするには、ローカルの管理アクセス許可が必要です。


## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Azure Information Protection 統合されたラベル付けクライアントをインストールするためのオプション

ユーザー向けにクライアントをインストールするオプションは次の 2 つです。

**実行可能ファイル (.exe) のバージョンのクライアントを実行する**: 対話形式またはサイレント モードで実行できるお勧めのインストール方法です。 この方法ではインストーラーが前提条件の多くを確認し、満たされていない前提条件を自動的にインストールできるため、柔軟性に優れたお勧めの方法です。 [手順](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**Windows インストーラー (.msi) バージョンのクライアントを展開する**: グループ ポリシー、構成マネージャー、Microsoft Intune などの一元的な展開メカニズムを使用するサイレント インストールでのみサポートされています。 Intune とモバイル デバイス管理 (MDM) で管理されている Windows 10 PC では、インストールで実行可能ファイルがサポートされていないため、この方法が必要です。 ただし、このインストール方法を使用する場合は、依存関係にあるソフトウェアの確認と、インストールまたはアンインストールを手動で行う必要があります。実行可能ファイルのインストーラーであれば、各コンピューターでインストーラーによってこの作業が実行されます。 [手順](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

Azure Information Protection 統合ラベル付けクライアントがインストールされたら、選択したインストール方法を繰り返してこのクライアントを更新するか、Windows Update を使用してクライアントを自動的にアップグレードします。 アップグレードについて詳しくは、「[Azure Information Protection クライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」セクションをご覧ください。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>実行可能ファイルのインストーラーを使用して Azure Information Protection 統合されたラベル付けクライアントをインストールするには

Microsoft Update カタログを使用していない場合、または Intune などの一元的な展開方法を使用して .msi を展開する場合は、次の手順に従ってクライアントをインストールします。

1. [Microsoft ダウンロードセンター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)から Azure Information Protection 統合されたラベル付けクライアント (ファイル名 AzInfoProtection_UL) の実行可能バージョンをダウンロードします。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。 

2. 既定のインストールの場合は、実行可能ファイル ( **AzInfoProtection_UL**など) を実行するだけです。 一方、インストール オプションを表示するには、 **/help** を付けて実行可能ファイルを実行します。`AzInfoProtection_UL.exe /help`

    サイレント モードでクライアントをインストールする例: `AzInfoProtection_UL.exe /quiet`
    
    PowerShell コマンドレットだけをサイレント インストールする例: `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    ヘルプ画面に表示されていない追加のパラメーター:
    
    - Office 2010 を実行するコンピューターにクライアントをインストールするとき、ユーザーがそのコンピューターのローカル管理者ではない場合またはそのユーザーを表示したくない場合は、**ServiceLocation** パラメーターを指定します。 [詳細情報](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: MICROSOFT.NET Framework 4.6.2 のバージョンの要件を省略する場合にこのパラメーターを使用します。 [詳細情報](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry=0**: このパラメーターは、インストール オプション **[Microsoft に利用状況の統計を送信して、Azure Information Protection の改善に協力します]** を無効にするときに使用します。 

3. インストールを完了するには: 

    - お使いのコンピューターが Office 2010 を実行する場合は、コンピューターを再起動します。 
        
        クライアントが ServiceLocation パラメーターを使用してインストールされていない場合、Azure Information Protection 統合クライアント (Word など) を使用するいずれかの Office アプリケーションを初めて開くときに、レジストリを更新するためのプロンプトを確認する必要があります。初回使用時。 [サービス検索](client-deployment-notes.md#rms-service-discovery)はレジストリ キーの設定に使用されます。 
    
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

1. PowerShell セッションから、まず[connect-AipService](https://docs.microsoft.com/powershell/module/aipservice/connect-aipservice)を実行し、Azure Rights Management サービスに接続するための管理者の資格情報を指定します。 次[に、AipServiceConfiguration](https://docs.microsoft.com/powershell/module/aipservice/get-aipserviceconfiguration)を実行します。 
 
    Azure Rights Management サービス用の PowerShell モジュールをまだインストールしていない場合は、「 [AIPService powershell モジュールのインストール](../install-powershell.md)」を参照してください。

2. 出力から、**LicensingIntranetDistributionPointUrl** の値を確認します。

    例: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. この値から、 **/_wmcs/licensing** 文字列を削除します。 例: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    残りの文字列は、ServiceLocation パラメーターに指定する値です。

Office 2010 と Azure RMS のクライアントのサイレント インストールの例: `AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>DowngradeDotNetRequirement インストール パラメーターの詳細について

Windows Update を使用した自動アップグレードをサポートし、Office アプリケーションとの信頼できる統合のために、Azure Information Protection 統合ラベル付けクライアントは Microsoft .NET Framework バージョン4.6.2 を使用します。 既定では、実行可能ファイルによる対話型インストールによってこのバージョンが確認され、ない場合はインストールが試行されます。 インストール後はコンピューターの再起動が必要です。

この Microsoft .NET Framework の新しいバージョンのインストールが現実的ではない場合は、**DowngradeDotNetRequirement = True** パラメーターと値を使用してクライアントをインストールすることで、Microsoft .NET Framework バージョン 4.5.1 がインストールされていれば要件を省略できます。

例: `AzInfoProtection_UL.exe DowngradeDotNetRequirement=True`

このパラメーターは注意して使用することをお勧めします。また、この古いバージョンの Microsoft .NET で Azure Information Protection 統合されたラベル付けクライアントを使用した場合に、Office アプリケーションがハングする問題が報告されていることを知らせてください。フレームワーク. ハングすることがある場合は、その他のトラブルシューティングを行う前に推奨されているバージョンにアップグレードしてください。 

また、Windows Update を使用して Azure Information Protection の統一されたラベル付けクライアントを更新する場合、クライアントを新しいバージョンにアップグレードするには、別のソフトウェア展開メカニズムが必要であることに注意してください。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>.Msi インストーラーを使用して Azure Information Protection 統合されたラベル付けクライアントをインストールするには

集中展開の場合は、Azure Information Protection 統合ラベル付けクライアントの .msi インストールバージョンに固有の次の情報を使用します。 

ソフトウェアの展開方法に Intune を使用する場合は、次の手順を実行するとともに、「[Microsoft Intune でアプリを追加する](/intune/deploy-use/add-apps)」をご覧ください。

1. Azure Information Protection 統合されたラベル付けクライアント (AzInfoProtection_UL) の .msi バージョンを[Microsoft ダウンロードセンター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードします。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。

2. .msi ファイルを実行する各コンピューターで、次のソフトウェアの依存関係が満たされていることを確認する必要があります。 たとえば、.msi バージョンのクライアントとこれらをまとめるか、次の依存関係を満たすコンピューターにのみ展開します。
    
    |Office のバージョン|オペレーティング システム|ソフトウェア|操作|
    |--------------------|--------------|----------------|---------------------|
    |Office 365 1902 以降を除くすべてのバージョン|Windows 10 バージョン 1809 のみ、17763.348 より前のオペレーティング システム ビルド|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Install|
    |Office 2016|サポートされているすべてのバージョン|64 ビット: [KB317866](https://www.microsoft.com/en-us/download/details.aspx?id=55007)<br /><br />32 ビット: [KB317866](https://www.microsoft.com/en-us/download/details.aspx?id=54999)<br /><br /> バージョン: 1.0|Install|
    |Office 2013|サポートされているすべてのバージョン|64 ビット: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 ビット: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />バージョン: 1.0|Install|
    |Office 2010|サポートされているすべてのバージョン|[Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> バージョン: 2.1|Install|
    |Office 2010|Windows 8.1 と Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB2843630 または KB2919355 がインストールされていない場合はインストールします|
    |Office 2010|Windows 8 と Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|Install|
    |Office 2010|Windows 7 および Windows Server 2008 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB3125574 がインストールされていない場合はインストールします|
    |適用できません|Windows 7|[vc_redist.x86.exe](https://www.microsoft.com/en-us/download/details.aspx?id=48145)|Install|
    |適用できません|Windows 7|KB2627273 <br /><br /> ファイル名に含まれるバージョン番号: v4|アンインストール|

3. 既定のインストールでは、 **のように、** /quiet`AzInfoProtection_UL.msi /quiet` を付けて .msi を実行します。 ただし、次の1つの例外を除き、[実行可能ファイルのインストーラーの指示](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)に記載されている追加のインストールパラメーターを指定することが必要になる場合があります。
    
    - **Allowtelemetry = 0**の代わりに、**使用状況の統計情報を Microsoft に送信して Azure Information Protection の向上に役立つ**インストールオプションを無効にするには、 **ENABLETELEMETRY = 0**を指定します。 

## <a name="next-steps"></a>次のステップ:
Azure Information Protection 統合されたラベル付けクライアントをインストールしたので、このクライアントのサポートに必要な追加情報については、次を参照してください。

- [クライアント ファイルおよび使用状況ログの記録](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)

