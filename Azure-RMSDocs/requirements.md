---
title: Azure Information Protection の要件 - AIP
description: 組織に Azure Information Protection をデプロイするために必要な前提条件を確認します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3d90fdf263c15f80e23229bba427cb8d2b68f74e
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316672"
---
# <a name="azure-information-protection-requirements"></a>Azure Information Protection の要件

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection をデプロイする前に、システムが次の前提条件を満たしていることを確認してください。

- [Azure Information Protection のサブスクリプション](#subscription-for-azure-information-protection)
- [Azure Active Directory](#azure-active-directory)
- [クライアント デバイス](#client-devices)
- [アプリケーション](#applications)
- [ファイアウォールとネットワーク インフラストラクチャ](#firewalls-and-network-infrastructure)

## <a name="subscription-for-azure-information-protection"></a>Azure Information Protection のサブスクリプション

使用する Azure Information Protection の機能に応じて、次のいずれかを持っている必要があります。

- **[Azure Information Protection プラン](https://azure.microsoft.com/pricing/details/information-protection/)** 。 Azure Information Protection スキャナーまたはクライアント (クラシック、または統合ラベル付け) を使用した分類、ラベル付け、保護に必要です

- **[Azure Information Protection を含む Office 365 プラン](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)** 。 保護のみの場合に必要です。

使用する Azure Information Protection 機能がサブスクリプションに含まれていることを確認するには、「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)」で機能の一覧をチェックしてください。

ライセンスについて質問がある場合は、ライセンスについての[よく寄せられる質問](https://azure.microsoft.com/pricing/details/information-protection#faq)に目を通してください。

> [!TIP]
> 保護された電子メールを個人用のメール アドレスに送信するために、お使いのプランで [Office 365 Message Encryption の新機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)がサポートされているかどうかを確認する必要がありますか? たとえば、Gmail、Yahoo、Microsoft などです。 次のリソースを参照してください。
>
> - [Exchange Online サービスの説明](/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description)
>
> - [Microsoft 365 コンプライアンス ライセンスの比較](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-business-service-description)
>
> - [Office 365 Education](/office365/servicedescriptions/office-365-platform-service-description/office-365-education)
>
> - [Office 365 US Government](/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/office-365-us-government)

サブスクリプションまたはライセンスに関するご質問は、このページでは投稿しないでください。 代わりに、ライセンスについての[よく寄せられる質問](https://azure.microsoft.com/pricing/details/information-protection#faq)で回答されているかどうかを確認してください。 ここにご質問に対する回答がない場合は、Microsoft のアカウント マネージャーまたは [Microsoft サポート](information-support.md#to-contact-microsoft-support)にお問い合わせください。

## <a name="azure-active-directory"></a>Azure Active Directory

Azure Information Protection の認証と承認をサポートするには、Azure Active Directory (AD) が必要です。 オンプレミスのディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。

- Azure Information Protection では **シングル サインオン (SSO)** がサポートされているため、ユーザーが資格情報の入力を繰り返し求められることはありません。 フェデレーションに別のベンダーのソリューションを使用する場合は、そのベンダーで Azure AD 向けの構成方法を確認します。 WS-Trust は、これらのソリューションでシングル サインオンをサポートするための、一般的な要件です。 

- Azure Information Protection で **多要素認証 (MFA)** がサポートされるのは、必要なクライアント ソフトウェアと正しく構成された MFA 対応インフラストラクチャがある場合です。

条件付きアクセスは、Azure Information Protection によって保護されているドキュメントのプレビューでサポートされます。 詳細については、次をご覧ください。[条件付きアクセスに利用できるクラウド アプリとして Azure Information Protection が一覧に記載されています。これはどのように動作しますか。](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

Office 2010 を使用する場合、証明書ベースまたは多要素認証を使用する場合、UPN 値がユーザーのメール アドレスと一致しない場合など、特定のシナリオには追加の前提条件が必要です。 詳細については、「[Azure Information Protection に対する Azure AD の追加要件](requirements-azure-ad.md)」をご覧ください。

詳細については、次をご覧ください。

- [What is Azure AD Directory? (Azure AD ディレクトリとは)](/azure/active-directory/fundamentals/active-directory-whatis)
- [オンプレミスの Active Directory ドメインと Azure Active Directory を統合する](/azure/architecture/reference-architectures/identity/azure-ad)。

## <a name="client-devices"></a>クライアント デバイス

ユーザーのコンピューターまたはモバイル デバイスでは、Azure Information Protection をサポートしているオペレーティング システムを実行する必要があります。

- [クライアント デバイスでサポートされるオペレーティング システム](#supported-operating-systems-for-client-devices)
- [仮想マシン](#virtual-machines)
- [サーバーのサポート](#server-support)
- [クライアントごとの追加要件](#additional-requirements-per-client)

### <a name="supported-operating-systems-for-client-devices"></a>クライアント デバイスでサポートされるオペレーティング システム

次のオペレーティング システムでは、Azure Information Protection 統合ラベル付けと Azure Information Protection クライアントの両方がサポートされています。 

- **Windows 10** (x86、x64)。 Windows 10 RS4 ビルド以降では、手書きはサポートされていません。
 
- **Windows 8.1** (x86、x64)

- **Windows 8** (x86、x64)

- **Windows Server 2019**

- **Windows Server 2016**

- **Windows Server 2012 R2** および **Windows Server 2012**

[どちらのクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)でも、ユーザーがドキュメントや電子メールを分類してラベル付けすることができます。

以前のバージョンの Windows におけるサポートについて詳しくは、お使いの Microsoft アカウントまたはサポート担当者にお問い合わせください。

> [!NOTE]
> Azure Information Protection クライアントで Azure Rights Management サービスを使用してデータを保護する場合、Azure Rights Management サービスをサポートする[同じデバイス](#client-devices)からデータを使用できます。
>
### <a name="arm64"></a>ARM64 

現在、ARM64 はサポートされて **いません**。 

### <a name="virtual-machines"></a>仮想マシン

仮想マシンを使用する場合は、お使いの仮想デスクトップ ソリューションのソフトウェア ベンダーに Azure Information Protection 統合ラベル付けまたは Azure Information Protection クライアントの実行に必要な追加の構成があるかどうかを確認します。 

たとえば、Citrix ソリューションでは、Office、Azure Information Protection 統合ラベル付けクライアント、または Azure Information Protection クライアントのために [Citrix アプリケーション プログラミング インターフェイス (API) フックを無効にする](https://support.citrix.com/article/CTX107825)ことが必要になる場合があります。 

これらのアプリケーションでは、それぞれ次のファイルが使用されます: **winword.exe**、**excel.exe**、**outlook.exe**、**powerpnt.exe**、**msip.app.exe**、**msip.viewer.exe**

### <a name="server-support"></a>サーバー サポート

上記の各サーバー バージョンでは、リモート デスクトップ サービスについて Azure Information Protection クライアントがサポートされています。 

Azure Information Protection クライアントとリモート デスクトップ サービスを使用しているときに、ユーザー プロファイルを削除する場合は、 **%Appdata%\Microsoft\Protect** フォルダーを削除しないでください。

また、Server Core と Nano Server はサポートされていません。

### <a name="additional-requirements-per-client"></a>クライアントごとの追加要件

各 Azure Information Protection クライアントには追加の前提条件があります。 詳細については、次の情報を参照してください。

- [Azure Information Protection 統合ラベル付けクライアントの前提条件](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- [Azure Information Protection クライアントの前提条件](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)

## <a name="applications"></a>アプリケーション

Azure Information Protection クライアントでは、次のいずれかの Office エディションの Microsoft **Word**、**Excel**、**PowerPoint**、**Outlook** を使用して、ドキュメントと電子メールにラベルを付け、保護することができます。

- Microsoft 365 Apps for Business または Microsoft 365 Business Premium の **Office アプリの最小バージョン 1805**、ビルド 9330.2078。 

    このエディションは、ユーザーに Azure Rights Management (別名 Azure Information Protection for Microsoft 365) のライセンスが割り当てられている場合にのみサポートされます。

- **Microsoft 365 Apps for Enterprise**

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013 Service Pack 1**

- **Office Professional Plus 2010 Service Pack 2**

Office の他のエディションは、Rights Management サービスを使用してドキュメントや電子メールを保護できません。 これらのエディションでは、Azure Information Protection は分類のみのサポートで、保護を適用するラベルはユーザーに表示されません。 

それ以外の場合、これらのラベルは Azure Information Protection バーまたは Office リボンの統合ラベル付けクライアントに表示されます (クラシック クライアントの場合 **[保護]** ボタンから、統合ラベル付けクライアントの場合 **[秘密度]** ボタンから)。 

詳細については、「[Azure Rights Management データ保護をサポートするアプリケーション](requirements-applications.md)」をご覧ください。

### <a name="office-features-and-capabilities-not-supported"></a>サポートされていない Office の特徴と機能

- Azure Information Protection クライアントでは、クラシックでも統合ラベル付けでも、同じコンピューター上で複数のバージョンの Office を使用したり、Office のユーザー アカウントを切り替えたりすることはサポートされていません。

- Office の[差し込み印刷](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705)機能は、どの Azure Information Protection 機能でもサポートされていません。

## <a name="firewalls-and-network-infrastructure"></a>ファイアウォールとネットワーク インフラストラクチャ

特定の接続を許可するように構成されたファイアウォール、または同様の中間ネットワーク デバイスがある場合、ネットワーク接続の要件は次の Office に関する記事に記載されています:「[Microsoft 365 Common および Office Online](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online)」。

Azure Information Protection には、次の追加要件があります。

- **統合ラベル付けクライアント**。 ラベルとラベル ポリシーをダウンロードするには、HTTPS で次の URL を許可してください: **_.protection.outlook.com_*

- **Web プロキシ**。 認証が必要な Web プロキシを使用している場合には、ユーザーの Active Directory サインイン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。

    プロキシを使用してトークンを取得するときに **Proxy.pac** ファイルをサポートするには、次の新しいレジストリ キーを追加します。

    - **パス:** `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIP\`
    - **キー:** `UseDefaultCredentialsInProxy`
    - **種類:** `DWORD`
    - **値:** `1`
    
- **TLS クライアント/サービス間接続**。 **aadrm.com** URL への TLS クライアント/サービス間接続を終了しないでください (たとえば、パケット レベルの検査を実行するためなど)。 この操作によって、RMS クライアントが使用している証明書のピン留めが解除されます。この証明書とは、Azure Rights Management サービスとの通信を保護するために、Microsoft が管理する CA と共に使用されているものです。
     
    クライアント接続が Azure Rights Management サービスに到達する前に終了しているかどうかを確認するには、次の PowerShell コマンドを使用します。

    ```PowerShell
    $request = [System.Net.HttpWebRequest]::Create("https://admin.na.aadrm.com/admin/admin.svc")
    $request.GetResponse()
    $request.ServicePoint.Certificate.Issuer
    ```

    結果には、発行元の CA が Microsoft CA からのものであることが示されます (例: `CN=Microsoft Secure Server CA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`)。 
    
    発行元の CA 名が Microsoft からのものでない場合、クライアントとサービス間のセキュリティで保護された接続は終了しており、ファイアウォール上で再構成する必要がある可能性があります。

- **TLS バージョン 1.2 以降** (統合ラベル付けクライアントのみ)。 暗号として安全なプロトコルを使用し、Microsoft のセキュリティ ガイドラインに準拠するには、統合ラベル付けクライアントでバージョン 1.2 以降の TLS を使用する必要があります。

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>AD RMS と Azure RMS の共存

同じ組織内の同じユーザーがコンテンツを保護できるように、同じ組織内で AD RMS と Azure RMS をサイド バイ サイドで使用することは、AD RMS で、Azure Information Protection での [HYOK (Hold Your Own Key) 保護](configure-adrms-restrictions.md)に対して **のみ** サポートされています。

このシナリオは、[移行](migrate-from-ad-rms-to-azure-rms.md)中にはサポート "*されません*"。
サポートされている移行パスは次のとおりです。

* [AD RMS から Azure Information Protection へ](migrate-from-ad-rms-to-azure-rms.md)

* [Azure Information Protection から AD RMS へ](/powershell/module/aipservice/Set-AipServiceMigrationUrl)

> [!TIP]
> Azure Information Protection をデプロイした後で、このクラウド サービスを使用したくなくなった場合は、「[Azure Information Protection の使用停止と非アクティブ化](decommission-deactivate.md)」をご覧ください。

同じ組織内で両方のサービスがアクティブになっている他の移行以外のシナリオについては、その一方のみを使用して特定のユーザーがコンテンツを保護できるように、両方のサービスを構成する必要があります。 このようなシナリオは次のように構成します。

* [AD RMS から Azure RMS への移行](migrate-from-ad-rms-to-azure-rms.md)にリダイレクトを使用します

* 同時に複数のユーザーに対して両方のサービスをアクティブにする必要がある場合は、サービス側の構成を使用して排他性を適用します。  クラウド サービスで Azure RMS オンボード制御を使用し、発行 URL の ACL を使用して AD RMS の **読み取り専用** モードを設定します。

### <a name="service-tags"></a>サービス タグ

Azure エンドポイントと NSG を使用している場合は、次のサービス タグについて、すべてのポートへのアクセスを許可してください。

- **AzureInformationProtection**
- **AzureActiveDirectory**
- **AzureFrontDoor.Frontend**

さらに、この場合、Azure Information Protection サービスは、次の 2 つの特定の IP アドレスにも依存します。

 - **13.107.6.181** 
 - **13.107.9.181**
 - **ポート 443** (HTTPS トラフィック用)

これらの特定の IP アドレスへの (またこのポート経由での) 発信アクセスを許可する規則を作成してください。

## <a name="supported-on-premises-servers-for-azure-rights-management-data-protection"></a>Azure Rights Management データ保護でサポートされているオンプレミス サーバー

Azure Rights Management コネクタを使用すると、次のオンプレミス サーバーは Azure Information Protection でサポートされます。

このコネクタは、Office ドキュメントや電子メールを保護するために Azure Information Protection によって使用される Azure Rights Management サービスとオンプレミス サーバーの間の通信インターフェイスおよびリレーとして機能します。 

このコネクタを使用するには、Active Directory フォレストと Azure Active Directory とのディレクトリ同期を構成する必要があります。

サポートされているサーバーは次のとおりです。

|サーバーの種類  |サポートされているバージョン  |
|---------|---------|
|**Exchange Server**     | - Exchange Server 2016 </br>- Exchange Server 2013 </br>- Exchange Server 2010       |
|**Office SharePoint Server**     |- Office SharePoint Server 2016 </br>- Office SharePoint Server 2013 </br>- Office SharePoint Server 2010         |
|**Windows Server を実行し、ファイル分類インフラストラクチャ (FCI) を使用するファイル サーバー**     |- Windows Server 2016 </br>- Windows Server 2012 R2 </br>- Windows Server 2012       |
| | |

詳細については、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」を参照してください。

## <a name="supported-operating-systems-for-azure-rights-management"></a>Azure Rights Management でサポートされているオペレーティング システム

次のオペレーティング システムでは、AIP のデータ保護を提供する Azure Rights Management サービスがサポートされています。

|OS  |サポートされているバージョン  |
|---------|---------|
|**Windows コンピューター**     |- Windows 7 (x86、x64) </br>- Windows 8 (x86、x64) </br>- Windows 8.1 (x86、x64) </br>- Windows 10 (x86、x64)       | 
|**macOS**     |   macOS 10.8 (Mountain Lion) 以降      |
|**Android 端末およびタブレット**     | Android 6.0 以降        |
|**iPhone と iPad**     | iOS 11.0 以降        |
|**Windows Phone およびタブレット** | Windows 10 Mobile|
| | |



## <a name="next-steps"></a>次のステップ

AIP の要件をすべて確認し、システムが準拠していることを確認したら、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」に進みます。