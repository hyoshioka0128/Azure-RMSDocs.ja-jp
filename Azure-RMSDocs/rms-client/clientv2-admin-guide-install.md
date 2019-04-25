---
title: ユーザーの Azure Information Protection の統合されたラベル付けクライアントをインストールします。
description: 手順と、Azure Information Protection を展開する管理者向けの情報は、Windows のエンタープライズ ネットワーク上のラベル付けのクライアントを統合します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: c54754c5ec016aaaa54874b2be5bd0ac2d112e90
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183696"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>管理者ガイド: ユーザーの Azure Information Protection の統合されたラベル付けクライアントをインストールします。

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

社内のネットワークに Azure Information Protection の統合されたラベル付けクライアントをインストールする前に、コンピューターに必要なオペレーティング システムのバージョンと Azure Information Protection 用のアプリケーションがあることを確認します。「[Azure Information Protection の要件](../requirements.md)」で確認してください。 

次のセクションに記載されている Azure Information Protection の統合されたラベル付けクライアントに必要な追加の前提条件を確認します。 インストール プログラムでは、一部の前提条件が確認されません。

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection の統合されたラベル付けクライアントの追加の前提条件

- Microsoft .NET Framework 4.6.2
    
    既定では、Azure Information Protection のクライアントを統一されたにラベル付けのフル インストールが Microsoft .NET Framework 4.6.2 の最小バージョンを必要とし、実行可能インストーラーから、セットアップ ウィザードをダウンロードしてこれをインストールしようとこれがない場合前提条件です。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。 推奨はされていませんが、この要件は、セットアップ ウィザードを使用する際に、[カスタム インストール パラメーター](#more-information-about-the-downgradedotnetrequirement-installation-parameter)を使用することで省略できます。
    
    この前提条件は、実行可能インストーラー、Windows Update、または Windows インストーラーを使用してクライアントをサイレント モードでインストールする場合には、自動的にはインストールされていません。 これらのシナリオでは、必要に応じてこの前提条件をインストールしてください。そうしないと、インストールが失敗します。 Microsoft .NET Framework 4.6.2 (オフライン インストーラー) は、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53344)からダウンロードできます。

- Microsoft .NET Framework 4.5.2
    
    Azure Information Protection ビューアーを別にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。これがない場合、実行可能インストーラーではダウンロードまたはインストールされません。

- Windows PowerShell バージョン 4.0
    
    クライアント用の PowerShell モジュールには、Windows PowerShell バージョン 4.0 が必要で、以前のオペレーティング システムにインストールする必要がある場合があります。 詳細については、「[How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)」(Windows PowerShell 4.0 のインストール方法) を参照してください。 インストーラーでは、この前提条件のチェックやインストールは行われません。 実行中の Windows PowerShell のバージョンを確認するには、PowerShell セッションで「`$PSVersionTable`」と入力します。

- 800 x 600 より大きい画面の解像度
    
    解像度が 800 x 600 以下だと、エクスプローラーでファイルやフォルダーを右クリックしても、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスを完全に表示できません。


- Microsoft Online Services サインイン アシスタント 7.250.4303.0
    
    Office 2010 を実行するコンピューターには、Microsoft Online Services サインイン アシスタント バージョン 7.250.4303.0 が必要です。 このバージョンは、クライアントのインストールに含まれています。 以降のバージョンのサインイン アシスタントがあれば、Azure Information Protection の統合されたラベル付けクライアントをインストールする前にアンインストールします。 たとえば、バージョンを確認し、**[コントロール パネル]** > **[プログラムと機能]** > **[プログラムのアンインストールまたは変更]** を使用して、サインイン アシスタントをアンインストールします。

- KB 4482887
    
    Windows 10 バージョン 1809 の場合のみ、17763.348 より前のオペレーティング システム ビルドでは、Office アプリケーションに正しい Information Protection バーが確実に表示されるように、[2019 年 3 月 1 日—KB4482887 (OS ビルド 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) がインストールされます。 Office 365 1902 以降をお持ちの場合、この更新プログラムは必要ありません。

- KB 2533623
    
    Windows 7 Service Pack 1 を実行しているコンピューターには、KB 2533623 が必要です。 この更新プログラムの詳細については、「[マイクロソフト セキュリティ アドバイザリ: 安全でないライブラリ読み込みにより、リモートでコードが実行される](https://support.microsoft.com/en-us/kb/2533623)」を参照してください。 この更新プログラムは直接インストールすることもでき、また、その更新プログラムを包括する別の更新プログラムによって置き換えられることもあります。
    
    この必要な更新プログラムがインストールされていない場合、クライアントのインストールにより、インストールが必要だと警告が表示されます。 クライアントのインストール後にこの更新プログラムをインストールできますが、一部の操作はブロックされ、メッセージが再び表示されます。  

- Visual Studio 2015 の Visual C++ 再頒布可能パッケージ (32 ビット バージョン)
    
    Windows 7 Service Pack 1 を実行しているコンピューターでは、次のダウンロード ページから **vc_redist.x86.exe** をインストールしてください: [Visual Studio 2015 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
    
    この前提条件、クライアントのインストールはチェックされませんが、PDF ファイル分類および保護に Azure Information Protection のクライアントを統一されたにラベル付けする必要があります。

- グループ ポリシーを構成して Azure Information Protection アドインが無効にならないようにする
    
    Office 2013 およびそれ以降のバージョンの場合、グループ ポリシーを構成して、Office アプリケーション用の **Microsoft Azure Information Protection** アドインが常に有効になるようにします。 この構成を行わないと、Microsoft Azure Information Protection アドインが無効にされる場合があり、ユーザーが Office アプリケーションで自分のドキュメントや電子メールにラベル付けできなくなります。
    
    - Outlook の場合。Office ドキュメントの「[システム管理者によるアドインの制御](https://docs.microsoft.com/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins)」に記載されているグループ ポリシー設定を使用します。
    
    - Word、Excel、PowerPoint の場合: サポート記事「[No Add-ins loaded due to group policy settings for Office 2013 and Office 2016 programs](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)」 (Office 2013 および Office 2016 プログラムのグループ ポリシー設定によりアドインが読み込まれない) に記載されているグループ ポリシー設定 **[管理対象アドインの一覧]** を使用します。 
        
        Azure Information Protection に次のプログラム識別子 (ProgID) を指定して、オプションを **[1: アドインを常に有効にする]** に設定します。
        
        Word の場合: `MSIP.WordAddin`
        
        Excel の場合: `MSIP.ExcelAddin`
        
        PowerPoint の場合: `MSIP.PowerPointAddin`

> [!IMPORTANT]
> Azure Information Protection の統合されたラベル付けクライアントのインストールには、ローカルの管理者権限が必要です。


## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>ユーザーの Azure Information Protection の統合されたラベル付けクライアントをインストールするオプション

ユーザー向けにクライアントをインストールするオプションは次の 2 つです。

**実行可能ファイル (.exe) のバージョンのクライアントを実行する**: 対話形式またはサイレント モードで実行できるお勧めのインストール方法です。 この方法ではインストーラーが前提条件の多くを確認し、満たされていない前提条件を自動的にインストールできるため、柔軟性に優れたお勧めの方法です。 [手順](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**Windows インストーラー (.msi) バージョンのクライアントを展開する**: グループ ポリシー、構成マネージャー、Microsoft Intune などの一元的な展開メカニズムを使用するサイレント インストールでのみサポートされています。 Intune とモバイル デバイス管理 (MDM) で管理されている Windows 10 PC では、インストールで実行可能ファイルがサポートされていないため、この方法が必要です。 ただし、このインストール方法を使用する場合は、依存関係にあるソフトウェアの確認と、インストールまたはアンインストールを手動で行う必要があります。実行可能ファイルのインストーラーであれば、各コンピューターでインストーラーによってこの作業が実行されます。 [手順](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

Azure Information Protection の統合されたラベル付けクライアントをインストールした後、選択したインストール方法を繰り返すことによって、このクライアントを更新または Windows の更新を使用して、クライアントが自動的にアップグレードできます。 アップグレードについて詳しくは、「[Azure Information Protection クライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」セクションをご覧ください。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>Azure Information Protection をインストールするには、実行可能インストーラーを使用してラベル付けのクライアントを統合

Microsoft Update カタログを使用していない場合、または Intune などの一元的な展開方法を使用して .msi を展開する場合は、次の手順に従ってクライアントをインストールします。

1. Azure Information Protection の統合されたラベル付けクライアント (AzInfoProtection_UL のファイル名) の実行可能ファイルのバージョンをダウンロード、 [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)します。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。 

2. 既定のインストールで実行するだけです、実行可能ファイルは、たとえば、 **AzInfoProtection_UL.exe**します。 一方、インストール オプションを表示するには、**/help** を付けて実行可能ファイルを実行します。`AzInfoProtection_UL.exe /help`

    サイレント モードでクライアントをインストールする例: `AzInfoProtection_UL.exe /quiet`
    
    PowerShell コマンドレットだけをサイレント インストールする例: `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    ヘルプ画面に表示されていない追加のパラメーター:
    
    - **ServiceLocation**: このパラメーターは、Office 2010 を実行しているコンピューターにクライアントをインストールするとき、ユーザーがそのコンピューターのローカル管理者ではない場合またはそのユーザーにプロンプトを表示したくない場合に使用します。 [詳細情報](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: このパラメーターは、Microsoft Framework .NET 4.6.2 のバージョンの要件を省略する場合に使用します。 [詳細情報](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry=0**: このパラメーターは、インストール オプション **[Microsoft に利用状況の統計を送信して、Azure Information Protection の改善に協力します]** を無効にするときに使用します。 

3. インストールを完了するには: 

    - お使いのコンピューターが Office 2010 を実行する場合は、コンピューターを再起動します。 
        
        Azure Information Protection の統合されたクライアント (たとえば、Word など) を使用する Office アプリケーションのいずれかを初めて開くときに、クライアントでは、ServiceLocation パラメーターにインストールされていない場合、は、このレジストリを更新するプロンプトを確認する必要があります。初めて使用します。 [サービス検索](client-deployment-notes.md#rms-service-discovery)はレジストリ キーの設定に使用されます。 
    
    - その他のバージョンの Office では、Office アプリケーションとエクスプローラーのインスタンスをすべて再起動します。 
        
5. 既定で %temp% フォルダーに作成されるインストール ログ ファイルを確認することで、インストールが成功したか確認できます。 インストール パラメーター **/log** を使用してこの場所を変更できます。 
 
    このファイルの名前は次の形式です: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    以下に例を示します。**Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    このログ ファイルで、次の文字列を検索します: **Product: Microsoft Azure Information Protection -- Installation completed successfully.** インストールに失敗した場合、このログ ファイルには、問題の特定と解決に役立つ詳細が含まれます。

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>ServiceLocation インストール パラメーターの詳細について

Office 2010 を使っていてローカル管理者権限を持たないユーザーのためにクライアントをインストールするときは、ServiceLocation パラメーターと Azure Rights Management サービスの URL を指定します。 このパラメーターと値により、次のレジストリ キーが作成され、設定されます。

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

次の手順で、ServiceLocation パラメーターに指定する値を特定します。 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>ServiceLocation パラメーターに指定する値を特定するには

1. PowerShell セッションから、最初に [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) を実行し、管理者の資格情報を指定して Azure Rights Management サービスに接続します。 [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration) を実行します。 
 
    Azure Rights Management サービス用の PowerShell モジュールをまだインストールしていない場合は、「[AADRM PowerShell モジュールのインストール](../install-powershell.md)」を参照してください。

2. 出力から、 **LicensingIntranetDistributionPointUrl** の値を確認します。

    以下に例を示します。**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. この値から、**/_wmcs/licensing** 文字列を削除します。 例: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    残りの文字列は、ServiceLocation パラメーターに指定する値です。

Office 2010 と Azure RMS のクライアントのサイレント インストールの例: `AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>DowngradeDotNetRequirement インストール パラメーターの詳細について

Windows 更新プログラムを使用して Office アプリケーションの信頼性の高い統合を自動アップグレードをサポートするには、は、Azure Information Protection の統合されたラベル付けクライアントは、Microsoft .NET Framework バージョン 4.6.2 を使用します。 既定では、実行可能ファイルによる対話型インストールによってこのバージョンが確認され、ない場合はインストールが試行されます。 インストール後はコンピューターの再起動が必要です。

この Microsoft .NET Framework の新しいバージョンのインストールが現実的ではない場合は、**DowngradeDotNetRequirement = True** パラメーターと値を使用してクライアントをインストールすることで、Microsoft .NET Framework バージョン 4.5.1 がインストールされていれば要件を省略できます。

たとえば次のようになります。`AzInfoProtection_UL.exe DowngradeDotNetRequirement=True`

Office アプリケーションが Azure Information Protection の統合されたラベル付けクライアントは Microsoft .NET の以前のバージョンと共に使用するとハングに関する報告された問題があることのサポート技術情報で、注意して、このパラメーターを使用することをお勧めします。フレームワーク。 ハングすることがある場合は、その他のトラブルシューティングを行う前に推奨されているバージョンにアップグレードしてください。 

また、更新、Azure Information Protection の統合のラベル付けクライアントを保持する Windows 更新プログラムを使用する場合は、以降のバージョンにクライアントをアップグレードする他のソフトウェア展開メカニズムにする必要なにも注意してください。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>Azure Information Protection をインストールするには、.msi インストーラーを使用してラベル付けのクライアントを統合

一元的な展開は、Azure Information Protection の統合されたラベル付けクライアントの msi インストール バージョンに固有の次の情報を使用します。 

ソフトウェアの展開方法に Intune を使用する場合は、次の手順を実行するとともに、「[Microsoft Intune でアプリを追加する](/intune/deploy-use/add-apps)」をご覧ください。

1. Azure Information Protection の統合されたラベル付けクライアント (AzInfoProtection_UL) の .msi バージョンをダウンロード、 [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)します。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。 

2. .msi ファイルを実行する各コンピューターで、次のソフトウェアの依存関係が満たされていることを確認する必要があります。 たとえば、.msi バージョンのクライアントとこれらをまとめるか、次の依存関係を満たすコンピューターにのみ展開します。
    
    |Office のバージョン|オペレーティング システム|ソフトウェア|操作|
    |--------------------|--------------|----------------|---------------------|
    |Office 365 1902 以降を除くすべてのバージョン|Windows 10 バージョン 1809 のみ、17763.348 より前のオペレーティング システム ビルド|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|インストール|
    |Office 2016|サポートされているすべてのバージョン|64 ビット。[KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=55007)<br /><br />32 ビット。[KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=54999)<br /><br /> バージョン:1.0|インストール|
    |Office 2013|サポートされているすべてのバージョン|64 ビット。[KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 ビット。[KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />バージョン:1.0|インストール|
    |Office 2010|サポートされているすべてのバージョン|[Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> バージョン:2.1|インストール|
    |Office 2010|Windows 8.1 と Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB2843630 または KB2919355 がインストールされていない場合はインストールします|
    |Office 2010|Windows 8 と Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|インストール|
    |Office 2010|Windows 7 および Windows Server 2008 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB3125574 がインストールされていない場合はインストールします|
    |適用なし|Windows 7|[vc_redist.x86.exe](https://www.microsoft.com/en-us/download/details.aspx?id=48145)|インストール|
    |適用なし|Windows 7|KB2627273 <br /><br /> ファイル名に含まれるバージョン番号: v4|アンインストール|

3. 既定のインストールでは、`AzInfoProtection_UL.msi /quiet` のように、**/quiet** を付けて .msi を実行します。 ただし、[実行可能ファイルのインストーラーの手順](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)に記載されている追加のインストール パラメーターを指定する必要がある場合があります。  


## <a name="next-steps"></a>次の手順
これで、Azure Information Protection の統一されたラベル付けクライアントをインストールした場合は、このクライアントをサポートする必要があります追加については、次を参照してください。

- [クライアント ファイルおよび使用状況ログの記録](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)

