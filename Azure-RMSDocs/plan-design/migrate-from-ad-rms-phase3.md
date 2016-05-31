---
# required metadata

title: AD RMS から Azure Rights Management への移行 - フェーズ 3 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 移行フェーズ 3 - サービス構成のサポート

*適用対象: Active Directory Rights Management サービス、Azure Rights Management*


AD RMS から Azure Rights Management (Azure RMS) への移行フェーズ 3 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Rights Management への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 6. から手順 7. を説明します。.


## 手順 6.  IRM と Exchange Online の統合を構成する

事前に AD RMS から Exchange Online に TDP をインポートしていた場合、この TDP を削除して、Azure RMS に移行した後にテンプレートおよびポリシーが競合しないようにする必要があります。 これを行うには、Exchange Online から [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) コマンドレットを使用します。

**マイクロソフト管理の**Azure RMS テナント キー トポロジを選択した場合:

-   記事「[Office 365: Configuration for clients and online services (Office 365: クライアントとオンライン サービスの構成)](../deploy-use/configure-office365.md)」の「[Exchange Online: IRM configuration (Exchange Online: IRM 構成)](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」セクションを参照してください。 このセクションには、Exchange Online サービスに接続して、Azure RMS からテナント キーをインポートし、Exchange Online の IRM 機能を有効にするために実行する、一般的なコマンドが含まれています。 次の手順を完了した後は、Exchange Online で RMS のすべての機能を使用できます。

**顧客管理 (BYOK)** の Azure RMS テナント キー トポロジを選択した場合:

-   「[BYOK の料金と制限事項](byok-price-restrictions.md)」の説明のとおり、Exchange Online では RMS の機能を制限付きで使用できます。

## 手順 7. RMS コネクタをデプロイする
AD RMS で Exchange サーバーまたは SharePoint サーバーの Information Rights Management (IRM) 機能を使用していた場合、最初にこれらのサーバーで IRM を無効にし、AD RMS の構成を削除する必要があります。 次に、Rights Management (RMS) コネクタをデプロイします。これは、オンプレミス サーバーと Azure RMS の間の通信インターフェイス (リレー) として機能します。

最後にこの手順では、電子メール メッセージを保護するために使用されていた複数の TPD を Azure RMS にインポートした場合、Exchange Server コンピューター上のレジストリを手動で編集して、RMS コネクタにすべての TPD URL をリダイレクトする必要があります。

> [!NOTE]
> 開始する前に、「[Azure RMS をサポートするオンプレミス サーバー](../get-started/requirements-servers.md)」で、Azure RMS をサポートするオンプレミス サーバーのバージョンを確認してください。.

### Exchange サーバーで IRM を無効にし、AD RMS の構成を削除する

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

6.  各 Exchange サーバーで、管理者としてコマンド プロンプトを実行して **iisreset** と入力し、IIS をリセットします。.

### SharePoint サーバーで IRM を無効にし、AD RMS の構成を削除する

1.  RMS で保護されたライブラリからドキュメントがチェックアウトされていないことを確認します。 ある場合、この手順の最後でそれらにアクセスできなくなります。

2.  SharePoint サーバーの全体管理 Web サイトの **[サイド リンク バー]** セクションで、**[セキュリティ]** をクリックします。.

3.  **[セキュリティ]** ページの **[情報ポリシー]** セクションで、**[Information Rights Management の構成]** をクリックします。.

4.  **[Information Rights Management]** ページの **[Information Rights Management]** セクションで、**[このサーバーでは IRM を使用しない]** を選択して、**[OK]** をクリックします。.

5.  各 SharePoint サーバー コンピューターで、SharePoint サーバーを実行するアカウントの \ProgramData\Microsoft\MSIPC\Server\*&lt;SID フォルダーの内容を削除します。&gt;*.

#### RMS コネクタのインストールと構成

-   記事「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」の説明に従います。

#### Exchange のみで複数の TPD の場合:レジストリを編集します。

-   各 Exchange サーバーで、インポートした各追加 TPD に対して次のレジストリ キーを手動で追加し、TPD の URL を RMS コネクタにリダイレクトします。 これらのレジストリ エントリは移行に固有であり、Microsoft RMS コネクタ用のサーバー構成ツールでは追加されません。

    これらのレジストリの編集を行うときは、次の手順を使用します。

    -   *ConnectorFQDN* は、DNS で定義したコネクタの名前に置き換えます。 たとえば、**rmsconnector.contoso.com** です。.

    -   オンプレミス サーバーとの通信に HTTP または HTTPS のどちらを使用するようにコネクタを構成しているかにより、コネクタの URL に HTTP または HTTPS プレフィックスを使用してください。

Exchange 2013 の場合 - レジストリの編集 1:


**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**次のように入力します。**

Reg_SZ

**Value:**

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

**Value:**

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

**Value:**

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

**Value:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**データ:**

Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

以上の手順を完了した後、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」の「**次のステップ**」セクションに進むことができます。

## 次のステップ
移行を続行するには、「[移行フェーズ 4 - 移行後のタスク](migrate-from-ad-rms-phase4.md)」に進んでください。.

<!--HONumber=Apr16_HO4-->


