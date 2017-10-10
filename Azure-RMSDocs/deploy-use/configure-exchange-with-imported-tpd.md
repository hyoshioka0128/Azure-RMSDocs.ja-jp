---
title: "Azure Information Protection から Azure Rights Management サービスに適するように Exchange Online IRM を構成する"
description: "Office 365 テナントは Office 365 Message Encryption の新しい機能に対応していない場合に管理者が Azure Rights Management サービスに適するように Exchange Online を構成するための情報と使用説明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a0c6fe7f7b6a34eea21b646ce5573ca03b13be3c
ms.sourcegitcommit: cd3320fa34acb90f05d5d3e0e83604cdd46bd9a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2017
---
# <a name="exchange-online-irm-configuration-when-you-have-imported-a-trusted-publishing-domain"></a>信頼された発行ドメインをインポートしているときの Exchange Online IRM 構成

>*適用対象: Azure Information Protection、Office 365*

以下の手順は、信頼された発行ドメイン (TPD) をインポートし、IRM に適するように Exchange Online を既に構成しているとき、以前に暗号化された電子メールを復号しなければならないときにのみご利用ください。

いずれの条件にも当てはまらない場合、ここの手順を利用せず、「[Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)」 (Azure Information Protection 上に構築される新しい Office 365 メッセージの暗号化機能の設定) の手順をご利用ください。

## <a name="exchange-online-irm-configuration-if-you-have-an-imported-tpd"></a>TPD をインポートしている場合の Exchange Online IRM 構成

Exchange Online を構成して Azure Rights Management サービスをサポートするには、Exchange Online で Information Rights Management (IRM) サービスを構成する必要があります。 これを行うには、Windows PowerShell を使用して (個別のモジュールをインストールする必要はありません)、[Exchange Online 用 PowerShell コマンド](https://technet.microsoft.com/library/jj200677.aspx)を実行します。

> [!NOTE]
> ご利用の Office 365 をマイクロソフトが移行するまで、マイクロソフト管理のテナント キーの既定の構成ではなく Azure Information Protection の顧客管理のテナント キー (BYOK) を使用する場合は、Azure Rights Management サービスをサポートするように Exchange Online を構成することはできません。
>
> Azure Rights Management サービスで BYOK を使用しているときに Exchange Online を構成しようとすると、キーをインポートするコマンド (次の手順 5) は、**[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]** というエラー メッセージで失敗します。

次の手順では、標準的な一連のコマンドを提供します。このシナリオで Azure Rights Management サービスを利用する目的で Exchange Online を有効にする場合に実行できます。

1.  コンピューターで Exchange Online 用 Windows PowerShell を初めて使用する場合は、署名済みスクリプトを実行するように Windows PowerShell を構成する必要があります。 [ **管理者として実行** ] オプションを使用して Windows PowerShell セッションを開始し、次のように入力します。

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  Windows PowerShell セッションで、リモート シェル アクセスが有効になっているアカウントを使用して Exchange Online にサインインします。 既定では、Exchange Online で作成されたすべてのアカウントではリモート シェル アクセスが有効になっていますが、[Set-User &lt;ユーザー ID&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx) コマンドを使用することで無効 (または有効) にすることができます。

    サインインするには、次のように入力します。

    ```
    $UserCredential = Get-Credential
    ```
    [ **Windows PowerShell 資格情報要求** ] ダイアログ ボックスで、Office 365 のユーザー名とパスワードを入力します。

3.  Exchange Online サービスに接続するには、次の 2 つのコマンドを実行します。

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  組織のテナントを作成した場所に応じて、Azure Information Protection テナント キーの場所を指定します。

    北アメリカ:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    ヨーロッパ:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    アジア:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    南アメリカ:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Office 365 Government (政府機関コミュニティ クラウド) の場合:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.govus.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  信頼された発行ドメイン (TPD) の形式で、Azure Rights Management サービスから構成データを Exchange Online にインポートします。 このデータには、Azure Information Protection テナント キーと Azure Rights Management テンプレートが含まれます。

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    このコマンドでは、Exchange Online での Azure Rights Management の TPD の基本名に **RMS Online** の名前が使用されています。 TPD がインポートされた後は、Exchange Online では **RMS Online - 1** という名前になります。

6.  Exchange Online で IRM 機能を利用できるように、Azure Rights Management の機能を有効にします。

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    このコマンドを実行した後は、Outlook クライアント、Outlook Web App、Exchange Active Sync 用の Rights Management が自動的に有効になります。

7.  必要に応じて、次のコマンドを使用して、この構成が正常に機能することをテストします。

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    例: **Test-IRMConfiguration -Sender  adams@contoso.com**

    このコマンドは、サービスへの接続の確認、構成の取得、URI、ライセンス、および任意のテンプレートの取得を含む一連のチェックを実行します。 Windows PowerShell セッションでは、これらのチェックのそれぞれの結果、およびすべてのチェックをパスした場合は最後にも、その結果が表示されます。 **全体的な結果:パス**

8.  リモート PowerShell セッションの切断:

    ```
    Remove-PSSession $Session
    ```

ユーザーは、Active Rights Management サービスを使用して電子メール メッセージを保護できるようになります。 たとえば、Outlook Web App で、拡張メニュー (**...**) から [**権限の設定**] を選択し、[ **転送不可** ] を選択するか、または使用可能なテンプレートの 1 つを選択して、電子メール メッセージおよび添付ファイルに情報保護を適用します。 ただし、Outlook Web App では、1 日分の UI がキャッシュされるため、電子メール メッセージに情報保護を適用する前、およびこれらの構成コマンドを実行した後は、この期間を待機します。 UI に新しい構成が反映されるよう更新される前は、 [ **権限の設定** ] メニューにはオプションは表示されません。

> [!IMPORTANT]
> Azure Rights Management 用の新規 [カスタム テンプレート](configure-custom-templates.md) を作成する、またはテンプレートを更新する場合は常に、次の Exchange Online の PowerShell コマンドを実行して (必要に応じて手順 2 および 3 を最初に実行します)、これらの変更を Exchange Online に同期します。`Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Exchange 管理者は、 [トランスポート ルール](https://technet.microsoft.com/library/dd302432.aspx)、 [データ損失防止 (DLP) ポリシー](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)、および [保護されたボイス メール](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (ユニファイド メッセージング) などの情報保護を自動的に適用する機能を構成できます。


### <a name="office-365-message-encryption"></a>Office 365 メッセージの暗号化
前のセクションで説明されているのと同じ手順を実行します。ただし、テンプレートを表示したくない場合は、手順 6 の前に次のコマンドを実行して、Outlook Web App および Outlook クライアントで IRM テンプレートが使用できないようにします。 `Set-IRMConfiguration -ClientAccessServerEnabled $false`

これで、 [トランスポート ルール](https://technet.microsoft.com/library/dd302432.aspx) を構成して、受信者が組織外部に居る場合にメッセージ セキュリティを自動的に更新し、[ **Office 365 のメッセージの暗号化を適用** ] オプションが選択できるようになります。

メッセージの暗号化の詳細については、Exchange ライブラリの「 [Office 365 での暗号化](https://technet.microsoft.com/library/dn569286.aspx) 」を参照してください。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
