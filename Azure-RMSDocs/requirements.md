---
title: Azure Information Protection の要件 - AIP
description: Azure Information Protection を組織に展開するために必要な前提条件を特定します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/25/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bcb3006bdd7575385d37be066b627ef49f770c70
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047713"
---
# <a name="azure-information-protection-requirements"></a>Azure Information Protection の要件

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection を展開する前に、システムが次の前提条件を満たしていることを確認してください。

- [Azure Information Protection のサブスクリプション](#subscription-for-azure-information-protection)
- [Azure Active Directory](#azure-active-directory)
- [クライアント デバイス](#client-devices)
- [アプリケーション](#applications)
- [ファイアウォールとネットワーク インフラストラクチャ](#firewalls-and-network-infrastructure)

## <a name="subscription-for-azure-information-protection"></a>Azure Information Protection のサブスクリプション

使用する Azure Information Protection の機能に応じて、次のいずれかを用意する必要があります。

- ** [Azure Information Protection プラン](https://azure.microsoft.com/pricing/details/information-protection/)**。 Azure Information Protection スキャナーまたはクライアント (クラシック、または統合されたラベル付け) を使用して、分類、ラベル付け、保護に必要

- ** [Azure Information Protection を含む Office 365 プラン](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)**。 保護のみに必要です。

使用する Azure Information Protection 機能がサブスクリプションに含まれていることを確認するには Azure Information Protection の[価格](https://azure.microsoft.com/pricing/details/information-protection)に関する機能の一覧を確認してください。

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

Azure Information Protection の認証と承認をサポートするには、Azure Active Directory (AD) が必要です。 オンプレミスのディレクター (AD DS) のユーザーアカウントを使用するには、ディレクトリ統合も構成する必要があります。

- Azure Information Protection では**シングルサインオン (SSO)** がサポートされているので、ユーザーが資格情報の入力を繰り返し求められることはありません。 フェデレーションに別のベンダーソリューションを使用する場合は、そのベンダーに Azure AD を構成する方法を確認してください。 WS-Trust は、これらのソリューションでシングル サインオンをサポートするための、一般的な要件です。 

- 必要なクライアントソフトウェアがあり、MFA をサポートするインフラストラクチャが正しく構成されている場合は、Azure Information Protection で**multi-factor authentication (MFA)** がサポートされます。

条件付きアクセスは、Azure Information Protection によって保護されているドキュメントのプレビューでサポートされます。 詳細について[は、「条件付きアクセスに使用できるクラウドアプリとして Azure Information Protection が表示される」を参照してください。これはどのように動作しますか](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)。

詳細については、次のリンクを参照してください。

- [Azure Information Protection の Azure Active Directory の要件](requirements-azure-ad.md)

- [Azure Information Protection 向けのユーザーとグループの準備](prepare.md)

## <a name="client-devices"></a>クライアント デバイス

ユーザーのコンピューターまたはモバイルデバイスは、Azure Information protection をサポートするオペレーティングシステム上で実行する必要があります。

### <a name="supported-operating-systems-for-client-devices"></a>クライアントデバイスでサポートされているオペレーティングシステム

次のオペレーティングシステムは、Azure Information Protection 統合されたラベル付けと Azure Information Protection クライアントの両方をサポートしています。 

- **Windows 10** (x86、x64)。 手書きは、Windows 10 RS4 ビルド以降ではサポートされていません。
 
- **Windows 8.1** (x86、x64)

- **Windows 8** (x86、x64)

- **Windows Server 2019**

- **Windows Server 2016**

- **Windows server 2012 R2**および**windows server 2012**

[どちらのクライアントも](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)、ユーザーがドキュメントや電子メールを分類してラベル付けすることができます。

以前のバージョンの Windows でのサポートの詳細については、Microsoft アカウントまたはサポート担当者にお問い合わせください。

> [!NOTE]
> Azure Information Protection クライアントが Azure Rights Management サービスを使用してデータを保護する場合、Azure Rights Management サービスをサポートする[同じデバイス](requirements-client-devices.md)でデータを使用できます。
>

### <a name="virtual-machines"></a>仮想マシン
仮想マシンを使用している場合は、Azure Information Protection 統合されたラベル付けまたは Azure Information Protection クライアントの実行に必要な追加の構成として、仮想デスクトップソリューションのソフトウェアベンダーがあるかどうかを確認します。 

たとえば、Citrix ソリューションでは、Office 用の[Citrix アプリケーションプログラミングインターフェイス (API) フック](https://support.citrix.com/article/CTX107825)、Azure Information Protection 統合されたラベル付けクライアント、または Azure Information Protection クライアントを無効にする必要がある場合があります。 

これらのアプリケーションは、それぞれ**winword.exe**、 **excel.exe**、 **outlook.exe**、 **powerpnt.exe**、 **msip.app.exe**、 **msip.viewer.exe**の各ファイルを使用します。

### <a name="server-support"></a>サーバー サポート

上に示した各サーバーバージョンでは、Azure Information Protection クライアントがリモートデスクトップサービスでサポートされています。 

リモートデスクトップサービスで Azure Information Protection クライアントを使用しているときにユーザープロファイルを削除する場合は、 **%Appdata%\Microsoft\Protect**フォルダーを削除しないでください。

また、Server Core と Nano Server はサポートされていません。

### <a name="additional-requirements-per-client"></a>クライアントごとの追加要件

各 Azure Information Protection クライアントには、追加の前提条件があります。 詳細については、次の情報を参照してください。

- [Azure Information Protection 統合されたラベル付けクライアントの前提条件](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- [Azure Information Protection クライアントの前提条件](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)

## <a name="applications"></a>アプリケーション

Azure Information Protection クライアントは、次のいずれかの Office エディションから Microsoft **Word**、 **Excel**、 **PowerPoint**、 **Outlook**を使用して、ドキュメントや電子メールのラベル付けと保護を行うことができます。

- **Office アプリの最小バージョン 1805**。 Office 365 Business または Microsoft 365 Business から9330.2078 をビルドします。 

    このエディションは、ユーザーに Azure Rights Management のライセンスが割り当てられている場合にのみサポートされます (Office 365 の Azure Information Protection とも呼ばれます)。

- **Office 365 ProPlus**

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013 Service Pack 1**

- **Office Professional Plus 2010 Service Pack 2**

Office の他のエディションは、Rights Management サービスを使用してドキュメントや電子メールを保護できません。 これらのエディションでは、Azure Information Protection が分類のみでサポートされており、保護を適用するラベルはユーザーに対して表示されません。 

これらのラベルは、Azure Information Protection バーまたは Office リボンの統一されたラベル付けクライアント (従来のクライアントの [**保護**] ボタンまたは統合ラベル付けクライアントの [**秘密度**] ボタンから) に表示されます。 

詳細については、「 [Azure Rights Management データ保護をサポートするアプリケーション](requirements-applications.md)」を参照してください。

### <a name="office-features-and-capabilities-not-supported"></a>サポートされていない Office の機能

- Azure Information Protection クライアントは、従来のラベル付けと統一されたラベル付けの両方を含み、同じコンピューターで複数のバージョンの Office をサポートしたり、Office のユーザーアカウントを切り替えたりすることはできません。

- Office[メールのマージ](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705)機能は、Azure Information Protection 機能ではサポートされていません。

## <a name="firewalls-and-network-infrastructure"></a>ファイアウォールとネットワーク インフラストラクチャ

特定の接続を許可するように構成されているファイアウォールまたは同様の介在するネットワークデバイスがある場合は、この Office 記事の「 [office 365 の url と IP アドレスの範囲 > Microsoft 365 Common と Office Online](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online)」にネットワーク接続の要件が記載されています。

Azure Information Protection には、次の追加要件があります。

- 統一された**ラベル付けクライアント**。 ラベルとラベルポリシーをダウンロードするには、HTTPS で次の URL を許可してください: ***. protection.outlook.com**

- **Web プロキシ**。 認証が必要な web プロキシを使用する場合は、ユーザーの Active Directory ログオン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。

    
- **TLS クライアントとサービス間の接続**。 **Aadrm.com** URL に対してパケットレベルの検査を実行するなど、TLS クライアントからサービスへの接続を終了しないでください。 この操作によって、RMS クライアントが使用している証明書のピン留めが解除されます。この証明書とは、Azure Rights Management サービスとの通信を保護するために、Microsoft が管理する CA と共に使用されているものです。
     
    Azure Rights Management サービスに到達する前にクライアント接続が終了しているかどうかを確認するには、次の PowerShell コマンドを使用します。

    ```ps
    $request = [System.Net.HttpWebRequest]::Create("https://admin.na.aadrm.com/admin/admin.svc")
    $request.GetResponse()
    $request.ServicePoint.Certificate.Issuer
    ```

    結果には、発行元の CA が Microsoft CA からのものであることが示されます。たとえば、のようになり `CN=Microsoft Secure Server CA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US` ます。 
    
    発行元 CA の名前が Microsoft からのものではない場合、セキュリティで保護されたクライアントとサービス間の接続が終了し、ファイアウォールで再構成が必要になる可能性が非常に高くなります。

- **TLS バージョン1.2 以降**(統一されたラベル付けクライアントのみ)。 統一されたラベル付けクライアントを使用するには、1.2 以上の TLS バージョンが必要です。これにより、暗号化が安全なプロトコルを使用し、Microsoft のセキュリティガイドラインに合わせることができます。
    
### <a name="on-premises-servers"></a>オンプレミスのサーバー

Azure Information Protection の Azure Rights Management サービスでは、次のオンプレミスサーバーがサポートされています。

- **Exchange Server**

- **SharePoint Server**

- ファイル分類インフラストラクチャをサポートする**Windows Server ファイルサーバー**

このシナリオに関する追加の要件については、「[Azure Rights Management データ保護をサポートするオンプレミス サーバー](requirements-servers.md)」をご覧ください。

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>AD RMS と Azure RMS の共存

同じ組織内で AD RMS と Azure RMS をサイドバイサイドで使用して、同じ組織内の同じユーザーがコンテンツを保護することは、Azure Information Protection での[HYOK (独自のキーの保持) 保護](configure-adrms-restrictions.md)の AD RMS で**のみ**サポートされています。

このシナリオは、[移行](migrate-from-ad-rms-to-azure-rms.md)中にはサポートされ*ません*。
サポートされている移行パスは次のとおりです。

* [AD RMS から Azure Information Protection へ](migrate-from-ad-rms-to-azure-rms.md)

* [Azure Information Protection から AD RMS へ](/powershell/module/aipservice/Set-AipServiceMigrationUrl)

> [!TIP]
> Azure Information Protection をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Information Protection の使用停止と非アクティブ化](decommission-deactivate.md)」をご覧ください。

同じ組織内で両方のサービスがアクティブになっているその他の非移行シナリオについては、両方のサービスが、特定のユーザーがコンテンツを保護できるように、両方のサービスを構成する必要があります。 これは次のようにして構成できます。

* AD RMS にリダイレクトを使用して[Azure RMS 移行を行う](migrate-from-ad-rms-to-azure-rms.md)

* 同時に複数のユーザーに対して両方のサービスをアクティブにする必要がある場合は、サービス側の構成を使用して排他性を適用します。  クラウドサービスの Azure RMS オンボードコントロールと、発行 URL の ACL を使用して、AD RMS の**読み取り**専用モードを設定します。

### <a name="service-tags"></a>サービス タグ

次のサービスタグのすべてのポートへのアクセスを許可してください。

- **AzureInformationProtection**
- **AzureActiveDirectory**
- **AzureFrontDoor**

Azure Information Protection サービスは、次の2つの特定の IP アドレスにも依存します。
 - **13.107.6.181** 
 - **13.107.9.181**

これらの特定の IP アドレスへの発信アクセスを許可する規則を作成してください。 
