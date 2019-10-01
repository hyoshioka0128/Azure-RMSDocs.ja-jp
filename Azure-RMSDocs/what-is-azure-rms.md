---
title: Azure Rights Management protection の概要-AIP
description: Azure Information Protection が使用する保護テクノロジである Azure Rights Management (Azure RMS) に関する情報。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/30/2019
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
ms.openlocfilehash: 0cc51afb848dc754d33e5f0d425741ef84eff453
ms.sourcegitcommit: 28c1de5f9d1426f160f0e0bafcf9f76769e662b6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71679171"
---
# <a name="what-is-azure-rights-management"></a>Azure Active Directory Rights Management の概要

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management (多くの場合は Azure RMS に省略して表現) とは、[Azure Information Protection](what-is-information-protection.md) が使用する保護テクノロジです。

このクラウドベースの保護サービスでは、暗号化、ID、承認のポリシーを使用して、ファイルや電子メールを保護します。また、多数のデバイス (携帯電話、タブレット、および PC) で使用できます。 データが組織の外に出ても継続的に保護されるので、情報を組織の内外で保護できます。

たとえば、ドキュメントはパートナー企業に電子メールで送信されたり、クラウド ドライブに保存されたりします。 Azure RMS が提供する持続的な保護により、企業データがセキュリティで保護されるだけでなく、法定コンプライアンス、法的証拠開示要件、または一般的な情報管理の効率化が促進されます。

ただし、承認された人間やサービス (検索やインデックス作成など) は、保護されたデータの読み取りと検査を続行できます。 ピアツーピアの暗号化を使用する他の情報保護ソリューションでは、このような機能を簡単に達成できません。 この機能は "データに対する推論" と呼ばれ、組織のデータの管理を維持する上で重要な要素です。

次の図では、このサービスがオンプレミスのサーバーやサービスに加えて、Office 365 にどのように保護ソリューションを提供するのかを示します。 また、エンド ユーザーの間でよく使用される Windows、macOS、iOS、Android を実行するデバイスでも保護がサポートされます。


![Azure RMS のしくみ](./media/AzRMS_elements.png)

この保護は、Office 365 サブスクリプションでの使用に加えて、Azure Information Protection のサブスクリプションでも使用することができます。 ここでは、使用できるサブスクリプションと [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/) サイトでサポートされる機能の詳細情報についても説明します。

## <a name="business-problems-solved-by-azure-rights-management"></a>Azure Rights Management が解決するビジネス上の問題

次の表は、文書や電子メールの保護で組織が抱えるビジネス上の要件や問題、および Azure Rights Management テクノロジでのその対処方法に関する説明です。


|要件または問題|Azure RMS による解決方法|
|--------------------------|-----------------------|
|複数のファイルの種類を保護する|√ 初期の Rights Management の実装では、Rights Management のネイティブな保護を使って、Office ファイルのみを保護できました。 現在の**汎用的な保護**は、さらに多くの[ファイルの種類](./rms-client/client-admin-guide-file-types.md)がサポートされることを意味します。汎用的な保護は、Rights Management 共有アプリケーションによって最初に提供され、現在は Azure Information Protection クライアントによって提供されています。|
|あらゆる場所のファイルを保護する|√ ファイルが[保護](./rms-client/client-classify-protect.md)されると、クラウド ストレージ サービスなど、IT の制御下にないストレージにファイルが保存またはコピーされる場合でも、その保護は維持されます。|
|情報を安全に共有する|√ [保護された](./rms-client/client-classify-protect.md)ファイルは、他のユーザーと安全に共有できます (例: メールの添付ファイル、SharePoint サイトへのリンク)。 機密情報がメール メッセージ内にある場合は、メールを保護するか、または単に Outlook の [転送不可] オプションを使うことができます。 <br /><br />メール メッセージ全体を保護するのではなく、保護されたファイルを添付する利点は、メールのテキストが暗号化されないため、組織外にメールを送る場合に、初めて使うときの説明をメールに含めることができることです。 説明を読むことは誰でもできますが、添付されたドキュメントは保護されているので、メールまたはドキュメントが他の人に転送されたとしても、承認されているユーザーだけがドキュメントを開くことができます。|
|監査と監視|√ 保護されたファイルが組織外部に出た後も、ファイルの[使用状況を監査および監視](log-analyze-usage.md)できます。<br /><br />たとえば、Contoso, Ltd の社員がFabrikam, Inc. の 3 人の社員と共同プロジェクトに携わっていて、読み取り専用の保護ドキュメントをこの 3 人に電子メールで送信するものとします。 Azure Rights Management の監査機能では次の情報を提供できます。<br /><br />- Fabrikam 社内の指定されたユーザーがドキュメントを開いたかどうか、および開いた日時。<br /><br />- ドキュメントが転送されたり他のユーザーがアクセスできる共有場所に保存されたりして、指定外のユーザーがドキュメントを開こうとしたかどうか (試みは失敗します)。<br /><br />- 指定されたユーザーがドキュメントを印刷または変更しようとしたかどうか (試みは失敗します)。<br /><br />さらに、[ドキュメント追跡サイト](./rms-client/client-track-revoke.md)を使うと、ユーザーや管理者は、保護されたドキュメントを追跡でき、必要な場合は、ドキュメントへのアクセスを取り消すことができます。|
|Windows コンピューターに限らず、広く使われているデバイスをサポートする|√ [サポートされるデバイス](./requirements-client-devices.md)には次のものが含まれます。<br /><br />- Windows コンピューターと携帯電話<br /><br />- Mac コンピューター<br /><br />- iOS タブレットと携帯電話<br /><br />- Android タブレットと携帯電話|
|企業間のコラボレーションをサポートする|√ Azure Rights Management はクラウド サービスであるため、保護されたコンテンツを他の組織と共有する前に、信頼関係を明示的に構成する必要がありません。 相手組織が Office 365 または Azure AD ディレクトリを既に導入している場合、組織間のコラボレーションは自動的にサポートされます。 そうでない場合、ユーザーは無料の[個人向け RMS](rms-for-individuals.md) サブスクリプションにサインアップするか、[Azure Information Protection への認証をサポートしているアプリケーション](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)用に Microsoft アカウントを使用することができます。|
|オンプレミスのサービスや Office 365 をサポートする|√  Azure Rights Management は、[Office 365 とシームレスに](office-apps-services-support.md)連携するだけでなく、[RMS コネクタ](deploy-rms-connector.md)をデプロイすると、次のオンプレミス サービスで使うこともできます。<br /><br />- Exchange Server<br /><br />- SharePoint Server<br /><br />- ファイル分類インフラストラクチャを実行する Windows Server|
|簡単なアクティブ化|√ 新しいサブスクリプションの場合は、自動的にアクティブ化されます。 既存のサブスクリプションの場合、[Rights Management サービスをアクティブ化する](activate-service.md)には、管理ポータルで数回クリックするだけです。 または、コマンド ラインで管理する方がよければ、2 つの PowerShell コマンドだけで済みます。|
|必要に応じて組織全体でスケーリングする能力|√ Azure Rights Management はクラウド サービスとして動作し、Azure の柔軟性を活かしてスケールアップおよびスケールアウトするため、追加のオンプレミス サーバーをプロビジョニングまたはデプロイする必要がありません。|
|シンプルで柔軟なポリシーを作成する能力|√ [カスタム保護テンプレート](configure-policy-templates.md)を使用すると、管理者はポリシーを簡単に適用でき、ユーザーは適切なレベルの保護を各ドキュメントに適用してアクセスを組織内のユーザーに制限できます。<br /><br />たとえば、全社的戦略が記載された書類を全従業員が共有する場合、社内の全従業員に読み取り専用ポリシーを適用することが考えられます。 また、財務報告など、より機密性の高いドキュメントについては、アクセスを経営幹部にのみ制限することが考えられます。|
|広範なアプリケーションのサポート|√ Azure Rights Management は Microsoft Office のアプリケーションやサービスと緊密に統合されており、[Azure Information Protection クライアント](./rms-client/aip-client.md )を使うことで、他のアプリケーションにもサポートを広げることができます。<br /><br />√ [Azure Information Protection SDK](./develop/developers-guide.md) では、Azure Information Protection をサポートするカスタム アプリケーションを作成するための API を社内開発者やソフトウェア ベンダーに提供します。<br /><br />詳しくは、「[Rights Management API をサポートするその他のアプリケーション](api-support.md)」をご覧ください。|
|IT 部門がデータの制御を維持する必要がある|√ 組織では独自のテナント キーを管理し、"[Bring Your Own Key](plan-implement-tenant-key.md)" (BYOK) ソリューションを利用し、ハードウェア セキュリティ モジュール (HSM) にテナント キーを保存することを選択できます。<br /><br />√ 監査と[使用状況の記録](log-analyze-usage.md)に対応しています。分析してビジネスに必要な洞察に活用したり、誤用を監視したり、(情報の漏えいが発生した場合) 裁判分析を実行したりできます。<br /><br />√ [スーパー ユーザー機能](configure-super-users.md)を利用した委任アクセスにより、退職者によって保護されたドキュメントであっても、IT 部門は保護されたコンテンツに常にアクセスできます。 これに対し、ピア ツー ピアの暗号化ソリューションでは、企業データにアクセスできなくなるおそれがあります。<br /><br />√ Azure AD Connect などの[ハイブリッド ID ソリューション](/azure/active-directory/hybrid/)を使用して、オンプレミスの Active Directory アカウントに対して共通の ID をサポートするために [Azure RMS が必要とするディレクトリの属性のみ](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms)を同期します。<br /><br />√ AD FS を使用して、パスワードをクラウドにレプリケートすることなくシングル サインオンを有効にします。<br /><br />√ 組織では常に、以前に Azure Rights Management によって保護されていたコンテンツへのアクセスを失わずに、Azure Rights Management サービスの使用を停止できます。 使用停止オプションの詳細については、「[Azure Rights Management の使用停止と非アクティブ化](decommission-deactivate.md)」を参照してください。 さらに、Active Directory Rights Management サービス (AD RMS) をデプロイした組織は、以前に AD RMS によって保護されていたデータへのアクセスを失わずに [Azure Rights Management サービスに移行](migrate-from-ad-rms-to-azure-rms.md)できます。|
> [!TIP]
> オンプレミス版の Rights Management である Active Directory Rights Management サービス (AD RMS) の知識がある場合は、「[Azure Rights Management と AD RMS を比較する](compare-on-premise.md)」の比較表も参照してください。

## <a name="security-compliance-and-regulatory-requirements"></a>セキュリティ、コンプライアンス、および規制の要件
Azure Rights Management は、次のセキュリティ、コンプライアンス、および規制の要件をサポートしています。

√ 業界標準の暗号化を使用し、FIPS 140-2 をサポートします。 詳細については、「[Azure RMS で使用される暗号化の制御: アルゴリズムとキーの長さ](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)」の情報を参照してください。

テナントキーを Microsoft Azure データセンターに格納するための nCipher nShield ハードウェアセキュリティモジュール (HSM) のサポートを√。 自社の地域でのみキーを使用できるように、Azure Rights Management では北米、EMEA (ヨーロッパ、中東、およびアフリカ)、およびアジアのデータ センターで独立したセキュリティ ワールドを使っています。

√ 次の認定を受けています。

-   ISO/IEC 27001:2013 ([ISO/IEC 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/) を含む)

-   SOC 2 SSAE 16/ISAE 3402 認証

-   HIPAA BAA

-   EU モデル条項

-   Office 365 認証の Azure Active Directory の一部としての FedRAMP (HHS によって FedRAMP Agency Authority to Operate を発行)

-   PCI DSS レベル 1

外部の証明書の詳細については、「 [Azure トラスト センター](https://azure.microsoft.com/support/trust-center/compliance/)」を参照してください。

## <a name="next-steps"></a>次の手順

Azure Rights Management サービスの動作に関する技術的な詳細については、「[Azure RMS の機能の詳細](how-does-it-work.md)」をご覧ください。

