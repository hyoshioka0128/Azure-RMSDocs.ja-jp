---
title: Azure Information Protection 統合されたラベル付けクライアントをユーザーにインストールする
description: Azure Information Protection 統合された Windows 用のラベル付けクライアントを企業ネットワークに展開するための管理者向けの手順と情報です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3afb97e9094d74eb98b67b375def7a24f6dcc104
ms.sourcegitcommit: e6b594b8d15f81884b0999f5c0009386aef02cc3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2020
ms.locfileid: "88073688"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>管理者ガイド: Azure Information Protection 統合されたユーザー用ラベル付けクライアントのインストール

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> **Windows 7 と Office 2010 向けに拡張された Microsoft サポートをご利用のお客様は、これらのバージョンの Azure Information Protection サポートを受けることもできます。詳細については、サポート担当者にお問い合わせください。*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection 統合されたラベル付けクライアントをエンタープライズネットワークにインストールする前に、コンピューターに必要なオペレーティングシステムのバージョンとアプリケーションがあることを確認してください。 Azure Information Protection: [Azure Information Protection の要件](../requirements.md)を確認してください。 

次に、次のセクションで説明するように、Azure Information Protection 統合されたラベル付けクライアントに必要な追加の前提条件を確認します。 インストール プログラムでは、一部の前提条件が確認されません。

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection の統合ラベル付けクライアントの追加の前提条件

「 [Azure Information Protection の要件](../requirements.md)」に記載されている項目に加えて、AIP 統合ラベルクライアントの次の前提条件が満たされています。

|要件  |説明  |
|---------|---------|
|**Microsoft .NET Framework 4.6.2**     | 既定では Azure Information Protection 統合されたラベル付けクライアントの完全インストールには、Microsoft .NET Framework 4.6.2 の最小バージョンが必要です。 </br></br>このフレームワークがインストールされていない場合は、実行可能ファイルインストーラーのセットアップウィザードによって、この前提条件のダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。       |
|**Microsoft .NET Framework 4.5.2**     | Azure Information Protection ビューアーが個別にインストールされている場合、ビューアーアプリケーションには Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。 </br></br>**重要:** ビューアーにこのフレームワークがない場合は、実行可能ファイルのインストーラーによってダウンロードまたはインストール*されません*。        |
|**Windows PowerShell の最小バージョン4.0**     |   クライアントの PowerShell モジュールには、Windows PowerShell 4.0 の最小バージョンが必要です。これは、古いオペレーティングシステムにインストールする必要がある場合があります。 </br></br>詳細については、「[How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)」(Windows PowerShell 4.0 のインストール方法) を参照してください。 </br></br>**重要:** インストーラーでは、この前提条件を確認したりインストールしたりすることは*ありません*。 実行中の Windows PowerShell のバージョンを確認するには、PowerShell セッションで「`$PSVersionTable`」と入力します。      |
|**800 x 600 より大きい画面の解像度**    |     解像度が 800 x 600 以下だと、エクスプローラーでファイルやフォルダーを右クリックしても、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスを完全に表示できません。    |
|**Microsoft Online Services サインイン アシスタント 7.250.4303.0**     |   Office 2010 を実行しているコンピューターには、クライアントインストールに含まれている Microsoft Online Services サインインアシスタントバージョン7.250.4303.0 が必要です。 </br></br>新しいバージョンのサインインアシスタントがある場合は、Azure Information Protection 統合ラベル付けクライアントをインストールする前にアンインストールしてください。 </br></br>たとえば、バージョンを確認し、[**コントロールパネル]** プログラムを使用してサインインアシスタントをアンインストールし、[  >  **Program and Features**  >  **プログラムのアンインストールまたは変更**] を使用します。      |
|**KB 4482887**     | Windows 10 バージョン 1809 の場合のみ、17763.348 より前のオペレーティング システム ビルドでは、Office アプリケーションに正しい Information Protection バーが確実に表示されるように、[2019 年 3 月 1 日—KB4482887 (OS ビルド 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) がインストールされます。 </br></br>Office 365 1902 以降をお持ちの場合、この更新プログラムは必要ありません。        |
|**管理者のアクセス許可**| Azure Information Protection の統合ラベル付けクライアントをインストールするには、ローカルの管理アクセス許可が必要です。| 
|   |  |
        
### <a name="configure-your-group-policy-to-prevent-disabling-aip"></a>AIP が無効にならないようにグループポリシーを構成する

Office バージョン2013以降では、Office アプリケーション用の**Microsoft Azure Information Protection**アドインが常に有効になるように、グループポリシーを構成することをお勧めします。  このアドインがなければ、ユーザーは Office アプリケーションでドキュメントや電子メールにラベルを付けることができません。   

- **Outlook の場合:**「[システム管理者によるアドインの制御](https://docs.microsoft.com/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins)」に記載されているグループポリシー設定を使用します。
- **Word、Excel、PowerPoint の場合:**[Office 2013 および office 2016 プログラムのグループポリシー設定が原因で、「アドインが読み込まれていません](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)」に記載されている**管理対象アドインの**グループポリシー設定の一覧を使用します。 . 

    AIP に次のプログラム識別子 (ProgID) を指定し、オプションを1に設定します。この**アドインは常に有効になっ**ています。

    |Application  |ProgID  |
    |---------|---------|
    |Word     |     `MSIP.WordAddin`    |
    |Excel     |  `MSIP.ExcelAddin`       |
    |PowerPoint     |   `MSIP.PowerPointAddin`      |
    | | | 

## <a name="applications"></a>アプリケーション

Azure Information Protection の統一されたラベル付けクライアントは、次のいずれかの Office エディションの Office アプリケーション Word、Excel、PowerPoint、Outlook を使用して、ドキュメントや電子メールにラベルを付け、保護することができます。

- ユーザーに Azure Rights Management (別名: Azure Information Protection for Office 365) のライセンスが割り当てられている場合は、Office 365 Business または Microsoft 365 Business の最小バージョン 1805、ビルド 9330.2078 の Office アプリ
- Office 365 ProPlus
- Office Professional Plus 2019
- Office Professional Plus 2016
- Office Professional Plus 2013 Service Pack 1
- Office Professional Plus 2010 Service Pack 2

Office の他のエディション (**標準**など) では、Rights Management サービスを使用してドキュメントや電子メールを保護することはできません。 これらのエディションでは、**ラベル付け**のためだけに Azure Information Protection がサポートされています。 そのため、保護を適用するラベルは、Azure Information Protection の秘密度ボタンまたはバーにユーザーに表示されません。

保護サービスをサポートする Office のエディションについては、「[Azure Rights Management データ保護をサポートするアプリケーション](https://docs.microsoft.com/azure/information-protection/requirements-applications)」を参照してください。

### <a name="office-features-and-capabilities-not-supported"></a>サポートされていない Office の機能

Azure Information Protection 統合ラベル付けクライアントは、同じコンピューター上で複数のバージョンの Office をサポートしたり、Office のユーザーアカウントを切り替えたりすることはできません。

Office メールのマージ機能は、Azure Information Protection 機能ではサポートされていません。

## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Azure Information Protection 統合されたラベル付けクライアントをインストールするためのオプション

ユーザー向けにクライアントをインストールするオプションは次の 2 つです。

**実行可能ファイル (.exe) のバージョンのクライアントを実行する**: 対話形式またはサイレント モードで実行できるお勧めのインストール方法です。 この方法ではインストーラーが前提条件の多くを確認し、満たされていない前提条件を自動的にインストールできるため、柔軟性に優れたお勧めの方法です。 [手順](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**Windows インストーラー (.msi) バージョンのクライアントを展開する**: グループ ポリシー、構成マネージャー、Microsoft Intune などの一元的な展開メカニズムを使用するサイレント インストールでのみサポートされています。 Intune とモバイル デバイス管理 (MDM) で管理されている Windows 10 PC では、インストールで実行可能ファイルがサポートされていないため、この方法が必要です。 ただし、このインストール方法を使用する場合は、依存関係にあるソフトウェアの確認と、インストールまたはアンインストールを手動で行う必要があります。実行可能ファイルのインストーラーであれば、各コンピューターでインストーラーによってこの作業が実行されます。 [手順](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

Azure Information Protection 統合ラベル付けクライアントがインストールされたら、選択したインストール方法を繰り返してこのクライアントを更新するか、Windows Update を使用してクライアントを自動的にアップグレードします。 アップグレードについて詳しくは、「[Azure Information Protection クライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」セクションをご覧ください。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>実行可能ファイルのインストーラーを使用して Azure Information Protection 統合されたラベル付けクライアントをインストールするには

Microsoft Update カタログを使用していない場合、または Intune などの一元的な展開方法を使用して .msi を展開する場合は、次の手順に従ってクライアントをインストールします。

1. [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)から Azure Information Protection 統合されたラベル付けクライアント (ファイル名 AzInfoProtection_UL) の実行可能バージョンをダウンロードします。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。 

2. 既定のインストールの場合は、実行可能ファイル ( **AzInfoProtection_UL.exe**など) を実行するだけです。 ただし、インストールオプションを表示するには、まず、次のように **/help**を使用して実行可能ファイルを実行します。`AzInfoProtection_UL.exe /help`

    サイレント モードでクライアントをインストールする例: `AzInfoProtection_UL.exe /quiet`
    
    PowerShell コマンドレットだけをサイレント インストールする例: `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    ヘルプ画面に表示されていない追加のパラメーター:
    
    - Office 2010 を実行するコンピューターにクライアントをインストールするとき、ユーザーがそのコンピューターのローカル管理者ではない場合またはそのユーザーを表示したくない場合は、**ServiceLocation** パラメーターを指定します。 [詳細情報](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: MICROSOFT.NET Framework 4.6.2 のバージョンの要件を省略する場合にこのパラメーターを使用します。 [詳細情報](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry=0**: このパラメーターは、インストール オプション **[Microsoft に利用状況の統計を送信して、Azure Information Protection の改善に協力します]** を無効にするときに使用します。 

3. インストールを完了するには: 

    - お使いのコンピューターが Office 2010 を実行する場合は、コンピューターを再起動します。 
        
        クライアントが ServiceLocation パラメーターを使用してインストールされなかった場合、Azure Information Protection 統合クライアント (Word など) を使用するいずれかの Office アプリケーションを初めて開くときに、この初回使用時にレジストリを更新するように求めるプロンプトが表示されます。 [サービス検索](client-deployment-notes.md#rms-service-discovery)はレジストリ キーの設定に使用されます。 
    
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

3. この値から、**/_wmcs/licensing** 文字列を削除します。 例: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    残りの文字列は、ServiceLocation パラメーターに指定する値です。

Office 2010 と Azure RMS のクライアントのサイレント インストールの例: `AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>DowngradeDotNetRequirement インストール パラメーターの詳細について

Windows Update を使用した自動アップグレードをサポートし、Office アプリケーションとの信頼できる統合のために、Azure Information Protection 統合ラベル付けクライアントは Microsoft .NET Framework バージョン4.6.2 を使用します。 既定では、実行可能ファイルによる対話型インストールによってこのバージョンが確認され、ない場合はインストールが試行されます。 インストール後はコンピューターの再起動が必要です。

この Microsoft .NET Framework の新しいバージョンのインストールが現実的ではない場合は、**DowngradeDotNetRequirement = True** パラメーターと値を使用してクライアントをインストールすることで、Microsoft .NET Framework バージョン 4.5.1 がインストールされていれば要件を省略できます。

例: `AzInfoProtection_UL.exe DowngradeDotNetRequirement=True`

このパラメーターは注意して使用することをお勧めします。また、この古いバージョンの Microsoft .NET Framework で Azure Information Protection 統合されたラベル付けクライアントを使用した場合に、Office アプリケーションがハングする問題が報告されていることを知らせてください。 ハングすることがある場合は、その他のトラブルシューティングを行う前に推奨されているバージョンにアップグレードしてください。 

また、Windows Update を使用して Azure Information Protection の統一されたラベル付けクライアントを更新する場合、クライアントを新しいバージョンにアップグレードするには、別のソフトウェア展開メカニズムが必要であることに注意してください。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>.Msi インストーラーを使用して Azure Information Protection 統合されたラベル付けクライアントをインストールするには

集中展開の場合は、Azure Information Protection 統合ラベル付けクライアントの .msi インストールバージョンに固有の次の情報を使用します。 

ソフトウェアの展開方法に Intune を使用する場合は、次の手順を実行するとともに、「[Microsoft Intune でアプリを追加する](/intune/deploy-use/add-apps)」をご覧ください。

1. Azure Information Protection 統合されたラベル付けクライアント (AzInfoProtection_UL) の .msi バージョンを[Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)からダウンロードします。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。

1. .msi ファイルを実行する各コンピューターで、次のソフトウェアの依存関係が満たされていることを確認する必要があります。 たとえば、.msi バージョンのクライアントとこれらをまとめるか、次の依存関係を満たすコンピューターにのみ展開します。
    
    |Office のバージョン|オペレーティング システム|ソフトウェア|アクション|
    |--------------------|--------------|----------------|---------------------|
    |Office 365 1902 以降を除くすべてのバージョン|Windows 10 バージョン 1809 のみ、17763.348 より前のオペレーティング システム ビルド|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|インストール|
    |Office 2016|サポートされているすべてのバージョン|64 ビット: [KB317866](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 ビット: [KB317866](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> バージョン: 1.0|インストール|
    |Office 2013|サポートされているすべてのバージョン|64 ビット: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 ビット: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />バージョン: 1.0|インストール|
    |Office 2010|サポートされているすべてのバージョン|[Microsoft Online Services サインインアシスタント](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> バージョン: 2.1|インストール|
    |Office 2010|Windows 8.1 および Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB2843630 または KB2919355 がインストールされていない場合はインストールします|
    |Office 2010|Windows 8 と Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|インストール|
    
   

1. 既定のインストールでは、`AzInfoProtection_UL.msi /quiet` のように、**/quiet** を付けて .msi を実行します。

    場合によっては、追加のインストールパラメーターを指定する必要があります。 詳細については、「[実行可能ファイルインストーラーの手順](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)」を参照してください。

    > [!NOTE]
    > 既定では、[**使用状況の統計情報を Microsoft インストールに送信して Azure Information Protection を向上させる**] オプションが有効になっています。 このオプションを無効にするには、次のいずれかを実行してください。
    >
    >- インストール中に、 **Allowtelemetry = 0**を指定します。
    >- インストール後、レジストリキーを次のように更新します: **EnableTelemetry = 0**。
    >

## <a name="next-steps"></a>次のステップ
Azure Information Protection 統合されたラベル付けクライアントをインストールしたので、このクライアントのサポートに必要な追加情報については、次を参照してください。

- [クライアントのファイルと使用状況ログ](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)

