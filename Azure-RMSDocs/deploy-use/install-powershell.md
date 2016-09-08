---
title: "Azure Rights Management 用 Windows PowerShell をインストールする | Azure RMS"
description: "Microsoft Azure RMS 用の Windows PowerShell をインストールするには、次の情報を参考にしてください。"
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 0f22d69387b89a590b516d3a93148fec82b23acd


---

# Azure Rights Management 用 Windows PowerShell をインストールする

>*適用対象: Azure Rights Management、Office 365*

Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 用の Windows PowerShell をインストールするには、次の情報を使用します。

この PowerShell モジュールを使用すると、インターネットに接続され次のセクションで提示する前提条件を満たす任意のコンピューターを使って、コマンドラインから [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を管理できます。 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell は、自動化のためのスクリプトをサポートし、高度な構成シナリオのために必要になる場合があります。 管理タスクと、モジュールがサポートする構成に関する詳細については、「[Windows PowerShell を使用した Azure Rights Management の管理](administer-powershell.md)」を参照してください。

## 必要条件
次の表に、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell をインストールして使用するための前提条件を示します。

|要件|詳細情報|
|---------------|--------------------|
|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理モジュールをサポートする Windows のバージョン|「 **Azure Rights Management Administration Tool のダウンロード ページ** 」の [ [システム要件](http://go.microsoft.com/fwlink/?LinkId=257721)] セクションで、サポートされるオペレーティング システムの一覧を確認します。|
|Windows PowerShell の最小バージョン:2.0|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理モジュールのサポートは、Windows PowerShell 2.0 で導入されました。<br /><br />既定では、ほとんどの Windows オペレーティング システムと共にバージョン 2.0 以上の Windows PowerShell がインストールされます。 Windows PowerShell 2.0 をインストールする必要がある場合は、「 [Windows PowerShell 2.0 のインストール](http://msdn.microsoft.com/library/ff637750.aspx)」を参照してください。<br /><br />ヒント: PowerShell セッションで「`$PSVersionTable`」と入力すると、実行中の Windows PowerShell のバージョンを確認できます。|
|Microsoft .NET Framework の最小バージョン: 4.5<br /><br />注: 最近のオペレーティング システムには、このバージョンの Microsoft .NET Framework が付属しています。このため、手動でインストールする必要があるのは、クライアントのオペレーティング システムが Windows 8.0 よりも前のバージョンの場合か、サーバーのオペレーティング システムが Windows Server 2012 よりも前のバージョンの場合に限ります。|Microsoft .NET Framework の最小バージョンがまだインストールされていない場合は、[Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653) をダウンロードできます。<br /><br />この最小バージョンの Microsoft .NET Framework は、[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理モジュールで使用されるクラスの一部で必要になります。|

> [!NOTE]
> Rights Management 管理モジュールのバージョン 2.5.0.0 以降、Microsoft Online Services サインイン アシスタントは必要なくなりました。
> 
> Rights Management 管理モジュールの以前のバージョンがインストールされている場合は、最新バージョンをインストールする前に、[**プログラムと機能**] を使用して **Windows Azure AD Rights Management の管理**をアンインストールしてください。


## Rights Management 管理モジュールのインストール方法

1.  Microsoft ダウンロード センターに移動し、[Azure Rights Management Administration Tool](https://go.microsoft.com/fwlink/?LinkId=257721) をダウンロードします。これには、Windows PowerShell 用の [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 管理モジュールが含まれています。

2.  [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] インストーラー ファイルをダウンロードして保存したローカル フォルダーで、プラットフォーム用にダウンロードした実行可能ファイル (WindowsAzureADRightsManagementAdministration_x64 または WindowsAzureADRightsManagementAdministration_x86.exe) をダブルクリックし、Azure AD Rights Management Administration セットアップ ウィザードを開始します。

3.  ウィザードを完了します。

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell がインストールされます。

## 次のステップ
使用可能なコマンドレットを確認するには、[ **管理者として実行** ] オプションを使用して、Windows PowerShell を起動し、次のように入力します。

```
Get-Command -Module aadrm
```
特定のコマンドレットのヘルプを表示するには、 `the Get-Help <cmdlet_name>` コマンドを使用します。

詳細情報:

-   使用可能なすべてのコマンドレットの一覧: [Azure Rights Management コマンドレット](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Windows PowerShell をサポートする主要な構成シナリオの一覧: [Windows PowerShell を使用した Azure Rights Management の管理](administer-powershell.md)

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] サービスを構成するコマンドを実行するには、[Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) コマンドレットを使用して前もってサービスに接続しておく必要があります。 目的の構成コマンドの実行が完了したら、 [Disconnect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) コマンドレットを使用してサービスとの接続を切断します。

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] をまだアクティブ化していない場合は、サービスに接続した後で、[Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) コマンドレットを使用してアクティブ化することができます。

## 関連項目
[Windows PowerShell を使用した Azure Rights Management の管理](administer-powershell.md)



<!--HONumber=Aug16_HO4-->


