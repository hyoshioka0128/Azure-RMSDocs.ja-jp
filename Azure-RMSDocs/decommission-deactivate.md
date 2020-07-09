---
title: Azure RMS の使用停止と非アクティブ化
description: Azure Information Protection からクラウドベースの保護サービスを今後使用しないと決定した場合の詳細および手順です。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b4892290dc9063f987f2432d5124e43ac509ec89
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136663"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>Azure Information Protection の使用停止と非アクティブ化

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection から Azure Rights Management サービスを使用することで、組織でコンテンツを保護するかどうかを常に制御できます。 この情報保護サービスを使用しないことに決定した場合、以前に保護されていたコンテンツから締め出されることはありません。

以前に保護されていたコンテンツに引き続きアクセスする必要がない場合、サービスを無効にして、Azure Information Protection のサブスクリプションの有効期限を終わらせることができます。 たとえば、これは、Azure Information Protection を運用環境にデプロイする前のテストが完了した場合も該当します。

ただし、運用環境および保護されたドキュメントと電子メールに Azure Information Protection をデプロイしている場合は、Azure Rights Management サービスを非アクティブ化する前に、Azure Information Protection テナントキーと適切な信頼された発行ドメイン (TPD) のコピーがあることを確認してください。 サービスが非アクティブになった後に Azure Rights Management によって保護されていたコンテンツへのアクセスを保持できるように、サブスクリプションの有効期限が切れる前に、キーと TPD のコピーがあることを確認してください。 

BYOK (Bring Your Own Key) ソリューションを使用し、HSM で独自のキーを生成して管理している場合、Azure Information Protection テナント キーが既に与えられています。 [今後のクラウド終了の準備](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631)手順に従っている場合は、適切な TPD もあります。 ただし、テナントキーが Microsoft によって管理されている場合 (既定)、 [Azure Information Protection テナントキーの操作](operations-tenant-key.md)でテナントキーをエクスポートする手順に関する記事を参照してください。

> [!TIP]
> サブスクリプションの有効期限が切れた後も、延長された期間中、Azure Information Protection テナントでコンテンツを利用できます。 ただし、テナント キーをエクスポートすることはできなくなります。

Azure Information Protection テナントキーと TPD がある場合は Rights Management オンプレミス (AD RMS) をデプロイし、信頼された発行ドメイン (TPD) としてテナントキーをインポートできます。 Azure Information Protection のデプロイは次の方法で使用停止できます。

|条件|… 手順|
|----------------------------|--------------|
|すべてのユーザーに Rights Management を引き続き利用させたいが、Azure Information Protection ではなくオンプレミス ソリューションを利用する場合    →|Office 2016 または Office 2013 の**LicensingRedirection**レジストリキーを使用して、オンプレミスのデプロイにクライアントをリダイレクトします。 手順については、「RMS クライアントのデプロイに関する注意事項」の「[サービスの検出」セクション](./rms-client/client-deployment-notes.md)を参照してください。 Office 2010 の場合は、「 [Office レジストリ設定](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」で説明されているように、office 2010 の**licenseserverredirection**レジストリキーを使用します。|
|Rights Management テクノロジの使用を完全に停止する場合|指定の管理者に[スーパー ユーザー権限](configure-super-users.md)を付与し、このユーザー用の [Azure Information Protection クライアント](./rms-client/client-admin-guide-install.md)をインストールします。<br /><br />この管理者は、このクライアントから PowerShell モジュールを使用して、Azure Information Protection によって保護されていたフォルダー内のファイルの一括暗号化解除を行うことができます。 ファイルは保護のない状態に戻り、Azure Information Protection や AD RMS などの、Rights Management テクノロジなしで読めるようになります。 この PowerShell モジュールは Azure Information Protection と AD RMS の両方で使用できるため、Azure Information Protection から保護サービスを非アクティブ化する前または後にファイルを復号化するか、またはその組み合わせを選択できます。|
|Azure Information Protection によって保護されていたすべてのファイルを識別することはできません。 あるいは、読み取れなかった保護ファイルをすべてのユーザーが自動的に読み取れるようにする場合。    →|RMS クライアントデプロイノートの[「サービス検出」セクション](./rms-client/client-deployment-notes.md)で説明されているように、office 2016 および office 2013 の**LicensingRedirection**レジストリキーを使用して、すべてのクライアントコンピューターにレジストリ設定を展開します。 Office 2010 の場合は、「 [Office レジストリ設定](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」で説明されているように、 **licenseserverredirection**レジストリキーを使用します。<br /><br />また、「 [Office レジストリ設定](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」で説明されているように、 **DisableCreation**を**1**に設定して、ユーザーが新しいファイルを保護できないように、別のレジストリ設定をデプロイします。|
|読み取れなかったファイルに、制御された手動回復サービスを実行する場合|データ回復グループの指定のユーザーに[スーパー ユーザー権限](configure-super-users.md)を付与し、それらのユーザー用の [Azure Information Protection クライアント](./rms-client/client-admin-guide-install.md)をインストールして、標準ユーザーから要求されたときにそれらのユーザーがファイルの保護を解除できるようにします。<br /><br />すべてのコンピューターで、「 [Office レジストリ設定](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」に説明されているように、 **DisableCreation**を**1**に設定して、ユーザーが新しいファイルを保護できないように、レジストリ設定を展開します。|

この表に記載された各手順の詳細については、以下のリソースをご覧ください。

- AD RMS とデプロイのリファレンスについては、「 [Active Directory Rights Management サービスの概要](https://technet.microsoft.com/library/hh831364.aspx)」を参照してください。

- Azure Information Protection テナント キーを TPD ファイルとしてインポートする方法については、「[信頼された発行ドメインを追加する](https://technet.microsoft.com/library/cc771460.aspx)」を参照してください。

- Azure Information Protection クライアントでの PowerShell の使用については、「[Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md)」をご覧ください。

Azure Information Protection から保護サービスを非アクティブ化する準備ができたら、次の手順を使用します。

## <a name="deactivating-rights-management"></a>Rights Management の非アクティブ化
保護サービスの Azure Rights Management を非アクティブ化するには、次のいずれかの手順に従います。

> [!TIP]
> PowerShell コマンドレット ( [-AipService](/powershell/module/aipservice/disable-aipservice)) を使用して、Rights Management を非アクティブ化することもできます。

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>Microsoft 365 管理センターから Rights Management を非アクティブ化するには

1. Office 365 管理者向けの [Rights Management ページ](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) に移動します。
    
    サインインを求められたら、Office 365 のグローバル管理者であるアカウントを使用します。

2. [**Rights Management**] ページで、[**非アクティブ化**] をクリックします。

3.  **Rights Management を非アクティブ化**するように求めるメッセージが表示されたら、[**非アクティブ化**] をクリックします。

"**Rights Management はアクティブ化されていません**" というテキストと、アクティブ化するオプションが表示されます。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Azure ポータルから Rights Management を非アクティブ化するには

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。

    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

2. 初期**Azure Information Protection**ウィンドウで、[**保護のアクティブ化**] を選択します。 

3.  [ **Azure Information Protection 保護のアクティブ化**] ウィンドウで、[**非アクティブ化**] を選択します。 **[はい]** を選択して選択肢を確定します。

情報バーに **[非アクティブ化が正常に完了しました]\(Deactivation finished successfully\)** と表示され、**[非アクティブ化]** が **[アクティブ化]** に変わります。 
