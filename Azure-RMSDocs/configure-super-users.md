---
title: Azure Rights Management のスーパー ユーザーを構成する - AIP
description: Azure Information Protection からの Azure Rights Management サービスのスーパー ユーザー機能を理解し、実装して、Azure Rights Management で保護している組織のデータを、権限を持つユーザーとサービスが常に読み取り、検査することができるようにします。 この機能は 'データに対する推論' と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c4b4df01be10ce033dd7369e71420e949750e667
ms.sourcegitcommit: 1e6394044d646278ae582c7713cac8ffb9bf4c1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169909"
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection からの Azure Rights Management サービスのスーパー ユーザー機能によって、Azure Rights Management で保護している組織のデータを、権限を持つユーザーとサービスが常に読み取り、検査することができるようにします。 必要であれば、保護は削除したり、変更したりできます。

スーパー ユーザーは、組織の Azure Information Protection テナントによって保護されているドキュメントと電子メールに対する Rights Management のフル コントロール[使用権限](configure-usage-rights.md)を常に持ちます。 この機能は “データに対する推論” と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。 たとえば、次のいずれかのシナリオでこの機能を使用することがあります。

- 退職した従業員によって保護されたファイルを読み取る必要がある。

- IT 管理者は、ファイルに対して構成されている現在の保護ポリシーを削除し、新しい保護ポリシーを適用する必要がある。

- Exchange Server で、検索操作のためにメールボックスにインデックスを付ける必要がある。

- 既に保護されているファイルを検査する必要があるデータ損失防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、およびマルウェア対策製品用の既存の IT サービスがある。

- 監査、法律、またはその他のコンプライアンス上の理由で、ファイルを一括で復号化する必要がある。

## <a name="configuration-for-the-super-user-feature"></a>スーパー ユーザー機能の構成

既定で、スーパー ユーザー機能は無効であり、このロールはどのユーザーにも割り当てられていません。 これは、Exchange に Rights Management コネクタを構成すると自動的に有効にされますが、Exchange Online、SharePoint Online、または SharePoint Server を実行する標準的なサービスには必要ありません。

スーパー ユーザー機能を手動で有効にする必要がある場合は、PowerShell コマンドレット [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature) を使用します。次に、必要に応じて [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) コマンドレットを使用してユーザー (またはサービス アカウント) を割り当てたり、[Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) コマンドレットを使用して、必要に応じてこのグループにユーザー (または他のグループ) を追加したりします。 

スーパー ユーザーにグループを使用すると管理しやすくなりますが、パフォーマンス上の理由から、Azure Rights Management では[グループ メンバーシップがキャッシュされる](prepare.md#group-membership-caching-by-azure-information-protection)ことに注意してください。 したがって、新しいユーザーをスーパー ユーザーとして割り当てて、すぐにコンテンツの暗号化を解除する必要がある場合には、Set-AadrmSuperUserGroup を使用して構成した既存のグループにユーザーを追加するのではなく、Add-AadrmSuperUser を使用してユーザーを追加します。

> [!NOTE]
> Azure Rights Management 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[Installing the AADRM PowerShell module](install-powershell.md)」(AADRM PowerShell のインストール) を参照してください。

いつスーパー ユーザー機能を有効にするか、ユーザーをスーパー ユーザーとして追加するかは関係ありません。 たとえば、木曜日にこの機能を有効にして金曜日にユーザーを追加した場合、そのユーザーはその週の最初に保護されていたコンテンツをすぐに開くことができます。

## <a name="security-best-practices-for-the-super-user-feature"></a>スーパー ユーザー機能のセキュリティ ベスト プラクティス

- Office 365 または Azure Information Protection テナントのグローバル管理者が割り当てられている管理者、または [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) コマンドレットを使用して、GlobalAdministrator ロールが割り当てられている管理者を制限し、監視します。 これらのユーザーは、スーパー ユーザー機能を有効にし、ユーザー (および自分自身) をスーパー ユーザーとして割り当てることができ、組織で保護するすべてのファイルを複合化できます。

- スーパー ユーザーとして割り当てられた個々のユーザーおよびサービス アカウントを表示するには、[Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser) コマンドレットを使用します。 スーパー ユーザー グループが構成されているかどうかを確認するには、[Get-AadrmSuperUserGroup](/powershell/module/aadrm/get-aadrmsuperusergroup) コマンドレットと標準的なユーザー管理ツールを使用して、どのユーザーがこのグループのメンバーであるかを調べます。 すべての管理アクションと同様に、スーパー機能の有効化や無効化、およびスーパー ユーザーの追加や削除はログに記録され、 [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) コマンドを使用して監査できます。 例については、次のセクションを参照してください。 スーパー ユーザーがファイルを復号化すると、この操作はログに記録され、[使用状況ログ](log-analyze-usage.md)で監査できます。

- 日常的なサービスでスーパー ユーザー機能を必要としない場合は、必要なときにのみ有効にし、 [Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature) コマンドレットを使用して、再度無効にします。

### <a name="example-auditing-for-the-super-user-feature"></a>スーパー ユーザー機能の監査の例

次のログの抜粋に、[Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) コマンドレットの使用によるいくつかのエントリの例を示します。 

この例では、Contoso 社の管理者は、スーパー ユーザー機能が無効になっていることを確認し、スーパー ユーザーとして Richard Simone を追加します。Richard が Azure Rights Management サービス用に構成された唯一のスーパー ユーザーであることを確認してから、Richard は退職した従業員によって保護されたいくつかのファイルを復号化できるようにスーパー ユーザー機能を有効にします。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>スーパー ユーザーのスクリプト作成オプション
Azure Rights Management のスーパー ユーザーが割り当てられているだれかが、複数の場所で、複数のファイルから保護を削除することが必要になる場合がよくあります。 これは手動で行うことができますが、スクリプト化するとより効率的に (そしてより確実に) 行うことができます。 この場合、[Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを使用し、必要に応じて [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) コマンドレットも使用します。 

分類と保護を使用している場合、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) を使用して、保護を適用しない新しいラベルを適用したり、保護を適用したラベルを削除したりすることもできます。 

これらのコマンドレットの詳細については、「Azure Information Protection クライアント管理者ガイド」の「[Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)」(PowerShell と Azure Information Protection クライアントの使用) を参照してください。

> [!NOTE]
> AzureInformationProtection モジュールは、Azure Information Protection のために Azure Rights Management サービスを管理する [AADRM PowerShell モジュール](administer-powershell.md)とは異なるモジュールであり、AADRM PowerShell モジュールを補完するモジュールです。

### <a name="guidance-for-using-unprotect-rmsfile-for-ediscovery"></a>電子情報開示での Unprotect-RMSFile の使用に関するガイダンス

Unprotect-RMSFile コマンドレットを使用し、PST ファイルの保護コンテンツを復号できますが、このコマンドレットは電子情報開示プロセスの一環としてよく考えて使用してください。 1 台のコンピューター上で大きなファイルに対して Unprotect-RMSFile を実行すると、リソースが大量に消費されます (メモリとディスク領域)。このコマンドレットでサポートされている最大ファイル サイズは 5GB です。

理想としては、[Office 365 の電子情報開示](/office365/securitycompliance/ediscovery)は、保護されているメールとメールに添付されている保護ファイルを検索し、抽出する目的で使用します。 スーパー ユーザー機能は Exchange Online と自動的に統合されるので、Office 365 セキュリティ/コンプライアンス センターの電子情報開示では、暗号化されているアイテムをエクスポート前に検索したり、暗号化されているメールをエクスポート時に復号したりできます。

Office 365 の電子情報開示を利用できない場合、Azure Rights Management サービスと統合されており、同じようにデータを解決する別の電子情報開示ソリューションを用意できることがあります。 あるいは、ご利用の電子情報開示ソリューションで保護コンテンツが自動的に読み取られず、復号できない場合、複数の手順からなる以下の解決策を利用できます。この解決策では Unprotect-RMSFile をより効率的に実行できます。

1. Exchange Online、Exchange Server、またはユーザーがメールを保存したワークステーションから PST ファイルにメールをエクスポートします。

2. その PST ファイルを電子情報開示ツールにインポートします。 このツールでは保護コンテンツを読み取れないため、インポートしたアイテムはエラーを出すことが予想されます。

3. ツールで開けないすべてのアイテムから、今度は保護アイテムだけを含む新しい PST ファイルを生成します。 この 2 つ目の PST ファイルは、元の PST ファイルよりも小さくなる可能性が高くなります。

4. 小さくなったこの 2 つ目の PST ファイルで Unprotect-RMSFile を実行し、そのコンテンツを復号します。 出力から、新しく復号された PST ファイルを情報開示ツールにインポートします。

メールボックスと PST ファイル全体で電子情報開示を実行する方法について詳しくは、ブログ投稿「[Azure Information Protection and eDiscovery Processes](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-and-eDiscovery-Processes/ba-p/270216)」 (Azure Information Protection と電子情報開示プロセス) をご覧ください。

