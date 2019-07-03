---
title: Rights Management コネクタのレジストリ設定 - AIP
description: RMS コネクタを使用するサーバーでのレジストリ設定に関する情報です。 これらの設定を構成する場合は、Microsoft RMS コネクタ用のサーバー構成ツールを使用することをお勧めします。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e9bb701dcf48aaa514cdf71a6dc6c10c671f618c
ms.sourcegitcommit: a2542aec8cd2bf96e94923740bf396badff36b6a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2019
ms.locfileid: "67535053"
---
# <a name="registry-setting-for-the-rights-management-connector"></a>Rights Management コネクタのレジストリ設定

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*


次のセクションの表は、Exchange、SharePoint、または Windows Server を実行しているサーバーのレジストリ設定を手動で追加または確認する場合にのみ使用してください。 このレジストリ設定により、[RMS コネクタ](deploy-rms-connector.md)を使用するようにサーバーが構成されます。 これらのサーバーを構成する場合は、Microsoft RMS コネクタ用のサーバー構成ツールを使用することをお勧めします。

これらの設定を使用する場合の手順:

-   *\<YourTenantURL>* は Azure Information Protection テナントの Azure Rights Management サービス URL です。 この値を見つけるには、次の操作を実行します。

    1.  実行、 [Get AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) Azure Rights Management サービスのコマンドレット。 既に AIPService モジュールをインストールしていない場合は、次を参照してください。 [AIPService PowerShell モジュールをインストールする](install-powershell.md)します。

    2.  出力から、 **LicensingIntranetDistributionPointUrl** の値を確認します。

        以下に例を示します。**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  この値から、 **/_wmcs/licensing** 文字列を削除します。 残りの文字列が Azure Rights Management サービス URL です。 この例では、Azure Rights Management サービス URL は次の値になります。

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**
        
        次の PowerShell コマンドを実行することで、値が正しいことを確認できます。
        
            (Get-AipServiceConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

-   *\<ConnectorFQDN>* は、DNS で定義したコネクタの負荷分散名です。 たとえば、 **rmsconnector.contoso.com**です。

-   オンプレミス サーバーとの通信に HTTPS を使用するようにコネクタを構成している場合は、コネクタの URL に HTTPS プレフィックスを使用してください。 詳細については、「[HTTPS を使用するための RMS コネクタの構成](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)」セクションを参照してください。 Azure Rights Management サービス URL では常に HTTPS が使用されます。


## <a name="exchange-2016-or-exchange-2013-registry-settings"></a>Exchange 2016 または Exchange 2013 のレジストリ設定

**レジストリ パス:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**種類:** Reg_SZ

**値:** 既定

**データ:** https:// *\<YourTenantURL>* /_wmcs/certification

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**種類:** Reg_SZ

**値:** 既定

**データ:** https:// *\<YourTenantURL>* /_wmcs/Licensing

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**種類:** Reg_SZ

**値:** https:// *\<YourTenantURL>*


**データ:** Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http:// *<\ConnectorFQDN>*

- https:// *<\ConnectorFQDN>*

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https:// *<\YourTenantURL>*


**データ:** Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http:// *<\ConnectorFQDN>*

- https:// *<\ConnectorFQDN>*


## <a name="exchange-2010-registry-settings"></a>Exchange 2010 のレジストリ設定

**レジストリ パス:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**種類:** Reg_SZ

**値:** 既定

**データ:** https:// *<\YourTenantURL>* /_wmcs/certification

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**種類:** Reg_SZ

**値:** 既定

**データ:** https:// *<\YourTenantURL>* /_wmcs/Licensing

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**種類:** Reg_SZ

**値:** https:// *<\YourTenantURL>*

**データ:** Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http:// *<\ConnectorFQDN>*

- https:// *<\ConnectorFQDN>*

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https:// *<\YourTenantURL>*

**データ:** Exchange サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http:// *<\ConnectorFQDN>*

- https:// *<\ConnectorFQDN>*


## <a name="sharepoint-2016-or-sharepoint-2013-registry-settings"></a>SharePoint 2016 または SharePoint 2013 のレジストリ設定

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**種類:** Reg_SZ

**値:** https:// *<\YourTenantURL>* /_wmcs/licensing


**データ:** SharePoint サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http:// *<\ConnectorFQDN>* /_wmcs/licensing

- https:// *<\ConnectorFQDN>* /_wmcs/licensing

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**種類:** Reg_SZ

**値:** 既定

**データ:** SharePoint サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http:// *<\ConnectorFQDN>* /_wmcs/certification

- https:// *<\ConnectorFQDN>* /_wmcs/certification

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**種類:** Reg_SZ

**値:** 既定


**データ:** SharePoint サーバーから RMS コネクタへの通信で HTTP または HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http:// *<\ConnectorFQDN>* /_wmcs/licensing

- https:// *<\ConnectorFQDN>* /_wmcs/licensing




## <a name="file-server-and-file-classification-infrastructure-registry-settings"></a>ファイル サーバーとファイル分類インフラストラクチャのレジストリ設定

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**種類:** Reg_SZ

**値:** 既定

**データ:** http:// *<\ConnectorFQDN>* /_wmcs/licensing

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**種類:** Reg_SZ

**値:** 既定

**データ:** http:// *<\ConnectorFQDN>* /_wmcs/certification


「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」に戻ります。
