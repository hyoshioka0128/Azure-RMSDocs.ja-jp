---
title: "Windows PowerShell を使用した Azure Rights Management サービスの管理 | Azure Information Protection"
description: "Azure Information Protection の Azure Rights Management (AADRM) の Windows PowerShell モジュールを使用して、組織でこのサービスを管理する方法について説明します。"
author: cabailey
manager: mbaldwin
ms.date: 10/19/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3046fc94e92dfadd3158e2bdf0ed7eda51e8e8bc
ms.openlocfilehash: c36a5a53f0a83afedb1e840a60a59d281a751f17


---

# Windows PowerShell を使用した Azure Rights Management サービスの管理

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection の Azure Rights Management サービスは、[!INCLUDE[o365_2](../includes/o365_2_md.md)] 管理センターまたは Azure クラシック ポータルを使用してアクティブ化できますが、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (AADRM) の Windows PowerShell モジュールを使用してアクティブ化することもできます。

Azure Rights Management サービスをアクティブ化したら、それ以降サービスを管理する必要はなくなる場合があります。 ただし、高度な構成シナリオでは、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell モジュールの使用が必要になる場合があります。 次の表に、Windows PowerShell を使用する高度な構成シナリオの一部を示します。 使用可能なコマンドレットの完全なリストと各コマンドレットの詳細情報については、「 [Azure Rights Management コマンドレット](http://msdn.microsoft.com/library/azure/dn629398.aspx)」を参照してください。

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 用の Windows PowerShell モジュールをインストールする必要がある場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。

また、Azure Rights Management サービス (Azure RMS) と Active Directory Rights Management サービス (AD RMS) の両方をサポートする、Windows PowerShell モジュールの補助的な **RMSProtection** というモジュールもあります。 たとえば、このモジュールでは複数ファイルの保護と、複数ファイルからの保護の削除をサポートしており、フォルダーに含まれるすべてのファイルを包括的に保護できます。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](configure-super-users.md)」トピックの「[スーパー ユーザーのスクリプト作成オプション](configure-super-users.md#scripting-options-for-super-users)」セクションを参照してください。

|実行するタスク|使用するコマンドレット|
|-------------------|------------------------------|
|オンプレミスの Rights Management (AD RMS または Windows RMS) から Azure Information Protection に移行する。|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスに接続する、またはこのサービスから切断する。|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|独自のテナント キーを生成および管理する - BYOK (Bring Your Own Key) シナリオ。|[Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスをアクティブ化または非アクティブ化する。|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Azure Information Protection の文書管理サイトをアクティブ化または非アクティブ化する。|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Azure Rights Management サービスの段階的なデプロイのためのオンボード コントロールを構成する。|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|組織の権利ポリシー テンプレートを作成および管理する。|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Expまたはt-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Impまたはt-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|インターネット接続を利用しないで、組織によって保護されたコンテンツにアクセスできる最大日数を構成します (使用ライセンスの有効期間)。|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] のスーパー ユーザー機能を管理する。|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get–AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスの管理が許可されているユーザーとグループを管理する。|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理タスクのログを取得する。|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] の使用状況ログを記録および分析する。|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスの現在の構成を表示する。|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|組織を Azure Information Protection からオンプレミスの AD RMS デプロイに移行する。|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|






<!--HONumber=Oct16_HO3-->


