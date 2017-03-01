---
title: "Azure Rights Management のスーパー ユーザーを構成する - AIP"
description: "Azure Information Protection からの Azure Rights Management サービスのスーパー ユーザー機能を理解し、実装して、Azure Rights Management で保護している組織のデータを、権限を持つユーザーとサービスが常に読み取り、検査することができるようにします。 この機能は &quot;データに対する推論&quot; と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: f1c50d67ba03cee9846e81f98aad6da0da33a951
ms.lasthandoff: 02/24/2017


---

# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection からの Azure Rights Management サービスのスーパー ユーザー機能によって、Azure Rights Management で保護している組織のデータを、権限を持つユーザーとサービスが常に読み取り、検査することができるようにします。 さらに必要に応じて、保護を削除したり、以前に適用されていた保護を変更したりできます。 スーパー ユーザーは常に、組織の Azure Information Protection テナントによって付与されたすべての使用ライセンスに対して完全な所有者権限を持ちます。 この機能は “データに対する推論” と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。 たとえば、次のいずれかのシナリオでこの機能を使用することがあります。

-   退職した従業員によって保護されたファイルを読み取る必要がある。

-   IT 管理者は、ファイルに対して構成されている現在の保護ポリシーを削除し、新しい保護ポリシーを適用する必要がある。

-   Exchange Server で、検索操作のためにメールボックスにインデックスを付ける必要がある。

-   既に保護されているファイルを検査する必要があるデータ損失防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、およびマルウェア対策製品用の既存の IT サービスがある。

-   監査、法律、またはその他のコンプライアンス上の理由で、ファイルを一括で復号化する必要がある。

既定で、スーパー ユーザー機能は無効であり、このロールはどのユーザーにも割り当てられていません。 これは、Exchange に Rights Management コネクタを構成すると自動的に有効にされますが、Exchange Online、SharePoint Online、または SharePoint Server を実行する標準的なサービスには必要ありません。

スーパー ユーザー機能を手動で有効にする必要がある場合は、Windows PowerShell コマンドレット [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx) を使用します。次に、必要に応じて [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) コマンドレットを使用してユーザー (またはサービス アカウント) を割り当てたり、[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx) コマンドレットを使用して、必要に応じてこのグループにユーザー (または他のグループ) を追加したりします。 

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。

スーパー ユーザー機能のセキュリティ ベスト プラクティス:

-   Office 365 または Azure Information Protection テナントのグローバル管理者が割り当てられている管理者、または [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) コマンドレットを使用して、GlobalAdministrator ロールが割り当てられている管理者を制限し、監視します。 これらのユーザーは、スーパー ユーザー機能を有効にし、ユーザー (および自分自身) をスーパー ユーザーとして割り当てることができ、組織で保護するすべてのファイルを複合化できます。

-   スーパー ユーザーとして割り当てられた個々のユーザーおよびサービス アカウントを表示するには、[Get-AadrmSuperUser コマンドレット](https://msdn.microsoft.com/library/azure/dn629408.aspx)を使用します。 スーパー ユーザー グループが構成されているかどうかを確認するには、[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) コマンドレットと標準的なユーザー管理ツールを使用して、どのユーザーがこのグループのメンバーであるかを調べます。 すべての管理アクションと同様に、スーパー機能の有効化や無効化、およびスーパー ユーザーの追加や削除はログに記録され、 [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) コマンドを使用して監査できます。 スーパー ユーザーがファイルを復号化すると、この操作はログに記録され、[使用状況ログ](log-analyze-usage.md)で監査できます。

-   日常的なサービスでスーパー ユーザー機能を必要としない場合は、必要なときにのみ有効にし、 [Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) コマンドレットを使用して、再度無効にします。

次のログの抜粋に、Get-AadrmAdminLog コマンドレットの使用によるいくつかのエントリの例を示します。 この例では、Contoso 社の管理者は、スーパー ユーザー機能が無効になっていることを確認し、スーパー ユーザーとして Richard Simone を追加します。Richard が Azure Rights Management サービス用に構成された唯一のスーパー ユーザーであることを確認してから、Richard は退職した従業員によって保護されたいくつかのファイルを復号化できるようにスーパー ユーザー機能を有効にします。

`2015-08-01T18:58:20    admin@contoso.com    GetSuperUserFeatureState    Passed    Disabled`

`2015-08-01T18:59:44    admin@contoso.com    AddSuperUser -id rsimone@contoso.com    Passed    True`

`2015-08-01T19:00:51    admin@contoso.com    GetSuperUser    Passed    rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com    SetSuperUserFeatureState -state Enabled    Passed    True`

## <a name="scripting-options-for-super-users"></a>スーパー ユーザーのスクリプト作成オプション
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] のスーパー ユーザーが割り当てられているだれかが、複数の場所で、複数のファイルから保護を削除することが必要になる場合がよくあります。 これは手動で行うことができますが、スクリプト化するとより効率的に (そしてより確実に) 行うことができます。 この場合、[Unprotect-RMSFile](/powershell/azureinformationprotection/vlatest/unprotect-rmsfile) コマンドレットを使用し、必要に応じて [Protect-RMSFile](/powershell/azureinformationprotection/vlatest/protect-rmsfile) コマンドレットも使用します。 

分類と保護を使用している場合、[Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) を使用して、保護を適用しない新しいラベルを適用したり、保護を適用したラベルを削除したりすることもできます。 

これらのコマンドレットの詳細については、「Azure Information Protection クライアント管理者ガイド」の「[Using PowerShell with the Azure Information Protection client](../rms-client/client-admin-guide-powershell.md)」(PowerShell と Azure Information Protection クライアントの使用) を参照してください。

> [!NOTE]
> AIP モジュールは、RMS 保護ツールでインストールされる RMS 保護 PowerShell モジュールを置き換えます。 これらのモジュールは、[Azure Rights Management 用のメインの Windows PowerShell モジュール](administer-powershell.md)とは異なり、補足するものです。 AIP モジュールは、Azure Information Protection、Azure Information Protection 用 Azure Rights Management サービス (Azure RMS) と、Active Directory Rights Management サービス (AD RMS) をサポートしています。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


