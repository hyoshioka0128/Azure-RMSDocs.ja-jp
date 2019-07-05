---
title: Azure Information Protection の AIPService PowerShell モジュールをインストールします。
description: Azure Information Protection からの保護サービス用の PowerShell をインストールする手順です。 このモジュールの名前は、AIPService です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d6f5ccc34669781f4ec9723014d5254444255649
ms.sourcegitcommit: 849c493cef6b2578945c528f4e17373a2ef26287
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/04/2019
ms.locfileid: "67563392"
---
# <a name="installing-the-aipservice-powershell-module"></a>AIPService PowerShell モジュールのインストール

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection からの保護サービス用の Windows PowerShell モジュールをインストールするのには、次の情報を使用します。 このモジュールの名前は、AIPService、AADRM をという名前が以前のバージョンが置き換えられます。

インターネットに接続し、次のセクションに記載の前提条件を満たす任意のコンピューターを使用して、コマンドラインからの保護サービス (Azure Rights Management) を管理するのにこの PowerShell モジュールを使用できます。 Azure Information Protection 用 Windows PowerShell では、自動化のためのスクリプトをサポートまたは高度な構成シナリオのために必要な場合があります。 管理タスクと、モジュールがサポートする構成の詳細については、次を参照してください。 [PowerShell を使用して Azure Information Protection からの保護を管理する](administer-powershell.md)します。

## <a name="prerequisites"></a>前提条件
このテーブルには、インストールして Azure Information Protection からの保護サービス用 AIPService PowerShell モジュールを使用する前提条件が一覧表示します。

|要件|詳細情報|
|---------------|--------------------|
|Windows PowerShell の最小バージョン:3.0|PowerShell セッションで「`$PSVersionTable`」と入力すると、実行中の Windows PowerShell のバージョンを確認できます。 <br /><br /> 新しいバージョンの Windows PowerShell をインストールする必要がある場合は、「[既存の Windows PowerShell をアップグレードする](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell)」を参照してください。|
|Microsoft .NET Framework の最小バージョン:4.5<br /><br />注:このバージョンの Microsoft .NET Framework は、クライアント オペレーティング システムが Windows 8.0 よりも前か、サーバー オペレーティング システムが Windows Server 2012 より小さい場合にのみに手動でインストールする必要があるために、以降のオペレーティング システムに含まれています。|Microsoft .NET Framework の最小バージョンがまだインストールされていない場合は、[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653) をダウンロードできます。<br /><br />この最小バージョンの Microsoft .NET Framework は AIPService モジュールが使用するクラスの一部で必要です。|

## <a name="if-you-have-the-aadrm-module-installed"></a>AADRM モジュールをインストールした場合

AIPService モジュールには、以前のモジュールでは、AADRM が置き換えられます。 古いモジュールをインストールした場合はをアンインストールし、AIPService モジュールをインストールします。

新しいモジュールは、既存のスクリプトは引き続き機能するために、古いモジュールでコマンドレット名に別名を持っています。 ただし、元のモジュールがサポート対象外になる前に、これらの参照を更新を計画します。 AADRM モジュールのサポートは 2020 年 7 月 15日年を終了します。

開始と PowerShell セッションをアンインストールし、PowerShell ギャラリーから AADRM モジュールをインストールした場合、**管理者として実行**オプション、および種類。

    Uninstall-Module -Name AADRM

Azure Rights Management Administration Tool で AADRM モジュールをインストールした場合に使用して**プログラムと機能**をアンインストールする**Windows Azure AD Rights Management の管理**します。

## <a name="how-to-install-the-aipservice-module"></a>AIPService モジュールをインストールする方法

AIPService モジュールは、 [PowerShell ギャラリー](/powershell/gallery/readme) Microsoft ダウンロード センターからは使用できません。 

### <a name="to-install-the-aipservice-module-from-the-powershell-gallery"></a>PowerShell ギャラリーから AIPService モジュールをインストールするには

PowerShell ギャラリーを初めてお使いの場合は、「[PowerShell ギャラリーの概要](/powershell/gallery/psgallery/psgallery_gettingstarted)」を参照してください。 PowerShellGet モジュールと NuGet プロバイダーのインストールを含む、ギャラリー要件の手順に従います。

PowerShell ギャラリーで AIPService モジュールについての詳細を表示する、次を参照してください。、 [AIPService ページ](https://www.powershellgallery.com/packages/AIPService)します。

AIPService モジュールをインストールするには、使用の PowerShell セッションを開始、**管理者として実行**オプション、および種類。

    Install-Module -Name AIPService

信頼されていないリポジトリからのインストールについての警告が表示される場合は、Y キーを押して確認できます。 または N キーを押してコマンドを使用して、信頼されたリポジトリとして PowerShell ギャラリーを構成および`Set-PSRepository -Name PSGallery -InstallationPolicy Trusted`し AIPService モジュールをインストールするコマンドを再実行します。  

ギャラリーからインストールされた AIPService モジュールの以前のバージョンがある場合は、」と入力して最新のバージョン更新に。

    Update-Module -Name AIPService


## <a name="next-steps"></a>次の手順
Windows PowerShell セッションで、インストールされているモジュールのバージョンを確認します。 このチェックは、以前のバージョンからアップグレードした場合に特に重要です。

```
(Get-Module AIPService –ListAvailable).Version
```

注:このコマンドが失敗した場合は、まず実行**Import-module AIPService**します。

使用可能なコマンドレットを確認するには、次のコマンドを入力します。

```
Get-Command -Module AIPService
```

`Get-Help <cmdlet_name>` コマンドを使って特定のコマンドレットのヘルプをご覧ください。また、 **-online** パラメーターを使って Microsoft のドキュメント サイトで最新のヘルプをご覧ください。 以下に例を示します。

```
Get-Help Connect-AipService -online
```

詳しくは、次のトピックをご覧ください。

-   使用可能なコマンドレットの完全な一覧:[AIPService モジュール](/powershell/module/aipservice/?view=azureipps#aipservice)

-   PowerShell をサポートする主要な構成シナリオの一覧:[PowerShell を使用して Azure Information Protection からの保護を管理します。](administer-powershell.md)

使用して、サービスに接続する必要があります、保護サービスを構成するコマンドを実行する前に、 [Connect AipService](/powershell/module/aipservice/connect-aipservice)コマンドレット。

使用して、サービスからのベスト プラクティスとして、構成コマンドの実行が完了したら、切断、[切断 AipService](/powershell/module/aipservice/disconnect-aipservice)コマンドレット。 切断しない場合は、非アクティブ状態の後に自動的に切断されます。 この自動切断の挙動によって、PowerShell セッションで再接続が必要になる場合があります。 

> [!NOTE]
> 保護サービスがまだアクティブでない場合はこれを行うを使用して、サービスに接続した後、[有効にする AipService](/powershell/module/aipservice/enable-aipservice)コマンドレット。

