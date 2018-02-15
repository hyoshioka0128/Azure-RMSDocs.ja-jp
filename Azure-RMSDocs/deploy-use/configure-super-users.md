---
title: "Azure Rights Management のスーパー ユーザーを構成する - AIP"
description: "Azure Information Protection の Azure Rights Management サービスのスーパー ユーザー機能を理解して実装することで、承認されたユーザーやサービスにのみ、Azure Rights Management が保護する組織のデータの読み取りと検査を許可することができます。 この機能は \"データの推論\" とも呼ばれ、組織のデータの制御を維持する上で重要な要素です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a134d6619f67bfc3d26cb1726fe07e8ffca403cd
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2018
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection の Azure Rights Management サービスのスーパー ユーザー機能を使用すると、承認されたユーザーやサービスにのみ、Azure Rights Management が保護する組織のデータの読み取りと検査を許可することができます。 必要に応じて、以前に適用していた保護を解除するか、保護を変更します。 

スーパー ユーザーは、組織の Azure Information Protection テナントで保護されているドキュメントと電子メールに対して、Rights Management フル コントロール[使用権限](configure-usage-rights.md)を常に持っています。 この機能は "データの推論" とも呼ばれ、組織のデータの制御を維持する上で重要な要素です。 たとえば、次のようなシナリオでこの機能を使用します。

- ある従業員が退職するので、その従業員が保護したファイルを読み取る必要がある。

- IT 管理者が、ファイルに構成されていた現行の保護ポリシーを削除し、新しい保護ポリシーを適用する必要がある。

- Exchange Server で、検索操作のためにメールボックスのインデックスを作成する必要がある。

- 既に保護されているファイルを検査する必要があるデータ損失防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、およびマルウェア対策製品用の既存の IT サービスがある。

- 監査、法律などのコンプライアンス上の理由からファイルの暗号化を一括解除する必要がある。

既定でスーパー ユーザー機能は有効ではないので、このロールが割り当てられているユーザーはいません。 この機能は Exchange の Rights Management コネクタを構成すると自動的に有効になります。Exchange Online、SharePoint Online、または SharePoint Server を実行する標準サービスには必要のない機能です。

スーパー ユーザー機能を手動で有効にする必要がある場合は、PowerShell コマンドレット [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature) を使用し、必要に応じて [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) コマンドレットまたは [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) コマンドレットを使用してユーザー (またはサービス アカウント) を割り当て、必要に応じてユーザー (または他のグループ) をこのグループに追加します。 

スーパー ユーザーのグループを使用する方が管理は簡単ですが、パフォーマンス上の理由から、Azure Rights Management では[グループのメンバーシップをキャッシュ](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection)している点に注意してください。 そのため、コンテンツの暗号化をすぐに解除するために新しいユーザーをスーパー ユーザーに割り当てる必要がある場合は、Set-AadrmSuperUserGroup を使用して構成した既存のグループにユーザーを追加するのではなく、Add-AadrmSuperUser を使用してそのユーザーを追加します。

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。

スーパー ユーザー機能のセキュリティのベスト プラクティス:

- Office 365 または Azure Information Protection テナントのグローバル管理者が割り当てられている管理者、または [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) コマンドレットを使用して GlobalAdministrator ロールが割り当てられている管理者を制限および監視します。 これらのユーザーは、スーパー ユーザー機能を有効にして、ユーザー (および自分自身) をスーパー ユーザーとして割り当てることができます。また、組織が保護するすべてのファイルの暗号化を解除することもできます。

- スーパー ユーザーとして個別に割り当てられているユーザーおよびサービスのアカウントを確認するには、[Get-AadrmSuperUser コマンドレット](/powershell/module/aadrm/get-aadrmsuperuser)を使用します。 スーパー ユーザー グループが構成されているかどうかを確認するには、[Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperusergroup) コマンドレットと標準のユーザー管理ツールを使用して、どのユーザーがこのグループのメンバーであるかを確認します。 すべての管理操作と同様に、スーパー ユーザー機能の有効/無効の切り替えはログに記録されます。また、[Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) コマンドを使用して監査することができます。 スーパー ユーザーがファイルの暗号化を解除すると、その操作はログに記録され、[使用状況ログ](log-analyze-usage.md)で監査できます。

- 日常的なサービスにスーパー ユーザー機能が必要ない場合は、必要なときにのみ機能を有効にし、[Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature) コマンドレットを使用して機能を再度無効にします。

次のログの抜粋は、Get-AadrmAdminLog コマンドレットを使用した場合のエントリ例です。 この例では、Contoso Ltd の管理者はスーパー ユーザー機能が無効であることを確認し、Richard Simone をスーパー ユーザーとして追加し、Richard が Azure Rights Management サービスに構成されている唯一のスーパー ユーザーであることを確認してから、スーパー ユーザー機能を有効にします。これで、Richard は、退職した従業員が保護していたファイルの暗号化を解除できるようになりました。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>スーパー ユーザー向けのスクリプト オプション
多くの場合、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] のスーパー ユーザーが割り当てられているユーザーは、複数の場所にある複数のファイルから保護を解除する必要があります。 手動でこの操作を実行することもできますが、スクリプト化する方が効率的です (多くの場合、信頼性も高くなります)。 そのためには、必要に応じて [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットと [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) コマンドレットを使用します。 

分類と保護を使用している場合は、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) を使用して保護を適用しない新しいラベルを適用するか、保護を適用したラベルを削除する方法もあります。 

これらのコマンドレットの詳細については、Azure Information Protection クライアントの管理者ガイドの「[Azure Information Protection クライアントでの PowerShell の使用](../rms-client/client-admin-guide-powershell.md)」を参照してください。

> [!NOTE]
> AzureInformationProtection モジュールは、RMS Protection Tool と共にインストールされる RMS Protection PowerShell モジュールを置き換えます。 これらのモジュールはどちらも、[Azure Rights Management 用のメインの Windows PowerShell モジュール](administer-powershell.md)とは異なり、これを補完するものです。 AzureInformationProtection モジュールは、Azure Information Protection、Azure Information Protection 用 Azure Rights Management サービス (Azure RMS)、および Active Directory Rights Management Services (AD RMS) をサポートします。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

