---
title: Azure Information Protection と AD RMS の比較 - AIP
description: Active Directory Rights Management サービス (AD RMS) を理解している、または以前にデプロイしたことがある場合、Azure Information Protection には機能や要件の面でどのような違いがあるのか疑問に思われるかもしれません。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8e7cce8032a713f77f40714650fb37bfae257ec4
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383909"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Azure Information Protection と AD RMS の比較

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 *

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Active Directory Rights Management サービス (AD RMS) を理解している、または以前にデプロイしたことがある場合、Azure Information Protection には、情報保護ソリューションとして機能や要件の面でどのような違いがあるのか疑問に思われるかもしれません。

Azure Information Protection の主な相違点を次に示します。

|差  |説明  |
|---------|---------|
|**サーバー インフラストラクチャは必要ありません。**     |  AD RMS で必要とされる追加サーバーと PKI 証明書が、Azure Information Protection では必要ありません。Microsoft Azure により処理されるためです。 <br><br>そのため、クラウド ソリューションを短時間でデプロイして簡単に管理できます。       |
|**クラウドベースの認証**     |  Azure Information Protection は、内部ユーザーと他の組織からのユーザー両方の認証に Azure AD を使用します。 <br><br>つまり、ユーザーは内部ネットワークに接続されていなくても認証でき、保護されたコンテンツを他の組織のユーザーと共有することが容易になります。 <br><br>多くの組織は、Azure サービスを実行しているか Microsoft 365 を持っているため、Azure AD にユーザーアカウントを既に持っています。 ただし、そうでない場合は、個人向け RMS サブスクリプションを使用して無料アカウントを作成するか、[Azure Information Protection への認証をサポートしているアプリケーション](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)用に、Microsoft アカウントを使用することができます。 <br><br>これに対して、保護されたコンテンツを別の組織と AD RMS 共有するには、各組織に対して明示的な信頼を構成する必要があります。       |
|**モバイルデバイスの組み込みサポート**     | Azure Information Protection がモバイルデバイスと Mac コンピューターをサポートするために、展開の変更は必要ありません。 <br><br>AD RMS でこれらのデバイスをサポートするには、モバイル デバイス拡張機能をインストールし、フェデレーション用に AD FS を構成して、パブリック DNS サービスの追加レコードを作成する必要があります。        |
|**既定のテンプレート**     |  Azure Information Protection によって、自分の組織へのコンテンツのアクセスを制限する既定のテンプレートが自動的に作成されます。 これらのテンプレートを使用すると、機密データの保護をすぐに開始することが簡単になります。 <br><br>AD RMS には既定のテンプレートはありません。       |
|**部門別テンプレート**     | スコープ テンプレートとも呼ばれます。 Azure Information Protection では、ユーザーが作成する追加テンプレートに対する部門別テンプレートがサポートされています。 <br><br>この構成では、ユーザーのサブセットを指定して、そのユーザーのクライアント アプリケーションで特定のテンプレートを表示することができます。 ユーザーに表示されるテンプレートの数を制限すると、異なるユーザー グループに対して定義した適切なポリシーを簡単に選択できるようになります。 <br><br>AD RMS では、部門別テンプレートはサポートされていません。        |
|**ドキュメントの追跡と取り消し**     |  Azure Information Protection は、これらの機能を Azure Information Protection クラシッククライアントでのみサポートしていますが、AD RMS はまったくサポートされていません。       |
|**分類とラベル付け**     | Azure Information Protection は、分類、および必要に応じて保護を適用するラベルをサポートします。 これらの機能には、 [AIP 統合ラベルと従来のクライアント](rms-client/use-client.md#choose-your-windows-labeling-solution)の両方が用意されています。 <br><br>AIP クライアントを使用して、Office アプリケーション、ファイルエクスプローラー、PowerShell、およびオンプレミスのデータストア用のスキャナーとの分類とラベル付けを統合します。 <br><br>   AD RMS は、これらの分類とラベル付け機能をサポートしていません。        |
| | |

さらに、Azure Information Protection はクラウド サービスであるため、オンプレミスのサーバー ベースのソリューションより速く新しい機能や修正を提供できます。 Windows Server では AD RMS の新機能は計画されていません。


### <a name="detailed-comparison-between-aip-and-ad-rms"></a>AIP と AD RMS の詳細な比較

詳細については、次の表を参照してください。 

セキュリティに関する比較について質問がある場合は、この記事の「[署名と暗号化のための暗号化制御](#cryptographic-controls-for-signing-and-encryption)」セクションを参照してください。


|差|Azure Information Protection|AD RMS|
|----------|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
| **Information Rights Management (IRM)**|では、Microsoft Online services とオンプレミスの Microsoft サーバー製品の両方で IRM 機能がサポートされています。|では、オンプレミスの Microsoft サーバー製品と Exchange Online の IRM 機能がサポートされています。|
| **セキュリティで保護されたコラボレーション**|認証に Azure AD を使用する組織とのドキュメントに対して、安全なコラボレーションを自動的に有効にします。|組織外のドキュメントで安全にコラボレーションするには、2 つの組織間の直接のポイントツーポイント関係で、認証の信頼を明示的に定義する必要があります。 <br><br>信頼されたユーザー ドメイン (TUD)、または Active Directory フェデレーション サービス (AD FS) を使用して作成したフェデレーションによる信頼のいずれかを構成する必要があります。|
| **保護された電子メール**|認証の信頼関係がない場合、保護されたメール (必要に応じて、自動的に保護される Office ドキュメントの添付ファイルも一緒に) をユーザーに送信します。 <br><br>ソーシャル プロバイダーによるフェデレーション、またはワンタイム パスコードと表示用の Web ブラウザーを使用すると、このシナリオが可能になります。|認証の信頼関係がない場合は、保護されたメールを送信しません。|
| **クライアントサポート**|では、保護と消費の両方のアクティビティについて、AIP 統合ラベルとクラシッククライアントの両方がサポートされています。 |では、AIP 統合ラベルクライアントの使用のみがサポートされており、 [Active Directory Rights Management サービスモバイルデバイス拡張機能](./active-directory-rights-manage-mobile-device.md)をインストールする必要があります。 <br><br>では、保護と消費の両方のアクティビティに対して AIP classic クライアントがサポートされています。 
| **多要素認証 (MFA)**|では、コンピューターとモバイルデバイスの MFA がサポートされています。<br /><br />詳細については、「[多要素認証 (MFA) と Azure RMS](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection)」を参照してください。|IIS が証明書を要求するように構成されている場合は、スマート カード認証をサポートします。|
| **暗号化モード**|では、暗号化モード2が既定でサポートされています。これは、キーの長さと暗号化アルゴリズムに推奨されるセキュリティレベルを提供するためです。|では、暗号化モード1が既定でサポートされています。また、推奨されるセキュリティレベルに対して暗号化モード2をサポートするには、追加の構成が必要です。<br /><br />詳細については、「[AD RMS の暗号化モード](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh867439(v=ws.10))」を参照してください。|
| **ライセンス**|コンテンツを保護するには、Microsoft 365 の Azure Information Protection ライセンスまたは Azure Rights Management ライセンスが必要です。 <br /><br />AIP によって保護されているコンテンツを使用するためのライセンスは必要ありません (別の組織のユーザーが含まれます)。<br /><br />ライセンスの詳細 (P1 ライセンスと P2 ライセンスの違いを含む) については、Azure Information Protection サイトの [機能一覧](https://www.microsoft.com/cloud-platform/azure-information-protection-features) を参照してください。|AD RMS によってコンテンツを保護し、保護されたコンテンツを使用するには、RMS ライセンスが必要です。<br /><br />ライセンスの詳細については、「 [クライアントアクセスライセンス」および](https://www.microsoft.com/Licensing/product-licensing/client-access-license.aspx) 「一般的な情報の管理ライセンス」を参照してください。ただし、特定の情報については、microsoft パートナーまたは microsoft 担当者にお問い合わせください。|
| | | |

## <a name="cryptographic-controls-for-signing-and-encryption"></a>署名と暗号化のための暗号化制御
Azure Information Protection は既定で、すべての公開キーの暗号化に RSA 2048 を使用し、署名操作に SHA 256 を使用します。 これに対し、AD RMS は、RSA 1024 および RSA 2048 をサポートし、署名操作用に SHA 1 または SHA 256 をサポートします。

Azure Information Protection と AD RMS のいずれも対称暗号化に AES 128 を使用しています。

Azure Information Protection は、テナント キーのサイズが 2048 ビットである場合に FIPS 140-2 に準拠しています。Azure Rights Management サービスがアクティブ化されたときは、これが既定です。 

暗号化の制御の詳細については、「[Azure RMS で使用される暗号化の制御: アルゴリズムとキーの長さ](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)」を参照してください。


## <a name="next-steps"></a>次のステップ
デバイスのサポートや最小バージョンなど、Azure Information Protection を使用するための要件の詳細については、「 [Azure Information Protection の要件](requirements.md)」を参照してください。

AD RMS から Azure Information Protection に移行する場合は、「 [AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

[Active Directory Rights Management サービスモバイルデバイス拡張機能](./active-directory-rights-manage-mobile-device.md)の概要」をご覧ください。 

次の Faq をご確認ください。
- [Azure Information Protection と Microsoft Information Protection の違いは何ですか。](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)
- [Azure Information Protection と Azure Rights Management の違いは何ですか。](faqs.md#whats-the-difference-between-azure-information-protection-and-azure-rights-management)