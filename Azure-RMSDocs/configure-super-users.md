---
title: Azure Rights Management のスーパー ユーザーを構成する - AIP
description: Azure Information Protection から Azure Rights Management サービスのスーパーユーザー機能を理解して実装することで、承認されたユーザーとサービスが組織の保護されたデータをいつでも読み取り、検査 ("理由") できるようになります。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4397be5c6206c74bcf8753e5452cd19b02b31316
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136737"
---
# <a name="configuring-super-users-for-azure-information-protection-and-discovery-services-or-data-recovery"></a>Azure Information Protection と、検出サービスまたはデータ復旧用のスーパー ユーザーの構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection の Azure Rights Management サービスのスーパー ユーザー機能を使用すると、承認されたユーザーやサービスにのみ、Azure Rights Management が保護する組織のデータの読み取りと検査を許可することができます。 必要であれば、保護は削除したり、変更したりできます。

スーパー ユーザーは、組織の Azure Information Protection テナントで保護されているドキュメントと電子メールに対して、Rights Management フル コントロール[使用権限](configure-usage-rights.md)を常に持っています。 この機能は “データに対する推論” と呼ばれることがあり、組織のデータの管理を維持する上で重要な要素です。 たとえば、次のようなシナリオでこの機能を使用します。

- ある従業員が退職するので、その従業員が保護したファイルを読み取る必要がある。

- IT 管理者が、ファイルに構成されていた現行の保護ポリシーを削除し、新しい保護ポリシーを適用する必要がある。

- Exchange Server で、検索操作のためにメールボックスのインデックスを作成する必要がある。

- 既に保護されているファイルを検査する必要があるデータ損失防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、およびマルウェア対策製品用の既存の IT サービスがある。

- 監査、法律などのコンプライアンス上の理由からファイルの暗号化を一括解除する必要がある。

## <a name="configuration-for-the-super-user-feature"></a>スーパー ユーザー機能の構成

既定でスーパー ユーザー機能は有効ではないので、このロールが割り当てられているユーザーはいません。 Exchange 用の Rights Management コネクタを構成すると、自動的に有効になります。また、Exchange Online、Microsoft Sharepoint Server、または SharePoint を実行する標準サービスでは、Microsoft 365 には必要ありません。

スーパーユーザー機能を手動で有効にする必要がある場合は、 [PowerShell コマンドレットを使用](/powershell/module/aipservice/enable-aipservicesuperuserfeature)して、 [AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser)コマンドレットまたは[AipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup)コマンドレットを使用し、必要に応じてユーザー (またはサービスアカウント) を割り当てます。また、必要に応じて、ユーザー (またはその他のグループ) をこのグループに追加します。 

スーパー ユーザーのグループを使用する方が管理は簡単ですが、パフォーマンス上の理由から、Azure Rights Management では[グループのメンバーシップをキャッシュ](prepare.md#group-membership-caching-by-azure-information-protection)している点に注意してください。 そのため、新しいユーザーを、すぐにコンテンツの暗号化を解除するスーパーユーザーに割り当てる必要がある場合は、AipServiceSuperUserGroup を使用して構成した既存のグループにユーザーを追加するのではなく、AipServiceSuperUser を使用してそのユーザーを追加します。

> [!NOTE]
> Azure Rights Management 用の Windows PowerShell モジュールをまだインストールしていない場合は、「 [AIPService PowerShell モジュールのインストール](install-powershell.md)」を参照してください。

いつスーパー ユーザー機能を有効にするか、ユーザーをスーパー ユーザーとして追加するかは関係ありません。 たとえば、木曜日にこの機能を有効にして金曜日にユーザーを追加した場合、そのユーザーはその週の最初に保護されていたコンテンツをすぐに開くことができます。

## <a name="security-best-practices-for-the-super-user-feature"></a>スーパー ユーザー機能のセキュリティ ベスト プラクティス

- Office 365 または Azure Information Protection テナントのグローバル管理者が割り当てられている管理者、または、 [Add Aipserviceroleベースの管理者](/powershell/module/aipservice/add-aipservicerolebasedadministrator)コマンドレットを使用して globaladministrator ロールが割り当てられている管理者を制限および監視します。 これらのユーザーは、スーパー ユーザー機能を有効にして、ユーザー (および自分自身) をスーパー ユーザーとして割り当てることができます。また、組織が保護するすべてのファイルの暗号化を解除することもできます。

- スーパーユーザーとして個別に割り当てられているユーザーとサービスアカウントを確認するには、 [AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser)コマンドレットを使用します。 スーパーユーザーグループが構成されているかどうかを確認するには、 [AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup)コマンドレットと標準のユーザー管理ツールを使用して、どのユーザーがこのグループのメンバーであるかを確認します。 すべての管理操作と同様に、スーパー機能の有効化または無効化、スーパーユーザーの追加または削除はログに記録され、 [Get AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)コマンドを使用して監査することができます。 例については、次のセクションを参照してください。 スーパー ユーザーがファイルの暗号化を解除すると、その操作はログに記録され、[使用状況ログ](log-analyze-usage.md)で監査できます。

- 日常的なサービスでスーパーユーザー機能を必要としない場合は、必要なときにのみ機能を有効にし、 [disable-Aipservices Uperuserfeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature)コマンドレットを使用して再度無効にします。

### <a name="example-auditing-for-the-super-user-feature"></a>スーパー ユーザー機能の監査の例

次のログの抜粋では、 [Get AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)コマンドレットの使用に関するいくつかのエントリの例を示しています。 

この例では、Contoso Ltd の管理者はスーパー ユーザー機能が無効であることを確認し、Richard Simone をスーパー ユーザーとして追加し、Richard が Azure Rights Management サービスに構成されている唯一のスーパー ユーザーであることを確認してから、スーパー ユーザー機能を有効にします。これで、Richard は、退職した従業員が保護していたファイルの暗号化を解除できるようになりました。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>スーパー ユーザー向けのスクリプト オプション
Azure Rights Management のスーパー ユーザーが割り当てられているだれかが、複数の場所で、複数のファイルから保護を削除することが必要になる場合がよくあります。 手動でこの操作を実行することもできますが、スクリプト化する方が効率的です (多くの場合、信頼性も高くなります)。 そのためには、必要に応じて [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットと [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) コマンドレットを使用します。 

分類と保護を使用している場合は、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) を使用して保護を適用しない新しいラベルを適用するか、保護を適用したラベルを削除する方法もあります。 

これらのコマンドレットの詳細については、Azure Information Protection クライアントの管理者ガイドの「[Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md)」を参照してください。

> [!NOTE]
> AzureInformationProtection モジュールは、Azure Information Protection 用に Azure Rights Management サービスを管理する[Aipservice PowerShell モジュール](administer-powershell.md)とは異なり、補足しています。

### <a name="guidance-for-using-unprotect-rmsfile-for-ediscovery"></a>電子情報開示での Unprotect-RMSFile の使用に関するガイダンス

Unprotect-RMSFile コマンドレットを使用し、PST ファイルの保護コンテンツを復号できますが、このコマンドレットは電子情報開示プロセスの一環としてよく考えて使用してください。 1 台のコンピューター上で大きなファイルに対して Unprotect-RMSFile を実行すると、リソースが大量に消費されます (メモリとディスク領域)。このコマンドレットでサポートされている最大ファイル サイズは 5GB です。

理想としては、[Office 365 の電子情報開示](https://docs.microsoft.com/microsoft-365/compliance/ediscovery)は、保護されているメールとメールに添付されている保護ファイルを検索し、抽出する目的で使用します。 スーパー ユーザー機能は Exchange Online と自動的に統合されるので、Office 365 セキュリティ/コンプライアンス センターまたは Microsoft 365 コンプライアンス センターの電子情報開示では、暗号化されているアイテムをエクスポート前に検索したり、暗号化されているメールをエクスポート時に復号したりできます。

Office 365 の電子情報開示を利用できない場合、Azure Rights Management サービスと統合されており、同じようにデータを解決する別の電子情報開示ソリューションを用意できることがあります。 あるいは、ご利用の電子情報開示ソリューションで保護コンテンツが自動的に読み取られず、復号できない場合、複数の手順からなる以下の解決策を利用できます。この解決策では Unprotect-RMSFile をより効率的に実行できます。

1. Exchange Online、Exchange Server、またはユーザーがメールを保存したワークステーションから PST ファイルにメールをエクスポートします。

2. その PST ファイルを電子情報開示ツールにインポートします。 このツールでは保護コンテンツを読み取れないため、インポートしたアイテムはエラーを出すことが予想されます。

3. ツールで開けないすべてのアイテムから、今度は保護アイテムだけを含む新しい PST ファイルを生成します。 この 2 つ目の PST ファイルは、元の PST ファイルよりも小さくなる可能性が高くなります。

4. 小さくなったこの 2 つ目の PST ファイルで Unprotect-RMSFile を実行し、そのコンテンツを復号します。 出力から、新しく復号された PST ファイルを情報開示ツールにインポートします。

メールボックスと PST ファイル全体で電子情報開示を実行する方法について詳しくは、ブログ投稿「[Azure Information Protection and eDiscovery Processes](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-and-eDiscovery-Processes/ba-p/270216)」 (Azure Information Protection と電子情報開示プロセス) をご覧ください。

