---
title: "AD RMS から Azure Information Protection への移行 - フェーズ 4"
description: "AD RMS から Azure Information Protection への移行のフェーズ 4 には、手順 8 から 9 が含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 51a689248834f2578655d62752c19b7a387068a5
ms.sourcegitcommit: 237ce3a0cc4921da5a08ed5753e6491403298194
translationtype: HT
---
# <a name="migration-phase-4---supporting-services-configuration"></a>移行フェーズ 4 - サービス構成のサポート

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*


AD RMS から Azure Information Protection への移行フェーズ 4 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 8 から手順 9 を説明します。



## <a name="step-8-configure-irm-integration-for-exchange-online"></a>手順 8. IRM と Exchange Online の統合を構成する

事前に AD RMS から Exchange Online に TDP をインポートしていた場合、この TDP を削除して、Azure Information Protection に移行した後にテンプレートおよびポリシーが競合しないようにする必要があります。 これを行うには、Exchange Online から [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) コマンドレットを使用します。

**マイクロソフト管理の** Azure Information Protection テナント キー トポロジを選択した場合:

1. 記事「[Office 365: クライアントとオンライン サービスの構成](../deploy-use/configure-office365.md)」の「[Exchange Online: IRM 構成](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」セクションの手順を参照してください。 このセクションには、Exchange Online サービスに接続して、Azure Information Protection からテナント キーをインポートし、Exchange Online の IRM 機能を有効にするために実行する、一般的なコマンドが含まれています。 次の手順を完了した後は、Exchange Online で Azure Rights Management 保護のすべての機能を使用できます。

2. Exchange Online 用に IRM を有効にする標準の構成に加えて、次の PowerShell コマンドを実行し、AD RMS 保護を使って送信されたメールをユーザーが読めるようにします。

    *\<yourcompany.domain>* を実際の組織のドメイン名に置き換えます。

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation
        $list += "https://adrms.<yourcompany.domain>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list
        Set-IRMConfiguration -internallicensingenabled $false
        Set-IRMConfiguration -internallicensingenabled $true


**顧客管理 (BYOK)** の Azure Information Protection テナント キー トポロジを選択した場合:

-   「[BYOK の料金と制限事項](byok-price-restrictions.md)」の説明のとおり、Exchange Online では Rights Management 保護の機能を制限付きで使用できます。


## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>手順 9. Exchange サーバーおよび SharePoint サーバー用に IRM 統合を構成する

AD RMS で Exchange サーバーまたは SharePoint サーバーの Information Rights Management (IRM) 機能を使っている場合は、Rights Management (RMS) コネクタをデプロイする必要があります。このコネクタは、オンプレミスのサーバーと Azure Information Protection の保護サービスの間のインターフェイス (リレー) として機能します。

ここでは、コネクタをインストールして構成し、Exchange および SharePoint で IRM を無効にして、コネクタを使うようにこれらのサーバーを構成する手順を説明します。 最後に、メール メッセージの保護に使われていた AD RMS データ構成ファイル (.xml) を Azure Information Protection にインポートしてある場合、Exchange Server コンピューターのレジストリを手動で編集して、すべての信頼された発行ドメインの URL を RMS コネクタにリダイレクトする必要があります。

> [!NOTE]
> 開始する前に、「[Azure RMS をサポートするオンプレミス サーバー](../get-started/requirements-servers.md)」で、Azure Rights Management サービスがサポートしているオンプレミス サーバーのバージョンを確認してください。

### <a name="install-and-configure-the-rms-connector"></a>RMS コネクタのインストールと構成

記事「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」の説明に従って、手順 1 から 4 を実行します。 コネクタの説明の手順 5 はまだ実行しないでください。 

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Exchange サーバーで IRM を無効にし、AD RMS の構成を削除する

1.  各 Exchange サーバーでフォルダー **\ProgramData\Microsoft\DRM\Server\S-1-5-18** を見つけて、そのフォルダーのすべてのエントリを削除します。

2. Exchange サーバーのいずれかで次の PowerShell コマンドを実行して、Azure Rights Management を使って保護されているメールをユーザーが読めるようにします。

    これらのコマンドを実行する前に、\<*Your Tenant URL*> を実際の Azure Rights Management サービスの URL に置き換えます。

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation 
        $list + "<Your Tenant URL>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list

3.  次に、内部受信者に送信されるメッセージの IRM 機能を無効にします。

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. その後、同じコマンドレットを使って、Microsoft Office Outlook Web App および Microsoft Exchange ActiveSync で IRM を無効にします。

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最後に、同じコマンドレットを使用してキャッシュされている証明書をクリアします。

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  各 Exchange サーバーで、たとえば管理者としてコマンド プロンプトを実行して「**iisreset**」と入力し、IIS をリセットします。

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>SharePoint サーバーで IRM を無効にし、AD RMS の構成を削除する

1.  RMS で保護されたライブラリからドキュメントがチェックアウトされていないことを確認します。 ある場合、この手順の最後でそれらにアクセスできなくなります。

2.  SharePoint サーバーの全体管理 Web サイトの **[サイド リンク バー]** セクションで、 **[セキュリティ]**をクリックします。

3.  **[セキュリティ]** ページの **[情報ポリシー]** セクションで、 **[Information Rights Management の構成]**をクリックします。

4.  **[Information Rights Management]** ページの **[Information Rights Management]** セクションで、 **[このサーバーでは IRM を使用しない]**を選択して、 **[OK]**をクリックします。

5.  各 SharePoint サーバー コンピューターで、\ProgramData\Microsoft\MSIPC\Server\\<*SharePoint サーバーを実行しているアカウントの SID*> フォルダーの内容を削除します。

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>コネクタを使うように Exchange と SharePoint を構成する

1. 「[手順 5: RMS コネクタを使用するためのサーバーの構成](../deploy-use/configure-servers-rms-connector.md)」の RMS コネクタのデプロイ手順に戻ります。

    SharePoint サーバーだけを使っている場合は、[次の手順](#next-steps)に進んで移行を続けます。 

2. 各 Exchange サーバーで、インポートした各構成データファイル (.xml) の次のセクションにレジストリ キーを手動で追加し、信頼された発行ドメインの URL を RMS コネクタにリダイレクトします。 これらのレジストリ エントリは移行に固有であり、Microsoft RMS コネクタ用のサーバー構成ツールでは追加されません。

    これらのレジストリの編集を行うときは、次の手順を使用します。

    -   *connector FQDN* は、DNS で定義したコネクタの名前に置き換えます。 たとえば、 **rmsconnector.contoso.com**です。

    -   オンプレミス サーバーとの通信に HTTP または HTTPS のどちらを使用するようにコネクタを構成しているかにより、コネクタの URL に HTTP または HTTPS プレフィックスを使用してください。

#### <a name="registry-edits-for-exchange"></a>Exchange に関するレジストリの編集

すべての Exchange サーバーで、準備フェーズの間に LicenseServerRedirection に追加したレジストリ値を削除します。 これらの値は、次のパスに追加されました。

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection


Exchange 2013 および Exchange 2016 の場合 - レジストリ編集 1:


**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https://\<AD RMS イントラネット ライセンス URL\>/_wmcs/licensing

**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://\<コネクタの FQDN\>/_wmcs/licensing

- https://\<コネクタの FQDN\>/_wmcs/licensing


---

Exchange 2013 の場合 - レジストリの編集 2:

**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 

**種類:** Reg_SZ

**値:** https://\<AD RMS エクストラネット ライセンス URL\>/_wmcs/licensing

**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://\<コネクタの FQDN\>/_wmcs/licensing

- https://\<コネクタの FQDN\>/_wmcs/licensing

---

Exchange 2010 の場合 - レジストリの編集 1:


**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https://\<AD RMS イントラネット ライセンス URL\>/_wmcs/licensing

**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://\<コネクタの FQDN\>/_wmcs/licensing

- https://\<コネクタの名前\>/_wmcs/licensing


---

Exchange 2010 の場合 - レジストリの編集 2:


**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https://\<AD RMS エクストラネット ライセンス URL\>/_wmcs/licensing

**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://\<コネクタの FQDN\>/_wmcs/licensing

- https://\<コネクタの FQDN\>/_wmcs/licensing

---


## <a name="next-steps"></a>次のステップ
移行を続行するには、「[移行フェーズ 5 - 移行後のタスク](migrate-from-ad-rms-phase5.md)」に進んでください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]