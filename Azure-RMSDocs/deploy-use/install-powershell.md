---
title: "Azure Rights Management 用 Windows PowerShell をインストールする | Azure Information Protection"
description: "Azure Information Protection から Azure Rights Management サービス用 Windows PowerShell をインストールする手順です。 このモジュールの名前は AADRM です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: c114059e99f3caed4fa5e2c48fe0428cb5847f68


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
|Windows PowerShell の最小バージョン:2.0|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理モジュールのサポートは、Windows PowerShell 2.0 で導入されました。<br /><br />既定では、ほとんどの Windows オペレーティング システムと共にバージョン 2.0 以上の Windows PowerShell がインストールされます。 Windows PowerShell 2.0 をインストールする必要がある場合は、「 [Windows PowerShell 2.0 のインストール](http://msdn.microsoft.com/library/ff637750.aspx)」を参照してください。<br /><br />ヒント: PowerShell セッションで「`$PSVersionTable`」と入力すると、実行中の Windows PowerShell のバージョンを確認できます。|
|Microsoft .NET Framework の最小バージョン: 4.5<br /><br />注: 最近のオペレーティング システムには、このバージョンの Microsoft .NET Framework が付属しています。このため、手動でインストールする必要があるのは、クライアントのオペレーティング システムが Windows 8.0 よりも前のバージョンの場合か、サーバーのオペレーティング システムが Windows Server 2012 よりも前のバージョンの場合に限ります。|Microsoft .NET Framework の最小バージョンがまだインストールされていない場合は、[Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653) をダウンロードできます。<br /><br />この最小バージョンの Microsoft .NET Framework は、[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理モジュールで使用されるクラスの一部で必要になります。|

> [!NOTE]
> Rights Management 管理モジュールのバージョン 2.5.0.0 以降、Microsoft Online Services サインイン アシスタントは必要なくなりました。
> 
> Rights Management 管理モジュールの以前のバージョンがインストールされている場合は、最新バージョンをインストールする前に、[**プログラムと機能**] を使用して **Windows Azure AD Rights Management の管理**をアンインストールしてください。


## <a name="how-to-install-the-rights-management-administration-module"></a>Rights Management 管理モジュールのインストール方法

1.  Microsoft ダウンロード センターに移動し、[Azure Rights Management Administration Tool](https://go.microsoft.com/fwlink/?LinkId=257721) をダウンロードします。これには、Windows PowerShell 用の [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 管理モジュールが含まれています。

2.  [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] インストーラー ファイルをダウンロードして保存したローカル フォルダーで、プラットフォーム用にダウンロードした実行可能ファイル (WindowsAzureADRightsManagementAdministration_x64 または WindowsAzureADRightsManagementAdministration_x86.exe) をダブルクリックし、Azure AD Rights Management Administration セットアップ ウィザードを開始します。

3.  ウィザードを完了します。

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell がインストールされます。

## <a name="next-steps"></a>次のステップ
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
> Azure Rights Management サービスがまだアクティブ化されていない場合は、サービスに接続した後で、[Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) コマンドレットを使用してアクティブ化することができます。

## <a name="see-also"></a>関連項目
[Windows PowerShell を使用した Azure Rights Management の管理](administer-powershell.md)



<!--HONumber=Nov16_HO2-->


