---
title: Azure Information Protection 統合されたラベル付けクライアントをユーザーにインストールする
description: Azure Information Protection 統合された Windows 用のラベル付けクライアントを企業ネットワークに展開するための管理者向けの手順と情報です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/21/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f818a94e954b245d329a2cdb2dc1ce419e83c4ce
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560103"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>管理者ガイド: Azure Information Protection 統合されたユーザー用ラベル付けクライアントのインストール

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP and Legacy Windows And office versions](../known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。*
>
>***関連**: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 従来のクライアントについては、「 [従来のクライアント管理者ガイド](client-admin-guide-install.md)」を参照してください。

Azure Information Protection 統合されたラベル付けクライアントをエンタープライズネットワークにインストールする前に、コンピューターに必要なオペレーティングシステムのバージョンとアプリケーションがインストールされていることを確認してください。 Azure Information Protection: [Azure Information Protection の要件](../requirements.md) と、 [エンタープライズネットワークに統一されたラベル付けクライアントをインストールするための追加の要件](reqs-ul-client.md)があります。

## <a name="supported-applications-for-the-unified-labeling-client"></a>統一されたラベル付けクライアントでサポートされるアプリケーション

Azure Information Protection の統一されたラベル付けクライアントは、次のいずれかの Office エディションの Office アプリケーション Word、Excel、PowerPoint、Outlook を使用して、ドキュメントや電子メールにラベルを付け、保護することができます。

- **Office アプリ**。[更新チャネルによる Microsoft 365 アプリにサポートされている表](/officeupdates/update-history-microsoft365-apps-by-date)に記載されているバージョンについては、ユーザーに Azure Rights Management (Azure Information Protection for Office 365 ともいう) のライセンスが割り当てられている場合は、Microsoft 365 Apps for Business または Microsoft 365 Business Premium の Office アプリの最小バージョン 1805、ビルド 9330.2078
- **Microsoft 365 Apps for Enterprise**
- **Office Professional Plus 2019**
- **Office Professional Plus 2016**
- **Office Professional Plus 2013 Service Pack 1**
- **Office Professional Plus 2010 Service Pack 2**

Office の他のエディション ( **standard** など) では、Rights Management サービスを使用してドキュメントや電子メールを保護することはできません。 これらのエディションでは、 **ラベル付け** のためだけに Azure Information Protection がサポートされています。 

そのため、保護を適用するラベルは、Azure Information Protection の秘密度ボタンまたはバーにユーザーに表示されません。

保護サービスをサポートする Office のエディションについては、「[Azure Rights Management データ保護をサポートするアプリケーション](../requirements-applications.md)」を参照してください。

> [!IMPORTANT]
> Office 2010 の拡張サポートは、2020年10月13日に終了しました。 詳細については、「 [AIP and Legacy Windows And Office versions](../known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。

## <a name="unified-labeling-client-installation-options"></a>クライアントインストールオプションの統合ラベル

ユーザー向けにクライアントをインストールするオプションは次の 2 つです。

|オプション  |説明  | I
|---------|---------|
|**クライアントの実行可能 (.exe) バージョンを実行する**     |   対話形式またはサイレント モードで実行できるお勧めのインストール方法です。 <br><br>この方法ではインストーラーが前提条件の多くを確認し、満たされていない前提条件を自動的にインストールできるため、柔軟性に優れたお勧めの方法です。 <br><br>詳細については、「 [実行可能ファイルのインストーラーを使用して AIP 統合ラベルクライアントをインストール](#install-the-aip-unified-labeling-client-using-the-executable-installer)する」を参照してください。|
|**Windows インストーラー (.msi) バージョンのクライアントを展開する**     |     グループ ポリシー、構成マネージャー、Microsoft Intune などの一元的な展開メカニズムを使用するサイレント インストールでのみサポートされています。 <br><br>Intune とモバイル デバイス管理 (MDM) で管理されている Windows 10 PC では、インストールで実行可能ファイルがサポートされていないため、この方法が必要です。 <br><br> ただし、このインストール方法を使用する場合は、依存関係にあるソフトウェアの確認と、インストールまたはアンインストールを手動で行う必要があります。実行可能ファイルのインストーラーであれば、各コンピューターでインストーラーによってこの作業が実行されます。 <br><br>詳細については、「 [.msi インストーラーを使用して、統合されたラベル付けクライアントをインストール](#install-the-unified-labeling-client-using-the-msi-installer)する」を参照してください。 |
|     |         |


Azure Information Protection 統合ラベル付けクライアントがインストールされたら、選択したインストール方法を繰り返してこのクライアントを更新するか、Windows Update を使用してクライアントを自動的にアップグレードします。 

アップグレードについて詳しくは、「[Azure Information Protection クライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」セクションをご覧ください。

## <a name="install-the-aip-unified-labeling-client-using-the-executable-installer"></a>実行可能ファイルのインストーラーを使用して、AIP 統合ラベルクライアントをインストールします。

Microsoft Update カタログを使用して *いない* 場合、または Intune などの一元的な展開方法を使用して [ **.msi** を展開](#install-the-unified-labeling-client-using-the-msi-installer)する場合は、次の手順に従ってクライアントをインストールします。

**.Exe ファイルを使用して、統一されたラベル付けクライアントをインストールするに** は、次のようにします。

1. [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)から Azure Information Protection 統合されたラベル付けクライアント (ファイル名 **AzInfoProtection_UL**) の実行可能バージョンをダウンロードします。 
    
    > [!IMPORTANT]
    > プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。 
    >
 
1. 既定のインストールの場合は、実行可能ファイル ( **AzInfoProtection_UL.exe** など) を実行するだけです。 

    すべてのインストールオプションを表示するには、まず、 **/help** を使用して実行可能ファイルを実行します。 `AzInfoProtection_UL.exe /help`

    次に例を示します。 
    - クライアントをサイレントインストールするには、次のようにします。 `AzInfoProtection_UL.exe /quiet`
    
    - PowerShell コマンドレットだけをサイレントインストールするには、次のようにします。 `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    ヘルプ画面に表示されていない追加のパラメーター:
        
    |パラメーター  |説明  |
    |---------|---------|
    |**AllowTelemetry = 0**     |    このパラメーターは、インストール オプション **[Microsoft に利用状況の統計を送信して、Azure Information Protection の改善に協力します]** を無効にするときに使用します。     |
    |**ServiceLocation**     |  このパラメーターは、Office 2010 を実行しているコンピューターにクライアントをインストールするとき、ユーザーがそのコンピューターのローカル管理者ではない場合またはそのユーザーにプロンプトを表示したくない場合に使用します。 <br><br>**重要**: Office 2010 の拡張サポートは、2020年10月13日に終了しました。 詳細については、「 [AIP and Legacy Windows And Office versions](../known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。 |
    | | |

1. インストールを完了するには、すべての Office アプリケーションとエクスプローラーのすべてのインスタンスを再起動します。 

    > [!NOTE]
    > コンピューターが [Office 2010](../known-issues.md#aip-and-legacy-windows-and-office-versions)を実行している場合は、コンピューターを再起動します。 
    >
    > クライアントが **Servicelocation** パラメーターを使用してインストールされなかった場合、Azure Information Protection 統合クライアント (Word など) を使用するいずれかの Office アプリケーションを初めて開くときに、この初回使用時にレジストリを更新するように求めるプロンプトが表示されます。 
    >
    > [サービス検索](client-deployment-notes.md#rms-service-discovery)はレジストリ キーの設定に使用されます。 
    > 
        
1. インストールログファイルを確認して、インストールが正常に完了したことを確認します。既定では、 **% temp%** フォルダーに作成されます。 

    インストールログファイルの名前付け形式は次のとおりです。 `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    例: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    このログファイルで、次の文字列を検索します。 **Product: Microsoft Azure Information Protection--インストールが正常に完了** しました。 インストールに失敗した場合、このログ ファイルには、問題の特定と解決に役立つ詳細が含まれます。

    > [!TIP]
    > インストールログファイルの場所は、 **/log** インストールパラメーターを使用して変更できます。 
    >  
### <a name="more-information-about-the-servicelocation-installation-parameter"></a>ServiceLocation インストール パラメーターの詳細について

[Office 2010](../known-issues.md#aip-and-legacy-windows-and-office-versions)を使用していて、ローカルの管理アクセス許可を持たないユーザーのクライアントをインストールする場合は、 **Servicelocation** パラメーターと AZURE Rights Management サービスの URL を指定します。 
    
> [!IMPORTANT]
> Office 2010 の拡張サポートは、2020年10月13日に終了しました。 詳細については、「 [AIP and Legacy Windows And Office versions](../known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。
>

このパラメーターと値により、次のレジストリ キーが作成され、設定されます。

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation`

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation`


**ServiceLocation パラメーターに指定する値を特定するには、次のように** します。

1. PowerShell セッションから、まず [connect-AipService](/powershell/module/aipservice/connect-aipservice) を実行し、Azure Rights Management サービスに接続するための管理者の資格情報を指定します。 次 [に、AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)を実行します。 
 
    Azure Rights Management サービス用の PowerShell モジュールをまだインストールしていない場合は、「 [AIPService powershell モジュールのインストール](../install-powershell.md)」を参照してください。

2. 出力から、**LicensingIntranetDistributionPointUrl** の値を確認します。

    例: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. この値から、**/_wmcs/licensing** 文字列を削除します。 例: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    残りの文字列は、ServiceLocation パラメーターに指定する値です。

たとえば、 [Office 2010](../known-issues.md#aip-and-legacy-windows-and-office-versions) 用にクライアントをサイレントインストールし、Azure RMS するには、次のようにします。

```powershell
AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
```


## <a name="install-the-unified-labeling-client-using-the-msi-installer"></a>.Msi インストーラーを使用して、統一されたラベル付けクライアントをインストールする

集中展開の場合は、Azure Information Protection 統合ラベル付けクライアントの **.msi** インストールバージョンに固有の次の情報を使用します。 

ソフトウェアの展開方法に Intune を使用する場合は、次の手順を実行するとともに、「[Microsoft Intune でアプリを追加する](/mem/intune/apps/apps-add)」をご覧ください。

**統合されたラベル付けクライアントを .msi ファイルと共にインストールするには**

1. Azure Information Protection 統合されたラベル付けクライアント (**AzInfoProtection_UL**) の **.Msi** バージョンを [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53018)からダウンロードします。 
    
    > [!IMPORTANT]
    > プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。
    > 

1. **.Msi** ファイルを実行するコンピューターごとに、次のソフトウェアの依存関係が配置されていることを確認する必要があります。 

    たとえば、 **.msi** バージョンのクライアントを使用してパッケージ化するか、次の依存関係を満たすコンピューターにのみ展開します。
    
    |Office のバージョン|オペレーティング システム|ソフトウェア|操作|
    |--------------------|--------------|----------------|---------------------|
    |**Office 365 1902 以降を除くすべてのバージョン**|Windows 10 バージョン 1809 のみ、17763.348 より前のオペレーティング システム ビルド|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|インストール|
    |**Office 2016**|サポートされているすべてのバージョン|64 ビット: [KB317866](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 ビット: [KB317866](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> バージョン: 1.0|インストール|
    |**Office 2013**|サポートされているすべてのバージョン|64 ビット: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 ビット: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />バージョン: 1.0|インストール|
    |[**Office 2010**](../known-issues.md#aip-and-legacy-windows-and-office-versions)|サポートされているすべてのバージョン|[Microsoft Online Services サインインアシスタント](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> バージョン: 2.1|インストール|
    |[**Office 2010**](../known-issues.md#aip-and-legacy-windows-and-office-versions)|Windows 8.1 および Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|KB2843630 または KB2919355 がインストールされていない場合はインストールします|
    |[**Office 2010**](../known-issues.md#aip-and-legacy-windows-and-office-versions)|Windows 8 と Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> ファイル名に含まれるバージョン番号: v3|インストール|
    | | | | |

    > [!IMPORTANT]
    > Office 2010 の拡張サポートは、2020年10月13日に終了しました。 詳細については、「 [AIP and Legacy Windows And Office versions](../known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。
    >

1. 既定のインストールでは、`AzInfoProtection_UL.msi /quiet` のように、**/quiet** を付けて .msi を実行します。

    場合によっては、追加のインストールパラメーターを指定する必要があります。 詳細については、「 [実行可能ファイルインストーラーの手順](#install-the-aip-unified-labeling-client-using-the-executable-installer)」を参照してください。

    > [!NOTE]
    > 既定では、[ **使用状況の統計情報を Microsoft インストールに送信して Azure Information Protection を向上させる** ] オプションが有効になっています。 このオプションを無効にするには、次のいずれかを実行してください。
    >
    >- インストール中に、 **Allowtelemetry = 0** を指定します。
    >- インストール後、レジストリキーを次のように更新します: **EnableTelemetry = 0**。
    >

## <a name="next-steps"></a>次のステップ
Azure Information Protection 統合されたラベル付けクライアントをインストールしたので、このクライアントのサポートに必要な追加情報については、次を参照してください。

- [クライアントのファイルと使用状況ログ](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)