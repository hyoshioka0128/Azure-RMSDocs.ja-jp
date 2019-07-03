---
title: Azure Information Protection の要件 - AIP
description: 組織の Azure Information Protection をデプロイするための前提条件を特定します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 17b41c32b760e0bff2dcb430689fb8bbebacc22d
ms.sourcegitcommit: a2542aec8cd2bf96e94923740bf396badff36b6a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2019
ms.locfileid: "67535159"
---
# <a name="requirements-for-azure-information-protection"></a>Azure Information Protection の要件

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

組織の Azure Information Protection をデプロイする前に、次の前提条件が満たされていることを確認します。 

## <a name="subscription-for-azure-information-protection"></a>Azure Information Protection のサブスクリプション

**分類、ラベル付け、保護の場合**: [Azure Information Protection プラン](https://azure.microsoft.com/pricing/details/information-protection/)を取得する必要があります。 

**保護のみの場合**: [Azure Information Protection を含む Office 365 プラン](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を取得する必要があります。

使用する Azure Information Protection 機能を含むサブスクリプションを組織が所有していることを確認するには、「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)」ページの機能一覧をご覧ください。

ライセンスについて質問がある場合は、ライセンスについての[よく寄せられる質問](https://azure.microsoft.com/pricing/details/information-protection#faq)に目を通してください。

> [!TIP]
> 保護された電子メールを個人用の電子メール アドレスに送信するために、お使いの Office 365 プランまたは Exchange Online スタンドアロン プランで [Office 365 Message Encryption の新機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)をサポートしているかどうかを確認する必要がありますか? たとえば、Gmail、Yahoo、Microsoft などです。 次のリソースを参照してください。
>
> - [Exchange Online サービスの説明](https://technet.microsoft.com/library/exchange-online-service-description.aspx)
>
> - [Office 365 Education](https://technet.microsoft.com/library/mt844095.aspx)
>
> - [Office 365 US Government](https://technet.microsoft.com/library/mt774581.aspx)

サブスクリプションまたはライセンスに関するご質問は、このページでは投稿しないでください。 代わりに、ライセンスについての[よく寄せられる質問](https://azure.microsoft.com/pricing/details/information-protection#faq)で回答されているかどうかを確認してください。 ここにご質問に対する回答がない場合は、Microsoft のアカウント マネージャーまたは [Microsoft サポート](information-support.md#to-contact-microsoft-support)にお問い合わせください。

## <a name="azure-active-directory"></a>Azure Active Directory

組織には Azure Information Protection のユーザー認証と承認をサポートするための Azure Active Directory (Azure AD) が必要です。 また、内部設置型ディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。

Azure Information Protection ではシングル サインオン (SSO) がサポートされます。したがって、ユーザーが資格情報の入力を繰り返し求められることはありません。 フェデレーションに別のベンダーのソリューションを使用する場合は、そのベンダーで Azure AD 向けの構成方法を確認します。 WS-Trust は、これらのソリューションでシングル サインオンをサポートするための、一般的な要件です。 

必要なクライアント ソフトウェアと正しく構成された MFA サポート インフラストラクチャがある場合は、Azure Information Protection で多要素認証 (MFA) がサポートされます。

条件付きアクセスは、Azure Information Protection によって保護されているドキュメントのプレビューでサポートされます。 詳細については、次の FAQ を参照してください: [条件付きアクセスに利用できるクラウド アプリとして Azure Information Protection が一覧に記載されています。これはどのように動作しますか。](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

認証要件の詳細については、「[Azure Information Protection の Azure Active Directory の要件](requirements-azure-ad.md)」をご覧ください。 

承認用のユーザーとグループ アカウントの要件の詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

## <a name="client-devices"></a>クライアント デバイス

ユーザーは Azure Information Protection をサポートするオペレーティング システムを実行するクライアント デバイス (コンピューターまたはモバイル デバイス) を所有している必要があります。

次のデバイスでは、Azure Information Protection の統合されたラベル付けクライアント、および Azure Information Protection クライアントをサポートします。 [両方のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)分類して、文書や電子メールをラベル付けできるようにします。

- Windows 10 (x86、x64)
    
    - Windows 10 RS4 Build 以降では、手書きはサポートされていません。 

- Windows 8.1 (x86、x64)

- Windows 8 (x86、x64)

- Windows 7 Service Pack 1 (x86、x64)

- Windows Server 2016 

- Windows Server 2012 R2 および Windows Server 2012

- Windows Server 2008 R2 

物理コンピューターでクライアントをインストールする方法に加えてインストールすることも、仮想マシンでします。 仮想デスクトップ ソリューションのソフトウェア ベンダーが実行する必要がある追加の構成を持つかどうかを確認、Azure Information Protection の統合されたラベル付けクライアントまたは Azure Information Protection クライアント。 たとえば、Citrix のソリューションにならない場合があります[Citrix アプリケーション プログラミング インターフェイス (API) フックを無効にする](https://support.citrix.com/article/CTX107825)for Office (winword.exe、excel.exe、outlook.exe、powerpoint.exe) および実行可能ファイル、AzureInformation Protection の統一されたラベル付けクライアントまたは Azure Information Protection クライアント (msip.app.exe、msip.viewer.exe)。

表示されているサーバー バージョンでは、Azure Information Protection クライアントは、リモート デスクトップ サービスのサポートされます。 リモート デスクトップ サービスを Azure Information Protection クライアントを使用する場合にユーザー プロファイルを削除する場合は削除しないでください、 **%Appdata%\Microsoft\Protect**フォルダー。

データを使用できる、Azure Information Protection クライアントは、Azure Rights Management サービスを使用して、データを保護するときに、[同じデバイス](requirements-client-devices.md)Azure Rights Management サービスをサポートします。

Azure Information Protection クライアントは、それぞれの管理者ガイドに記載されている追加の前提条件があります。

- Azure Information Protection 統合ラベル付けクライアント:[前提条件](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- Azure Information Protection クライアント:[前提条件](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)


## <a name="applications"></a>[アプリケーション]

Azure Information Protection クライアントがラベルし、Office アプリケーションを使用してドキュメントや電子メールを保護**Word**、 **Excel**、 **PowerPoint**、および**Outlook**から次の Office エディションのいずれか。

- ユーザーに Azure Rights Management (別名: Azure Information Protection for Office 365) のライセンスが割り当てられている場合は、Office 365 Business または Microsoft 365 Business の最小バージョン 1805、ビルド 9330.2078 の Office アプリ

- Office 365 ProPlus

- Office Professional Plus 2019

- Office Professional Plus 2016

- Office Professional Plus 2013 Service Pack 1

- Office Professional Plus 2010 Service Pack 2

Office の他のエディションは、Rights Management サービスを使用してドキュメントや電子メールを保護できません。 これらのエディションの場合、Azure Information Protection は分類についてのみサポートされます。 そのため、保護を適用するラベルは、Azure Information Protection バーまたは Office リボンの **[保護]** ボタンでユーザーに表示されません。 

Azure Information Protection クライアントは、同じコンピューターに Office の複数のバージョンをサポートしていません。 これらのクライアントもできないユーザー アカウントの切り替え Office にあります。

保護サービスをサポートする Office のエディションについては、「[Azure Rights Management データ保護をサポートするアプリケーション](requirements-applications.md)」を参照してください。

## <a name="firewalls-and-network-infrastructure"></a>ファイアウォールとネットワーク インフラストラクチャ

特定の接続を許可するように構成されたファイアウォール、または同様の中間ネットワーク デバイスがある場合、ネットワーク接続の要件は、Office の記事「[Office 365 URL および IP アドレス範囲](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」に記載されています。 「**Microsoft 365 Common および Office Online**」セクションをご覧ください。

Office の記事の情報に加えて、Azure Information Protection に固有の要件は以下のとおりです。

- 認証が必要な Web プロキシを使用している場合には、ユーザーの Active Directory ログオン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。

- **aadrm.com** URL への TLS クライアント/サービス間接続を終了しないでください (たとえばパケット レベルの検査を行うために)。 終了すると、RMS クライアントが使用している証明書のピン留めが解除されます。この証明書とは、Azure Rights Management サービスとの通信を保護するために、Microsoft が管理する CA とともに使用されているものです。
    
    - ヒント:Chrome ではセキュリティで保護された接続の状態がアドレス バーに表示されるため、このブラウザーを使うと、Azure Rights Management サービスに到達する前にクライアント接続が終了するかどうかをすぐに確認できます。 ブラウザーのアドレス バーに次の URL を入力します: `https://admin.na.aadrm.com/admin/admin.svc` 
    
        ブラウザー ウィンドウに表示されるものについては気に留める必要はありません。 その代わりに、アドレス バーの鍵マークをクリックしてサイトの情報を確認します。 サイトの情報で発行元の証明機関 (CA) を確認できます。 証明書が Microsoft CA によって発行されたものでない場合、クライアントとサービス間のセキュリティで保護された接続は終了し、ファイアウォール上で再構成する必要がある場合があります。 次の図は、Microsoft が発行した CA の例です。 証明書を発行したのが内部 CA である場合、この構成は Azure Information Protection との互換性がありません。
        
        ![Azure Information Protection 接続に対して発行された証明書の確認](./media/certificate-checking.png)

### <a name="on-premises-servers"></a>オンプレミス サーバー

オンプレミス サーバーで Azure Information Protection から Azure Rights Management サービスを使用する必要がある場合、次の製品がサポートされます。

- Exchange Server

- SharePoint Server

- ファイル分類インフラストラクチャをサポートする Windows Server ファイル サーバー

このシナリオに関する追加の要件については、「[Azure Rights Management データ保護をサポートするオンプレミス サーバー](requirements-servers.md)」をご覧ください。

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>AD RMS と Azure RMS の共存

次のデプロイ シナリオは、Azure Information Protection を使った [HYOK 保護](configure-adrms-restrictions.md) ("Hold Your Own Key" 構成) 用に AD RMS を 使用している場合を除き、サポートされません。

- 同一組織での AD RMS および Azure RMS の並列実行 (移行時を除く。詳細については、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照)。

[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)、および [Azure Information Protection から AD RMS への移行](/powershell/module/aipservice/Set-AipServiceMigrationUrl)には、サポートされている移行パスがあります。 Azure Information Protection をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Information Protection の使用停止と非アクティブ化](decommission-deactivate.md)」をご覧ください。

