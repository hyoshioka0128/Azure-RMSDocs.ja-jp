---
title: "Windows PowerShell を使用した Azure Rights Management サービスの管理 | Azure Information Protection"
description: "Azure Information Protection の Azure Rights Management (AADRM) の PowerShell モジュールを使用して、組織でこのサービスを管理する方法について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/14/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 16d6a8a00db28c23fd650a1b8beba00333ba6ea4
ms.openlocfilehash: f9aa0d5910ba4868878ae54c446793bfc031d3c2


---

# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>Windows PowerShell を使用した Azure Rights Management サービスの管理

>*適用対象: Azure Information Protection、Office 365*

PowerShell を使って、Azure Information Protection のために Azure Rights Management サービスを管理する必要がありますか。 あなたがグローバル管理者で、このサービスに対して必要な構成が、それをアクティブ化 (または非アクティブ化) し、Rights Management テンプレートを構成するだけである場合は、必要ないかもしれません。

しかし、構成がさらに詳細なものの場合、またあなたがグローバル管理者ではなくてもグローバル管理者によってサービスを管理する権限を付与されている場合は、PowerShell を使う必要があります。 また、コマンドラインでの制御とスクリプトの使用をいっそう効率的にするときも、PowerShell を使うのがよい場合があります。

次のセクションの表では、PowerShell を使う高度な構成シナリオの一部を示します。 PowerShell を使わずに構成できる場合は、そのことも表に示してあります。

使用可能なコマンドレットの完全なリストと各コマンドレットの詳細情報については、「 [Azure Rights Management コマンドレット](http://msdn.microsoft.com/library/azure/dn629398.aspx)」を参照してください。

> [!NOTE]
> この PowerShell モジュールをインストールする方法については、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」をご覧ください。

このサービス側 PowerShell モジュールに加えて、Azure Information Protection クライアントでは補助 PowerShell モジュール **AzureInformationProtection** がインストールされます。 このクライアント モジュールは、たとえばフォルダー内のすべてのファイルを一括して保護できるように、複数のファイルの分類と保護をサポートしています。 詳細については、管理者ガイドの「[Using PowerShell with the Azure Information Protection client](../rms-client/client-admin-guide-powershell.md)」(Azure Information Protection クライアントでの PowerShell の使用) を参照してください。

## <a name="cmdlets-grouped-by-administration-task"></a>管理タスク別にグループ化されたコマンドレット

|実行するタスク|使用するコマンドレット|
|-------------------|------------------------------|
|オンプレミスの Rights Management (AD RMS または Windows RMS) から Azure Information Protection に移行する。|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスに接続する、またはこのサービスから切断する。|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|独自のテナント キーを生成および管理する - BYOK (Bring Your Own Key) シナリオ。|[Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスをアクティブ化または非アクティブ化する。<br /><br />管理ポータルからこれらのアクションを実行することもできます。 詳細については、「[Rights Management をアクティブにする](activate-service.md)」を参照してください。|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Azure Information Protection の文書管理サイトをアクティブ化または非アクティブ化する。|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Azure Rights Management サービスの段階的なデプロイのためのオンボード コントロールを構成する。|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|組織の Rights Management テンプレートを作成および管理する。<br /><br />PowerShell の方がきめ細かく制御できますが、これらのアクションの大部分は Azure クラシック ポータルで実行することもできます。 詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](configure-custom-templates.md)」を参照してください。|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Export-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|インターネット接続を利用しないで、組織によって保護されたコンテンツにアクセスできる最大日数を構成します (使用ライセンスの有効期間)。|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] のスーパー ユーザー機能を管理する。|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスの管理が許可されているユーザーとグループを管理する。|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理タスクのログを取得する。|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] の使用状況ログを記録および分析する。|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスの現在の構成を表示する。|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|組織を Azure Information Protection からオンプレミスの AD RMS デプロイに移行する。|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Feb17_HO2-->


