---
title: "Rights Management コネクタのレジストリ設定 - AIP"
description: "RMS コネクタを使用するサーバーでのレジストリ設定に関する情報です。 これらの設定を構成する場合は、Microsoft RMS コネクタ用のサーバー構成ツールを使用することをお勧めします。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b894be1ef3d41a9faf6c3fd3b3fd8c5b94a62517
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="registry-setting-for-the-rights-management-connector"></a>Rights Management コネクタのレジストリ設定

>*適用対象: Azure Information Protection、Office 365*


次のセクションの表は、Exchange、SharePoint、または Windows Server を実行しているサーバー上で、[RMS コネクタ](deploy-rms-connector.md)を使用するようにサーバーを構成するレジストリ設定を手動で追加または確認する場合にのみ使用してください。 これらのサーバーを構成する場合は、Microsoft RMS コネクタ用のサーバー構成ツールを使用することをお勧めします。

これらの設定を使用する場合の手順:

-   *MicrosoftRMSURL* は、組織の Microsoft RMS サービスの URL です。 この値を見つけるには、次の操作を実行します。

    1.  Azure RMS 用の [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) コマンドレットを実行します。 Azure RMS 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。

    2.  出力から、 **LicensingIntranetDistributionPointUrl** の値を確認します。

        例: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  この値から、**/_wmcs/licensing** 文字列を削除します。 残りの文字列が Microsoft RMS の URL です。 この例では、Microsoft RMS の URL は次の値になります。

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

-   *ConnectorFQDN* は、DNS で定義したコネクタの負荷分散名です。 たとえば、 **rmsconnector.contoso.com**です。

-   オンプレミス サーバーとの通信に HTTPS を使用するようにコネクタを構成している場合は、コネクタの URL に HTTPS プレフィックスを使用してください。 詳細については、「[HTTPS を使用するための RMS コネクタの構成](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)」セクションを参照してください。 Microsoft RMS の URL では常に HTTPS が使用されます。


## <a name="exchange-2016-or-exchange-2013-registry-settings"></a>Exchange 2016 または Exchange 2013 のレジストリ設定

**レジストリ パス:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**種類:** Reg_SZ

**値:** 既定

**データ:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**種類:** Reg_SZ

**値:** 既定

**データ:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**種類:** Reg_SZ

**値:** https://*MicrosoftRMSURL*


**データ:** Exchange サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https://*MicrosoftRMSURL*


**データ:** Exchange サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## <a name="exchange-2010-registry-settings"></a>Exchange 2010 のレジストリ設定

**レジストリ パス:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**種類:** Reg_SZ

**値:** 既定

**データ:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**種類:** Reg_SZ

**値:** 既定

**データ:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**種類:** Reg_SZ

**値:** https://*MicrosoftRMSURL*

**データ:** Exchange サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**種類:** Reg_SZ

**値:** https://*MicrosoftRMSURL*

**データ:** Exchange サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## <a name="sharepoint-2016-or-sharepoint-2013-registry-settings"></a>SharePoint 2016 または SharePoint 2013 のレジストリ設定

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**種類:** Reg_SZ

**値:** https://*MicrosoftRMSURL*/_wmcs/licensing


**データ:** SharePoint サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**種類:** Reg_SZ

**値:** 既定

**データ:** SharePoint サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://*ConnectorFQDN*/_wmcs/certification

- https://*ConnectorFQDN*/_wmcs/certification

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**種類:** Reg_SZ

**値:** 既定


**データ:** SharePoint サーバーから RMS コネクタへの通信で HTTP と HTTPS のどちらを使用しているかによって、次のいずれかの形式を使用します。

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing




## <a name="file-server-and-file-classification-infrastructure-registry-settings"></a>ファイル サーバーとファイル分類インフラストラクチャのレジストリ設定

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**種類:** Reg_SZ

**値:** 既定

**データ:** http://*ConnectorFQDN*/_wmcs/licensing

---

**レジストリ パス:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**種類:** Reg_SZ

**値:** 既定

**データ:** http://*ConnectorFQDN*/_wmcs/certification


「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」に戻ります。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]