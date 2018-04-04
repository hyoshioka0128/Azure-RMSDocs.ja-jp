---
title: Azure Rights Management のスーパー ユーザーを構成する - AIP
description: Azure Information Protection からの Azure Rights Management サービスのスーパー ユーザー機能を理解し、実装して、Azure Rights Management で保護している組織のデータを、権限を持つユーザーとサービスが常に読み取り、検査することができるようにします。 この機能は 'データに対する推論' と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5d35f7faed0e02a253e5ba48cbdb2bca0aa76419
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection からの Azure Rights Management サービスのスーパー ユーザー機能によって、Azure Rights Management で保護している組織のデータを、権限を持つユーザーとサービスが常に読み取り、検査することができるようにします。 さらに必要に応じて、保護を削除したり、以前に適用されていた保護を変更したりできます。 

スーパー ユーザーは、組織の Azure Information Protection テナントによって保護されているドキュメントと電子メールに対する Rights Management のフル コントロール[使用権限](configure-usage-rights.md)を常に持ちます。 この機能は “データに対する推論” と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。 たとえば、次のいずれかのシナリオでこの機能を使用することがあります。

- 退職した従業員によって保護されたファイルを読み取る必要がある。

- IT 管理者は、ファイルに対して構成されている現在の保護ポリシーを削除し、新しい保護ポリシーを適用する必要がある。

- Exchange Server で、検索操作のためにメールボックスにインデックスを付ける必要がある。

- 既に保護されているファイルを検査する必要があるデータ損失防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、およびマルウェア対策製品用の既存の IT サービスがある。

- 監査、法律、またはその他のコンプライアンス上の理由で、ファイルを一括で復号化する必要がある。

## <a name="configuration-for-the-super-user-feature"></a>スーパー ユーザー機能の構成

既定で、スーパー ユーザー機能は無効であり、このロールはどのユーザーにも割り当てられていません。 これは、Exchange に Rights Management コネクタを構成すると自動的に有効にされますが、Exchange Online、SharePoint Online、または SharePoint Server を実行する標準的なサービスには必要ありません。

スーパー ユーザー機能を手動で有効にする必要がある場合は、PowerShell コマンドレット [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature) を使用します。次に、必要に応じて [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) コマンドレットを使用してユーザー (またはサービス アカウント) を割り当てたり、[Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) コマンドレットを使用して、必要に応じてこのグループにユーザー (または他のグループ) を追加したりします。 

スーパー ユーザーにグループを使用すると管理しやすくなりますが、パフォーマンス上の理由から、Azure Rights Management では[グループ メンバーシップがキャッシュされる](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection)ことに注意してください。 したがって、新しいユーザーをスーパー ユーザーとして割り当てて、すぐにコンテンツの暗号化を解除する必要がある場合には、Set-AadrmSuperUserGroup を使用して構成した既存のグループにユーザーを追加するのではなく、Add-AadrmSuperUser を使用してユーザーを追加します。

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[AADRM PowerShell モジュールのインストール](install-powershell.md)」を参照してください。

いつスーパー ユーザー機能を有効にするか、ユーザーをスーパー ユーザーとして追加するかは関係ありません。 たとえば、木曜日にこの機能を有効にして金曜日にユーザーを追加した場合、そのユーザーはその週の最初に保護されていたコンテンツをすぐに開くことができます。

## <a name="security-best-practices-for-the-super-user-feature"></a>スーパー ユーザー機能のセキュリティ ベスト プラクティス

- Office 365 または Azure Information Protection テナントのグローバル管理者が割り当てられている管理者、または [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) コマンドレットを使用して、GlobalAdministrator ロールが割り当てられている管理者を制限し、監視します。 これらのユーザーは、スーパー ユーザー機能を有効にし、ユーザー (および自分自身) をスーパー ユーザーとして割り当てることができ、組織で保護するすべてのファイルを複合化できます。

- スーパー ユーザーとして割り当てられた個々のユーザーおよびサービス アカウントを表示するには、[Get-AadrmSuperUser コマンドレット](/powershell/module/aadrm/get-aadrmsuperuser)を使用します。 スーパー ユーザー グループが構成されているかどうかを確認するには、[Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperusergroup) コマンドレットと標準的なユーザー管理ツールを使用して、どのユーザーがこのグループのメンバーであるかを調べます。 すべての管理アクションと同様に、スーパー機能の有効化や無効化、およびスーパー ユーザーの追加や削除はログに記録され、 [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) コマンドを使用して監査できます。 例については、次のセクションを参照してください。 スーパー ユーザーがファイルを復号化すると、この操作はログに記録され、[使用状況ログ](log-analyze-usage.md)で監査できます。

- 日常的なサービスでスーパー ユーザー機能を必要としない場合は、必要なときにのみ有効にし、 [Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature) コマンドレットを使用して、再度無効にします。

### <a name="example-auditing-for-the-super-user-feature"></a>スーパー ユーザー機能の監査の例

次のログの抜粋に、[Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) コマンドレットの使用によるいくつかのエントリの例を示します。 

この例では、Contoso 社の管理者は、スーパー ユーザー機能が無効になっていることを確認し、スーパー ユーザーとして Richard Simone を追加します。Richard が Azure Rights Management サービス用に構成された唯一のスーパー ユーザーであることを確認してから、Richard は退職した従業員によって保護されたいくつかのファイルを復号化できるようにスーパー ユーザー機能を有効にします。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>スーパー ユーザーのスクリプト作成オプション
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] のスーパー ユーザーが割り当てられているだれかが、複数の場所で、複数のファイルから保護を削除することが必要になる場合がよくあります。 これは手動で行うことができますが、スクリプト化するとより効率的に (そしてより確実に) 行うことができます。 この場合、[Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを使用し、必要に応じて [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) コマンドレットも使用します。 

分類と保護を使用している場合、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) を使用して、保護を適用しない新しいラベルを適用したり、保護を適用したラベルを削除したりすることもできます。 

これらのコマンドレットの詳細については、「Azure Information Protection クライアント管理者ガイド」の「[Using PowerShell with the Azure Information Protection client](../rms-client/client-admin-guide-powershell.md)」(PowerShell と Azure Information Protection クライアントの使用) を参照してください。

> [!NOTE]
> AzureInformationProtection モジュールは、RMS 保護ツールでインストールされた RMS 保護 PowerShell モジュールを置き換えます。 これらのモジュールは、[Azure Rights Management 用の PowerShell モジュール](administer-powershell.md)とは異なり、補足するものです。 AzureInformationProtection モジュールは、Azure Information Protection、Azure Information Protection 用 Azure Rights Management サービス (Azure RMS)、および Active Directory Rights Management サービス (AD RMS) をサポートしています。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

