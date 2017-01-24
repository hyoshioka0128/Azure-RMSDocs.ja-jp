---
title: "AD RMS から Azure Information Protection に移行する - フェーズ 3 | Azure Information Protection"
description: "AD RMS から Azure Information Protection への移行のフェーズ 3 には、手順 6 ～ 7 が含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 0ad1df8a8343052a85f85b94e0413fe0a0265d4b


---

# <a name="migration-phase-3---supporting-services-configuration"></a>移行フェーズ 3 - サービス構成のサポート

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*


AD RMS から Azure Information Protection への移行フェーズ 3 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 6 から手順 7 を説明します。


## <a name="step-6-configure-irm-integration-for-exchange-online"></a>手順 6. IRM と Exchange Online の統合を構成する

事前に AD RMS から Exchange Online に TDP をインポートしていた場合、この TDP を削除して、Azure Information Protection に移行した後にテンプレートおよびポリシーが競合しないようにする必要があります。 これを行うには、Exchange Online から [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) コマンドレットを使用します。

**マイクロソフト管理の** Azure Information Protection テナント キー トポロジを選択した場合:

-   記事「[Office 365: Configuration for clients and online services (Office 365: クライアントとオンライン サービスの構成)](../deploy-use/configure-office365.md)」の「[Exchange Online: IRM configuration (Exchange Online: IRM 構成)](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」セクションを参照してください。 このセクションには、Exchange Online サービスに接続して、Azure Information Protection からテナント キーをインポートし、Exchange Online の IRM 機能を有効にするために実行する、一般的なコマンドが含まれています。 次の手順を完了した後は、Exchange Online で Azure Rights Management 保護のすべての機能を使用できます。

**顧客管理 (BYOK)** の Azure Information Protection テナント キー トポロジを選択した場合:

-   「[BYOK の料金と制限事項](byok-price-restrictions.md)」の説明のとおり、Exchange Online では Rights Management 保護の機能を制限付きで使用できます。

## <a name="step-7-deploy-the-rms-connector"></a>手順 7. RMS コネクタをデプロイする
AD RMS で Exchange サーバーまたは SharePoint サーバーの Information Rights Management (IRM) 機能を使用していた場合、最初にこれらのサーバーで IRM を無効にし、AD RMS の構成を削除する必要があります。 次に、Rights Management (RMS) コネクタをデプロイします。これは、オンプレミス サーバーと Azure Information Protection の保護サービスの間の通信インターフェイス (リレー) として機能します。

最後にこの手順では、電子メール メッセージを保護するために使用されていた複数の AD RMS データ構成ファイル (.xml) を Azure Information Protection にインポートした場合、Exchange Server コンピューター上のレジストリを手動で編集して、RMS コネクタにすべての信頼された発行ドメインの URL をリダイレクトする必要があります。

> [!NOTE]
> 開始する前に、「[Azure RMS をサポートするオンプレミス サーバー](../get-started/requirements-servers.md)」で、Azure Rights Management サービスがサポートしているオンプレミス サーバーのバージョンを確認してください。

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Exchange サーバーで IRM を無効にし、AD RMS の構成を削除する

1.  各 Exchange サーバーで次のフォルダーを見つけて、そのフォルダーのすべてのエントリを削除します。\ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  いずれかの Exchange サーバーから、最初に Exchange [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) コマンドレットを使用して、内部受信者に送信されるメッセージの IRM 機能を無効にします。

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  次に、同じコマンドレットを使用して、外部受信者に送信されるメッセージの IRM 機能を無効にします。

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  次に、同じコマンドレットを使用して、Microsoft Office Outlook Web App および Microsoft Exchange ActiveSync で IRM を無効にします。

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

5.  各 SharePoint サーバー コンピューターで、\ProgramData\Microsoft\MSIPC\Server\*&lt;SharePoint サーバーを実行しているアカウントの SID&gt;* フォルダーの内容を削除します。

#### <a name="install-and-configure-the-rms-connector"></a>RMS コネクタのインストールと構成

-   記事「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」の説明に従います。

#### <a name="for-exchange-only-and-multiple-tpds-edit-the-registry"></a>Exchange のみで複数の TPD の場合:レジストリを編集します。

-   各 Exchange サーバーで、インポートした追加の構成データファイル (.xml) ごとに次のレジストリ キーを手動で追加し、信頼された発行ドメインの URL を RMS コネクタにリダイレクトします。 これらのレジストリ エントリは移行に固有であり、Microsoft RMS コネクタ用のサーバー構成ツールでは追加されません。

    これらのレジストリの編集を行うときは、次の手順を使用します。

    -   *ConnectorFQDN* は、DNS で定義したコネクタの名前に置き換えます。 たとえば、 **rmsconnector.contoso.com**です。

    -   オンプレミス サーバーとの通信に HTTP または HTTPS のどちらを使用するようにコネクタを構成しているかにより、コネクタの URL に HTTP または HTTPS プレフィックスを使用してください。

Exchange 2013 の場合 - レジストリの編集 1:


**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**次のように入力します。**

Reg_SZ

**値:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Exchange 2013 の場合 - レジストリの編集 2:

**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**次のように入力します。**

Reg_SZ

**値:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Exchange 2010 の場合 - レジストリの編集 1:



**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**次のように入力します。**

Reg_SZ

**値:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Exchange 2010 の場合 - レジストリの編集 2:


**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**次のように入力します。**

Reg_SZ

**値:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

以上の手順を完了した後、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」の「**次のステップ**」セクションに進むことができます。

## <a name="next-steps"></a>次のステップ
移行を続行するには、「[移行フェーズ 4 - 移行後のタスク](migrate-from-ad-rms-phase4.md)」に進んでください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


