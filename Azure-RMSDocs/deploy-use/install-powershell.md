---
title: "Azure Rights Management 用に PowerShell をインストールする - AIP"
description: "Azure Information Protection から Azure Rights Management サービス用 Windows PowerShell をインストールする手順です。 このモジュールの名前は AADRM です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5946ab7315b646abf119cb32cd66ac62535253c9
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="installing-windows-powershell-for-azure-rights-management"></a>Azure Rights Management 用 Windows PowerShell をインストールする

>*適用対象: Azure Information Protection、Office 365*

以下の情報は、Azure Information Protection から Azure Rights Management サービス用 Windows PowerShell をインストールする場合に役立ちます。

この PowerShell モジュールを使用すると、インターネットに接続され、次のセクションでリストする前提条件を満たす任意のコンピューターを使って、コマンドラインから Azure Rights Management サービスを管理できます。 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell は、自動化のためのスクリプトをサポートし、高度な構成シナリオのために必要になる場合があります。 管理タスクと、モジュールがサポートする構成に関する詳細については、「[Windows PowerShell を使用した Azure Rights Management の管理](administer-powershell.md)」を参照してください。

## <a name="prerequisites"></a>必要条件
次の表に、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell をインストールして使用するための前提条件を示します。

|要件|詳細情報|
|---------------|--------------------|
|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理モジュールをサポートする Windows のバージョン|「 **Azure Rights Management Administration Tool のダウンロード ページ** 」の [ [システム要件](http://go.microsoft.com/fwlink/?LinkId=257721)] セクションで、サポートされるオペレーティング システムの一覧を確認します。|
|Windows PowerShell の最小バージョン: 3.0|PowerShell セッションで「`$PSVersionTable`」と入力すると、実行中の Windows PowerShell のバージョンを確認できます。 <br /><br /> 新しいバージョンの Windows PowerShell をインストールする必要がある場合は、「[既存の Windows PowerShell をアップグレードする](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell)」を参照してください。|
|Microsoft .NET Framework の最小バージョン: 4.5<br /><br />注: 最近のオペレーティング システムには、このバージョンの Microsoft .NET Framework が付属しています。このため、手動でインストールする必要があるのは、クライアントのオペレーティング システムが Windows 8.0 よりも前のバージョンの場合か、サーバーのオペレーティング システムが Windows Server 2012 よりも前のバージョンの場合に限ります。|Microsoft .NET Framework の最小バージョンがまだインストールされていない場合は、[Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653) をダウンロードできます。<br /><br />この最小バージョンの Microsoft .NET Framework は、[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理モジュールで使用されるクラスの一部で必要になります。|

> [!NOTE]
> Rights Management 管理モジュールのバージョン 2.5.0.0 以降、Microsoft Online Services サインイン アシスタントは必要なくなりました。
> 
> Rights Management 管理モジュールの以前のバージョンがインストールされている場合は、最新バージョンをインストールする前に、**[プログラムと機能]** を使用して **Windows Azure AD Rights Management の管理**をアンインストールしてください。


## <a name="how-to-install-the-rights-management-administration-module"></a>Rights Management 管理モジュールのインストール方法

1. Microsoft ダウンロード センターに移動し、[Azure Rights Management Administration Tool](https://go.microsoft.com/fwlink/?LinkId=257721) を探します。これには、Windows PowerShell 用の [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 管理モジュールが含まれています。

2. [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] インストーラー ファイル **WindowsAzureADRightsManagementAdministration_x64** をダウンロードして保存します。 次に、このファイルをダブルクリックして、Azure AD Rights Management 管理セットアップ ウィザードを開始します。

3.  ウィザードを完了します。

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell がインストールされます。

## <a name="next-steps"></a>次の手順
Windows PowerShell セッションを開始し、インストールされているモジュールのバージョンを確認します。 このチェックは、以前のバージョンからアップグレードした場合に特に重要です。

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

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] サービスを構成するコマンドを実行するには、[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) コマンドレットを使用して前もってサービスに接続しておく必要があります。 

構成コマンドの実行が完了したら、ベスト プラクティスとしては、[Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) コマンドレットを使用してサービスとの接続を切断します。 切断しない場合は、非アクティブ状態の後に自動的に切断されます。 この自動切断の挙動によって、PowerShell セッションで再接続が必要になる場合があります。 

> [!NOTE]
> Azure Rights Management サービスがまだアクティブ化されていない場合は、サービスに接続した後で、[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm) コマンドレットを使用してアクティブ化することができます。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]