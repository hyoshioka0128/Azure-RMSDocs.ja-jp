---
title: "Azure Information Protection の要件"
description: "組織の Azure Information Protection をデプロイするための前提条件を特定します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/09/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 66874f6e60c2cd5efb2dedaae470170811a84a67
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# Azure Information Protection の要件
<a id="requirements-for-azure-information-protection" class="xliff"></a>

>*適用対象: Azure Information Protection、Office 365*

組織の Azure Information Protection をデプロイする前に、次の前提条件が満たされていることを確認します。 

|要件|詳細情報|
|---------------|--------------------|
|Azure Information Protection のサブスクリプション|分類、ラベル付け、保護については、[Azure Information Protection プラン](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)を取得する必要があります。 保護のみの場合は、[Rights Management を含む Office 365 プラン](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を取得する必要があります。<br /><br /> Azure Information Protection サイトの[サブスクリプション情報](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)および[機能一覧](https://www.microsoft.com/cloud-platform/azure-information-protection-features)を見て、使用する Azure Information Protection 機能を含むサブスクリプションを組織が所有していることを確認します。<br /><br />注意: サブスクリプションまたはライセンスに関するご質問がある場合は、このページに投稿するのではなく、当社担当者または [Microsoft サポート](information-support.md#to-contact-microsoft-support)にお問い合わせください。 |
|Azure Active Directory|組織には Azure Information Protection のユーザー認証と承認をサポートするための Azure Active Directory (Azure AD) が必要です。 また、オンプレミスのディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。<br /><br />必要なクライアント ソフトウェアと正しく構成された MFA サポート インフラストラクチャがある場合は、Azure Information Protection で多要素認証 (MFA) がサポートされます。<br /><br />認証要件の詳細については、「[Azure Information Protection の Azure Active Directory の要件](requirements-azure-ad.md)」をご覧ください。 <br /><br />承認用のユーザーとグループ アカウントの要件の詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](../plan-design/prepare.md)」をご覧ください。|
|クライアント デバイス|ユーザーは Azure Information Protection をサポートするオペレーティング システムを実行するクライアント デバイス (コンピューターまたはモバイル デバイス) を所有している必要があります。<br /><br />次のデバイスでは、Azure Information Protection クライアントをサポートします。これにより、ユーザーは次の Office のドキュメントや電子メールの分類およびラベル付けを行うことができます。<br /><br />- Windows 10 (x86、x64)<br /><br />- Windows 8.1 (x86、x64)<br /><br />- Windows 8 (x86、x64)<br /><br />- Windows 7 Service Pack 1 (x86、x64)<br /><br />- Windows Server 2016 <br /><br /> - Windows Server 2012 R2 および Windows Server 2012<br /><br />Azure Rights Management サービスを使用して、このクライアントがデータを保護する場合、Azure Rights Management サービスをサポートする同じデバイス (Windows、Mac、iOS、Android) からデータを使用できます。 <br /><br />Azure Rights Management サービスをサポートするデバイスの詳細については、「[Azure Rights Management データ保護をサポートするクライアント デバイス](../get-started/requirements-client-devices.md)」をご覧ください。|
|アプリケーション|Azure Information Protection クライアントは、次の Office エディションのいずれかの Office アプリケーション **Word**、**Excel**、**PowerPoint**、**Outlook** を使用して、ファイルと電子メールにラベルを付け、保護することができます。<br /><br /> - Office 365 ProPlus と 2016 アプリまたは 2013 アプリ (クイック実行または Windows インストーラー ベースのインストール)<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010 <br /><br />Office の他のエディションは、Rights Management サービスを使用してドキュメントや電子メールを保護できません。 これらのエディションでは、Azure Information Protection は分類のみのサポートで、保護を適用するラベルは、Azure Information Protection バーに表示されません。 <br /><br />データ保護サービスをサポートする Office のエディションについては、「[Azure Rights Management データ保護をサポートするアプリケーション](requirements-applications.md)」を参照してください。|
|インターネットと依存クラウド サービスへの接続をサポートするインフラストラクチャ|特定の接続を許可するように構成する必要があるファイアウォールまたは同様の介在するネットワーク デバイスがある場合は、Office 記事「[Office 365 URL および IP アドレス範囲](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」の「[Office 365 ポータルと共有](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity)」セクションで **Azure Rights Management (RMS)** に関する情報を参照してください。<br /><br />RSS フィードを購読して最新の情報を入手するには、この Office 記事の手順を使用してください。<br /><br />Office の記事の情報に加えて、Azure Information Protection に固有の要件は以下のとおりです。<br /><br />- **api.informationprotection.azure.com** TCP 443 の HTTPS トラフィックを許可します。<br /><br />- TLS クライアント/サービス間接続を終了しないでください (たとえばパケット レベルの検査を行うために)。 終了すると、Azure RMS との通信を保護するのに RMS クライアントが Microsoft が管理する CA と使用する証明書のピン留めが解除されます。<br /><br />- 認証が必要な Web プロキシを使用している場合には、ユーザーの Active Directory ログオン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。|

オンプレミス サーバーで Azure Information Protection から Azure Rights Management サービスを使用する必要がある場合、次の製品がサポートされます。

-   Exchange Server

-   SharePoint Server

-   ファイル分類インフラストラクチャをサポートする Windows Server ファイル サーバー

このシナリオに関する追加の要件については、「[Azure Rights Management データ保護をサポートするオンプレミス サーバー](requirements-servers.md)」をご覧ください。

> [!IMPORTANT]
> 次のデプロイ シナリオは、Azure Information Protection を使用した AD RMS 保護 ("Hold Your Own Key" または HYOK 構成) を使用している場合を除き、サポートされません。
> 
> -   同一組織での AD RMS および Azure RMS の並列実行 (移行時を除く。詳細については、「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照)。
> 
> [AD RMS から Azure Information Protection への移行](http://technet.microsoft.com/library/Dn858447.aspx)、および [Azure Information Protection から AD RMS への移行](/powershell/module/aadrm/Set-AadrmMigrationUrl)には、サポートされている移行パスがあります。 Azure Information Protection をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Information Protection の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」をご覧ください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


