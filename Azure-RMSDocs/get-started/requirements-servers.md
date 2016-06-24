---
# required metadata

title: Azure RMS の要件&#58; Azure Rights Management をサポートするオンプレミス サーバー | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Azure RMS の要件: Azure RMS をサポートするオンプレミス サーバー

*適用対象: Azure Rights Management、Office 365*

Azure RMS コネクタを使用する場合、次のオンプレミス サーバー製品で Azure RMS がサポートされます。このコネクタがオンプレミス サーバーと Azure RMS との通信インターフェイス (リレー) として動作します。 さらに、この構成では Active Directory フォレストと Azure Active Directory とのディレクトリ同期を構成する必要があります。

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Windows Server を実行し、ファイル分類インフラストラクチャ (FCI) を使用するファイル サーバー**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Windows Server 2008 R2 を実行するファイル サーバーには、RMS の保護を適用する組み込みのファイル管理タスク アクションがないため、このシナリオには RMS コネクタを使用できません。 ただし、Azure RMS を使用してファイルを保護できる実行可能ファイルまたはスクリプトを実行するカスタムのファイル管理タスクを構成する場合、これらのオペレーティング システムでファイル分類インフラストラクチャと Azure RMS を使用できます。 たとえば、[RMS Protection コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)を使用する Windows PowerShell スクリプトなどがあります。
    > 
    > 最新の Windows Server を実行しているサーバーでこれらのコマンドレットを使うこともできます。この場合、すべてのファイル タイプが保護されるという利点があります。 RMS コネクタでは Office ファイルのみ保護されます。 操作手順については、「[Windows Server ファイル分類インフラストラクチャ &#40;FCI&#41; での RMS の保護](../rms-client/configure-fci.md)」を参照してください。

RMS コネクタは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 でサポートされています。

これらのオンプレミス サーバーで RMS コネクタを構成する方法の詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。

## 次のステップ
その他の要件を確認するには、「[Azure Rights Management の要件](requirements-azure-rms.md)」を参照してください。


<!--HONumber=May16_HO2-->


