---
title: "オンプレミス サーバーでのデータ保護のサポート | Azure Information Protection"
description: "Rights Management コネクタを使用して、Azure Information Protection から Azure Rights Management サービスを使用できるオンプレミス サーバー製品を特定します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: e4bf159cea6298e5a5577a2fa4de3dd3beeb47d9


---


# <a name="onpremises-servers-that-support-azure-rights-management-data-protection"></a>Azure Rights Management データ保護をサポートするオンプレミス サーバー

>*適用対象: Azure Information Protection、Office 365*

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

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Windows Server 2008 R2 を実行するファイル サーバーには、Rights Management の保護を適用する組み込みのファイル管理タスク アクションがないため、このシナリオには Rights Management コネクタを使用できません。 ただし、Azure RMS を使用してファイルを保護できる実行可能ファイルまたはスクリプトを実行するカスタムのファイル管理タスクを構成する場合、これらのオペレーティング システムでファイル分類インフラストラクチャと Azure RMS を使用できます。 たとえば、[RMS Protection コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)を使用する Windows PowerShell スクリプトなどがあります。
    > 
    > 最新の Windows Server を実行しているサーバーでこれらのコマンドレットを使うこともできます。この場合、すべてのファイル タイプが保護されるという利点があります。 RMS コネクタでは Office ファイルのみ保護されます。 操作手順については、「[Windows Server ファイル分類インフラストラクチャ &#40;FCI&#41; での RMS の保護](../rms-client/configure-fci.md)」を参照してください。

Rights Management コネクタは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 でサポートされています。

これらのオンプレミス サーバーで Rights Management コネクタを構成する方法の詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」をご覧ください。

## <a name="next-steps"></a>次のステップ
その他の要件を確認するには、「[Azure Rights Management の要件](requirements-azure-rms.md)」を参照してください。



<!--HONumber=Nov16_HO2-->


