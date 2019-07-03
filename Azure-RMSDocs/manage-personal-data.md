---
title: Azure Information Protection の個人データの管理
description: Azure Information Protection で使用される個人データと、その表示、エクスポート、削除方法について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 99a51862-83e9-4a1e-873a-a84ae1465f07
ms.reviewer: aashishr
ms.suite: ems
ms.openlocfilehash: 900b447f67bab09e0cfcb2ed243f2c6a3de71135
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521174"
---
# <a name="manage-personal-data-for-azure-information-protection"></a>Azure Information Protection の個人データの管理

Azure Information Protection を構成して使用すると、Azure Information Protection サービスによって電子メール アドレスと IP アドレスが格納され、使用されます。 これらの個人データは、次の項目に使用されます。

- Azure Information Protection ポリシー

- 保護サービス用のテンプレート

- スーパー ユーザーと、保護サービスを代理管理者 

- 保護サービス用の管理のログ

- 保護サービスの使用状況ログ

- ドキュメント追跡ログ

- Azure Information Protection クライアントと RMS クライアントの使用状況ログ 


[!INCLUDE [GDPR-related guidance](./includes/gdpr-intro-sentence.md)]


## <a name="viewing-personal-data-that-azure-information-protection-uses"></a>Azure Information Protection によって使用される個人データの表示

管理者は Azure を使用して、スコープ付きポリシーや、ラベル構成内での保護設定の電子メール アドレスを指定できます。 詳しくは、「[スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法](configure-policy-scope.md)」および「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。 

Azure Rights Management サービスからの保護を適用するように構成するラベル、電子メール アドレスでも確認できます保護テンプレート から PowerShell コマンドレットを使用して、 [AIPService モジュール](/powershell/module/aipservice)します。 この PowerShell モジュールでは、[スーパー ユーザー](configure-super-users.md)になるユーザーや、Azure Rights Management サービスの管理者になるユーザーを電子メール アドレスで指定することもできます。 

Azure Information Protection を使用してドキュメントや電子メールを分類し、保護した場合、電子メール アドレスとユーザーの IP アドレスがログ ファイルに保存される可能性があります。


### <a name="protection-templates"></a>保護テンプレート

実行、 [Get AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)保護テンプレートの一覧を取得するコマンドレットです。 テンプレート ID を使用すると、特定のテンプレートの詳細を取得できます。 `RightsDefinitions` オブジェクトは個人データを表示します (存在する場合)。 

例:
```
PS C:\Users> Get-AipServiceTemplate -TemplateId fcdbbc36-1f48-48ca-887f-265ee1268f51 | select *


TemplateId              : fcdbbc36-1f48-48ca-887f-265ee1268f51
Names                   : {1033 -> Confidential}
Descriptions            : {1033 -> This data includes sensitive business information. Exposing this data to
                          unauthorized users may cause damage to the business. Examples for Confidential information
                          are employee information, individual customer projects or contracts and sales account data.}
Status                  : Archived
RightsDefinitions       : {admin@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT,
                          REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER,
                          AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@aip500.onmicrosoft.com -> VIEW,
                          VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT,
                          EDITRIGHTSDATA, OBJMODEL, OWNER, admin2@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT,
                          DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER}
ContentExpirationDate   : 1/1/0001 12:00:00 AM
ContentValidityDuration : 0
ContentExpirationOption : Never
LicenseValidityDuration : 7
ReadOnly                : False
LastModifiedTimeStamp   : 1/26/2018 6:17:00 PM
ScopedIdentities        : {}
EnableInLegacyApps      : False
LabelId                 :
```

### <a name="super-users-and-delegated-administrators-for-the-protection-service"></a>スーパー ユーザーと、保護サービスを代理管理者

実行、 [Get AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser)コマンドレットと[get aipservicerolebasedadministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator)コマンドレットをユーザーは、スーパー ユーザー ロールまたは保護するためのグローバル管理者ロールに割り当てられているを参照してください。Azure Information Protection からのサービス (Azure Rights Management)。 これらいずれかのロールが割り当てられているユーザーについては、電子メール アドレスが表示されます。


### <a name="administration-logs-for-the-protection-service"></a>保護サービス用の管理のログ

実行、 [Get AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) Azure Information Protection からの保護サービス (Azure Rights Management) の管理操作のログを取得するコマンドレットです。 このログには、個人データが電子メール アドレスと IP アドレスの形式で記録されます。 ログはプレーン テキストで、ダウンロード後は特定の管理者の詳細をオフラインで検索できます。

以下に例を示します。
```
PS C:\Users> Get-AipServiceAdminLog -Path '.\Desktop\admin.log' -FromTime 4/1/2018 -ToTime 4/30/2018 -Verbose
The Rights Management administration log was successfully generated and can be found at .\Desktop\admin.log.
```

### <a name="usage-logs-for-the-protection-service"></a>保護サービスの使用状況ログ
実行、 [Get AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog) Azure Information Protection からの保護サービスを使用するエンドユーザーのアクションのログを取得するコマンドレットです。 ログには、個人データが電子メール アドレスと IP アドレスの形式で記録される場合があります。 ログはプレーン テキストで、ダウンロード後は特定の管理者の詳細をオフラインで検索できます。

以下に例を示します。
```
PS C:\Users> Get-AipServiceUserLog -Path '.\Desktop\' -FromDate 4/1/2018 -ToDate 4/30/2018 -NumberOfThreads 10
Acquiring access to your user log…
Downloading the log for 2018-04-01.
Downloading the log for 2018-04-03.
Downloading the log for 2018-04-06.
Downloading the log for 2018-04-09.
Downloading the log for 2018-04-10.
Downloaded the log for 2018-04-01. The log is available at .\Desktop\rmslog-2018-04-01.log.
Downloaded the log for 2018-04-03. The log is available at .\Desktop\rmslog-2018-04-03.log.
Downloaded the log for 2018-04-06. The log is available at .\Desktop\rmslog-2018-04-06.log.
Downloaded the log for 2018-04-09. The log is available at .\Desktop\rmslog-2018-04-09.log.
Downloaded the log for 2018-04-10. The log is available at .\Desktop\rmslog-2018-04-10.log.
Downloading the log for 2018-04-12.
Downloading the log for 2018-04-13.
Downloading the log for 2018-04-14.
Downloading the log for 2018-04-16.
Downloading the log for 2018-04-18.
Downloaded the log for 2018-04-12. The log is available at .\Desktop\rmslog-2018-04-12.log.
Downloaded the log for 2018-04-13. The log is available at .\Desktop\rmslog-2018-04-13.log.
Downloaded the log for 2018-04-14. The log is available at .\Desktop\rmslog-2018-04-14.log.
Downloaded the log for 2018-04-16. The log is available at .\Desktop\rmslog-2018-04-16.log.
Downloaded the log for 2018-04-18. The log is available at .\Desktop\rmslog-2018-04-18.log.
Downloading the log for 2018-04-24.
Downloaded the log for 2018-04-24. The log is available at .\Desktop\rmslog-2018-04-24.log.
```   

### <a name="document-tracking-logs"></a>ドキュメント追跡ログ

実行、 [Get AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog)コマンドレットは、ドキュメント追跡サイトについて、特定のユーザーから情報を取得します。 関連付けられたドキュメント ログ情報を追跡する取得を使用して、 [Get AipServiceTrackingLog](/powershell/module/aipservice/get-aipservicetrackinglog?view=azureipps)コマンドレット。

以下に例を示します。
```
PS C:\Users> Get-AipServiceDocumentLog -UserEmail "admin@aip500.onmicrosoft.com"


ContentId             : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer                : admin@aip500.onmicrosoft.com
Owner                 : admin@aip500.onmicrosoft.com
ContentName           :
CreatedTime           : 3/6/2018 10:24:00 PM
Recipients            : {
                        PrimaryEmail: johndoe@contoso.com
                        DisplayName: JOHNDOE@CONTOSO.COM
                        UserType: External,
                        PrimaryEmail: alice@contoso0110.onmicrosoft.com
                        DisplayName: ALICE@CONTOSO0110.ONMICROSOFT.COM
                        UserType: External
                        }
TemplateId            :
PolicyExpires         :
EULDuration           :
SendRegistrationEmail : True
NotificationInfo      : Enabled: False
                        DeniedOnly: False
                        Culture:
                        TimeZoneId:
                        TimeZoneOffset: 0
                        TimeZoneDaylightName:
                        TimeZoneStandardName:

RevocationInfo        : Revoked: False
                        RevokedTime:
                        RevokedBy:


PS C:\Users> Get-AipServiceTrackingLog -UserEmail "admin@aip500.onmicrosoft.com"

ContentId            : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer               : admin@aip500.onmicrosoft.com
RequestTime          : 3/6/2018 10:45:57 PM
RequesterType        : External
RequesterEmail       : johndoe@contoso.com
RequesterDisplayName : johndoe@contoso.com
RequesterLocation    : IP: 167.220.1.54
                       Country: US
                       City: redmond
                       Position: 47.6812453974602,-122.120736471666

Rights               : {VIEW,OBJMODEL}
Successful           : False
IsHiddenInfo         : False
```

ObjectID による検索はできません。 ただし、`-UserEmail` パラメーターによる制限はなく、指定する電子メール アドレスがテナントの一部である必要はありません。 指定した電子メール アドレスがドキュメント追跡ログ内のどこかに保存されている場合は、コマンドレットの出力にドキュメント追跡エントリが返されます。

### <a name="usage-logs-for-the-azure-information-protection-clients-and-rms-client"></a>Azure Information Protection クライアントと RMS クライアントの使用状況ログ

ドキュメントと電子メールにラベルと保護が適用されている場合、電子メール アドレスと IP アドレスは、ユーザーのコンピューター上の次の場所にあるログ ファイルに格納される可能性があります。

- Azure Information Protection の統合されたラベル付けクライアントと Azure Information Protection クライアント: %localappdata%\Microsoft\MSIP\Logs

- RMS クライアントの場合: %localappdata%\Microsoft\MSIPC\msip\Logs

また、Azure Information Protection クライアントは、この個人データをローカル Windows イベント ログの **[アプリケーションとサービス ログ]**  >  **[Azure Information Protection]** に記録します。

Azure Information Protection クライアントがスキャナーを実行した場合、個人データは、スキャナーを実行する Windows Server コンピューター上の %localappdata%\Microsoft\MSIP\Scanner\Reports に保存されます。

Azure Information Protection のクライアントとスキャナーに関する情報のログ記録をオフにするには、次の構成を使います。

- Azure Information Protection クライアント:**LogLevel** を [[オフ]](./rms-client/client-admin-guide-customizations.md#change-the-local-logging-level) に構成する**クライアントの詳細設定**を作成します。

- Azure Information Protection スキャナー:[Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) コマンドレットを使って *ReportLevel* パラメーターを **[オフ]** に設定します。

[!INCLUDE [GDPR-related guidance](./includes/gdpr-hybrid-note.md)]

## <a name="securing-and-controlling-access-to-personal-information"></a>個人情報のセキュリティ保護とアクセス制御
Azure Portal で表示および指定する個人データは、次のいずれかの [Azure Active Directory 管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)を割り当てられたユーザーだけがアクセスできます。
    
- **Azure Information Protection 管理者**

- **コンプライアンス管理者**

- **コンプライアンス データの管理者**

- **セキュリティ管理者**

- **グローバル管理者**

AIPService モジュール (または以前のモジュールでは、AADRM) を使用して指定して表示される個人データが割り当てられているユーザーのみがアクセスできる、 **Azure Information Protection 管理者**、**コンプライアンス管理者**、**コンプライアンス データ管理者**、または**グローバル管理者**ロールから Azure Active Directory、または保護サービスのグローバル管理者ロール。

## <a name="updating-personal-data"></a>個人データの更新

Azure Information Protection ポリシーのスコープ付きポリシーと保護設定の電子メール アドレスは更新することができます。 詳しくは、「[スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法](configure-policy-scope.md)」および「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。 

保護の設定から PowerShell コマンドレットを使用して同じ情報を更新することができます、 [AIPService モジュール](/powershell/module/aipservice)します。

スーパー ユーザーと代理管理者の電子メール アドレスを更新することはできません。 代わりに、指定されたユーザー アカウントを削除し、更新後の電子メール アドレスを使ったユーザー アカウントを追加します。 

### <a name="protection-templates"></a>保護テンプレート

実行、[セット AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)コマンドレットで、保護テンプレートを更新します。 個人データが内にあるため、`RightsDefinitions`プロパティも必要になりますを使用する、[新規 AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)最新の情報を権限定義オブジェクトを作成して、権限を使用するコマンドレット定義オブジェクトを`Set-AipServiceTemplateProperty`コマンドレット。

### <a name="super-users-and-delegated-administrators-for-the-protection-service"></a>スーパー ユーザーと、保護サービスを代理管理者

スーパー ユーザーの電子メール アドレスを更新する必要がある場合には、次の操作を行います。

1. 使用[削除 AipServiceSuperUser](/powershell/module/aipservice/Remove-AipServiceSuperUser)ユーザーと古い電子メール アドレスを削除します。

2. 使用[追加 AipServiceSuperUser](/powershell/module/aipservice/Add-AipServiceSuperUser)ユーザーと新しいメール アドレスを追加します。

代理管理者の電子メール アドレスを更新する必要がある場合には、次の操作を行います。

1. 使用[削除 AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Remove-AipServiceRoleBasedAdministrator)ユーザーと古い電子メール アドレスを削除します。

2. 使用[追加 AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Add-AipServiceRoleBasedAdministrator)ユーザーと新しいメール アドレスを追加します。

## <a name="deleting-personal-data"></a>個人データの削除
Azure Information Protection ポリシーのスコープ付きポリシーと保護設定の電子メール アドレスは削除することができます。 詳しくは、「[スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法](configure-policy-scope.md)」および「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。 

PowerShell コマンドレットを使用して、同じ情報を削除する、保護設定を[AIPService モジュール](/powershell/module/aipservice)します。

スーパー ユーザーおよび代理管理者の電子メール アドレスを削除するを使用してこれらのユーザーを削除、[削除 AipServiceSuperUser](/powershell/module/aipservice/Remove-AipServiceSuperUser)コマンドレットと[削除 AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Remove-AipServiceRoleBasedAdministrator)します。 

ドキュメント追跡ログ、ログの管理、または保護サービスの使用状況ログでの個人データを削除するのにには、Microsoft サポートの要求を発生させる、次のセクションを使用します。

コンピューターに保存されているクライアント ログ ファイルとスキャナー ログ内の個人データを削除するには、標準の Windows ツールを使用して、ファイルやファイル内の個人データを削除します。 

### <a name="to-delete-personal-data-with-microsoft-support"></a>Microsoft サポートを通じて個人データを削除するには

次の 3 つの手順を使用すると、Microsoft がドキュメント追跡ログ、ログの管理、または保護サービスの使用状況ログでの個人データを削除することを要求できます。 

**ステップ 1: 削除リクエストを開始する**
[Microsoft サポートに連絡](information-support.md#to-contact-microsoft-support)して Azure Information Protection のサポート ケースを開き、テナントからデータを削除するよう要請します。 自分が Azure Information Protection テナントの管理者であることを証明する必要があります。また、このプロセスの確認には数日かかることを承知しておく必要があります。 リクエストを発行する際には、削除するデータの種類に応じて、追加情報を提供する必要があります。

- 管理ログを削除するには、**終了日**を指定します。 その終了日までのすべての管理者ログが削除されます。
- 使用状況ログを削除するには、**終了日**を指定します。 その終了日までのすべての使用状況ログが削除されます。
- ドキュメント追跡ログを削除するには、**UserEmail** を指定します。 その UserEmail に関連するすべてのドキュメント追跡情報が削除されます。

これらのデータの削除は永続的な操作です。 削除リクエストが処理された後にデータを回復する手段はありません。 管理者におかれては、削除リクエストを発行する前に、必要なデータをエクスポートすることをお勧めします。

**手順 2: 確認を待つ** Microsoft で、1 つ以上のログの削除を求めるお客様のリクエストが正当なものであることを確認します。 このプロセスには、最大で 5 営業日を要することがあります。

**手順 3: 削除の確認を受け取る** データが削除されたことを知らせる確認メールが、Microsoft カスタマー サポート サービス (CSS) から送信されます。 

## <a name="exporting-personal-data"></a>個人データのエクスポート
AIPService または AADRM PowerShell コマンドレットを使用するときに、個人データは利用の検索とエクスポートを PowerShell オブジェクトとして。 `ConvertTo-Json` コマンドレットを使用すると、PowerShell オブジェクトを JSON に変換して保存できます。

## <a name="restricting-the-use-of-personal-data-for-profiling-or-marketing-without-consent"></a>プロファイリングやマーケティングに個人データを同意なく使用することの制限
Azure Information Protection では、個人データに基くプロファイリングやマーケティングに関して、Microsoft の[プライバシー条項](https://privacy.microsoft.com/privacystatement)が適用されます。

## <a name="auditing-and-reporting"></a>監査とレポート
割り当てられているユーザーのみ[管理者のアクセス許可](#securing-and-controlling-access-to-personal-information)AIPService または ADDRM のモジュールの検索と個人データのエクスポートを使用しています。 これらの操作は、ダウンロード可能な管理ログに記録されます。

削除操作の場合、サポート リクエストは Microsoft によって実行された操作の監査およびレポート記録として機能します。 、削除後に削除されたデータは検索とエクスポートを使用できず、管理者は、これを確認する AIPService モジュールから Get コマンドレットを使用します。
