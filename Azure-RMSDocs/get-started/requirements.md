---
title: "Azure Information Protection の要件"
description: "組織の Azure Information Protection をデプロイするための前提条件を特定します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/10/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 74c0725857148fe12943bd9368173124cb059dcf
ms.sourcegitcommit: 1128ccda089727ac4a638e99532516474cef0ef4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-information-protection"></a>Azure Information Protection の要件

>*適用対象: Azure Information Protection、Office 365*

組織の Azure Information Protection をデプロイする前に、次の前提条件が満たされていることを確認します。 

## <a name="subscription-for-azure-information-protection"></a>Azure Information Protection のサブスクリプション

分類、ラベル付け、保護については、[Azure Information Protection プラン](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)を取得する必要があります。 

保護のみの場合は、[Rights Management を含む Office 365 プラン](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を取得する必要があります。

使用する Azure Information Protection 機能を含むサブスクリプションを組織が所有していることを確認するには、Azure Information Protection サイトの[サブスクリプション情報](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)および[機能一覧](https://www.microsoft.com/cloud-platform/azure-information-protection-features)を参照します。

> [!NOTE]
> サブスクリプションまたはライセンスに関するご質問がある場合は、このページに投稿するのではなく、弊社担当者または [Microsoft サポート](information-support.md#to-contact-microsoft-support)にお問い合わせください。

## <a name="azure-active-directory"></a>Azure Active Directory

組織には Azure Information Protection のユーザー認証と承認をサポートするための Azure Active Directory (Azure AD) が必要です。 また、オンプレミスのディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。

必要なクライアント ソフトウェアと正しく構成された MFA サポート インフラストラクチャがある場合は、Azure Information Protection で多要素認証 (MFA) がサポートされます。

認証要件の詳細については、「[Azure Information Protection の Azure Active Directory の要件](requirements-azure-ad.md)」をご覧ください。 

承認用のユーザーとグループ アカウントの要件の詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](../plan-design/prepare.md)」をご覧ください。

## <a name="client-devices"></a>クライアント デバイス

ユーザーは Azure Information Protection をサポートするオペレーティング システムを実行するクライアント デバイス (コンピューターまたはモバイル デバイス) を所有している必要があります。

次のデバイスでは、Azure Information Protection クライアントをサポートします。これにより、ユーザーは次のドキュメントや電子メールの分類およびラベル付けを行うことができます。

- Windows 10 (x86、x64)

- Windows 8.1 (x86、x64)

- Windows 8 (x86、x64)

- Windows 7 Service Pack 1 (x86、x64)

- Windows Server 2016 

- Windows Server 2012 R2 および Windows Server 2012

- Windows Server 2008 R2 

これらのサーバー バージョンでは、リモート デスクトップ サービスについて Azure Information Protection クライアントがサポートされています。 Azure Information Protection クライアントとリモート デスクトップ サービスを使用しているときに、ユーザー プロファイルを削除する場合は、**%LocalAppData%\Roaming\Microsoft\Protect** フォルダーを削除しないでください。

Azure Information Protection クライアントで Azure Rights Management サービスを使用してデータを保護する場合、Azure Rights Management サービスをサポートする[同じデバイス](requirements-client-devices.md)からデータを使用できます。

## <a name="applications"></a>アプリケーション

Azure Information Protection クライアントは、次の Office エディションのいずれかの Office アプリケーション **Word**、**Excel**、**PowerPoint**、**Outlook** を使用して、ドキュメントと電子メールにラベルを付け、保護することができます。

- Office 365 ProPlus と 2016 アプリまたは 2013 アプリ (クイック実行または Windows インストーラー ベースのインストール)

- Office Professional Plus 2016

- Office Professional Plus 2013 Service Pack 1

- Office Professional Plus 2010 Service Pack 2

Office の他のエディションは、Rights Management サービスを使用してドキュメントや電子メールを保護できません。 これらのエディションの場合、Azure Information Protection は分類についてのみサポートされます。 保護を適用するラベルは Azure Information Protection バーには表示されません。 

データ保護サービスをサポートする Office のエディションについては、「[Azure Rights Management データ保護をサポートするアプリケーション](requirements-applications.md)」を参照してください。

## <a name="firewalls-and-network-infrastructure"></a>ファイアウォールとネットワーク インフラストラクチャ

特定の接続を許可するように構成するファイアウォールまたは同様の介在するネットワーク デバイスがある場合は、Office 記事「[Office 365 URL および IP アドレス範囲](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」の「[Office 365 ポータルと共有](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity)」セクションで **Azure Rights Management (RMS)** に関する情報を参照してください。

RSS フィードを購読して最新の情報を入手するには、この Office 記事の手順を使用してください。

Office の記事の情報に加えて、Azure Information Protection に固有の要件は以下のとおりです。

- **api.informationprotection.azure.com** TCP 443 の HTTPS トラフィックを許可します。

- TLS クライアント/サービス間接続を終了しないでください (たとえばパケット レベルの検査を行うために)。 終了すると、Azure RMS との通信を保護するのに RMS クライアントが Microsoft が管理する CA と使用する証明書のピン留めが解除されます。

- 認証が必要な Web プロキシを使用している場合には、ユーザーの Active Directory ログオン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。


### <a name="on-premises-servers"></a>オンプレミス サーバー

オンプレミス サーバーで Azure Information Protection から Azure Rights Management サービスを使用する必要がある場合、次の製品がサポートされます。

- Exchange Server

- SharePoint Server

- ファイル分類インフラストラクチャをサポートする Windows Server ファイル サーバー

このシナリオに関する追加の要件については、「[Azure Rights Management データ保護をサポートするオンプレミス サーバー](requirements-servers.md)」をご覧ください。

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>AD RMS と Azure RMS の共存

次のデプロイ シナリオは、Azure Information Protection を使用した AD RMS 保護 ("Hold Your Own Key" または HYOK 構成) を使用している場合を除き、サポートされません。

- 同一組織での AD RMS および Azure RMS の並列実行 (移行時を除く。詳細については、「[AD RMS から Azure Information Protection への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照)。

[AD RMS から Azure Information Protection への移行](http://technet.microsoft.com/library/Dn858447.aspx)、および [Azure Information Protection から AD RMS への移行](/powershell/module/aadrm/Set-AadrmMigrationUrl)には、サポートされている移行パスがあります。 Azure Information Protection をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Information Protection の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」をご覧ください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


