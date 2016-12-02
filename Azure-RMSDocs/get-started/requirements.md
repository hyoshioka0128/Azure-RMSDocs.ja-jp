---
title: "Azure Information Protection の要件 | Azure Information Protection"
description: "組織の Azure Information Protection をデプロイするための前提条件を特定します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/01/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 25d60ee3f6debf8e28c039862e6a9b1f544d92ce
ms.openlocfilehash: dfadaa6941aa967511f19fd56ff90c78c62184a5


---

# <a name="requirements-for-azure-information-protection"></a>Azure Information Protection の要件

>*適用対象: Azure Information Protection、Office 365*

組織の Azure Information Protection をデプロイする前に、次の前提条件が満たされていることを確認します。 

|要件|詳細情報|
|---------------|--------------------|
|Azure Information Protection のサブスクリプション|Azure Information Protection サイトの[サブスクリプション情報](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)および[機能一覧](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)を見て、使用する Azure Information Protection 機能を含むサブスクリプションを組織が所有していることを確認します。|
|Azure Active Directory|組織には Azure Information Protection のユーザー認証をサポートするための Azure Active Directory (Azure AD) が必要です。 また、オンプレミスのディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。<br /><br />必要なクライアント ソフトウェアと正しく構成された MFA サポート インフラストラクチャがある場合は、Azure Information Protection で多要素認証 (MFA) がサポートされます。<br /><br />詳細については、「[Azure Information Protection の Azure Active Directory の要件](requirements-azure-ad.md)」をご覧ください。|
|クライアント デバイス|ユーザーは Azure Information Protection をサポートするオペレーティング システムを実行するクライアント デバイス (コンピューターまたはモバイル デバイス) を所有している必要があります。<br /><br />次のデバイスでは、Azure Information Protection クライアントをサポートします。これにより、ユーザーは次の Office のドキュメントや電子メールの分類およびラベル付けを行うことができます。<br /><br />- Windows 10 (x86、x64)<br /><br />- Windows 8.1 (x86、x64)<br /><br />- Windows 8 (x86、x64)<br /><br />- Windows 7 Service Pack 1 (x86、x64)<br /><br />Azure Rights Management サービスを使用して、このクライアントがデータを保護する場合は、Azure Rights Management サービスをサポートする同じデバイス (Windows、Mac、iOS、Android) から使用できます。 <br /><br />Azure Rights Management サービスをサポートするデバイスの詳細については、「[Azure Rights Management データ保護をサポートするクライアント デバイス](../get-started/requirements-client-devices.md)」をご覧ください。|
|アプリケーション|Azure Information Protection クライアントは、次の Office スイートの Office アプリケーション **Word**、**Excel**、**PowerPoint**、**Outlook** で作成されたファイルと電子メールのラベル付けと保護をサポートします。<br /><br /> - Office 365 ProPlus と 2016 アプリまたは 2013 アプリ (クイック実行または Windows インストーラー ベースのインストール)<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />Azure Rights Management サービスをサポートするアプリケーションの詳細については、「[Azure Rights Management データ保護をサポートするアプリケーション](requirements-applications.md)」をご覧ください。|
|インターネットと依存クラウド サービスへの接続をサポートするインフラストラクチャ|特定の接続を許可するように構成する必要があるファイアウォールまたは同様の介在するネットワーク デバイスがある場合は、Office 記事「[Office 365 URL および IP アドレス範囲](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」の「[Office 365 ポータルと共有](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity)」セクションで **Azure Rights Management (RMS)** に関する情報を参照してください。<br /><br />RSS フィードを購読して最新の情報を入手するには、この Office 記事の手順を使用してください。<br /><br />Office の記事の情報に加えて、Azure Information Protection に固有の要件は以下のとおりです。<br /><br />- **api.informationprotection.azure.com** TCP 443 の HTTPS トラフィックを許可します。<br /><br />- TLS クライアント/サービス間接続を終了しないでください (たとえばパケット レベルの検査を行うために)。 終了すると、Azure RMS との通信を保護するのに RMS クライアントが Microsoft が管理する CA と使用する証明書のピン留めが解除されます。<br /><br />- 認証が必要な Web プロキシを使用している場合には、ユーザーの Active Directory ログオン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。|

オンプレミス サーバーで Azure Information Protection から Azure Rights Management サービスを使用する必要がある場合、次の製品がサポートされます。

-   Exchange Server

-   SharePoint Server

-   ファイル分類インフラストラクチャをサポートする Windows Server ファイル サーバー

このシナリオに関する追加の要件については、「[Azure Rights Management データ保護をサポートするオンプレミス サーバー](requirements-servers.md)」をご覧ください。

> [!IMPORTANT]
> 次のデプロイ シナリオは、Azure Information Protection を使用した AD RMS 保護 ("Hold Your Own Key" または HYOK 構成) を使用している場合を除き、サポートされません。
> 
> -   同一組織での AD RMS および Azure RMS の並列実行 (移行時を除く。詳細については、「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照)。
> 
> [AD RMS から Azure Information Protection への移行](http://technet.microsoft.com/library/Dn858447.aspx)、および [Azure Information Protection から AD RMS への移行](http://msdn.microsoft.com/library/azure/dn629429.aspx)には、サポートされている移行パスがあります。 Azure Information Protection をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Information Protection の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」をご覧ください。






<!--HONumber=Dec16_HO1-->


