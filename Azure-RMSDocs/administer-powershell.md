---
title: PowerShell を使用した Azure Information Protection からの保護の管理
description: Azure Information Protection から保護サービスの PowerShell モジュールを使用して、テナントのこのサービスを管理する方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 04/28/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8ae0df982453206ec1069767dc0c25e74a996c1d
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384120"
---
# <a name="administering-protection-from-azure-information-protection-by-using-powershell"></a>PowerShell を使用した Azure Information Protection からの保護の管理

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection から、PowerShell を使用して保護サービスを管理する必要がありますか。 すべての構成を Azure portal または Microsoft 365 管理センターで行える場合は、使用する必要がない場合もあります。 ただし、一部の詳細な構成には PowerShell を使用する必要があり、効率的なコマンドライン コントロールとスクリプトのために PowerShell の使用を選ぶ可能性もあります。

次のセクションの表では、PowerShell を使う高度な構成シナリオの一部を示します。 PowerShell を使わずに構成できる場合は、そのことも表に示してあります。

このモジュールで使用可能なコマンドレットの完全な一覧については、「 [Aipservice](/powershell/module/aipservice/#aipservice)」を参照してください。

この PowerShell モジュールをインストールするには、「 [AIPService powershell モジュールのインストール](install-powershell.md)」を参照してください。

> [!TIP]
> このサービス側 PowerShell モジュールに加えて、Azure Information Protection クライアントでは補助 PowerShell モジュール **AzureInformationProtection** がインストールされます。 
>
> このクライアント モジュールは、たとえばフォルダー内のすべてのファイルを一括して保護できるように、複数のファイルの分類と保護をサポートしています。 詳細については、管理者ガイドの「 [Azure Information Protection クライアントでの PowerShell の使用](./rms-client/clientv2-admin-guide-powershell.md) 」を参照してください。

## <a name="cmdlets-grouped-by-administration-task"></a>管理タスク別にグループ化されたコマンドレット

|実行するタスク|使用するコマンドレット|
|-------------------|------------------------------|
|オンプレミスの Rights Management (AD RMS または Windows RMS) から Azure Information Protection に移行する。|[インポート-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)<br /><br />[設定-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)|
|組織の Rights Management サービスに接続する、またはこのサービスから切断する。|[接続-AipService](/powershell/module/aipservice/connect-aipservice)<br /><br />[切断-AipServiceService](/powershell/module/aipservice/disconnect-aipservice)|
|独自のテナント キーを生成および管理する - BYOK (Bring Your Own Key) シナリオ。|[設定-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)<br /><br />[AipServiceKeyVaultKey を使用します。](/powershell/module/aipservice/use-aipservicekeyvaultkey)<br /><br />[Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys)|
|組織の Rights Management サービスをアクティブにする、または非アクティブ化する。<br /><br />管理ポータルからこれらのアクションを実行することもできます。 詳細については、「[Activating the protection service from Azure Information Protection (Azure Information Protection の保護サービスのアクティブ化)](activate-service.md)」をご覧ください。|[-AipService を有効にする](/powershell/module/aipservice/enable-aipservice)<br /><br />[-AipService を無効にする](/powershell/module/aipservice/disable-aipservice)|
|Azure Rights Management サービスの段階的なデプロイのためのオンボード コントロールを構成する。|[Get-Aipserviceonworkplace Ingcontrolpolicy](/powershell/module/aipservice/get-aipserviceonboardingcontrolpolicy)<br /><br />[設定-Aipserviceonworkplace Ingcontrolpolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)|
|組織の Rights Management テンプレートを作成および管理する。<br /><br />PowerShell の方がきめ細かく制御できますが、これらのアクションの大部分は Azure Portal で実行することもできます。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。|[AipServiceTemplate を追加します。](/powershell/module/aipservice/add-aipservicetemplate)<br /><br />[Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)<br /><br />[Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)<br /><br />[Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)<br /><br />[インポート-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetemplate)<br /><br />[AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)<br /><br />[-AipServiceTemplate を削除します。](/powershell/module/aipservice/remove-aipservicetemplate)<br /><br />[Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)|
|インターネットに接続せずに、組織が保護するコンテンツにアクセスできる最大日数を構成します (使用ライセンスの有効期間)。|[AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/get-aipservicemaxuselicensevaliditytime)<br /><br />[AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)|
|組織の Rights Management のスーパー ユーザー機能を管理する。|[有効にする-Aipサービス Uperuserfeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature)<br /><br />[無効にする-Aipサービス Uperuserfeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature)<br /><br />[AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser)<br /><br />[AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser)<br /><br />[AipServiceSuperUser](/powershell/module/aipservice/remove-aipservicesuperuser)<br /><br />[AAipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup)<br /><br />[AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup)<br /><br />[AipServiceSuperUserGroup](/powershell/module/aipservice/clear-aipservicesuperusergroup)|
|組織の Rights Management サービスの管理が許可されているユーザーとグループを管理する。|[Aip-Serviceroleby Administrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator)<br /><br />[Aip-Serviceroleby Administrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator)<br /><br />[Aip-Serviceroleby Administrator](/powershell/module/aipservice/remove-aipservicerolebasedadministrator)|
|組織の Rights Management 管理タスクのログを取得する。|[Get AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)|
|Rights Management の使用状況ログを記録および分析する。|[Get-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog)|
|組織の Rights Management サービスの現在の構成を表示する。|[AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)|
|組織を Azure Information Protection からオンプレミスの AD RMS デプロイに移行する。|[AipServiceMigrationUrl](/powershell/module/aipservice/set-aipservicemigrationurl)<br /><br />[AipServiceMigrationUrl](/powershell/module/aipservice/get-aipservicemigrationurl)|
|Azure Information Protection のドキュメント追跡サイトを管理する。<br><br>**関連**: Classic クライアントのみ|[-AipServiceDocumentTrackingFeature を無効にします。](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature)<br /><br />[-AipServiceDocumentTrackingFeature の有効化](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)<br /><br />[Get-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature)<br /><br />[AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/set-aipservicedonottrackusergroup)<br /><br />[AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Clear-AipServiceDoNotTrackUserGroup)<br /><br />[AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/get-AipServiceDoNotTrackUserGroup)<br /><br />[Get AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)<br /><br />[Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)|
| | |
