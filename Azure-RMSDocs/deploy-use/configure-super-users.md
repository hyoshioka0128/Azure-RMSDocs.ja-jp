---
# required metadata

title: Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成

*適用対象: Azure Rights Management、Office 365*

Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) のスーパー ユーザー機能により、承認されたユーザーとサービスは、Azure RMS によって保護されている組織のデータをいつでも読み取り、検査することができます。 さらに必要に応じて、保護を削除したり、以前に適用されていた保護を変更したりできます。 スーパー ユーザーは常に、組織の RMS テナントによって付与されたすべての使用ライセンスに対して完全な所有者権限を持ちます。 この機能は “データに対する推論” と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。 たとえば、次のいずれかのシナリオでこの機能を使用することがあります。

-   退職した従業員によって保護されたファイルを読み取る必要がある。

-   IT 管理者は、ファイルに対して構成されている現在の保護ポリシーを削除し、新しい保護ポリシーを適用する必要がある。

-   Exchange Server で、検索操作のためにメールボックスにインデックスを付ける必要がある。

-   既に保護されているファイルを検査する必要があるデータ損失防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、およびマルウェア対策製品用の既存の IT サービスがある。

-   監査、法律、またはその他のコンプライアンス上の理由で、ファイルを一括で復号化する必要がある。

既定で、スーパー ユーザー機能は無効であり、このロールはどのユーザーにも割り当てられていません。 これは、Exchange に Rights Management コネクタを構成すると自動的に有効にされますが、Exchange Online、SharePoint Online、または SharePoint Server を実行する標準的なサービスには必要ありません。

スーパー ユーザー機能を手動で有効にする必要がある場合は、Windows PowerShell コマンドレット [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx) を使用します。次に、必要に応じて [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) コマンドレットを使用してユーザー (またはサービス アカウント) を割り当てたり、[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx) コマンドレットを使用して、必要に応じてこのグループにユーザー (または他のグループ) を追加したりします。 

> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。.

スーパー ユーザー機能のセキュリティ ベスト プラクティス:

-   Office 365 または Azure RMS テナントのグローバル管理者が割り当てられている管理者、または [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) コマンドレットを使用して、GlobalAdministrator ロールが割り当てられている管理者を制限し、監視します。 これらのユーザーは、スーパー ユーザー機能を有効にし、ユーザー (および自分自身) をスーパー ユーザーとして割り当てることができ、組織で保護するすべてのファイルを複合化できます。

-   スーパー ユーザーとして割り当てられた個々のユーザーおよびサービス アカウントを表示するには、[Get-AadrmSuperUser コマンドレット](https://msdn.microsoft.com/library/azure/dn629408.aspx)を使用します。 スーパー ユーザー グループが構成されているかどうかを確認するには、[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) コマンドレットと標準的なユーザー管理ツールを使用して、どのユーザーがこのグループのメンバーであるかを調べます。 すべての管理アクションと同様に、スーパー機能の有効化や無効化、およびスーパー ユーザーの追加や削除はログに記録され、 [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) コマンドを使用して監査できます。 スーパー ユーザーがファイルを復号化すると、この操作はログに記録され、[使用状況ログ](log-analyze-usage.md)で監査できます。.

-   日常的なサービスでスーパー ユーザー機能を必要としない場合は、必要なときにのみ有効にし、 [Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) コマンドレットを使用して、再度無効にします。

次のログの抜粋に、Get-AadrmAdminLog コマンドレットの使用によるいくつかのエントリの例を示します。 この例では、Contoso 社の管理者は、スーパー ユーザー機能が無効になっていることを確認し、スーパー ユーザーとして Richard Simone を追加します。Richard が Azure RMS 用に構成された唯一のスーパー ユーザーであることを確認してから、Richard は退職した従業員によって保護されたいくつかのファイルを復号化できるようにスーパー ユーザー機能を有効にします。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## スーパー ユーザーのスクリプト作成オプション
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] のスーパー ユーザーが割り当てられているだれかが、複数の場所で、複数のファイルから保護を削除することが必要になる場合がよくあります。 これは手動で行うことができますが、スクリプト化するとより効率的に (そしてより確実に) 行うことができます。 そのためには、 [RMS 保護ツールをダウンロード](http://www.microsoft.com/en-us/download/details.aspx?id=47256)します。 次に、[Unprotect-RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) コマンドレットを使用し、必要に応じて、[Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) コマンドレットも使用します。

これらのコマンドレットの詳細については、「[RMS 保護コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)」を参照してください。.

> [!NOTE]
> RMS 保護ツールに付属する RMS Protection PowerShell モジュールはメインの [Azure Rights Management 用 Windows PowerShell モジュール](administer-powershell.md)とは異なり、それを補足するものです。 RMS 保護モジュールは、Azure RMS と AD RMS の両方をサポートします。




<!--HONumber=Apr16_HO4-->


