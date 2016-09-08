---
title: "Azure Rights Management の要件 | Azure RMS"
description: "組織に Microsoft Azure Rights Management (Azure RMS) をデプロイするには、以下の要件を満たしていることを確認してください。 Azure Rights Management のデプロイのロードマップを使用して、組織の Rights Management をデプロイできます。"
author: cabailey
manager: mbaldwin
ms.date: 07/15/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c7b194493073bcd76fa7a7d06bb31a7811e8cc3e
ms.openlocfilehash: d56eb077ef76e1869c7d90141f1b35c1bdbfe9fa


---

# Azure Rights Management の要件

>*適用対象: Azure Rights Management、Office 365*


組織に Microsoft Azure Rights Management (Azure RMS) をデプロイするには、以下の要件を満たしていることを確認してください。 [Azure Rights Management のデプロイのロードマップ](../plan-design/deployment-roadmap.md)を使用して、組織の Rights Management をデプロイできます。

|要件|説明|
|---------------|--------------------|
|RMS のクラウド サブスクリプション|RMS をサポートするクラウド サブスクリプションが組織で必要です。<br /><br />ライセンス情報については、「[Cloud subscriptions that support Azure RMS (Azure RMS をサポートするクラウド サブスクリプション)](requirements-subscriptions.md)」を参照してください。|
|Azure AD ディレクトリ|RMS のユーザー認証をサポートするために組織で Azure AD ディレクトリが必要です。 また、オンプレミスのディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。<br /><br />必要なクライアント ソフトウェアと正しく構成された MFA サポート インフラストラクチャがある場合は、Azure RMS で Multi-Factor Authentication (MFA) がサポートされます。<br /><br />詳細については、「[Azure AD ディレクトリ](requirements-azure-ad.md)」を参照してください。|
|クライアント デバイス|ユーザーは RMS をサポートするオペレーティング システムを実行するクライアント デバイス (コンピューターまたはモバイル デバイス) を持っている必要があります。<br /><br />詳細については、「[Azure RMS をサポートするクライアント デバイス](requirements-client-devices.md)」を参照してください。|
|アプリケーション|ユーザーは、RMS をサポートするアプリケーションを実行する必要があります。<br /><br />詳細については、[Azure RMS をサポートするアプリケーション](requirements-applications.md)に関するセクションを参照してください。|
|インターネットと依存クラウド サービスへの接続をサポートするインフラストラクチャ|特定の接続を許可するように構成する必要があるファイアウォールまたは同様の介在するネットワーク デバイスがある場合は、Office 記事「[Office 365 URL および IP アドレス範囲](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」の「[Office 365 ポータルと共有](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)」セクションで **Azure Rights Management (RMS)** に関する情報を参照してください。<br /><br />RSS フィードを購読して最新の情報を入手するには、この Office 記事の手順を使用してください。<br /><br />Office の記事の情報に加えて、Azure RMS に固有の要件は以下のとおりです。<br /><br />- TLS クライアント/サービス間接続を終了しないでください (たとえばパケット レベルの検査を行うために)。 終了すると、Azure RMS との通信を保護するのに RMS クライアントが Microsoft が管理する CA と使用する証明書のピン留めが解除されます。<br /><br />- 認証が必要な Web プロキシを使用している場合には、ユーザーの Active Directory ログオン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。|

オンプレミス サーバーで Azure RMS を使用する場合は、以下の製品がサポートされます。

-   Exchange Server

-   SharePoint Server

-   ファイル分類インフラストラクチャをサポートする Windows Server ファイル サーバー

このシナリオに関する追加の Azure RMS 要件については、「[Azure Rights Management をサポートするオンプレミス サーバー](requirements-servers.md)」を参照してください。

> [!IMPORTANT]
> 次のデプロイ シナリオはサポートされていません。
> 
> -   同一組織での AD RMS および Azure RMS の並列実行 (移行時を除く。詳細については、「[AD RMS から Azure Rights Management への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照)。
> 
> 移行パスは、[AD RMS から Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) および [Azure RMS から AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx) の 2 つがサポートされています。 Azure RMS をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Rights Management の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」を参照してください。






<!--HONumber=Aug16_HO4-->


