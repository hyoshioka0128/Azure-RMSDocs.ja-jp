---
title: "Azure Rights Management と AD RMS の比較 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 67129d6cdac124947fc07aa4d42523686227752e
ms.openlocfilehash: ce79ec40cbd8ca3796a17920d27dc3872cd40842


---

# Azure Rights Management と AD RMS の比較

*適用対象: Active Directory Rights Management サービス、Azure Rights Management、Office 365*

Active Directory Rights Management サービス (AD RMS) を理解している、または以前にデプロイしたことがある場合、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) には機能や要件の面でどのような違いがあるのか疑問に思われるかもしれません。 

Azure RMS の主な違い:

- **サーバー インフラストラクチャが必要ない**: AD RMS では必要な追加サーバーと PKI 証明書が、Azure RMS では必要ありません。Microsoft Azure が自動的に処理します。 そのため、クラウド ソリューションを短時間でデプロイして簡単に管理できます。

- **クラウド ベースの認証**: Azure RMS は、内部ユーザーと他の組織からのユーザー両方の認証に Azure AD を使用します。 つまり、内部ネットワークに接続されていないモバイル ユーザーでも認証でき、保護されたコンテンツを他の組織のユーザーと簡単に共有できます。 多くの組織は、Azure サービスや Office 365 を使用しているため、Azure AD に既にユーザー アカウントがあります。 ない場合は、個人用 RMS で無料のアカウントを作成できます。 AD RMS で保護されたコンテンツを別の組織と共有するには、各組織との明示的な信頼関係を構成する必要があります。

- **モバイル デバイスの組み込みサポート**: Azure RMS でモバイル デバイスや Mac コンピューターをサポートする場合でも、デプロイを変更する必要はありません。 AD RMS でこれらのデバイスをサポートするには、モバイル デバイス拡張機能をインストールし、フェデレーション用に AD FS を構成して、パブリック DNS サービスの追加レコードを作成する必要があります。

- **既定のテンプレート**: Azure RMS では、サービスをアクティブ化すると 2 つの既定テンプレートが作成されるため、すぐにとても簡単に重要なデータの保護を開始できます。 AD RMS には既定のテンプレートはありません。

- **部門別テンプレート**: Azure RMS では、ユーザーが作成する追加テンプレートの構成設定として、部門別テンプレートがサポートされています。 この設定を使用するとクライアント アプリケーション (Office アプリケーションなど) でテンプレートを表示できるユーザーを指定でき、さまざまなユーザー グループに対して定義されている適切なポリシーを簡単に選択できます。 AD RMS では、部門別テンプレートはサポートされていません。

- **ドキュメントの追跡、失効、電子メール通知**: Azure RMS は RMS 共有アプリでこれらの機能をサポートしていますが、AD RMS はサポートしていません。


さらに、Azure RMS はクラウド サービスであるため、オンプレミスのサーバー ベースのソリューションより速く新しい機能や修正を提供できます。 Windows Server 2016 では AD RMS の新機能は計画されていません。

詳細および他の相違点については、次の表を使用して、Azure RMS と AD RMS の機能と利点を並べて比較することができます。 セキュリティに関する比較について質問がある場合は、この記事の「[署名と暗号化のための暗号化制御](compare-azure-rms-ad-rms.md#cryptographic-controls-for-signing-and-encryption)」セクションを参照してください。

> [!NOTE]
> 簡単に比較できるようにするために、ここでの一部の情報は「[Azure Rights Management の要件](../get-started/requirements-azure-rms.md)」と同じものを記載しています。 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] のより具体的なサポートおよびバージョン情報については、そのソースを参照してください。

|Azure RMS|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Exchange Online や SharePoint Online などの Microsoft Online Services および Office 365 で Information Rights Management (IRM) 機能をサポートします。<br /><br />さらに、Exchange Server、SharePoint Server などのオンプレミスの Microsoft サーバー製品、および Windows Server とファイル分類インフラストラクチャ (FCI) を実行するファイル サーバーもサポートします。|Exchange Server、SharePoint Server などのオンプレミスの Microsoft サーバー製品、および Windows Server とファイル分類インフラストラクチャ (FCI) を実行するファイル サーバーもサポートします。|
|組織と任意の組織のユーザー間の暗黙的な信頼関係を有効にします。 これは、ユーザーが [!INCLUDE[o365_1](../includes/o365_1_md.md)] または [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を使用しているか、ユーザーが個人用 RMS にサインアップしているときに、同じ組織または異なる組織のユーザー間で保護されたコンテンツを共有できることを意味します。|信頼関係は、信頼されたユーザー ドメイン (TUD) または Active Directory フェデレーション サービス (AD FS) を使用して作成したフェデレーションによる信頼関係を使用して、2 つの組織間で直接のポイントツーポイントの関係で明示的に定義される必要があります。|
|2 つの既定の権利ポリシー テンプレートが用意されています。これらのテンプレートは、コンテンツのアクセスを組織に制限します。一方のテンプレートは保護されたコンテンツの読み取り専用の表示を提供し、もう一方のテンプレートは保護されたコンテンツの書き込みまたは変更アクセス許可を提供します。<br /><br />ユーザーのサブセットのみが見ることのできる部門テンプレートを含む独自のカスタム テンプレートを作成することもできます。 詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。<br /><br />また、テンプレートで不十分な場合は、独自のアクセス許可セットを定義できます。|既定の権限ポリシー テンプレートがない場合は、作成してから配布する必要があります。 詳細については、「 [AD RMS ポリシー テンプレートに関する考慮事項](http://go.microsoft.com/fwlink/?LinkId=154765)」を参照してください。<br /><br />また、テンプレートで不十分な場合は、独自のアクセス許可セットを定義できます。|
|サポートされる Microsoft Office の最小バージョンは Office 2010 であり、このバージョンでは [RMS 共有アプリケーション](../rms-client/sharing-app-windows.md)が必要です。<br /><br />Microsoft Office for Mac:<br /><br />- Microsoft Office for Mac 2016: サポートされています<br /><br />- Microsoft Office for Mac 2011: サポートされていません|サポートされる最小バージョンは Microsoft Office is Office 2007 です。<br /><br />Microsoft Office for Mac:<br /><br />- Microsoft Office for Mac 2016: サポートされています<br /><br />- Microsoft Office for Mac 2011: サポートされています|
|Windows、Mac コンピューター、モバイル デバイス用の [RMS 共有アプリケーション](../rms-client/sharing-app-windows.md)をサポートします。<br /><br />また、RMS 共有アプリケーションは次の機能をサポートします。<br /><br />- 別組織のユーザーとの共有。<br /><br />- 電子メール通知。保護された添付ファイルをだれかが開こうとすると、送信者に通知されます。<br /><br />- ユーザー用のドキュメント追跡サイト。ドキュメントを失効させる機能があります。|Windows、Mac コンピューター、モバイル デバイス用の [RMS 共有アプリケーション](../rms-client/sharing-app-windows.md)をサポートします。 ただし、別組織のユーザーとの共有、電子メール通知、ドキュメント追跡サイトとユーザーがドキュメントを失効させる機能はサポートされていません。|
|RMS 共有アプリケーションを使用する場合、[ネイティブ保護または汎用的な保護](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)を使用して、すべてのファイルの種類を保護できます。<br /><br />他のアプリケーションについては、「[Azure RMS の要件: アプリケーション](../get-started/requirements-applications.md)」の表を参照してください。|RMS 共有アプリケーションを使用する場合、[ネイティブ保護または汎用的な保護](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)を使用して、すべてのファイルの種類を保護できます。<br /><br />他のアプリケーションについては、「[Azure RMS の要件: アプリケーション](../get-started/requirements-applications.md)」の表を参照してください。|
|Windows クライアントのサポートされる最小バージョンは Windows 7 です。|Windows クライアントのサポートされる最小バージョンは Windows Vista Service Pack 2 です。|
|モバイル デバイスのサポートには、Windows Phone、Android、iOS、および Windows RT が含まれます。<br /><br />Exchange ActiveSync IRM を使用する電子メール サポートが、このプロトコルをサポートするすべてのモバイル デバイス プラットフォーム上でもサポートされます。|モバイル デバイスのサポート対象には、Windows Phone、Android、iOS、Windows RT が含まれます。モバイル デバイスを使用するには、[Active Directory Rights Management サービスのモバイル デバイス拡張機能](http://technet.microsoft.com/library/dn673574.aspx)が必要です。<br /><br />Exchange ActiveSync IRM を使用する電子メール サポートが、このプロトコルをサポートするすべてのモバイル デバイス プラットフォーム上でサポートされます。|
|コンピューターとモバイル デバイス用の多要素認証 (MFA) をサポートします。<br /><br />詳細については、「[多要素認証 (MFA) と Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms)」を参照してください。|IIS が証明書を要求するように構成されている場合は、スマート カード認証をサポートします。|
|追加の構成なしで Cryptographic Mode 2 をサポートします。これによりキー長と暗号化アルゴリズムのセキュリティが強化されます。<br /><br />セキュリティに関する比較について質問がある場合は、この記事の「[署名と暗号化のための暗号化制御](#cryptographic-controls-for-signing-and-encryption)」セクションと「[AD RMS Cryptographic Modes (AD RMS の暗号化モード)](http://go.microsoft.com/fwlink/?LinkId=266659)」を参照してください。|既定で Cryptographic Mode 1 をサポートし、セキュリティを強化するために Cryptographic Mode 2 をサポートするには追加の構成が必要です。<br /><br />セキュリティに関する比較について質問がある場合は、この記事の「[署名と暗号化のための暗号化制御](#cryptographic-controls-for-signing-and-encryption)」セクションと「[AD RMS Cryptographic Modes (AD RMS の暗号化モード)](http://go.microsoft.com/fwlink/?LinkId=266659)」を参照してください。|
|AD RMS から、および必要な場合は AD RMS への、移行のサポート:<br /><br />- [AD RMS から Azure Rights Management への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [Azure Rights Management の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)|Azure RMS から、および Azure RMS への移行のサポート:<br /><br />- [Azure Rights Management の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)<br /><br />- [AD RMS から Azure Rights Management への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)|
|コンテンツを保護するには RMS ライセンスが必要です。 Azure RMS によって保護されたコンテンツを使用するのに、RMS ライセンスは必要ありません (別の組織のユーザーも含みます)。<br /><br />詳細については、「[Cloud subscriptions that support Azure RMS (Azure RMS をサポートするクラウド サブスクリプション)](../get-started/requirements-subscriptions.md)」を参照してください。|AD RMS によってコンテンツを保護し、保護されたコンテンツを使用するには、RMS ライセンスが必要です。<br /><br />AD RMS のライセンスの概要については、「 [Client Access Licenses and Management Licenses (クライアント管理ライセンスとアクセス ライセンス)](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) 」を参照してください。具体的な情報については、マイクロソフト パートナーまたはマイクロソフトの担当者に問い合わせてください。|

## 署名と暗号化のための暗号化制御
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]  は常に、すべての公開キーの暗号化に RSA 2048 を使用し、署名操作に SHA 256 を使用します。 これに対し、AD RMS は、RSA 1024 および RSA 2048 をサポートし、署名操作用に SHA 1 または SHA 256 をサポートします。

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] と AD RMS はどちらも対称暗号化に AES 128 を使用します。

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]  は、テナント キーが Microsoft によって作成および管理されるか (既定)、テナント キーを自分で管理する場合 (BYOK と呼ばれます)、FIPS 140-2 と互換性があります。 テナント キーの管理の詳細については、「[Azure Rights Management テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」を参照してください。

## 次のステップ
AD RMS から Azure RMS に移行する場合は、「[Migrating from AD RMS to Azure Rights Management (AD RMS から Azure Rights Management への移行)](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照してください。





<!--HONumber=Jul16_HO3-->


