---
title: Azure RMS データ保護に関するサーバー サポート - AIP
description: Rights Management コネクタを使用して、Azure Information Protection から Azure Rights Management サービスを使用できるオンプレミス サーバー製品を特定します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e8ce88ed734177fd35c733f115f157c94b70627d
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117937"
---
# <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするオンプレミス サーバー

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Rights Management コネクタを使用すると、次のオンプレミス サーバー製品は Azure Information Protection でサポートされます。 このコネクタは、Office ドキュメントや電子メールを保護するために、Azure Information Protection によって使用される Azure Rights Management サービスとオンプレミス サーバーの間の通信インターフェイス (リレー) として機能します。 

このコネクタを使用するには、Active Directory フォレストと Azure Active Directory とのディレクトリ同期を構成する必要があります。

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Windows Server を実行し、ファイル分類インフラストラクチャ (FCI) を使用するファイル サーバー**:

    -   Windows Server 2016

    -   Windows Server 2012 R2

    -   Windows Server 2012


    > 
    > 最新の Windows Server を実行しているサーバーでこれらのコマンドレットを使うこともできます。この場合、すべてのファイル タイプが保護されるという利点があります。 RMS コネクタでは Office ファイルのみ保護されます。 操作手順については、「[Windows Server ファイル分類インフラストラクチャ &#40;FCI&#41; での RMS の保護](./rms-client/configure-fci.md)」を参照してください。

Rights Management コネクタは、windows server 2016、Windows Server 2012 R2、Windows Server 2012 でサポートされています。

これらのオンプレミス サーバーで Rights Management コネクタを構成する方法の詳細については、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」をご覧ください。

## <a name="next-steps"></a>次の手順
その他の要件を確認するには、「[Azure Information Protection の要件](requirements.md)」をご覧ください。
