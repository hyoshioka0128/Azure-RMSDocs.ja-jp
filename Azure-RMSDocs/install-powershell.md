---
title: Azure Information Protection 用の AIPService PowerShell モジュールをインストールする
description: Azure Information Protection から保護サービス用の PowerShell をインストールする手順を説明します。 このモジュールの名前は AIPService です。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 23c18236413aaa2056d3eaaa30a64430de1e608b
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136836"
---
# <a name="installing-the-aipservice-powershell-module"></a>AIPService PowerShell モジュールのインストール

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection から保護サービス用の Windows PowerShell モジュールをインストールするには、次の情報を参照してください。 このモジュールの名前は AIPService で、AADRM という名前の以前のバージョンと置き換えられます。

この PowerShell モジュールを使用すると、インターネットに接続され、次のセクションに記載されている前提条件を満たす任意の Windows コンピューターを使用して、コマンドラインから保護サービス (Azure Rights Management) を管理できます。 Azure Information Protection 用の Windows PowerShell は、自動化のためのスクリプトをサポートするか、高度な構成シナリオで必要になる場合があります。 モジュールでサポートされている管理タスクと構成の詳細については、「 [PowerShell を使用した Azure Information Protection からの保護の管理](administer-powershell.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

次の表に、Azure Information Protection から保護サービス用の AIPService PowerShell モジュールをインストールして使用するための前提条件を示します。

|要件|詳細情報|
|---------------|--------------------|
|Windows PowerShell の最小バージョン: 3.0|PowerShell セッションで「`$PSVersionTable`」と入力すると、実行中の Windows PowerShell のバージョンを確認できます。 <br /><br /> 新しいバージョンの Windows PowerShell をインストールする必要がある場合は、「[既存の Windows PowerShell をアップグレードする](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell)」を参照してください。|
|Microsoft .NET Framework の最小バージョン: 4.5<br /><br />注: 最近のオペレーティング システムには、このバージョンの Microsoft .NET Framework が付属しています。このため、手動でインストールする必要があるのは、クライアントのオペレーティング システムが Windows 8.0 よりも前のバージョンの場合か、サーバーのオペレーティング システムが Windows Server 2012 よりも前のバージョンの場合に限ります。|Microsoft .NET Framework の最小バージョンがまだインストールされていない場合は、 [Microsoft .NET framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)をダウンロードできます。<br /><br />この Microsoft .NET Framework の最小バージョンは、AIPService モジュールで使用されるクラスの一部に必要です。|

## <a name="if-you-have-the-aadrm-module-installed"></a>AADRM モジュールがインストールされている場合

AIPService モジュールは、古いモジュール AADRM を置き換えます。 古いモジュールがインストールされている場合は、アンインストールしてから、AIPService モジュールをインストールします。

新しいモジュールには、既存のスクリプトが引き続き機能するように、古いモジュール内のコマンドレット名のエイリアスがあります。 ただし、古いモジュールがサポート対象外になる前に、これらの参照を更新することを計画してください。 AADRM モジュールのサポートは2020年7月15日に終了します。

PowerShell ギャラリーから AADRM モジュールをインストールした場合、アンインストールするには、[**管理者として実行**] オプションを使用して PowerShell セッションを開始し、次のように入力します。

```ps
Uninstall-Module -Name AADRM
```

Azure Rights Management 管理ツールを使用して AADRM モジュールをインストールした場合は、[**プログラムと機能**] を使用して、 **Windows Azure AD Rights Management 管理**をアンインストールします。

## <a name="how-to-install-the-aipservice-module"></a>AIPService モジュールをインストールする方法

AIPService モジュールは[PowerShell ギャラリー](https://www.powershellgallery.com/)上にあり、Microsoft ダウンロードセンターからは使用できません。

### <a name="to-install-the-aipservice-module-from-the-powershell-gallery"></a>PowerShell ギャラリーから AIPService モジュールをインストールするには

PowerShell ギャラリーを初めてお使いの場合は、「[PowerShell ギャラリーの概要](https://docs.microsoft.com/powershell/scripting/gallery/getting-started?view=powershell-6)」を参照してください。 PowerShellGet モジュールと NuGet プロバイダーのインストールを含む、ギャラリー要件の手順に従います。

PowerShell ギャラリーの AIPService モジュールの詳細を確認するには、 [Aipservice のページ](https://www.powershellgallery.com/packages/AIPService)にアクセスしてください。

AIPService モジュールをインストールするには、[**管理者として実行**] オプションを使用して PowerShell セッションを開始し、次のように入力します。

```ps
Install-Module -Name AIPService
```

信頼されていないリポジトリからのインストールについての警告が表示される場合は、Y キーを押して確認できます。 または、N キーを押し、コマンドを使用して PowerShell ギャラリーを信頼できるリポジトリとして構成して `Set-PSRepository -Name PSGallery -InstallationPolicy Trusted` から、コマンドを再実行して AIPService モジュールをインストールします。  

以前のバージョンの AIPService モジュールがギャラリーからインストールされている場合は、次のように入力して最新のバージョンに更新します。

```ps
Update-Module -Name AIPService
```

## <a name="next-steps"></a>次の手順

Windows PowerShell セッションで、インストールされているモジュールのバージョンを確認します。 このチェックは、以前のバージョンからアップグレードした場合に特に重要です。

```ps
(Get-Module AIPService –ListAvailable).Version
```

> [!NOTE]
> このコマンドが失敗した場合は、最初に**インポートモジュール AIPService**を実行します。
> 

使用可能なコマンドレットを確認するには、次のコマンドを入力します。

```ps
Get-Command -Module AIPService
```

`Get-Help <cmdlet_name>` コマンドを使って特定のコマンドレットのヘルプをご覧ください。また、**-online** パラメーターを使って Microsoft のドキュメント サイトで最新のヘルプをご覧ください。 次に例を示します。

```powershell
Get-Help Connect-AipService -online
```

詳細情報:

- 使用可能なコマンドレットの完全な一覧: [Aipservice モジュール](/powershell/module/aipservice/?view=azureipps#aipservice)

- PowerShell をサポートする主要な構成シナリオの一覧: [powershell を使用した Azure Information Protection からの保護の管理](administer-powershell.md)

保護サービスを構成するコマンドを実行する前に、 [connect-AipService](/powershell/module/aipservice/connect-aipservice)コマンドレットを使用してサービスに接続する必要があります。

構成コマンドの実行が完了したら、ベストプラクティスとして、 [disconnect-AipService](/powershell/module/aipservice/disconnect-aipservice)コマンドレットを使用してサービスから切断することをお勧めします。 切断しない場合は、非アクティブ状態の後に自動的に切断されます。 この自動切断の挙動によって、PowerShell セッションで再接続が必要になる場合があります。

> [!NOTE]
> 保護サービスがまだアクティブになっていない場合は、 [Enable-AipService](/powershell/module/aipservice/enable-aipservice)コマンドレットを使用して、サービスに接続した後でこれを行うことができます。
