---
title: "PowerShell を使用した Azure Rights Management の管理 - AIP"
description: "Azure Information Protection の Azure Rights Management (AADRM) の PowerShell モジュールを使用して、組織でこのサービスを管理する方法について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 94ec0107930e64d42ed55bce407c4b8c92f1df32
ms.sourcegitcommit: 0fa5dd38c9d66ee2ecb47dfdc9f2add12731485e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2017
---
# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>Windows PowerShell を使用した Azure Rights Management サービスの管理

>*適用対象: Azure Information Protection、Office 365*

PowerShell を使って、Azure Information Protection のために Azure Rights Management サービスを管理する必要がありますか。 あなたがグローバル管理者または[セキュリティ管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles)で、このサービスに対して必要な構成が、それをアクティブ化 (または非アクティブ化) し、Rights Management テンプレートを構成するだけである場合は、必要ないかもしれません。

ただし、構成がさらに詳細な場合、あるいはグローバル管理者やセキュリティ管理者ではなくてもグローバル管理者によってサービスを管理するアクセス許可を付与されている場合は、PowerShell を使う必要があります。 また、コマンドラインでの制御とスクリプトの使用をいっそう効率的にするときも、PowerShell を使うのがよい場合があります。

次のセクションの表では、PowerShell を使う高度な構成シナリオの一部を示します。 PowerShell を使わずに構成できる場合は、そのことも表に示してあります。

このモジュールに使用可能なコマンドレットの完全なリストと各コマンドレットの詳細情報については、「[AADRM](/powershell/module/aadrm/?view=azureipps#aadrm)」を参照してください。

> [!NOTE]
> この PowerShell モジュールをインストールする方法については、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」をご覧ください。

このサービス側 PowerShell モジュールに加えて、Azure Information Protection クライアントでは補助 PowerShell モジュール **AzureInformationProtection** がインストールされます。 このクライアント モジュールは、たとえばフォルダー内のすべてのファイルを一括して保護できるように、複数のファイルの分類と保護をサポートしています。 詳細については、管理者ガイドの「[Using PowerShell with the Azure Information Protection client](../rms-client/client-admin-guide-powershell.md)」(Azure Information Protection クライアントでの PowerShell の使用) を参照してください。

## <a name="cmdlets-grouped-by-administration-task"></a>管理タスク別にグループ化されたコマンドレット

|実行するタスク|使用するコマンドレット|
|-------------------|------------------------------|
|オンプレミスの Rights Management (AD RMS または Windows RMS) から Azure Information Protection に移行する。|[Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd)<br /><br />[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスに接続する、またはこのサービスから切断する。|[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice)<br /><br />[Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice)|
|独自のテナント キーを生成および管理する - BYOK (Bring Your Own Key) シナリオ。|[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)<br /><br />[Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey)<br /><br />[Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスをアクティブ化または非アクティブ化する。<br /><br />管理ポータルからこれらのアクションを実行することもできます。 詳細については、「[Rights Management をアクティブにする](activate-service.md)」を参照してください。|[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm)<br /><br />[Disable-Aadrm](/powershell/aadrm/vlatest/disable-aadrm)|
|Azure Information Protection の文書管理サイトをアクティブ化または非アクティブ化する。|[Disable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/disable-aadrmdocumenttrackingfeature)<br /><br />[Enable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/enable-aadrmdocumenttrackingfeature)<br /><br />[Get-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/get-aadrmdocumenttrackingfeature)<br /><br />[Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/set-aadrmdonottrackusergroup)<br /><br />[Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup)<br /><br />[Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup)|
|Azure Rights Management サービスの段階的なデプロイのためのオンボード コントロールを構成する。|[Get-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/get-aadrmonboardingcontrolpolicy)<br /><br />[Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy)|
|組織の Rights Management テンプレートを作成および管理する。<br /><br />PowerShell の方がきめ細かく制御できますが、これらのアクションの大部分は Azure Portal で実行することもできます。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。|[Add-AadrmTemplate](/powershell/aadrm/vlatest/add-aadrmtemplate)<br /><br />[Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate)<br /><br />[Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate)<br /><br />[Get-AadrmTemplateProperty](/powershell/aadrm/vlatest/get-aadrmtemplateproperty)<br /><br />[Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate)<br /><br />[New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition)<br /><br />[Remove-AadrmTemplate](/powershell/aadrm/vlatest/remove-aadrmtemplate)<br /><br />[Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty)|
|インターネット接続を利用しないで、組織によって保護されたコンテンツにアクセスできる最大日数を構成します (使用ライセンスの有効期間)。|[Get-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/get-aadrmmaxuselicensevaliditytime)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] のスーパー ユーザー機能を管理する。|[Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature)<br /><br />[Disable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/disable-aadrmsuperuserfeature)<br /><br />[Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser)<br /><br />[Get-AadrmSuperUser](/powershell/aadrm/vlatest/get-aadrmsuperuser)<br /><br />[Remove-AadrmSuperUser](/powershell/aadrm/vlatest/remove-aadrmsuperuser)<br /><br />[Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup)<br /><br />[Get-AadrmSuperUserGroup](/powershell/aadrm/vlatest/get-aadrmsuperusergroup)<br /><br />[Clear-AadrmSuperUserGroup](/powershell/aadrm/vlatest/clear-aadrmsuperusergroup)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスの管理が許可されているユーザーとグループを管理する。|[Add-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/add-aadrmrolebasedadministrator)<br /><br />[Get-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/get-aadrmrolebasedadministrator)<br /><br />[Remove-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/remove-aadrmrolebasedadministrator)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理タスクのログを取得する。|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] の使用状況ログを記録および分析する。|[Get-AadrmUserLog](/powershell/aadrm/vlatest/get-aadrmuserlog)|
|組織の [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスの現在の構成を表示する。|[Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration)|
|組織を Azure Information Protection からオンプレミスの AD RMS デプロイに移行する。|[Set-AadrmMigrationUrl](/powershell/aadrm/vlatest/set-aadrmmigrationurl)<br /><br />[Get-AadrmMigrationUrl](/powershell/aadrm/vlatest/get-aadrmmigrationurl)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
