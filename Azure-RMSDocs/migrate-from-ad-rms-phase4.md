---
title: AD RMS から Azure Information Protection への移行 - フェーズ 4
description: AD RMS から Azure Information Protection への移行のフェーズ 4 には、手順 8 から 9 が含まれます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e7431ebdf016b89e1750b833dc4fca2d9646b195
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316723"
---
# <a name="migration-phase-4---supporting-services-configuration"></a>移行フェーズ 4 - サービス構成のサポート

>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


AD RMS から Azure Information Protection への移行フェーズ 4 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 8 から手順 9 を説明します。

## <a name="step-8-configure-irm-integration-for-exchange-online"></a>手順 8.  IRM と Exchange Online の統合を構成する

> [!IMPORTANT]
> 移行したユーザーが保護された電子メールに対して選択できる受信者を制御することはできません。
>
> そのため、組織内のすべてのユーザーとメールが有効なグループに、Azure Information Protection で使用できる Azure AD のアカウントがあることを確認してください。
>
> 詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

選択した Azure Information Protection のテナントキートポロジに関係なく、次の操作を行います。

1. **前提条件**: Exchange Online が AD RMS によって保護されている電子メールの暗号化を解除できるようにするには、クラスターの AD RMS URL がテナントで使用可能なキーに対応していることを確認する必要があります。 

    これは、AD RMS クラスターの DNS SRV レコードを使用して実行されます。これは、Azure Information Protection を使用する Office クライアントを再構成するためにも使用されます。 

    [手順 7](migrate-from-ad-rms-phase3.md#step-7-reconfigure-windows-computers-to-use-azure-information-protection). でクライアントの再構成用の DNS SRV レコードを作成しなかった場合は、このレコードを今すぐ作成して Exchange Online をサポートします。 [手順](migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection)
    
    この DNS レコードが配置されると、Web とモバイルの電子メール クライアントに Outlook を使用しているユーザーはそのアプリで AD RMS によって保護された電子メールを表示できるようになります。また、Exchange では AD RMS からインポートしたキーを使用して、AD RMS によって保護されたコンテンツを暗号化解除、インデックス化、保管、保護できるようになります。  

1. **Exchange Online の [Get IRMConfiguration](/powershell/module/exchange/get-irmconfiguration) コマンドを実行します。** 

    このコマンドの実行でヘルプが必要な場合は、「[Exchange Online: IRM Configuration](configure-office365.md#exchangeonline-irm-configuration)」(Exchange Online: IRM 構成) の詳しい手順を参照してください。
    
    出力で、**AzureRMSLicensingEnabled** が **True** に設定されているかどうかを確認します。
    
    - **AzureRMSLicensingEnabled** が **True** に設定されている場合、この手順に対してこれ以上の構成は必要ありません。 
    
    - **AzureRMSLicensingEnabled** が **False** に設定されている場合は、を実行 `Set-IRMConfiguration -AzureRMSLicensingEnabled $true` し、Exchange Online で Azure Rights Management サービスを使用する準備ができていることを確認します。 
    
        詳細については、「 [Azure Information Protection の上に構築された新しい Microsoft 365 メッセージの暗号化機能のセットアップ](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)」の検証手順を参照してください。

## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>手順 9. Exchange サーバーおよび SharePoint サーバー用に IRM 統合を構成する

AD RMS で Exchange Server または SharePoint Server の Information Rights Management (IRM) 機能を使用している場合は、Rights Management (RMS) コネクタを展開する必要があります。

コネクタは、オンプレミスサーバーと Azure Information Protection の保護サービスの間の通信インターフェイス (リレー) として機能します。

ここでは、コネクタをインストールして構成し、Exchange および SharePoint で IRM を無効にして、コネクタを使うようにこれらのサーバーを構成する手順を説明します。 

最後に、の電子メールメッセージを保護するために使用された AD RMS .xml データ構成ファイルを Azure Information Protection にインポートした場合は、Exchange Server コンピューター上のレジストリを手動で編集して、すべての信頼された発行ドメインの Url を RMS コネクタにリダイレクトする必要があります。

> [!NOTE]
> 開始する前に、「[Azure RMS をサポートするオンプレミス サーバー](requirements.md#supported-on-premises-servers-for-azure-rights-management-data-protection)」で、Azure Rights Management サービスがサポートしているオンプレミス サーバーのバージョンを確認してください。

### <a name="install-and-configure-the-rms-connector"></a>RMS コネクタのインストールと構成

[Azure Rights Management コネクタのデプロイ](./deploy-rms-connector.md)に関する記事に記載されている手順を使用し、手順 1. ~ 4. を実行します。 

コネクタの説明の手順 5 はまだ実行しないでください。

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Exchange サーバーで IRM を無効にし、AD RMS の構成を削除する

> [!IMPORTANT]
> どの Exchange サーバーでも IRM をまだ構成していない場合は、手順 2. と 6. を実行します。
> 
> *LicensingLocation* パラメーターにすべての AD RMS クラスターのライセンス url が表示されない場合は、これらの手順を [すべて実行します。](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration)

1. 各 Exchange サーバーで、次のフォルダーを見つけて、そのフォルダー内のすべてのエントリを削除します。 **\programdata\microsoft\drm\server\s-1-5-18**

2. Exchange サーバーのいずれかで次の PowerShell コマンドを実行して、Azure Rights Management を使って保護されているメールをユーザーが読めるようにします。

    これらのコマンドを実行する前に、独自の Azure Rights Management サービスの URL に置き換えて *\<Your Tenant URL>* ください。

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation 
    $list += "<Your Tenant URL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    ```

    これで、 [Get IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration)を実行すると、すべての AD RMS クラスターのライセンス url と、 *LicensingLocation* パラメーターに表示される AZURE Rights Management サービスの url が表示されます。

3.  次に、内部受信者に送信されるメッセージの IRM 機能を無効にします。

    ```PowerShell
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. その後、同じコマンドレットを使って、Microsoft Office Outlook Web App および Microsoft Exchange ActiveSync で IRM を無効にします。

    ```PowerShell
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最後に、同じコマンドレットを使用してキャッシュされている証明書をクリアします。

    ```PowerShell
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  各 Exchange サーバーで、たとえば管理者としてコマンド プロンプトを実行して「**iisreset**」と入力し、IIS をリセットします。

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>SharePoint サーバーで IRM を無効にし、AD RMS の構成を削除する

1.  RMS で保護されたライブラリからドキュメントがチェックアウトされていないことを確認します。 ある場合、この手順の最後でそれらにアクセスできなくなります。

2.  SharePoint サーバーの全体管理 Web サイトの **[サイド リンク バー]** セクションで、**[セキュリティ]** をクリックします。

3.  **[セキュリティ]** ページの **[情報ポリシー]** セクションで、**[Information Rights Management の構成]** をクリックします。

4.  **[Information Rights Management]** ページの **[Information Rights Management]** セクションで、**[このサーバーでは IRM を使用しない]** を選択して、**[OK]** をクリックします。

5.  各 sharepoint サーバーコンピューターで、 \\ < *sharepoint server>を実行しているアカウントの \ProgramData\Microsoft\MSIPC\Server SID* フォルダーの内容を削除します。

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>コネクタを使うように Exchange と SharePoint を構成する

1. 「[手順 5: RMS コネクタを使用するためのサーバーの構成](./configure-servers-rms-connector.md)」の RMS コネクタのデプロイ手順に戻ります。

    SharePoint サーバーだけを使っている場合は、[次の手順](#next-steps)に進んで移行を続けます。 

2. 各 Exchange サーバーで、インポートした各構成データファイル (.xml) の次のセクションにレジストリ キーを手動で追加し、信頼された発行ドメインの URL を RMS コネクタにリダイレクトします。 これらのレジストリ エントリは移行に固有であり、Microsoft RMS コネクタ用のサーバー構成ツールでは追加されません。

    これらのレジストリの編集を行うときは、次の手順を使用します。

    -   *connector FQDN* は、DNS で定義したコネクタの名前に置き換えます。 たとえば、**rmsconnector.contoso.com** です。

    -   オンプレミス サーバーとの通信に HTTP または HTTPS のどちらを使用するようにコネクタを構成しているかにより、コネクタの URL に HTTP または HTTPS プレフィックスを使用してください。

#### <a name="registry-edits-for-exchange"></a>Exchange に関するレジストリの編集

すべての Exchange サーバーの LicenseServerRedirection に、Exchange のバージョンに応じて次のレジストリ値を追加します。

1. **Exchange 2013 と exchange 2016** の両方について、次のレジストリ値を追加します。

    - **レジストリパス:**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection`

    - **種類:** Reg_SZ

    - **値:** `https://\<AD RMS Intranet Licensing URL\>/_wmcs/licensing`

    - **データ:** Exchange サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

        - `http://\<connector FQDN\>/_wmcs/licensing`
        
        - `https://\<connector FQDN\>/_wmcs/licensing`

1. Exchange 2013 の場合は、次のレジストリ値を追加します。

    - **レジストリパス:**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection` 

    - **種類:** Reg_SZ

    - **値:** https:// \<AD RMS Extranet Licensing URL\> /_wmcs/ライセンス

    - **データ:** Exchange サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

        - `http://\<connector FQDN\>/_wmcs/licensing`

        - `https://\<connector FQDN\>/_wmcs/licensing`

## <a name="next-steps"></a>次のステップ
移行を続行するには、「[移行フェーズ 5 - 移行後のタスク](migrate-from-ad-rms-phase5.md)」に進んでください。