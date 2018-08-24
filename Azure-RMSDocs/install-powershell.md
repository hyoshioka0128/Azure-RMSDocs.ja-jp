---
title: AADRM 用 PowerShell のインストール - AIP
description: Azure Information Protection から Azure Rights Management サービス用 Windows PowerShell をインストールする手順です。 このモジュールの名前は AADRM です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/23/2018
ms.topic: article
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5fe03b296020e28234e439f634074746ff1bd677
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2018
ms.locfileid: "42808884"
---
# <a name="installing-the-aadrm-powershell-module"></a>AADRM PowerShell モジュールのインストール

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

以下の情報は、Azure Information Protection から Azure Rights Management サービス用 Windows PowerShell をインストールする場合に役立ちます。 このモジュールの名前は AADRM です。

この PowerShell モジュールを使用すると、インターネットに接続され、次のセクションでリストする前提条件を満たす任意のコンピューターを使って、コマンドラインから Azure Rights Management サービスを管理できます。 Azure Rights Management 用の Windows PowerShell は、自動化のためのスクリプトをサポートし、高度な構成シナリオのために必要になる場合があります。 管理タスクと、モジュールがサポートする構成に関する詳細については、「[Windows PowerShell を使用した Azure Rights Management の管理](administer-powershell.md)」を参照してください。

## <a name="prerequisites"></a>必要条件
この表には、Azure Information Protection から Azure Rights Management サービス用 AADRM PowerShell モジュールをインストールして使用するための前提条件が一覧表示されています。

|要件|詳細情報|
|---------------|--------------------|
|Windows PowerShell の最小バージョン: 3.0|PowerShell セッションで「`$PSVersionTable`」と入力すると、実行中の Windows PowerShell のバージョンを確認できます。 <br /><br /> 新しいバージョンの Windows PowerShell をインストールする必要がある場合は、「[既存の Windows PowerShell をアップグレードする](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell)」を参照してください。|
|Microsoft .NET Framework の最小バージョン: 4.5<br /><br />注: 最近のオペレーティング システムには、このバージョンの Microsoft .NET Framework が付属しています。このため、手動でインストールする必要があるのは、クライアントのオペレーティング システムが Windows 8.0 よりも前のバージョンの場合か、サーバーのオペレーティング システムが Windows Server 2012 よりも前のバージョンの場合に限ります。|Microsoft .NET Framework の最小バージョンがまだインストールされていない場合は、[Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653) をダウンロードできます。<br /><br />この最小バージョンの Microsoft .NET Framework は、AADRM モジュールで使用されるクラスの一部で必要になります。|

AADRM モジュールのバージョン 2.5.0.0 以降、Microsoft Online Services サインイン アシスタントは必要なくなりました。

> [!NOTE]
> 
> Azure Rights Management 管理ツールで AADRM モジュールのバージョンをインストールした場合、PowerShell ギャラリーから AADRM モジュールの最新バージョンをインストールする前に、**[プログラムと機能]** を使って **Windows Azure AD Rights Management の管理**をアンインストールしてください。


## <a name="how-to-install-the-aadrm-module"></a>AADRM モジュールをインストールする方法

AADRM モジュールは [PowerShell ギャラリー](/powershell/gallery/readme)に移動しており、Microsoft ダウンロード センターからは入手できません。 

### <a name="to-install-the-aadrm-module-from-the-powershell-gallery"></a>PowerShell ギャラリーから AADRM モジュールをインストールするには

PowerShell ギャラリーを初めてお使いの場合は、「[PowerShell ギャラリーの概要](/powershell/gallery/psgallery/psgallery_gettingstarted)」を参照してください。 PowerShellGet モジュールと NuGet プロバイダーのインストールを含む、ギャラリー要件の手順に従います。

PowerShell ギャラリーで AADRM モジュールの詳細を確認するには、[AADRM](https://www.powershellgallery.com/packages/AADRM) に関するページを参照してください。

AADRM モジュールをインストールするには、**[管理者として実行]** オプションを使用して PowerShell セッションを開始し、次のように入力します。

    Install-Module -Name AADRM

信頼されていないリポジトリからのインストールについての警告が表示される場合は、Y キーを押して確認できます。 または、N キーを押し、`Set-PSRepository -Name PSGallery -InstallationPolicy Trusted` コマンドを使って信頼されたリポジトリとして PowerShell ギャラリーを構成した後、コマンドを再び実行して AADRM モジュールをインストールします。  

以前のバージョンの AADRM モジュールをギャラリーからインストールした場合は、次のように入力して最新バージョンに更新します。

    Update-Module -Name AADRM


## <a name="next-steps"></a>次の手順
Windows PowerShell セッションで、インストールされているモジュールのバージョンを確認します。 このチェックは、以前のバージョンからアップグレードした場合に特に重要です。

```
(Get-Module AADRM –ListAvailable).Version
```

注: このコマンドが失敗した場合は、最初に **Import-module AADRM** を実行します。

使用可能なコマンドレットを確認するには、次のコマンドを入力します。

```
Get-Command -Module AADRM
```

`Get-Help <cmdlet_name>` コマンドを使って特定のコマンドレットのヘルプをご覧ください。また、**-online** パラメーターを使って Microsoft のドキュメント サイトで最新のヘルプをご覧ください。 次に例を示します。

```
Get-Help Connect-AadrmService -online
```

詳細情報:

-   使用可能なすべてのコマンドレットの一覧: [AADRM Module](/powershell/aadrm/vlatest/rightsmanagement)

-   PowerShell をサポートする主要な構成シナリオの一覧: [Windows PowerShell を使用した Azure Rights Management の管理](administer-powershell.md)

Azure Rights Management サービスを構成するコマンドを実行するには、[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) コマンドレットを使用して前もってサービスに接続しておく必要があります。 構成コマンドの実行が完了したら、ベスト プラクティスとしては、[Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) コマンドレットを使用してサービスとの接続を切断します。 切断しない場合は、非アクティブ状態の後に自動的に切断されます。 この自動切断の挙動によって、PowerShell セッションで再接続が必要になる場合があります。 

> [!NOTE]
> Azure Rights Management サービスがまだアクティブ化されていない場合は、サービスに接続した後で、[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm) コマンドレットを使用してアクティブ化することができます。

