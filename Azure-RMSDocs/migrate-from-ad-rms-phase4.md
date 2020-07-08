---
title: AD RMS から Azure Information Protection への移行 - フェーズ 4
description: AD RMS から Azure Information Protection への移行のフェーズ 4 には、手順 8 から 9 が含まれます。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5e1bdf52fd8d73231e9084d36d5d648a2e1ee88c
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048631"
---
# <a name="migration-phase-4---supporting-services-configuration"></a>移行フェーズ 4 - サービス構成のサポート

>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


AD RMS から Azure Information Protection への移行フェーズ 4 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 8 から手順 9 を説明します。

## <a name="step-8-configure-irm-integration-for-exchange-online"></a>手順 8.  IRM と Exchange Online の統合を構成する

> [!IMPORTANT]
> ユーザーを移行したどの受信者が保護されたメールを選択するか制御できないため、組織内のすべてのユーザーとメールを有効にしたグループに、Azure Information Protection で使用できる Azure AD のアカウントがあることを確認します。 [詳細情報](prepare.md)

選択した Azure Information Protection テナント キー トポロジから個別に、次の操作を行います。

1. AD RMS によって保護されている電子メールを Exchange Online が復号化できるようにするには、クラスターの AD RMS URL がテナントで使用可能なキーに対応していることを確認する必要があります。 これは、AD RMS クラスターの DNS SRV レコードを使用して実行されます。これは、Azure Information Protection を使用する Office クライアントを再構成するためにも使用されます。 手順 7 でクライアントの再構成用に DNS SRV レコードを作成しなかった場合は、ここで Exchange Online をサポートするためにこのレコードを作成します。 [手順](migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection)
    
    この DNS レコードが配置されると、Web とモバイルの電子メール クライアントに Outlook を使用しているユーザーはそのアプリで AD RMS によって保護された電子メールを表示できるようになります。また、Exchange では AD RMS からインポートしたキーを使用して、AD RMS によって保護されたコンテンツを暗号化解除、インデックス化、保管、保護できるようになります。  

2. Exchange Online の [Get-IRMConfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160).aspx) コマンドを実行します。 このコマンドの実行でヘルプが必要な場合は、「[Exchange Online: IRM Configuration](configure-office365.md#exchangeonline-irm-configuration)」(Exchange Online: IRM 構成) の詳しい手順を参照してください。
    
    出力で、**AzureRMSLicensingEnabled** が **True** に設定されているかどうかを確認します。
    
    - AzureRMSLicensingEnabled が **True** に設定されている場合は、この手順の追加の構成は必要ありません。 
    
    - AzureRMSLicensingEnabled が **False** に設定されている場合は、`Set-IRMConfiguration -AzureRMSLicensingEnabled $true` を実行し、[Azure Information Protection に基づいて構築された新しい Office 365 Message Encryption 機能を設定する方法](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)に関するページの検証手順を行い、Exchange Online が Azure Rights Management サービスを使用する準備が整っていることを確認します。 

## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>手順 9. Exchange サーバーおよび SharePoint サーバー用に IRM 統合を構成する

AD RMS で Exchange サーバーまたは SharePoint サーバーの Information Rights Management (IRM) 機能を使っている場合は、Rights Management (RMS) コネクタをデプロイする必要があります。このコネクタは、オンプレミスのサーバーと Azure Information Protection の保護サービスの間の通信インターフェイス (リレー) として機能します。

ここでは、コネクタをインストールして構成し、Exchange および SharePoint で IRM を無効にして、コネクタを使うようにこれらのサーバーを構成する手順を説明します。 最後に、メール メッセージの保護に使われていた AD RMS データ構成ファイル (.xml) を Azure Information Protection にインポートしてある場合、Exchange Server コンピューターのレジストリを手動で編集して、すべての信頼された発行ドメインの URL を RMS コネクタにリダイレクトする必要があります。

> [!NOTE]
> 開始する前に、「[Azure RMS をサポートするオンプレミス サーバー](./requirements-servers.md)」で、Azure Rights Management サービスがサポートしているオンプレミス サーバーのバージョンを確認してください。

### <a name="install-and-configure-the-rms-connector"></a>RMS コネクタのインストールと構成

記事「[Azure Rights Management コネクタをデプロイする](./deploy-rms-connector.md)」の説明に従って、手順 1 から 4 を実行します。 コネクタの説明の手順 5 はまだ実行しないでください。

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Exchange サーバーで IRM を無効にし、AD RMS の構成を削除する

> [!IMPORTANT]
> どの Exchange サーバーでも IRM をまだ構成していない場合は、手順 2. と 6. を実行します。
> 
> *LicensingLocation*パラメーターにすべての AD RMS クラスターのライセンス url が表示されない場合は、これらの手順を[すべて実行します。](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps)

1. 各 Exchange サーバーで、次のフォルダーを見つけて、そのフォルダー内のすべてのエントリを削除します。 **\programdata\microsoft\drm\server\s-1-5-18**

2. Exchange サーバーのいずれかで次の PowerShell コマンドを実行して、Azure Rights Management を使って保護されているメールをユーザーが読めるようにします。

    これらのコマンドを実行する前に、独自の Azure Rights Management サービスの URL に置き換えて *\<Your Tenant URL>* ください。

    ```ps
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation 
    $list += "<Your Tenant URL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    ```

    これで、 [Get IRMConfiguration](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps)を実行すると、すべての AD RMS クラスターのライセンス url と、 *LicensingLocation*パラメーターに表示される AZURE Rights Management サービスの url が表示されます。

3.  次に、内部受信者に送信されるメッセージの IRM 機能を無効にします。

    ```ps
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. その後、同じコマンドレットを使って、Microsoft Office Outlook Web App および Microsoft Exchange ActiveSync で IRM を無効にします。

    ```ps
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最後に、同じコマンドレットを使用してキャッシュされている証明書をクリアします。

    ```ps
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  各 Exchange サーバーで、たとえば管理者としてコマンド プロンプトを実行して「**iisreset**」と入力し、IIS をリセットします。

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>SharePoint サーバーで IRM を無効にし、AD RMS の構成を削除する

1.  RMS で保護されたライブラリからドキュメントがチェックアウトされていないことを確認します。 ある場合、この手順の最後でそれらにアクセスできなくなります。

2.  SharePoint サーバーの全体管理 Web サイトの **[サイド リンク バー]** セクションで、**[セキュリティ]** をクリックします。

3.  **[セキュリティ]** ページの **[情報ポリシー]** セクションで、**[Information Rights Management の構成]** をクリックします。

4.  **[Information Rights Management]** ページの **[Information Rights Management]** セクションで、**[このサーバーでは IRM を使用しない]** を選択して、**[OK]** をクリックします。

5.  各 sharepoint サーバーコンピューターで、 \\ < *sharepoint server>を実行しているアカウントの \ProgramData\Microsoft\MSIPC\Server SID*フォルダーの内容を削除します。

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>コネクタを使うように Exchange と SharePoint を構成する

1. 「[手順 5: RMS コネクタを使用するためのサーバーの構成](./configure-servers-rms-connector.md)」の RMS コネクタのデプロイ手順に戻ります。

    SharePoint サーバーだけを使っている場合は、[次の手順](#next-steps)に進んで移行を続けます。 

2. 各 Exchange サーバーで、インポートした各構成データファイル (.xml) の次のセクションにレジストリ キーを手動で追加し、信頼された発行ドメインの URL を RMS コネクタにリダイレクトします。 これらのレジストリ エントリは移行に固有であり、Microsoft RMS コネクタ用のサーバー構成ツールでは追加されません。

    これらのレジストリの編集を行うときは、次の手順を使用します。

    -   *connector FQDN* は、DNS で定義したコネクタの名前に置き換えます。 たとえば、**rmsconnector.contoso.com** です。

    -   オンプレミス サーバーとの通信に HTTP または HTTPS のどちらを使用するようにコネクタを構成しているかにより、コネクタの URL に HTTP または HTTPS プレフィックスを使用してください。

#### <a name="registry-edits-for-exchange"></a>Exchange に関するレジストリの編集

すべての Exchange サーバーの LicenseServerRedirection に、Exchange のバージョンに応じて次のレジストリ値を追加します。

---

Exchange 2013 および Exchange 2016 の場合 - レジストリ編集 1:


**レジストリパス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https:// \<AD RMS Intranet Licensing URL\> /_wmcs/ライセンス

**データ**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://\<connector FQDN\>/_wmcs/licensing

- https://\<connector FQDN\>/_wmcs/licensing


---

Exchange 2013 - レジストリの編集 2:

**レジストリパス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 

**種類:** Reg_SZ

**値:** https:// \<AD RMS Extranet Licensing URL\> /_wmcs/ライセンス

**データ**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://\<connector FQDN\>/_wmcs/licensing

- https://\<connector FQDN\>/_wmcs/licensing

---

Exchange 2010 の場合 - レジストリの編集 1:


**レジストリパス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https:// \<AD RMS Intranet Licensing URL\> /_wmcs/ライセンス

**データ**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://\<connector FQDN\>/_wmcs/licensing

- https://\<connector Name\>/_wmcs/licensing


---

Exchange 2010 の場合 - レジストリの編集 2:


**レジストリパス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https:// \<AD RMS Extranet Licensing URL\> /_wmcs/ライセンス

**データ**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://\<connector FQDN\>/_wmcs/licensing

- https://\<connector FQDN\>/_wmcs/licensing

---


## <a name="next-steps"></a>次のステップ
移行を続行するには、「[移行フェーズ 5 - 移行後のタスク](migrate-from-ad-rms-phase5.md)」に進んでください。
