---
title: PowerShell を使用して Azure Information Protection からの保護を管理します。
description: このサービスは、テナントを管理する、Azure Information Protection からの保護サービス用 PowerShell モジュールを使用する方法について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 018f889c11339b97013cadd0725330b95597dd41
ms.sourcegitcommit: a2542aec8cd2bf96e94923740bf396badff36b6a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2019
ms.locfileid: "67535043"
---
# <a name="administering-protection-from-azure-information-protection-by-using-powershell"></a>PowerShell を使用して Azure Information Protection からの保護を管理します。

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

PowerShell を使用して、Azure Information Protection からの保護サービスを管理する必要がありますか。 すべての構成を Azure portal または Microsoft 365 管理センターで行える場合は、使用する必要がない場合もあります。 ただし、一部の詳細な構成には PowerShell を使用する必要があり、効率的なコマンドライン コントロールとスクリプトのために PowerShell の使用を選ぶ可能性もあります。

次のセクションの表では、PowerShell を使う高度な構成シナリオの一部を示します。 PowerShell を使わずに構成できる場合は、そのことも表に示してあります。

詳細情報については、1 つは、このモジュールの使用可能なコマンドレットの完全な一覧については、次を参照してください。 [AIPService](/powershell/module/aipservice/?view=azureipps#aipservice)します。

> [!NOTE]
> この PowerShell モジュールをインストールするを参照してください。 [AIPService PowerShell モジュールをインストールする](install-powershell.md)します。

このサービス側 PowerShell モジュールに加えて、Azure Information Protection クライアントでは補助 PowerShell モジュール **AzureInformationProtection** がインストールされます。 このクライアント モジュールは、たとえばフォルダー内のすべてのファイルを一括して保護できるように、複数のファイルの分類と保護をサポートしています。 詳細については、管理者ガイドの「[Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)」(Azure Information Protection クライアントでの PowerShell の使用) を参照してください。

## <a name="cmdlets-grouped-by-administration-task"></a>管理タスク別にグループ化されたコマンドレット

|実行するタスク|使用するコマンドレット|
|-------------------|------------------------------|
|オンプレミスの Rights Management (AD RMS または Windows RMS) から Azure Information Protection に移行する。|[Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)<br /><br />[Set-AipServiceKeyProperties](/powershell/module/aipservice/setaipservicekeyproperties)|
|組織の Rights Management サービスに接続する、またはこのサービスから切断する。|[接続 AipService](/powershell/module/aipservice/connect-aipservice)<br /><br />[切断 AipServiceService](/powershell/module/aipservice/disconnect-aipservice)|
|独自のテナント キーを生成および管理する - BYOK (Bring Your Own Key) シナリオ。|[Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)<br /><br />[Use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey)<br /><br />[Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys)|
|組織の Rights Management サービスをアクティブにする、または非アクティブ化する。<br /><br />管理ポータルからこれらのアクションを実行することもできます。 詳細については、次を参照してください。 [Azure Information Protection からの保護サービスをアクティブ化する](activate-service.md)します。|[有効にする AipService](/powershell/module/aipservice/enable-aipservice)<br /><br />[無効にする AipService](/powershell/module/aipservice/disable-aipservice)|
|Azure Information Protection のドキュメント追跡サイトを管理する。|[無効にする AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature)<br /><br />[有効にする AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)<br /><br />[Get-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature)<br /><br />[Set-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/set-aipservicedonottrackusergroup)<br /><br />[Clear-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Clear-AipServiceDoNotTrackUserGroup)<br /><br />[Get-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/get-AipServiceDoNotTrackUserGroup)<br /><br />[Get-AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)<br /><br />[Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)|
|Azure Rights Management サービスの段階的なデプロイのためのオンボード コントロールを構成する。|[Get-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/get-aipserviceonboardingcontrolpolicy)<br /><br />[Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)|
|組織の Rights Management テンプレートを作成および管理する。<br /><br />PowerShell の方がきめ細かく制御できますが、これらのアクションの大部分は Azure Portal で実行することもできます。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。|[Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)<br /><br />[Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)<br /><br />[Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)<br /><br />[Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)<br /><br />[Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetemplate)<br /><br />[New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)<br /><br />[Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)<br /><br />[セット AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)|
|インターネット接続を利用しないで、組織によって保護されたコンテンツにアクセスできる最大日数を構成します (使用ライセンスの有効期間)。|[Get-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/get-aipservicemaxuselicensevaliditytime)<br /><br />[Set-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)|
|組織の Rights Management のスーパー ユーザー機能を管理する。|[有効にする AipServiceSuperUserFeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature)<br /><br />[無効にする AipServiceSuperUserFeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature)<br /><br />[追加 AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser)<br /><br />[Get-AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser)<br /><br />[Remove-AipServiceSuperUser](/powershell/module/aipservice/remove-aipservicesuperuser)<br /><br />[セット AAipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup)<br /><br />[Get-AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup)<br /><br />[クリア AipServiceSuperUserGroup](/powershell/module/aipservice/clear-aipservicesuperusergroup)|
|組織の Rights Management サービスの管理が許可されているユーザーとグループを管理する。|[追加 Aip ServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator)<br /><br />[Get-Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator)<br /><br />[--ServiceRoleBasedAdministrator 削除 Aip](/powershell/module/aipservice/remove-aipservicerolebasedadministrator)|
|組織の Rights Management 管理タスクのログを取得する。|[Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)|
|Rights Management の使用状況ログを記録および分析する。|[Get-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog)|
|組織の Rights Management サービスの現在の構成を表示する。|[Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)|
|組織を Azure Information Protection からオンプレミスの AD RMS デプロイに移行する。|[Set-AipServiceMigrationUrl](/powershell/module/aipservice/set-aipservicemigrationurl)<br /><br />[Get-AipServiceMigrationUrl](/powershell/module/aipservice/get-aipservicemigrationurl)|

