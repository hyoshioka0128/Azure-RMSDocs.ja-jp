---
title: Azure RMS の使用停止と非アクティブ化
description: Azure Information Protection からクラウドベースの保護サービスを今後使用しないと決定した場合の詳細および手順です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 683434b4094ca694539613279d0fae74bdde7be1
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520551"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>Azure Information Protection の使用停止と非アクティブ化

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection から Azure Rights Management サービスを使用することで、組織でコンテンツを保護するかどうかを常に制御できます。 この情報保護サービスを使用しないことに決定した場合、以前に保護されていたコンテンツから締め出されることはありません。

以前に保護されていたコンテンツに引き続きアクセスする必要がない場合、サービスを無効にして、Azure Information Protection のサブスクリプションの有効期限を終わらせることができます。 たとえば、これは、Azure Information Protection を運用環境にデプロイする前のテストが完了した場合も該当します。

ただし、運用環境で Azure Information Protection を展開し、文書やメールを保護している場合、Azure Rights Management サービスを無効にする前に Azure Information Protection テナント キーのコピーを用意してください。 サービスの無効化後に Azure Rights Management で保護されていたコンテンツに引き続きアクセスできるように、サブスクリプションが期限切れになる前にキーのコピーを用意しておいてください。 BYOK (Bring Your Own Key) ソリューションを使用し、HSM で独自のキーを生成して管理している場合、Azure Information Protection テナント キーが既に与えられています。 ただし、そのキーが Microsoft により管理されていた場合 (既定) は、「[Azure Information Protection テナント キーに対する操作](operations-tenant-key.md)」に記載されたテナント キーのエクスポート手順を参照してください。

> [!TIP]
> サブスクリプションの有効期限が切れた後も、延長された期間中、Azure Information Protection テナントでコンテンツを利用できます。 ただし、テナント キーをエクスポートすることはできなくなります。

Azure Information Protection テナント キーがある場合は、オンプレミスで Rights Management (AD RMS) をデプロイし、信頼された発行ドメイン (TPD) としてテナント キーをインポートできます。 Azure Information Protection のデプロイは次の方法で使用停止できます。

|条件|… 手順|
|----------------------------|--------------|
|すべてのユーザーに Rights Management を引き続き利用させたいが、Azure Information Protection ではなくオンプレミス ソリューションを利用する場合    →|クライアントを使用して、オンプレミス デプロイにリダイレクト、 **LicensingRedirection** Office 2016 または Office 2013 のレジストリ キー。 手順については、次を参照してください。、[サービス検索セクション](./rms-client/client-deployment-notes.md)RMS クライアント デプロイ ノート。 Office 2010 を使用して、 **LicenseServerRedirection** 」の説明に従って Office 2010 のレジストリ キー [Office Registry Settings](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)します。|
|Rights Management テクノロジの使用を完全に停止する場合|指定の管理者に[スーパー ユーザー権限](configure-super-users.md)を付与し、このユーザー用の [Azure Information Protection クライアント](./rms-client/client-admin-guide-install.md)をインストールします。<br /><br />この管理者は、Azure Information Protection によって保護されていたフォルダー内のファイルを一括で復号するのにこのクライアントからの PowerShell モジュールを使用できます。 ファイルは保護のない状態に戻り、Azure Information Protection や AD RMS などの、Rights Management テクノロジなしで読めるようになります。 この PowerShell モジュールは、Azure Information Protection と AD RMS の両方で使用できる、ために、または Azure Information Protection、または組み合わせから、保護サービスが非アクティブ化後する前にファイルを復号する選択肢があります。|
|Azure Information Protection によって保護されていたすべてのファイルを特定できないです。 あるいは、読み取れなかった保護ファイルをすべてのユーザーが自動的に読み取れるようにする場合。    →|使用してすべてのクライアント コンピューター上のレジストリ設定を展開、 **LicensingRedirection** Office 2016 と Office 2013、」の説明に従ってレジストリ キー、[サービス検索セクション](./rms-client/client-deployment-notes.md)で RMS クライアントデプロイに関する注意事項。 Office 2010 を使用して、 **LicenseServerRedirection** 」の説明に従って、レジストリ キー [Office Registry Settings](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)します。<br /><br />さらに、「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」の説明に従って、**DisableCreation** を **1** に設定して、ユーザーが新しいファイルを保護できないようにするための別のレジストリ設定をデプロイします。|
|読み取れなかったファイルに、制御された手動回復サービスを実行する場合|データ回復グループの指定のユーザーに[スーパー ユーザー権限](configure-super-users.md)を付与し、それらのユーザー用の [Azure Information Protection クライアント](./rms-client/client-admin-guide-install.md)をインストールして、標準ユーザーから要求されたときにそれらのユーザーがファイルの保護を解除できるようにします。<br /><br />すべてのコンピューターで、「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」の説明に従って、**DisableCreation** を **1** に設定して、ユーザーが新しいファイルを保護できないようにするためのレジストリ設定をデプロイします。|

この表に記載された各手順の詳細については、以下のリソースをご覧ください。

- AD RMS とデプロイメントの参照に関する詳細については、「 [Active Directory Rights Management サービスの概要](https://technet.microsoft.com/library/hh831364.aspx)」をご覧ください。

- Azure Information Protection テナント キーを TPD ファイルとしてインポートする方法については、「[信頼された発行ドメインを追加する](https://technet.microsoft.com/library/cc771460.aspx)」を参照してください。

- Azure Information Protection クライアントでの PowerShell の使用については、「[Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md)」をご覧ください。

Azure Information Protection からの保護サービスを非アクティブ化する準備ができたら、次の手順を使用します。

## <a name="deactivating-rights-management"></a>Rights Management の非アクティブ化
保護サービス、Azure Rights Management を非アクティブ化するのにには、次の手順のいずれかを使用します。

> [!TIP]
> PowerShell コマンドレットを使用することもできます。[無効 AipService](/powershell/module/aipservice/disable-aipservice)、Rights Management を非アクティブ化します。

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>Microsoft 365 管理センターから Rights Management を非アクティブ化するには

1. Office 365 管理者向けの [Rights Management ページ](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) に移動します。
    
    サインインを求められたら、Office 365 のグローバル管理者であるアカウントを使用します。

2. **[Rights Management]** ページで、 **[非アクティブ化]** をクリックします。

3.  **[Rights Management を非アクティブ化しますか?]** というメッセージが表示されたら、 **[非アクティブ化]** をクリックします。

**[Rights Management がアクティブ化されていません]** というテキストとアクティブ化するオプションが表示されます。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Azure ポータルから Rights Management を非アクティブ化するには

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ブレードに移動します。

    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 最初の **[Azure Information Protection]** ブレードで、 **[Protection activation]\(保護のアクティブ化\)** を選択します。 

3.  **[Azure Information Protection - Protection activation]\(Azure Information Protection - 保護のアクティブ化\)** ブレードで、 **[非アクティブ化]** を選びます。 **[はい]** を選択して選択肢を確定します。

情報バーに **[非アクティブ化が正常に完了しました]\(Deactivation finished successfully\)** と表示され、 **[非アクティブ化]** が **[アクティブ化]** に変わります。 
