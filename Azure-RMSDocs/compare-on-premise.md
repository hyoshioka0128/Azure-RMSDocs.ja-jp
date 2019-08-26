---
title: Azure Information Protection と AD RMS の比較 - AIP
description: Active Directory Rights Management サービス (AD RMS) を理解している、または以前にデプロイしたことがある場合、Azure Information Protection には機能や要件の面でどのような違いがあるのか疑問に思われるかもしれません。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a404bfbc36c8952214ed3c6814bab44368366170
ms.sourcegitcommit: 0d336e4b5386f4861db9492c7dce2ef0e8cf0d6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017621"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Azure Information Protection と AD RMS の比較

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Active Directory Rights Management サービス (AD RMS) を知っているか、以前にデプロイしたことがある場合、Azure Information Protection には情報保護ソリューションとしての機能や要件にどのような違いがあるのか疑問に思われるかもしれません。

Azure Information Protection の主な違いの一部:

- **サーバー インフラストラクチャは必要ない**: AD RMS で必要とされる追加サーバーと PKI 証明書が、Azure Information Protection では必要ありません。Microsoft Azure により処理されるためです。 そのため、クラウド ソリューションを短時間でデプロイして簡単に管理できます。

- **クラウド ベースの認証**:Azure Information Protection は、内部ユーザーと他の組織からのユーザー両方の認証に Azure AD を使用します。 つまり、ユーザーは内部ネットワークに接続されていなくても認証でき、保護されたコンテンツを他の組織のユーザーと共有することが容易になります。 多くの組織は、Azure サービスや Office 365 を使用しているため、Azure AD に既にユーザー アカウントがあります。 ただし、そうでない場合は、個人向け RMS サブスクリプションを使用して無料アカウントを作成するか、[Azure Information Protection への認証をサポートしているアプリケーション](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)用に、Microsoft アカウントを使用することができます。 これに対して、保護されたコンテンツを別の組織と AD RMS 共有するには、各組織に対して明示的な信頼を構成する必要があります。

- **モバイル デバイスの組み込みサポート**: Azure Information Protection がモバイルデバイスと Mac コンピューターをサポートするために、展開の変更は必要ありません。 AD RMS でこれらのデバイスをサポートするには、モバイル デバイス拡張機能をインストールし、フェデレーション用に AD FS を構成して、パブリック DNS サービスの追加レコードを作成する必要があります。

- **既定のテンプレート**: Azure Information Protection によって、自分の組織へのコンテンツのアクセスを制限する既定のテンプレートが自動的に作成されます。 これらのテンプレートを使用すると、機密データの保護をすぐに開始することが簡単になります。 AD RMS には既定のテンプレートはありません。

- **部門別テンプレート**: スコープ テンプレートとも呼ばれます。 Azure Information Protection では、ユーザーが作成する追加テンプレートに対する部門別テンプレートがサポートされています。 この構成では、ユーザーのサブセットを指定して、そのユーザーのクライアント アプリケーションで特定のテンプレートを表示することができます。 ユーザーに表示されるテンプレートの数を制限すると、異なるユーザー グループに対して定義した適切なポリシーを簡単に選択できるようになります。 AD RMS では、部門別テンプレートはサポートされていません。

- **ドキュメントの追跡と取り消し**: Azure Information Protection は Azure Information Protection クライアント (クラシック) でこれらの機能をサポートしていますが、AD RMS はサポートしていません。

- **分類とラベル付け**: Azure Information Protection は、分類、および必要に応じて保護を適用するラベルをサポートします。 これらの機能は、 [Azure Information Protection クライアント (クラシック) と Azure Information Protection 統合されたラベル付けクライアント](./rms-client/use-client.md#choose-which-azure-information-protection-client-to-use)で提供されます。 これらのクライアントを使用すると、分類とラベル付けを Office アプリケーション、ファイルエクスプローラー、PowerShell、およびオンプレミスデータストアのスキャナーと統合できます。 AD RMS は、これらの分類とラベル付け機能をサポートしていません。

さらに、Azure Information Protection はクラウド サービスであるため、オンプレミスのサーバー ベースのソリューションより速く新しい機能や修正を提供できます。 Windows Server では AD RMS の新機能は計画されていません。

その他の違いについては、次の表を使用して、並列比較を行うことができます。 セキュリティに関する比較について質問がある場合は、この記事の「[署名と暗号化のための暗号化制御](#cryptographic-controls-for-signing-and-encryption)」セクションを参照してください。

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|は、Microsoft Online services とオンプレミスの Microsoft サーバー製品の両方で information rights management (IRM) 機能をサポートしています。|は、オンプレミスの Microsoft サーバー製品および Exchange Online の information rights management (IRM) 機能をサポートしています。|
|認証に Azure AD を使用する組織とのドキュメントに対して、安全なコラボレーションを自動的に有効にします。|組織外のドキュメントで安全にコラボレーションするには、2 つの組織間の直接のポイントツーポイント関係で、認証の信頼を明示的に定義する必要があります。 信頼されたユーザー ドメイン (TUD)、または Active Directory フェデレーション サービス (AD FS) を使用して作成したフェデレーションによる信頼のいずれかを構成する必要があります。|
|認証の信頼関係がない場合、保護されたメール (必要に応じて、自動的に保護される Office ドキュメントの添付ファイルも一緒に) をユーザーに送信します。 ソーシャル プロバイダーによるフェデレーション、またはワンタイム パスコードと表示用の Web ブラウザーを使用すると、このシナリオが可能になります。|認証の信頼関係がない場合は、保護されたメールを送信しません。|
|では、Azure Information Protection クライアント (クラシック) と Azure Information Protection 統合されたラベル付けクライアントがサポートされています。|では、保護と消費アクティビティのために Azure Information Protection クライアント (クラシック) がサポートされています。 <br /><br />では、Azure Information Protection 統合されたラベル付けクライアントの使用のみがサポートされており、 [Active Directory Rights Management サービスモバイルデバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))をインストールする必要があります。
|コンピューターとモバイル デバイス用の多要素認証 (MFA) をサポートします。<br /><br />詳細については、「[多要素認証 (MFA) と Azure RMS](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection)」を参照してください。|IIS が証明書を要求するように構成されている場合は、スマート カード認証をサポートします。|
|では、暗号化モード2が既定でサポートされています。これは、キーの長さと暗号化アルゴリズムに推奨されるセキュリティレベルを提供するためです。|では暗号化モード1が既定でサポートされており、推奨されるセキュリティレベルで暗号化モード2をサポートするには追加の構成が必要です。<br /><br />詳細については、「 [AD RMS の暗号化モード](https://go.microsoft.com/fwlink/?LinkId=266659)」を参照してください。|
|コンテンツを保護するには、Office 365 の Azure Information Protection ライセンスまたは Azure Rights Management ライセンスが必要です。 <br /><br />Azure Information Protection で保護されたコンテンツを使用するには、ライセンスは必要ありません (別組織のユーザーも含まれます)。<br /><br />ライセンスの詳細 (P1 ライセンスと P2 ライセンスの違いを含む) については、Azure Information Protection サイトの[機能一覧](https://www.microsoft.com/cloud-platform/azure-information-protection-features)を参照してください。|AD RMS によってコンテンツを保護し、保護されたコンテンツを使用するには、RMS ライセンスが必要です。<br /><br />ライセンスの詳細については、「[クライアントアクセスライセンス」および](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx)「一般的な情報の管理ライセンス」を参照してください。ただし、特定の情報については、microsoft パートナーまたは microsoft 担当者にお問い合わせください。|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>署名と暗号化のための暗号化制御
Azure Information Protection は既定で、すべての公開キーの暗号化に RSA 2048 を、署名操作に SHA 256 を使用します。 これに対し、AD RMS は、RSA 1024 および RSA 2048 をサポートし、署名操作用に SHA 1 または SHA 256 をサポートします。

Azure Information Protection と AD RMS のいずれも対称暗号化に AES 128 を使用しています。

Azure Information Protection は、テナント キーのサイズが 2048 ビットである場合に FIPS 140-2 に準拠しています。Azure Rights Management サービスがアクティブ化されたときは、これが既定です。 

暗号化の制御の詳細については、「[Azure RMS で使用される暗号化の制御: アルゴリズムとキーの長さ](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)」を参照してください。


## <a name="next-steps"></a>次の手順
デバイスのサポートや最小バージョンなど、Azure Information Protection を使用するための要件の詳細については、「 [Azure Information Protection の要件](requirements.md)」を参照してください。

AD RMS から Azure Information Protection に移行する場合は、「 [AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

次の Faq をご確認ください。
- [Azure Information Protection と Microsoft Information Protection の違いは何ですか。](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)
- [Azure Information Protection と Azure Rights Management の違いは何ですか。](faqs.md#whats-the-difference-between-azure-information-protection-and-azure-rights-management)

