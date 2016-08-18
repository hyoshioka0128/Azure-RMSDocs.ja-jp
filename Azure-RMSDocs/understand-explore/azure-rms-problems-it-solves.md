---
title: "Azure RMS が解決する問題の種類 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 06f615c993d54ab1e8e4a94d7414302481d919b4
ms.openlocfilehash: 17756d4e641c10c0522f7a849634ae67630b363b


---


# Azure RMS が解決する問題の種類

*適用対象: Azure Rights Management、Office 365*

次の表を使用して、組織が抱えるビジネス上の要件や問題を特定し、Azure RMS による対処方法を説明します。

|要件または問題|Azure RMS による解決方法|
|--------------------------|-----------------------|
|あらゆる種類のファイルを保護する|√ 以前の Rights Management の実装では、ネイティブ保護を使用して、Office ファイルのみを保護できました。 ここで、[汎用的な保護](../rms-client/sharing-app-dialog-box.md#what-s-the-difference-between-generic-protection-and-built-in-native-protection)とは、あらゆる種類のファイルがサポートされることを意味します。|
|あらゆる場所のファイルを保護する|√ ファイルがある場所に保存されると ([保護済み](../rms-client/sharing-app-protect-in-place.md))、クラウド ストレージ サービスなど、IT の制御下にないストレージにファイルがコピーされる場合でも、保護は維持されます。|
|電子メールによるファイル共有をセキュリティで保護する|√ ファイルが電子メールで共有されるとき ([保護された共有](../rms-client/sharing-app-protect-by-email.md))、ファイルは電子メール メッセージの添付ファイルとして保護されます。保護された添付ファイルを開く方法に関する指示が与えられます。 電子メール テキストは暗号化されないので、受信者は常にこの手順を読むことができます。 ただし、添付されたドキュメントは保護されているので、電子メールまたはドキュメントが他の人に転送されたとしても、承認済みのユーザーのみがドキュメントを開くことができます。|
|監査と監視|√ 保護されたファイルが組織外部に出た後も、ファイルの[使用状況を監査および監視](../deploy-use/log-analyze-usage.md)できます。<br /><br />たとえば、Contoso, Ltd の社員が Fabrikam, Inc. の 3 人の社員と共同プロジェクトに携わっていて、読み取り専用の保護ドキュメントをこの 3 人に電子メールで送信するとします。 Azure RMS の監査機能は次の情報を提供できます。<br /><br />- Fabrikam 社内の指定されたユーザーがドキュメントを開いたかどうか、および開いた日時。<br /><br />- ドキュメントが転送されたり他のユーザーがアクセスできる共有場所に保存されたりして、指定外のユーザーがドキュメントを開こうとしたかどうか (試みは失敗します)。<br /><br />- 指定されたユーザーがドキュメントを印刷または変更しようとしたかどうか (試みは失敗します)。|
|Windows コンピューターに限らず、広く使用されるデバイスをすべてサポートする|√ [サポートされるデバイス](../get-started/requirements-client-devices.md)には次のものが含まれます。<br /><br />- Windows コンピューターと携帯電話<br /><br />- Mac コンピューター<br /><br />- iOS タブレットと携帯電話<br /><br />- Android タブレットと携帯電話|
|企業間のコラボレーションをサポートする|√ Azure RMS はクラウド サービスであるため、保護されたコンテンツを他の組織と共有する前に、信頼関係を明示的に構成する必要がありません。 相手組織が Office 365 または Azure AD ディレクトリを既に導入している場合、組織間のコラボレーションは自動的にサポートされます。 導入していない場合、無料の[個人用 RMS](rms-for-individuals.md) サブスクリプションに登録できます。|
|オンプレミスのサービスや Office 365 をサポートする|√  Azure RMS は [Office 365 とシームレスに](office-apps-services-support.md)連携します。[RMS コネクタ](../deploy-use/deploy-rms-connector.md)をデプロイすると、Azure RMS を次のオンプレミス サービスと使用することもできます。<br /><br />- Exchange Server<br /><br />- SharePoint Server<br /><br />- ファイル分類インフラストラクチャを実行する Windows Server|
|簡単なアクティブ化|√ ユーザーに対して [Rights Management サービスをアクティブ化](../deploy-use/activate-service.md)するために必要なのは、Azure クラシック ポータルで 2 回クリックすることだけです。|
|必要に応じて組織全体でスケーリングする能力|√ Azure RMS はクラウド サービスとして動作し、Azure の柔軟性を活かしてスケールアップおよびスケールアウトするため、追加のオンプレミス サーバーをプロビジョニングまたはデプロイする必要がありません。|
|シンプルで柔軟なポリシーを作成する能力|√ [権限ポリシーのカスタム テンプレート](../deploy-use/configure-custom-templates.md)を使用すると、管理者はポリシーを簡単に適用でき、ユーザーは適切なレベルの保護を各ドキュメントに適用してアクセスを組織内のユーザーに制限できます。<br /><br />たとえば、全社的戦略が記載された書類を全従業員が共有する場合、社内の全従業員に読み取り専用ポリシーを適用することが考えられます。 また、財務報告など、より機密性の高いドキュメントについては、アクセスを経営幹部にのみ制限することが考えられます。|
|広範なアプリケーションのサポート|√ Azure RMS は Microsoft Office のアプリケーションやサービスと緊密に統合されており、RMS 共有アプリケーションを使用することで他のアプリケーションにもサポートを広げることができます。<br /><br />√ [Microsoft Rights Management SDK](../develop/developers-guide.md#software-development-kits) は、Azure RMS をサポートするカスタム アプリケーションを作成するための API を社内開発者やソフトウェア ベンダーに提供します。<br /><br />詳細については、「[RMS API をサポートするその他のアプリケーション](api-support.md)」を参照してください。|
|IT 部門がデータの制御を維持する必要がある|√ 組織は独自のテナント キーを管理し、"[Bring Your Own Key](../plan-design/plan-implement-tenant-key.md)" (BYOK) ソリューションを利用し、ハードウェア セキュリティ モジュール (HSM) にテナント キーを保存することを選択できます。<br /><br />√ 監査と[使用状況の記録](../deploy-use/log-analyze-usage.md)に対応しています。分析してビジネスに必要な洞察に活用したり、誤用を監視したり、(情報の漏えいが発生した場合) 裁判分析を実行したりできます。<br /><br />√ [スーパー ユーザー機能](../deploy-use/configure-super-users.md)を利用した委任アクセスにより、退職者によって保護されたドキュメントであっても、IT 部門は保護されたコンテンツに常にアクセスできます。 これに対し、ピア ツー ピアの暗号化ソリューションでは、企業データにアクセスできなくなるおそれがあります。<br /><br />√ Azure AD Connect などの[ディレクトリ同期ツール](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)を使用して、オンプレミスの Active Directory アカウントに対して共通の ID をサポートするために [Azure RMS が必要とするディレクトリの属性のみ](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms)を同期します。<br /><br />√ AD FS を使用して、パスワードをクラウドにレプリケートすることなくシングル サインオンを有効にします。<br /><br />√ 組織は常に、以前に Azure RMS によって保護されていたコンテンツへのアクセスを失わずに、Azure RMS の使用を停止できます。 使用停止オプションの詳細については、「[Azure Rights Management の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」を参照してください。 さらに、Active Directory Rights Management サービス (AD RMS) をデプロイした組織は、以前に AD RMS によって保護されていたデータへのアクセスを失わずに [Azure RMS に移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)できます。|
> [!TIP]
> オンプレミス版の Rights Management である Active Directory Rights Management サービス (AD RMS) の知識がある場合は、「[Azure Rights Management と AD RMS を比較する](compare-azure-rms-ad-rms.md)」の比較表も参照してください。

## セキュリティ、コンプライアンス、および規制の要件
Azure RMS は、セキュリティ、コンプライアンス、規制に関する次の要件をサポートします。

√ 業界標準の暗号化を使用し、FIPS 140-2 をサポートします。 詳細については、「[Cryptographic controls used by Azure RMS: Algorithms and key lengths (Azure RMS で使用される暗号化の制御: アルゴリズムとキーの長さ)](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)」を参照してください。

√ Thales ハードウェア セキュリティ モジュール (HSM) をサポートし、テナント キーを Microsoft Azure データ センターに保存します。 自社の地域でのみキーを使用できるように、Azure RMS では北米、EMEA (欧州、中東、およびアフリカ)、およびアジアのデータ センターで独立したセキュリティ ワールドを使用しています。

√ 次の認定を受けています。

-   ISO/IEC 27001:2013 ([ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/) を含む)

-   SOC 2 SSAE 16/ISAE 3402 認証

-   HIPAA BAA

-   EU モデル条項

-   Office 365 認証の Azure Active Directory の一部としての FedRAMP (HHS によって FedRAMP Agency Authority to Operate を発行)

-   PCI DSS レベル 1

外部の証明書の詳細については、「 [Azure トラスト センター](http://azure.microsoft.com/support/trust-center/compliance/)」を参照してください。

## 次のステップ

管理者とユーザーから見た Azure RMS については、「[Azure RMS in action (Azure RMS の動作)](what-admins-users-see.md)」を参照してください。

Azure RMS の動作に関する技術的な詳細については、「[How does Azure RMS work (Azure RMS の機能の詳細)](how-does-it-work.md)」を参照してください。 


<!--HONumber=Jul16_HO3-->


