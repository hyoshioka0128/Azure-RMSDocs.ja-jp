---
title: Azure Information Protection と AD RMS の比較 - AIP
description: Active Directory Rights Management サービス (AD RMS) を理解している、または以前にデプロイしたことがある場合、Azure Information Protection には機能や要件の面でどのような違いがあるのか疑問に思われるかもしれません。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3e1de24471b89ac0081f5f5e93a25baf1d798e34
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181924"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Azure Information Protection と AD RMS の比較

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Active Directory Rights Management サービス (AD RMS) を知っているか、以前にデプロイしたことがある場合、Azure Information Protection には情報保護ソリューションとしての機能や要件にどのような違いがあるのか疑問に思われるかもしれません。

Azure Information Protection の主な違いの一部:

- **サーバー インフラストラクチャは必要ない**: AD RMS で必要とされる追加サーバーと PKI 証明書が、Azure Information Protection では必要ありません。Microsoft Azure により処理されるためです。 そのため、クラウド ソリューションを短時間でデプロイして簡単に管理できます。

- **クラウド ベースの認証**:Azure Information Protection は、内部ユーザーと他の組織からのユーザー両方の認証に Azure AD を使用します。 つまり、内部ネットワークに接続されていないモバイル ユーザーでも認証でき、保護されたコンテンツを他の組織のユーザーと簡単に共有できます。 多くの組織は、Azure サービスや Office 365 を使用しているため、Azure AD に既にユーザー アカウントがあります。 ただし、そうでない場合は、個人向け RMS サブスクリプションを使用して無料アカウントを作成するか、[Azure Information Protection への認証をサポートしているアプリケーション](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)用に、Microsoft アカウントを使用することができます。 AD RMS で保護されたコンテンツを別の組織と共有するには、各組織との明示的な信頼関係を構成する必要があります。

- **モバイル デバイスの組み込みサポート**: Azure RMS でモバイル デバイスや Mac コンピューターをサポートする場合でも、デプロイを変更する必要はありません。 AD RMS でこれらのデバイスをサポートするには、モバイル デバイス拡張機能をインストールし、フェデレーション用に AD FS を構成して、パブリック DNS サービスの追加レコードを作成する必要があります。

- **既定のテンプレート**: Azure Information Protection では、保護サービスをアクティブ化すると既定のテンプレートが作成されるため、すぐに簡単に重要なデータの保護を開始できます。 AD RMS には既定のテンプレートはありません。

- **部門別テンプレート**: スコープ テンプレートとも呼ばれます。 Azure Information Protection では、ユーザーが作成する追加テンプレートに対する部門別テンプレートがサポートされています。 この構成では、ユーザーのサブセットを指定して、そのユーザーのクライアント アプリケーションで特定のテンプレートを表示することができます。 ユーザーに表示されるテンプレートの数を制限すると、異なるユーザー グループに対して定義した適切なポリシーを簡単に選択できるようになります。 AD RMS では、部門別テンプレートはサポートされていません。

- **ドキュメントの追跡と取り消し**: Azure Information Protection は Azure Information Protection クライアントでこれらの機能をサポートしていますが、AD RMS ではサポートされていません。

- **分類とラベル付け**: Azure Information Protection は、Office アプリケーションおよびエクスプローラーと統合されている Azure Information Protection クライアントでこれらの機能をサポートしていますが、AD RMS ではサポートされていません。 


さらに、Azure Information Protection はクラウド サービスであるため、オンプレミスのサーバー ベースのソリューションより速く新しい機能や修正を提供できます。 Windows Server では AD RMS の新機能は計画されていません。

詳細および他の相違点については、次の表を使用して、Azure Information Protection と AD RMS の機能と利点を並べて比較することができます。 セキュリティに関する比較について質問がある場合は、この記事の「[署名と暗号化のための暗号化制御](#cryptographic-controls-for-signing-and-encryption)」セクションを参照してください。

> [!NOTE]
> 簡単に比較できるようにするために、ここでの一部の情報は「[Azure Information Protection の要件](requirements.md)」と同じものを記載しています。 Azure Rights Management のより具体的なサポートおよびバージョン情報については、そのソースを参照してください。

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Exchange Online や SharePoint Online などの Microsoft Online Services および Office 365 で Information Rights Management (IRM) 機能をサポートします。<br /><br />さらに、Exchange Server、SharePoint Server などのオンプレミスの Microsoft サーバー製品、および Windows Server とファイル分類インフラストラクチャ (FCI) を実行するファイル サーバーもサポートします。|Exchange Server、SharePoint Server などのオンプレミスの Microsoft サーバー製品、および Windows Server とファイル分類インフラストラクチャ (FCI) を実行するファイル サーバーもサポートします。|
|認証に Azure AD を使用する組織とのドキュメントに対して、安全なコラボレーションを自動的に有効にします。 これは、組織が内部的に、または他の組織と共有するドキュメントを保護できることを意味します。|組織外のドキュメントで安全にコラボレーションするには、2 つの組織間の直接のポイントツーポイント関係で、認証の信頼を明示的に定義する必要があります。 信頼されたユーザー ドメイン (TUD)、または Active Directory フェデレーション サービス (AD FS) を使用して作成したフェデレーションによる信頼のいずれかを構成する必要があります。|
|認証の信頼関係がない場合、保護されたメール (必要に応じて、自動的に保護される Office ドキュメントの添付ファイルも一緒に) をユーザーに送信します。 ソーシャル プロバイダーによるフェデレーション、またはワンタイム パスコードと表示用の Web ブラウザーを使用すると、このシナリオが可能になります。|認証の信頼関係がない場合は、保護されたメールを送信しません。|
|コンテンツのアクセスをユーザー自身の組織に制限する既定の保護テンプレートが用意されています。一方のテンプレートでは保護されたコンテンツの読み取り専用の表示が提供され、もう一方のテンプレートでは保護されたコンテンツの書き込みまたは変更アクセス許可が提供されます。<br /><br />ユーザーのサブセットのみが見ることのできる部門テンプレートを含む独自のカスタム テンプレートを作成することもできます。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。<br /><br />また、テンプレートで不十分な場合は、独自のアクセス許可セットを定義できます。|既定のテンプレートはありません。独自のテンプレートを作成してから配布する必要があります。 詳細については、「[AD RMS ポリシー テンプレートに関する考慮事項](https://go.microsoft.com/fwlink/?LinkId=154765)」をご覧ください。<br /><br />また、テンプレートで不十分な場合は、独自のアクセス許可セットを定義できます。|
|サポートされる Microsoft Office の最小バージョンは Office 2010 であり、このバージョンでは [Azure Information Protection クライアント](./rms-client/aip-client.md)が必要です。|サポートされる Microsoft Office の最小バージョンは、Office 2010 です。|
|Windows 用、iOS 用、および Android 用 [Azure Information Protection クライアント](./rms-client/aip-client.md)をサポートしています。 RMS 共有アプリにより、Mac コンピューターは引き続きサポートされます。<br /><br />また、Azure Information Protection クライアントには次のものが含まれます。<br /><br />- 別組織のユーザーとの共有。<br /><br />- ユーザー用のドキュメント追跡サイト。ドキュメントを失効させる機能があります。|Windows 用、iOS 用、および Android 用 [Azure Information Protection クライアント](./rms-client/aip-client.md)をサポートしています。 RMS 共有アプリにより、Mac コンピューターは引き続きサポートされます。 ただし、別組織のユーザーとの共有、ドキュメント追跡サイトとユーザーがドキュメントを失効させる機能はサポートされていません。|
|Azure Information Protection クライアントを使用すると、ほとんどの[ファイルの種類](./rms-client/client-admin-guide-file-types.md)を分類し、保護することができます。<br /><br />他のアプリケーションについては、「[Azure Rights Management データ保護をサポートするアプリケーション](./requirements-applications.md)」の表を参照してください。|Azure Information Protection クライアントを使用すると、ほとんどの[ファイルの種類](./rms-client/client-admin-guide-file-types.md)を保護することができます。<br /><br />他のアプリケーションについては、「[Azure Rights Management データ保護をサポートするアプリケーション](./requirements-applications.md)」の表を参照してください。|
|Windows クライアントのサポートされる最小バージョンは Windows 7 SP1 です。|Windows クライアントのサポートされる最小バージョンは Windows 7 SP1 です。|
|モバイル デバイスのサポートには、Windows 10 Mobile、Android、および iOS が含まれます。<br /><br />Exchange ActiveSync IRM を使用する電子メール サポートが、このプロトコルをサポートするすべてのモバイル デバイス プラットフォーム上でもサポートされます。|モバイル デバイスでは、Windows 10 Mobile、Android、iOS などがサポートされます。また、[Active Directory Rights Management サービスのモバイル デバイス拡張機能](https://technet.microsoft.com/library/dn673574.aspx)が必要です。<br /><br />Exchange ActiveSync IRM を使用する電子メール サポートが、このプロトコルをサポートするすべてのモバイル デバイス プラットフォーム上でサポートされます。|
|コンピューターとモバイル デバイス用の多要素認証 (MFA) をサポートします。<br /><br />詳細については、「[多要素認証 (MFA) と Azure RMS](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection)」を参照してください。|IIS が証明書を要求するように構成されている場合は、スマート カード認証をサポートします。|
|追加の構成なしで Cryptographic Mode 2 をサポートします。これによりキー長と暗号化アルゴリズムのセキュリティが強化されます。<br /><br />詳細については、この記事の「[署名と暗号化のための暗号化制御](#cryptographic-controls-for-signing-and-encryption)」セクションと、「[AD RMS の暗号化モード](https://go.microsoft.com/fwlink/?LinkId=266659)」をご覧ください。|既定で Cryptographic Mode 1 をサポートし、セキュリティを強化するために Cryptographic Mode 2 をサポートするには追加の構成が必要です。<br /><br />詳細については、この記事の「[署名と暗号化のための暗号化制御](#cryptographic-controls-for-signing-and-encryption)」セクションと、「[AD RMS の暗号化モード](https://go.microsoft.com/fwlink/?LinkId=266659)」をご覧ください。|
|AD RMS から、および必要な場合は AD RMS への、移行のサポート:<br /><br />- [AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [Azure Information Protection の使用停止と非アクティブ化](decommission-deactivate.md)|Azure Information Protection からの移行と Azure Information Protection への移行をサポートします。<br /><br />- [Azure Rights Management の使用停止と非アクティブ化](decommission-deactivate.md)<br /><br />- [AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)|
|コンテンツを保護するには、Azure Information Protection ライセンスまたは Azure Rights Management ライセンスと Office 365 が必要です。 Azure Information Protection で保護されたコンテンツを使用するには、ライセンスは必要ありません (別組織のユーザーも含まれます)。<br /><br />詳細については、Azure Information Protection サイトの[機能一覧](https://www.microsoft.com/cloud-platform/azure-information-protection-features)に関するページを参照してください。|AD RMS によってコンテンツを保護し、保護されたコンテンツを使用するには、RMS ライセンスが必要です。<br /><br />AD RMS のライセンスの概要については、「 [Client Access Licenses and Management Licenses (クライアント管理ライセンスとアクセス ライセンス)](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) 」を参照してください。具体的な情報については、マイクロソフト パートナーまたはマイクロソフトの担当者に問い合わせてください。|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>署名と暗号化のための暗号化制御
Azure Information Protection は既定で、すべての公開キーの暗号化に RSA 2048 を、署名操作に SHA 256 を使用します。 これに対し、AD RMS は、RSA 1024 および RSA 2048 をサポートし、署名操作用に SHA 1 または SHA 256 をサポートします。

Azure Information Protection と AD RMS のいずれも対称暗号化に AES 128 を使用しています。

Azure Information Protection は、テナント キーのサイズが 2048 ビットである場合に FIPS 140-2 に準拠しています。Azure Rights Management サービスがアクティブ化されたときは、これが既定です。 

暗号化の制御の詳細については、「[Azure RMS で使用される暗号化の制御: アルゴリズムとキーの長さ](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)」を参照してください。


## <a name="next-steps"></a>次の手順
AD RMS から Azure Information Protection に移行する場合は、「[AD RMS から Azure Information Protection に移行する](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。


