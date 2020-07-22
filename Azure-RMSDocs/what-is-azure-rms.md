---
title: Azure Rights Management protection の概要-AIP
description: Azure Information Protection が使用する保護テクノロジである Azure Rights Management (Azure RMS) に関する情報。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/21/2020
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
ms.openlocfilehash: 6c479bbb5f63bbbdc98165bc0c99f43a4e9503b4
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927405"
---
# <a name="what-is-azure-rights-management"></a>Azure Rights Management とは

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management (多くの場合は Azure RMS に省略して表現) とは、[Azure Information Protection](what-is-information-protection.md) が使用する保護テクノロジです。

Azure RMS は、暗号化ポリシー、id ポリシー、および承認ポリシーを使用して、電話、タブレット、Pc などの複数のデバイスでファイルや電子メールを保護するクラウドベースの保護サービスです。 保護の設定は、組織の境界が離れていても、コンテンツが組織内と組織外の両方で保護された状態を維持したままであっても、データに残ります。

次の図は、Azure RMS が Office 365、およびオンプレミスのサーバーとサービスに対して保護を提供する方法を示しています。 また、Windows、macOS、iOS、および Android を実行している一般的なエンドユーザーデバイスでも保護がサポートされています。

![Azure RMS のしくみ](./media/AzRMS_elements.png)

Office 365 サブスクリプションまたは Azure Information Protection のサブスクリプションで Azure RMS を使用します。 個々のサブスクリプションの種類とサポートされている機能の詳細については、 [Azure Information Protection 価格](https://azure.microsoft.com/pricing/details/information-protection/)に関するサイトを参照してください。

### <a name="sample-azure-rms-use-case"></a>サンプル Azure RMS のユースケース

従業員は、パートナー企業にドキュメントを電子メールで送信したり、ドキュメントをクラウドドライブに保存したりすることがあります。

Azure RMS の永続的な保護機能を使用すると、会社のデータを保護することができます。また、法令遵守、法的証拠開示要件、または情報管理のベストプラクティスについても法的に必要となる場合があります。

Azure RMS によって、検索やインデックス作成などの承認された人間やサービスが、保護されたデータの読み取りと検査を続行できるようになります。

承認されたユーザーとサービス ("データに対する推論" とも呼ばれます) への継続的なアクセスを保証することは、組織のデータの制御を維持するうえで重要な要素です。 この機能は、ピアツーピア暗号化を使用する他の情報保護ソリューションでは、簡単には実現できません。 

## <a name="business-problems-solved-by-azure-rights-management"></a>Azure Rights Management が解決するビジネス上の問題

次の一覧と表を使用して、組織がドキュメントや電子メールを保護する際に必要とするビジネス上の要件や問題、および Azure Rights Management テクノロジがニーズにどのように対処できるかを特定します。

- [保護機能](#protection-features)
- [コラボレーション機能](#collaboration-features)
- [プラットフォームのサポート機能](#platform-support-features)
- [インフラストラクチャの機能](#infrastructure-features)

> [!TIP]
> オンプレミスバージョンの Rights Management、Active Directory Rights Management サービス (AD RMS) に慣れている場合は、「 [Azure Rights Management と AD RMS](compare-on-premise.md)を比較する」の比較表をご覧ください。

### <a name="protection-features"></a>保護機能

|機能  |説明  |
|---------|---------|
|**複数のファイルの種類を保護する**     | Rights Management の初期の実装では、ネイティブの Rights Management 保護を使用して、Office ファイルのみを保護できます。 </br></br>現在、Rights Management 共有アプリケーションによって最初に提供され、Azure Information Protection クライアントによって提供される一般的な保護は、より多くの[ファイルの種類](./rms-client/client-admin-guide-file-types.md)がサポートされていることを意味します。        |
|**どこ**からでもファイルを保護できます。 | ファイルが[保護](./rms-client/client-classify-protect.md)されている場合、クラウドストレージサービスなどの管理下にないストレージに保存またはコピーされていても、ファイルは保護されたままになります。|
|     |         |


### <a name="collaboration-features"></a>コラボレーション機能

|機能  |説明  |
|---------|---------|
|**情報を安全に共有する**     |  [保護されたファイル](./rms-client/client-classify-protect.md)は、電子メールの添付ファイルや SharePoint サイトへのリンクなど、他のユーザーと安全に共有できます。 </br></br> 機密情報が電子メールメッセージ内にある場合は、電子メールを保護するか、Outlook の [**転送不可**] オプションを使用します。       |
|**企業間のコラボレーションをサポートする**     |  Azure Rights Management はクラウドサービスなので、保護されたコンテンツを共有する前に、他の組織との信頼を明示的に構成する必要はありません。 </br></br>Office 365 または Azure AD directory を既に所有している他の組織との共同作業が自動的にサポートされます。 </br></br>Office 365 または Azure AD directory を使用していない組織の場合、ユーザーは無料の個人用[RMS](rms-for-individuals.md)サブスクリプションにサインアップすることも、[サポートされているアプリケーション](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)に対して Microsoft アカウントを使用することもできます。       |
| | |

> [!TIP]
> 電子メールメッセージ全体を保護するのではなく、保護されたファイルを添付すると、電子メールテキストを暗号化解除しておくことができます。 
>
> たとえば、電子メールが組織外に送信されている場合は、初回使用時の指示を含めることができます。 保護されたファイルを添付した場合、基本的な手順はだれでも読むことができますが、電子メールやドキュメントを他のユーザーに転送した場合でも、承認されたユーザーのみがドキュメントを開くことができます。

### <a name="platform-support-features"></a>プラットフォームのサポート機能

Azure RMS は、次のようなさまざまなプラットフォームとアプリケーションをサポートしています。

|機能  |説明  |
|---------|---------|
|**一般的に使用されるデバイス** </br>Windows コンピューターだけではありません     | [サポートされているデバイス](./requirements-client-devices.md)は次のとおりです。 </br></br>- Windows コンピューターと携帯電話 </br>- Mac コンピューター </br>- iOS タブレットと携帯電話 </br>- Android タブレットと携帯電話        |
|**オンプレミスのサービス**     | [Office 365 とのシームレスな](office-apps-services-support.md)連携に加えて、 [RMS コネクタ](deploy-rms-connector.md)をデプロイするときに、次のオンプレミスサービスで Azure Rights Management を使用します。 </br></br>- Exchange Server </br>- SharePoint Server </br>- ファイル分類インフラストラクチャを実行する Windows Server        |
|**アプリケーションの拡張**     |Azure Rights Management は Microsoft Office のアプリケーションやサービスと緊密に統合されており、 [Azure Information Protection クライアント](./rms-client/aip-client.md )を使用して他のアプリケーションのサポートを拡張します。 </br></br>[Azure Information Protection sdk](./develop/developers-guide.md)は、Azure Information Protection をサポートするカスタムアプリケーションを作成するための api を社内開発者やソフトウェアベンダーに提供します。 </br></br>詳しくは、「[Rights Management API をサポートするその他のアプリケーション](api-support.md)」をご覧ください。         |
| | |

### <a name="infrastructure-features"></a>インフラストラクチャの機能

Azure RMS には、IT 部門とインフラストラクチャの組織をサポートするための次の機能が用意されています。

- **シンプルで柔軟なポリシーを作成**します。 カスタマイズされた[保護テンプレート](configure-policy-templates.md)を使用すると、管理者はポリシーを簡単に適用でき、ユーザーは各ドキュメントに適切なレベルの保護を適用し、組織内のユーザーにアクセスを制限することができます。 次に例を示します。

    - 企業全体にわたる戦略に関するホワイトペーパーをすべての従業員と共有するには、すべての社内従業員に読み取り専用ポリシーを適用します。 
    - 財務報告など、より機密性の高いドキュメントについては、役員のみにアクセスを制限します。

- **簡単なライセンス認証**。 新しいサブスクリプションの場合、ライセンス認証は自動的に有効になります。 既存のサブスクリプションの場合、 [Rights Management サービスをアクティブ化](activate-service.md)するには、管理ポータルで数回クリックするか、2つの PowerShell コマンドを使用する必要があります。

- **監査と監視サービス**。 これらのファイルが組織の境界内にある場合でも、保護されたファイルの[使用状況を監査および監視し](log-analyze-usage.md)ます。 

    たとえば、Contoso, Ltd. の従業員が Fabrikam, Inc. の3人の共同プロジェクトで作業している場合、Fabrikam 社のパートナーは、保護され、*読み取り*専用に制限されたドキュメントを送信する可能性があります。 

    Azure RMS の監査機能は次の情報を提供できます。

    - Fabrikam パートナーがドキュメントを開いているかどうか、およびそのタイミング。 
    - だれかが指定されておらず、ドキュメントを開くことができなかったかどうか。 これは、電子メールが転送されたか、共有の場所に保存された場合に発生する可能性があります。

    さらに、[ドキュメント追跡サイト](./rms-client/client-track-revoke.md)を使うと、ユーザーや管理者は、保護されたドキュメントを追跡でき、必要な場合は、ドキュメントへのアクセスを取り消すことができます。

- **組織全体に拡張する機能**。 Azure Rights Management は Azure の弾力性を持つクラウドサービスとして実行されるため、スケールアップとスケールアウトが可能です。そのため、追加のオンプレミスサーバーをプロビジョニングまたはデプロイする必要はありません。

- **データの制御を維持**します。 組織は、次のような IT 管理機能を利用できます。

    |機能  |説明  |
    |---------|---------|
    |テナントキーの管理    |   "[Bring Your Own Key](plan-implement-tenant-key.md)" (byok) ソリューションを使用して独自のテナントキーを管理し、テナントキーをハードウェアセキュリティモジュール (hsm) に格納します。      |
    |監査と使用状況ログ    |   監査と[使用状況ログ](log-analyze-usage.md)機能を使用して、ビジネス上の洞察を分析し、不正使用を監視し、情報の漏洩に関するフォレンジック分析を実行します。      |
    |アクセスの委任     |  [スーパーユーザー機能](configure-super-users.md)を使用してアクセスを委任し、ドキュメントが保護されている場合でも、組織を退職する従業員によって保護されている場合でも、常に保護されたコンテンツにアクセスできるようにします。 </br> これに対し、ピア ツー ピアの暗号化ソリューションでは、企業データにアクセスできなくなるおそれがあります。       |
    |Active Directory の同期     |   Azure AD Connect などの[ハイブリッド id ソリューション](/azure/active-directory/hybrid/)を使用して、オンプレミスの Active Directory アカウントの共通 id をサポートするために[Azure RMS 必要なディレクトリ属性だけ](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms)を同期します。      |
    |シングルサインオン     | AD FS を使用して、クラウドにパスワードをレプリケートせずにシングルサインオンを有効にします。        |
    |AD RMS からの移行 |Active Directory Rights Management サービス (AD RMS) をデプロイした場合は、以前に AD RMS によって保護されていたデータへのアクセスを失わずに、 [Azure Rights Management サービスに移行](migrate-from-ad-rms-to-azure-rms.md)します。 |
    | | |


> [!NOTE]
> Azure Rights Management によって以前に保護されていたコンテンツへのアクセスを失うことなく、Azure Rights Management サービスの使用を停止することは、常に選択肢となります。 
> 
> 詳細については、「 [Azure Rights Management の使用停止と非アクティブ](decommission-deactivate.md)化」を参照してください。 
> 



## <a name="security-compliance-and-regulatory-requirements"></a>セキュリティ、コンプライアンス、および規制の要件
Azure Rights Management は、次のセキュリティ、コンプライアンス、および規制の要件をサポートしています。

- **業界標準の暗号化を使用し、FIPS 140-2 をサポートします。** 詳細については、「[Cryptographic controls used by Azure RMS: Algorithms and key lengths (Azure RMS で使用される暗号化の制御: アルゴリズムとキーの長さ)](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)」を参照してください。

- テナントキーを Microsoft Azure データセンターに格納するため**の NCipher nShield ハードウェアセキュリティモジュール (HSM) のサポート**。 

    自社の地域でのみキーを使用できるように、Azure Rights Management では北米、EMEA (ヨーロッパ、中東およびアフリカ)、およびアジアのデータ センターで独立したセキュリティ ワールドを使っています。

- **次の標準の証明書。**

    -   ISO/IEC 27001:2013 (./インクルード[iso/iec 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))
    -   SOC 2 SSAE 16/ISAE 3402 認証
    -   HIPAA BAA
    -   EU モデル条項
    -   Office 365 認証の Azure Active Directory の一部としての FedRAMP (HHS によって FedRAMP Agency Authority to Operate を発行)
    -   PCI DSS レベル 1

これらの外部認定の詳細については、 [Azure セキュリティセンター](https://azure.microsoft.com/support/trust-center/compliance/)を参照してください。

## <a name="next-steps"></a>次のステップ

Azure Rights Management サービスの動作に関する技術的な詳細については、「[Azure RMS の機能の詳細](how-does-it-work.md)」をご覧ください。
