---
title: Azure Rights Management の保護の概要 - AIP
description: Azure Information Protection が使用する保護テクノロジである Azure Rights Management (Azure RMS) に関する情報。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aeeebcd7-6646-4405-addf-ee1cc74df5df
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: f23d9da0aae7d3cae681c829187f8371c84ca167
ms.sourcegitcommit: ee20112ada09165b185d9c0c9e7f1179fc39e7cf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/21/2021
ms.locfileid: "98659087"
---
# <a name="what-is-azure-rights-management"></a>Azure Rights Management とは

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連する内容**: [AIP の統合ラベル付けクライアントとクラシック クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Rights Management (Azure RMS) とは、[Azure Information Protection](what-is-information-protection.md) が使用する保護テクノロジです。

Azure RMS はクラウドベースの保護サービスであり、暗号化、ID、承認のポリシーを使用して、携帯電話、タブレット、PC などの複数のデバイスでファイルやメールを保護できます。 保護の設定は、組織の境界から外に出たときでもデータと共に保持されるので、組織の内と外の両方でコンテンツの保護が維持されます。

次の図は、Azure RMS により Microsoft 365 およびオンプレミスのサーバーとサービスに対して保護がどのように提供されるのかを示したものです。 また、保護は Windows、macOS、iOS、Android を実行する一般的なエンドユーザー デバイスによってもサポートされます。

![Azure RMS のしくみ](./media/AzRMS_elements.png)

Azure RMS は、Microsoft 365 サブスクリプションまたは Azure Information Protection 用のサブスクリプションで使用します。 個々のサブスクリプションの種類とサポートされている機能の詳細については、「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection/)」サイトを参照してください。

### <a name="sample-azure-rms-use-case"></a>Azure RMS のサンプル ユース ケース

従業員は、ドキュメントをパートナー企業にメールで送信したり、クラウド ドライブに保存したりすることがあります。

Azure RMS の永続的な保護を使用すると、会社のデータを保護するのに役立ち、法令遵守、法的証拠開示要件、または情報管理のベスト プラクティスのために法的に要求される場合もあります。

Azure RMS を使用すると、承認されたユーザーおよび検索やインデックス作成などのサービスが、保護されているデータの読み取りと検査を引き続き実行できることが保証されます。

承認されたユーザーとサービスに対して継続的なアクセスを保証することは ("データに対する推論" とも呼ばれます)、組織のデータの制御を維持するうえで重要な要素です。 ピアツーピアの暗号化を使用する他の情報保護ソリューションでは、このような機能を簡単に実現できない場合があります。 

## <a name="business-problems-solved-by-azure-rights-management"></a>Azure Rights Management が解決するビジネス上の問題

次の一覧と表を使用して、文書や電子メールの保護に関して組織が抱えるビジネス上の要件や問題、および Azure Rights Management テクノロジでそのニーズに対処する方法を確認してください。

- [保護機能](#protection-features)
- [コラボレーション機能](#collaboration-features)
- [プラットフォーム サポート機能](#platform-support-features)
- [インフラストラクチャ機能](#infrastructure-features)

> [!TIP]
> オンプレミス版の Rights Management である Active Directory Rights Management サービス (AD RMS) の知識がある場合は、「[Azure Rights Management と AD RMS を比較する](compare-on-premise.md)」の比較表も参照してください。

### <a name="protection-features"></a>保護機能

|機能  |説明  |
|---------|---------|
|**複数のファイルの種類を保護する**     | Rights Management の初期の実装では、Rights Management の組み込みの保護を使用して、Office ファイルのみを保護できました。 </br></br>Azure Information Protection では、サポートされるファイルの種類が追加されています。 詳しくは、[サポートされるファイルの種類](rms-client/clientv2-admin-guide-file-types.md)に関する記事を参照してください。         |
|**あらゆる場所のファイルを保護する**。 | ファイルが[保護](./rms-client/clientv2-classify-protect.md)されると、クラウド ストレージ サービスなど、IT の制御下にないストレージにファイルが保存またはコピーされる場合でも、その保護は維持されます。|
|     |         |


### <a name="collaboration-features"></a>コラボレーション機能

|機能  |説明  |
|---------|---------|
|**情報を安全に共有する**     |  [保護されたファイル](./rms-client/clientv2-classify-protect.md)は、メールへの添付や SharePoint サイトへのリンクなど、他のユーザーと安全に共有できます。 </br></br> 機密情報がメール メッセージ内にある場合は、メールを保護するか、または Outlook の **[転送不可]** オプションを使用します。       |
|**企業間のコラボレーションをサポートする**     |  Azure Rights Management はクラウド サービスであるため、保護されたコンテンツを他の組織と共有する前に、信頼関係を明示的に構成する必要がありません。 </br></br>Microsoft 365 または Azure AD ディレクトリを既に導入している他の組織とのコラボレーションは、自動的にサポートされます。 </br></br>Microsoft 365 または Azure AD ディレクトリを導入していない組織の場合は、ユーザーは無料の[個人用 RMS](rms-for-individuals.md) サブスクリプションにサインアップするか、[サポートされているアプリケーション](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)の Microsoft アカウントを使用することができます。       |
| | |

> [!TIP]
> メール メッセージ全体を保護するのではなく、保護されたファイルを添付すると、メールのテキストを暗号化されていない状態にしておくことができます。 
>
> たとえば、メールが組織外に送信される場合、初回使用時の指示を含めることができます。 保護されたファイルを添付した場合、基本的な指示はだれでも読むことができますが、メールまたはドキュメントが他の人に転送されたとしても、承認されているユーザーだけがドキュメントを開くことができます。

### <a name="platform-support-features"></a>プラットフォーム サポート機能

Azure RMS により、次のような広範なプラットフォームとアプリケーションがサポートされます。

|機能  |説明  |
|---------|---------|
|**一般的に使用されるデバイス** </br>Windows コンピューターだけではありません     | 次のような[クライアント デバイス](requirements.md#client-devices): </br></br>- Windows コンピューターと携帯電話 </br>- Mac コンピューター </br>- iOS タブレットと携帯電話 </br>- Android タブレットと携帯電話        |
|**オンプレミスのサービス**     | Azure Rights Management は、[Office 365 とシームレスに](office-apps-services-support.md)連携するだけでなく、[RMS コネクタ](deploy-rms-connector.md)をデプロイして、次のオンプレミス サービスでも使用します </br></br>- Exchange Server </br>- SharePoint Server </br>- ファイル分類インフラストラクチャを実行する Windows Server        |
|**アプリケーションの拡張性**     |Azure Rights Management は Microsoft Office のアプリケーションやサービスと緊密に統合されており、[Azure Information Protection クライアント](./rms-client/use-client.md )を使うことで、他のアプリケーションにもサポートを広げることができます。 </br></br>[Microsoft Information Protection SDK](/information-protection/develop/) により、Azure Information Protection をサポートするカスタム アプリケーションを作成するための API が社内開発者やソフトウェア ベンダーに提供されます。 </br></br>詳しくは、「[Rights Management API をサポートするその他のアプリケーション](api-support.md)」をご覧ください。         |
| | |

### <a name="infrastructure-features"></a>インフラストラクチャ機能

Azure RMS により、IT 部門とインフラストラクチャ組織をサポートするための次の機能が提供されます。

- [シンプルで柔軟なポリシーを作成する](#create-simple-and-flexible-policies)
- [簡単なアクティブ化](#easy-activation)
- [監査と監視のサービス](#auditing-and-monitoring-services)
- [組織全体でスケーリングする能力](#ability-to-scale-across-your-organization)
- [IT によるデータの制御の維持](#maintain-it-control-over-data)

> [!NOTE]
> 組織では常に、以前に Azure Rights Management によって保護されていたコンテンツへのアクセスを失わずに、Azure Rights Management サービスの使用を停止できます。 
> 
> 詳細については、[Azure Rights Management の使用停止と非アクティブ化](decommission-deactivate.md)に関する記事を参照してください。 
> 

#### <a name="create-simple-and-flexible-policies"></a>シンプルで柔軟なポリシーを作成する

カスタマイズされた保護テンプレートを使用すると、管理者はポリシーを簡単に適用でき、ユーザーは適切なレベルの保護を各ドキュメントに適用してアクセスを組織内のユーザーに制限できます。 

たとえば、全社的戦略が記載された書類を全従業員が共有する場合、社内の全従業員に読み取り専用ポリシーを適用します。 財務報告など、より機密性の高いドキュメントについては、アクセスを経営幹部にのみ制限します。

ラベル付け管理センターでラベル付けポリシーを構成します。

- **統合ラベル付けクライアント**:Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センター、または Microsoft 365 セキュリティ/コンプライアンス センターを使用します。

    詳細については、[Microsoft 365 の秘密度ラベルのドキュメント](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do)を参照してください。        

- **クラシック クライアント**:Azure portal を使用します。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。      


#### <a name="easy-activation"></a>簡単なアクティブ化

新しいサブスクリプションの場合は、自動的にアクティブ化されます。 既存のサブスクリプションの場合、[Rights Management サービスをアクティブ化する](activate-service.md)ために必要なのは、管理ポータルでの数回のクリック、または 2 つの PowerShell コマンドだけです。

#### <a name="auditing-and-monitoring-services"></a>監査と監視のサービス

保護されたファイルが組織外部に出た後も、ファイルの[使用状況を監査および監視します](log-analyze-usage.md)。 

たとえば、Contoso 社の従業員が Fabrikam 社の 3 人のユーザーと共同プロジェクトで作業している場合、Fabrikam 社のパートナーに対して、保護されていて "*読み取り専用*" に制限されたドキュメントを送信することがあります。 

Azure RMS の監査機能は次の情報を提供できます。

- Fabrikam のパートナーはドキュメントを開いたかどうか、それはいつか。 

- 指定されていなかった他のユーザーがドキュメントを開こうとしたかどうか、そして失敗したかどうか。 これは、メールが転送された場合、または共有の場所に保存された場合に発生する可能性があります。

> [!NOTE]
> クラシック クライアント ユーザーのみの場合、[ドキュメント追跡サイト](./rms-client/client-track-revoke.md)を使うと、ユーザーや管理者は、保護されたドキュメントを追跡したり、必要な場合は、アクセスを取り消したりすることができます。
> 

#### <a name="ability-to-scale-across-your-organization"></a>組織全体でスケーリングする能力

Azure Rights Management はクラウド サービスとして動作し、Azure の柔軟性を活かしてスケールアップおよびスケールアウトするため、追加のオンプレミス サーバーをプロビジョニングまたはデプロイする必要がありません。

#### <a name="maintain-it-control-over-data"></a>IT によるデータの制御の維持

組織は、次のような IT 管理機能を利用できます。

|機能  |説明  |
|---------|---------|
|**テナント キーの管理**    | Bring Your Own Key (BYOK) や二重キー暗号化 (DKE) などのテナント キー管理ソリューションを使用します。 <br><br>詳細については、以下を参照してください。 <br>- [AIP テナント キーの計画と実装](plan-implement-tenant-key.md) <br>- [Microsoft 365 ドキュメントの DKE](/microsoft-365/compliance/double-key-encryption).|
|**監査と使用状況のログ**    |   監査と[使用状況のログ](log-analyze-usage.md)の機能を使用して、ビジネス分析情報の分析、悪用の監視、情報漏えいのフォレンジック分析を実行します。      |
|**アクセスの委任**     |  [スーパー ユーザー機能](configure-super-users.md)でアクセスを委任し、退職者によって保護されたドキュメントであっても、IT 部門が保護されたコンテンツに常にアクセスできるようにします。 </br> これに対し、ピア ツー ピアの暗号化ソリューションでは、企業データにアクセスできなくなるおそれがあります。       |
|**Active Directory の同期**     |   Azure AD Connect などの[ハイブリッド ID ソリューション](/azure/active-directory/hybrid/)を使用して、オンプレミスの Active Directory アカウントに対して共通の ID をサポートするために [Azure RMS が必要とするディレクトリの属性のみ](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms)を同期します。      |
|**シングル サインオン**     | AD FS を使用して、パスワードをクラウドにレプリケートすることなくシングル サインオンを有効にします。        |
|**AD RMS からの移行** |Active Directory Rights Management サービス (AD RMS) をデプロイした場合は、以前に AD RMS によって保護されていたデータへのアクセスを失わずに [Azure Rights Management サービスに移行](migrate-from-ad-rms-to-azure-rms.md)します。 |
| | |

## <a name="security-compliance-and-regulatory-requirements"></a>セキュリティ、コンプライアンス、および規制の要件
Azure Rights Management では、セキュリティ、コンプライアンス、規制に関する次の要件をサポートします。

- **業界標準の暗号化を使用し、FIPS 140-2 をサポートします。** 詳細については、「[Cryptographic controls used by Azure RMS: Algorithms and key lengths (Azure RMS で使用される暗号化の制御: アルゴリズムとキーの長さ)](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)」を参照してください。

- **nCipher nShield ハードウェア セキュリティ モジュール (HSM) をサポート** し、テナント キーを Microsoft Azure データ センターに保存します。 

    自社の地域でのみキーを使用できるように、Azure Rights Management では北米、EMEA (欧州、中東およびアフリカ)、およびアジアのデータ センターで独立したセキュリティ ワールドを使っています。

- **以下の標準の証明書**:

    -   ISO/IEC 27001:2013 ([ISO/IEC 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/) を含む)
    -   SOC 2 SSAE 16/ISAE 3402 認証
    -   HIPAA BAA
    -   EU モデル条項
    -   Office 365 認証の Azure Active Directory の一部としての FedRAMP (HHS によって FedRAMP Agency Authority to Operate を発行)
    -   PCI DSS レベル 1

外部の証明書の詳細については、「 [Azure トラスト センター](https://azure.microsoft.com/support/trust-center/compliance/)」を参照してください。

## <a name="next-steps"></a>次のステップ

Azure Rights Management サービスの動作に関する技術的な詳細については、「[Azure RMS の機能の詳細](how-does-it-work.md)」をご覧ください。
