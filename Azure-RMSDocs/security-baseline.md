---
title: Azure Information Protection 用の Azure のセキュリティベースライン
description: 「Azure Information Protection のセキュリティベースライン」では、Azure のセキュリティベンチマークで指定されたセキュリティに関する推奨事項を実装するための手順に関するガイダンスとリソースを提供します。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/18/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: 376dcff12fe493c18da827dcfa67b12d2389b4f8
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240786"
---
# <a name="azure-security-baseline-for-azure-information-protection"></a>Azure Information Protection 用の Azure のセキュリティベースライン

このセキュリティベースラインは、 [Azure セキュリティベンチマークバージョン 2.0](/azure/security/benchmarks/overview) から Azure Information Protection へのガイダンスを適用します。 Azure セキュリティ ベンチマークには、Azure 上のクラウド ソリューションをセキュリティで保護する方法に関する推奨事項がまとめてあります。 コンテンツは、Azure セキュリティベンチマークで定義されている **セキュリティコントロール** と、Azure Information Protection に適用される関連ガイダンスによってグループ化されています。 Azure Information Protection に適用できない **コントロール** は除外されています。

Azure Information Protection 完全に Azure のセキュリティベンチマークにマップする方法については、「 [完全な Azure Information Protection のセキュリティベースラインマッピングファイル](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines)」を参照してください。

## <a name="network-security"></a>ネットワークのセキュリティ

*詳細については、[Azure セキュリティ ベンチマークの「ネットワークのセキュリティ](/azure/security/benchmarks/security-controls-v2-network-security)」を参照してください。*

### <a name="ns-6-simplify-network-security-rules"></a>NS-6: ネットワーク セキュリティ規則を簡略化する

**ガイダンス**: Virtual Network サービスタグを使用して、Azure Information Protection リソース用に構成されているネットワークセキュリティグループまたは Azure Firewall にネットワークアクセス制御を定義します。 

セキュリティ規則を作成するときは、特定の IP アドレスの代わりにサービスタグを使用します。 対応するサービスのトラフィックを許可または拒否するには、ルールの適切な送信元または送信先のフィールドに、{AzureInformationProtection} などのサービスタグ名を指定します。

サービス タグに含まれるアドレス プレフィックスの管理は Microsoft が行い、アドレスが変化するとサービス タグは自動的に更新されます。

- [サービス タグとその使用方法の概要](/azure/virtual-network/service-tags-overview)

- [Azure Information Protection サービスタグ](./requirements.md#service-tags)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="identity-management"></a>ID 管理

*詳細については、[Azure セキュリティ ベンチマークの「ID 管理](/azure/security/benchmarks/security-controls-v2-identity-management).* 」を参照してください。

### <a name="im-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system"></a>IM-1:Azure Active Directory を中央 ID および認証システムとして標準化する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。 組織のクラウドセキュリティプラクティスで Azure AD をセキュリティで保護するために、優先度を高く設定します。 

Azure AD id のセキュリティスコアを確認して、Microsoft のベストプラクティスの推奨事項と比較して、id のセキュリティ体制を評価します。 スコアを使用して、構成がベスト プラクティスの推奨事項とどの程度一致しているかを測定し、セキュリティ体制を強化します。

Azure AD を標準化して、以下での組織の ID とアクセス管理を統制します。

- Azure portal、Azure Storage、Azure Virtual Machines (Linux と Windows)、Azure Key Vault、サービスとしてのプラットフォーム (PaaS)、サービスとしてのソフトウェア (SaaS) アプリケーションなどの Microsoft Cloud リソース

- Azure 上のアプリケーションや企業ネットワーク リソースなどの組織のリソース

Azure AD は、Microsoft アカウントを持たないユーザーが、Microsoft 以外のアカウントを使用してアプリケーションやリソースにサインインできるようにするための外部 id をサポートしています。

- [Azure Active Directory のテナント](/azure/active-directory/develop/single-and-multi-tenant-apps)

- [Azure AD インスタンスを作成して構成する方法](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)

- [アプリケーションに外部 ID プロバイダーを使用する](/azure/active-directory/b2b/identity-providers)

- [Azure Active Directory の ID セキュリティ スコアとは](/azure/active-directory/fundamentals/identity-secure-score)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="im-2-manage-application-identities-securely-and-automatically"></a>IM-2:アプリケーション ID を安全かつ自動的に管理する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の id およびアクセス管理サービスです。 Azure Rights Management サービスは、Bring Your Own Key (BYOK) シナリオの Azure Key Vault に格納されている顧客のキーにアクセスするときに、Azure AD アプリケーション id を使用します。 キーにアクセスするために Azure Rights Management サービスを承認するには Azure Key Vault アクセスポリシーを構成します。これは Azure portal を使用するか、PowerShell を使用して行うことができます。

- [BYOK のために Azure Rights Management サービスを承認する](./byok-price-restrictions.md#authorizing-the-azure-rights-management-service-to-use-your-key)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="im-3-use-azure-ad-single-sign-on-sso-for-application-access"></a>IM-3:アプリケーションのアクセスに Azure AD シングル サインオン (SSO) を使用する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。 

Azure Information Protection は Azure AD を使用して、Azure リソース、クラウドアプリケーション、オンプレミスアプリケーションに id とアクセス管理を提供します。 これには、従業員などの企業 ID だけでなく、パートナー、ベンダー、サプライヤーなどの外部 ID も含まれます。 これにより、シングル サインオン (SSO) で、オンプレミスとクラウド内の組織のデータとリソースへのアクセスを管理し、セキュリティで保護することができます。 すべてのユーザー、アプリケーション、デバイスを Azure AD に接続することで、シームレスで安全なアクセスを実現し、可視性と制御性を高めることができます。

- [Azure Active Directory で Azure Information Protection にサインインします](./requirements.md)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="im-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access"></a>IM-4:すべての Azure Active Directory ベースのアクセスに強力な認証制御を使用する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、multi-factor authentication による強力な認証をサポートしています。 Azure Information Protection の認証と承認をサポートするには、Azure AD が必要です。 オンプレミス ディレクター (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。

- Azure Information Protection ではシングルサインオンがサポートされているため、ユーザーが資格情報の入力を繰り返し求められることはありません。 フェデレーションに別のベンダーのソリューションを使用する場合は、そのベンダーで Azure AD 向けの構成方法を確認します。 WS-Trust は、これらのソリューションでシングル サインオンをサポートするための、一般的な要件です。

- 必要なクライアントソフトウェアがあり、multi-factor authentication をサポートするインフラストラクチャが正しく構成されている場合、Azure Information Protection では多要素認証がサポートされます。

詳細については、次のリファレンスを参照してください。

- [Azure Active Directory を使用した認証の Azure Information Protection](./requirements.md)

**Azure Security Center の監視**: はい

**責任**: Customer

### <a name="im-5-monitor-and-alert-on-account-anomalies"></a>IM-5:アカウントの異常を監視してアラートを出す

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。 

Azure AD に関するその他のガイダンス:

- サインイン-サインインレポートには、マネージアプリケーションとユーザーサインインアクティビティの使用状況に関する情報が表示されます。
- 監査ログ - Azure AD 内のさまざまな機能によって行われたすべての変更についてログによる追跡可能性を提供します。 監査ログの例には、ユーザー、アプリ、グループ、ロール、ポリシーの追加や削除など、Azure AD 内のリソースに対して行われた変更が含まれます。
- リスクの高いサインイン - リスクの高いサインインは、ユーザー アカウントの正当な所有者ではない人によってサインインが試行された可能性があることを示す指標です。
- リスクのフラグ付きユーザー - リスクの高いユーザーは、侵害された可能性があるユーザー アカウントの指標です。
これらのデータ ソースは、Azure Monitor、Azure Sentinel、またはサードパーティの SIEM システムと統合できます。

また Azure Security Center は、失敗した認証試行の数が多すぎる、サブスクリプションで非推奨のアカウントなど、特定の不審なアクティビティについてもアラートを表示できます。

セキュリティ ソリューションである Azure Advanced Threat Protection (ATP) では、Active Directory シグナルを使用することで、高度な脅威、セキュリティ侵害を受けた ID、および悪意のある内部関係者のアクションを特定、検出、および調査できます。

- [Azure Active Directory の監査アクティビティ レポート](/azure/active-directory/reports-monitoring/concept-audit-logs) 

- [Azure AD の危険なサインインを表示する方法](/azure/active-directory/reports-monitoring/concept-risky-sign-ins) 

- [危険なアクティビティのフラグが設定された Azure AD ユーザーを識別する方法](/azure/active-directory/reports-monitoring/concept-user-at-risk) 

- [Azure Security Center でユーザーの ID およびアクセス アクティビティを監視する方法](/azure/security-center/security-center-identity-access) 

- [Azure Security Center の脅威インテリジェンス保護モジュールでのアラート](//azure/security-center/alerts-reference) 

- [Azure アクティビティ ログを Azure Monitor に統合する方法](/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="im-6-restrict-azure-resource-access-based-on-conditions"></a>IM-6:条件に基づいて Azure リソースへのアクセスを制限する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。 Azure AD で、Azure Information Protection の条件付きアクセスを構成します。 管理者は、標準の条件付きアクセスコントロールに基づいて、Azure Information Protection によって保護されたドキュメントについて、テナント内のユーザーへのアクセスをブロックまたは許可することができます。

多要素認証は、最も一般的に要求される条件の1つであり、構成済みの Intune ポリシーを使用したデバイスコンプライアンスは別のものです。 モバイルデバイスが組織パスワードの要件を満たしていること、オペレーティングシステムの最小バージョンがあること、および接続されているコンピューターがドメインに参加していることを条件として要求することができます。

- [Azure Information Protection の条件付きアクセスポリシー](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="privileged-access"></a>特権アクセス

*詳細については、[Azure セキュリティ ベンチマークの「特権アクセス](/azure/security/benchmarks/security-controls-v2-privileged-access)」を参照してください。*

### <a name="pa-1-protect-and-limit-highly-privileged-users"></a>PA-1:高い特権を持つユーザーを保護および制限する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。 

Azure Information Protection には、Azure AD に管理者レベルのロールが含まれています。 管理者ロールに割り当てられたユーザーには、Azure Information Protection サービスでの完全なアクセス許可が付与されます。 管理者ロールを使用して、Azure Information Protection ポリシーのラベルの構成、保護テンプレートの管理、保護のアクティブ化を行うことができます。 ただし、管理者ロールでは、Identity Protection Center、Privileged Identity Management、Monitor Microsoft 365 Service Health、または Office 365 セキュリティコンプライアンスセンターでのアクセス許可は付与されません &amp; 。

この特権を持つユーザーは、Azure 環境内のすべてのリソースを直接または間接的に読み取り、変更することができるため、高い特権を持つアカウントまたはロールの数を制限し、これらのアカウントを管理者特権で保護することができます。 Privileged Identity Management (PIM) を使用して、Azure リソースへのジャストインタイム (JIT) 特権アクセスと Azure AD を有効にします。 ジャストインタイムアクセスは、ユーザーが必要とする場合にのみ特権タスクを実行するための一時的なアクセス許可を付与します。 PIM を使用すると、Azure AD 組織に不審なアクティビティや安全でないアクティビティがある場合に、セキュリティ アラートを生成することもできます。

- [Azure Information Protection 管理者ロール](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azure AD での管理者ロールのアクセス許可](/azure/active-directory/users-groups-roles/directory-assign-admin-roles)

- [Azure Privileged Identity Management のセキュリティ アラートを使用する](/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [Azure AD でのハイブリッドおよびクラウド デプロイ用の特権アクセスをセキュリティで保護する](/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-2-restrict-administrative-access-to-business-critical-systems"></a>PA-2:ビジネス クリティカルなシステムへの管理アクセスを制限する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。 

Azure Information Protection には、Azure AD に管理者レベルのロールが含まれています。 管理者ロールに割り当てられたユーザーには、Azure Information Protection サービスでの完全なアクセス許可が付与されます。 管理者ロールを使用して、Azure Information Protection ポリシーのラベルの構成、保護テンプレートの管理、保護のアクティブ化を行うことができます。 管理者ロールでは、Identity Protection Center、Privileged Identity Management、Monitor Microsoft 365 Service Health、または Office 365 セキュリティコンプライアンスセンターでのアクセス許可は付与されません &amp; 。

- [Azure Information Protection 管理者ロール](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [管理者が実行できる操作 Azure Information Protection](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator-permissions)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-3-review-and-reconcile-user-access-regularly"></a>PA-3:ユーザー アクセスを定期的に確認して調整する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。

Azure AD を使用してリソースを管理し、ユーザーアカウントを確認し、割り当てを定期的にアクセスして、アカウントとそのアクセスが有効であることを確認します。 Azure AD アクセスレビューを実施して、グループメンバーシップ、エンタープライズアプリケーションへのアクセス、およびロールの割り当てを確認します。 Azure AD レポートで古いアカウントを検出します。 Azure AD の Privileged Identity Management 機能を使用してアクセスレビューレポートワークフローを作成し、レビュープロセスを容易にすることができます。

さらに、過剰な数の管理者アカウントが作成された場合にアラートを発行したり、古い管理者アカウントや不適切に構成されている管理者アカウントを特定するように Azure Privileged Identity Management を構成することもできます。 一部の Azure サービスでは、Azure AD によって管理されないローカルユーザーとロールがサポートされていることに注意してください。 これらのユーザーは、お客様が個別に管理する必要があります。

- [Azure Information Protection 管理者ロール](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [管理者が実行できる操作 Azure Information Protection](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator-permissions)

- [Privileged Identity Management (PIM) で Azure リソース ロールのアクセス レビューを作成する](/azure/active-directory/privileged-identity-management/pim-resource-roles-start-access-review) 

- [Azure AD の ID およびアクセス レビューの使用方法](/azure/active-directory/governance/access-reviews-overvie)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-4-set-up-emergency-access-in-azure-ad"></a>PA-4:Azure AD で緊急アクセスを設定する

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) と統合されて、リソースを管理します。 Azure AD 組織から誤ってロックアウトされるのを防ぐために、通常の管理者アカウントを使用できない場合にアクセスするための緊急アクセス用アカウントを設定します。 緊急アクセス用アカウントは高い特権を持っており、特定の個人に割り当てることはできません。 緊急アクセス用アカウントは、通常の管理者アカウントを使うことができない "緊急事態" に制限されます。

緊急アクセス用アカウントの資格情報 (パスワード、証明書、スマート カードなど) は安全に保管し、緊急時にのみそれらを使うことを許可された個人のみに知らせる必要があります。

- [Azure AD で緊急アクセス用アカウントを管理する](/azure/active-directory/users-groups-roles/directory-emergency-access)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-5-automate-entitlement-management"></a>PA-5:エンタイトルメント管理を自動化する 

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD)、Azure の既定の id およびアクセス管理サービスと統合されています。

Azure AD には、アクセス権の割り当て、レビュー、有効期限など、アクセス要求ワークフローを自動化するための資格管理機能が用意されています。 2 段階または複数段階の承認もサポートされています。

- [Azure AD アクセス レビューとは](/azure/active-directory/governance/access-reviews-overview) 

- [Azure AD エンタイトルメント管理とは](/azure/active-directory/governance/entitlement-management-overview)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-6-use-privileged-access-workstations"></a>PA-6:特権アクセス ワークステーションを使用する

**ガイダンス**: Azure Information Protection は、PowerShell を使用して顧客のワークステーションから管理できます。 

保護された分離ワークステーションは、管理者、開発者、重要なサービスオペレーターなど、機密性の高い役割のセキュリティにとって非常に重要です。 

管理タスクに高度にセキュリティ保護されたユーザー ワークステーションや Azure Bastion を使用します。 Azure Active Directory、Microsoft Defender Advanced Threat Protection (ATP)、または Microsoft Intune を使用して、管理タスクのためにセキュリティで保護されたマネージド ユーザー ワークステーションを展開します。 セキュリティで保護されたワークステーションを一元管理して、強力な認証、ソフトウェアとハードウェアのベースライン、制限された論理アクセスとネットワーク アクセスなどのセキュリティで保護された構成を実施できます。

- [Azure Information Protection 用の PowerShell の使用に関するガイダンス](./rms-client/client-admin-guide-powershell.md)

- [特権アクセス ワークステーションを理解する](/azure/active-directory/devices/concept-azure-managed-workstation) 

- [特権アクセス ワークステーションを展開する](/azure/active-directory/devices/howto-azure-managed-workstation)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-7-follow-just-enough-administration-least-privilege-principle"></a>PA-7:Just Enough Administration (最小限の特権の原則) に従う 

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。 

Azure Information Protection には、Azure AD に管理者レベルのロールが含まれています。 管理者ロールに割り当てられたユーザーには、Azure Information Protection サービスでの完全なアクセス許可が付与されます。 管理者ロールを使用して、Azure Information Protection ポリシーのラベルの構成、保護テンプレートの管理、保護のアクティブ化を行うことができます。 ただし、管理者ロールでは、Identity Protection Center、Privileged Identity Management、Monitor Microsoft 365 Service Health、または Office 365 セキュリティコンプライアンスセンターでのアクセス許可は付与されません &amp; 。

この特権を持つユーザーは、Azure 環境内のすべてのリソースを直接または間接的に読み取り、変更することができるため、高い特権を持つアカウントまたはロールの数を制限し、これらのアカウントを管理者特権で保護することができます。 Privileged Identity Management (PIM) を使用して、Azure リソースへのジャストインタイム (JIT) 特権アクセスと Azure AD を有効にします。 ジャストインタイムアクセスは、ユーザーが必要とする場合にのみ特権タスクを実行するための一時的なアクセス許可を付与します。 PIM を使用すると、Azure AD 組織に不審なアクティビティや安全でないアクティビティがある場合に、セキュリティ アラートを生成することもできます。

- [Azure Information Protection のアクセス許可レベルに含まれる権限](./configure-usage-rights.md#rights-included-in-permissions-levels)

- [Rights Management 発行者と Rights Management 所有者](./configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)

- [Azure Information Protection 管理者ロール](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azure AD での管理者ロールのアクセス許可](/azure/active-directory/users-groups-roles/directory-assign-admin-roles)

- [Azure Privileged Identity Management のセキュリティ アラートを使用する](/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [Azure AD でのハイブリッドおよびクラウド デプロイ用の特権アクセスをセキュリティで保護する](/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-8-choose-approval-process-for-microsoft-support"></a>PA-8: Microsoft サポートの承認プロセスを選択する  

**ガイダンス**: Azure Information Protection は、Azure カスタマーロックボックスをサポートして、データアクセス要求を確認、承認、および拒否したり、要求を確認したりできるようにします。 

- [ロックボックスの概要](/azure/security/fundamentals/customer-lockbox-overview)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="data-protection"></a>データ保護

*詳細については、[Azure セキュリティ ベンチマークの「データ保護](/azure/security/benchmarks/security-controls-v2-data-protection)」を参照してください。*

### <a name="dp-1-discovery-classify-and-label-sensitive-data"></a>DP-1:機密データを検出、分類、ラベル付けする

**ガイダンス**: Azure Information Protection では、機密情報の検出、分類、およびラベル付けを行うことができます。 

Azure Information Protection は、組織がラベルを適用してドキュメントや電子メールを分類および保護できるようにするクラウドベースのソリューションです。 ラベルの適用は、ルールと条件を使用して管理者が自動で実行するか、ユーザーが手動で実行するか、その組み合わせ (ユーザーに提示するレコメンデーションを管理者が定義する) で行うことができます。

- [Azure Information Protection の概要](./index.yml)

- [統一されたラベル付けクライアントをセットアップする方法に関するガイダンス](./rms-client/clientv2-user-guide.md)

**Azure Security Center の監視**: 適用なし

**責任**: 共有

### <a name="dp-2-protect-sensitive-data"></a>DP-2:機密データを保護する

**ガイダンス**: Azure Information Protection は、機密情報にラベルを付け、暗号化によってそのデータを保護する機能を提供することによって、データ保護を提供します。 保護は、Azure Rights Management サービスによって提供されます。

- [Azure Rights Management](./what-is-azure-rms.md)

**Azure Security Center の監視**: 適用なし

**責任**: 共有

### <a name="dp-3-monitor-for-unauthorized-transfer-of-sensitive-data"></a>DP-3:機密データの不正転送を監視する

**ガイダンス**: Azure Information Protection を使用すると、追跡と取り消しの機能を使用して、機密データの不正な転送を監視することができます。 追跡と取り消しを使用すると、ユーザーが送信したドキュメントをどのように使用しているかを追跡し、ユーザーがアクセスできなくなった場合にアクセスを取り消すことができます。 

- [追跡と取り消しに関するガイダンス](./rms-client/client-track-revoke.md)

**Azure Security Center の監視**: 適用なし

**責任**: 共有

## <a name="asset-management"></a>アセット管理

*詳細については、[Azure セキュリティ ベンチマークの「アセット管理](/azure/security/benchmarks/security-controls-v2-asset-management)」を参照してください。*

### <a name="am-1-ensure-security-team-has-visibility-into-risks-for-assets"></a>AM-1:セキュリティ チームが資産のリスクを確実に可視化できるようにする

**ガイダンス**:セキュリティ チームに Azure テナントとサブスクリプションのセキュリティ閲覧者アクセス許可を付与して、セキュリティ チームが Azure Security Center を使用してセキュリティ上のリスクを監視できるようにします。 

セキュリティ チームの責任がどのように構造化されているかによって、セキュリティ リスクの監視は中央のセキュリティ チームまたはローカル チームの責任になります。 ただし、セキュリティ分析情報とリスクは、常に組織内で一元的に集計する必要があります。 

セキュリティ閲覧者のアクセス許可は、テナント全体 (ルート管理グループ) に幅広く適用することも、管理グループまたは特定のサブスクリプションにスコープ指定することもできます。 

注:ワークロードとサービスを可視化するには、追加のアクセス許可が必要になることがあります。 

- [セキュリティ閲覧者ロールの概要](/azure/role-based-access-control/built-in-roles#security-reader)

- [Azure 管理グループの概要](/azure/governance/management-groups/overview)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

### <a name="am-3-use-only-approved-azure-services"></a>AM-3:承認された Azure サービスのみを使用する

**ガイダンス**: Azure Information Protection は Azure Resource Manager デプロイをサポートしていないか、または "リソースの許可" や "リソースの拒否" などの組み込みの Azure Policy 定義を使用してデプロイを制限する機能をお客様に許可します。 ただし、お客様は、セキュリティとコンプライアンスセンターでポリシーのラベル付けによって、Azure Information Protection の使用を制限することができます。 

- [セキュリティとコンプライアンスセンターを使用して情報保護を管理する](/microsoft-365/compliance/protect-information?amp;preserve-view=true&view=o365-worldwide)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="logging-and-threat-detection"></a>ログと脅威検出

*詳細については、[Azure セキュリティ ベンチマークの「ログと脅威検出](/azure/security/benchmarks/security-controls-v2-logging-threat-protection)」を参照してください。*

### <a name="lt-2-enable-threat-detection-for-azure-identity-and-access-management"></a>LT-2:Azure ID とアクセスの管理のために脅威検出を有効にする

**ガイダンス**: Azure Information Protection は Azure Active Directory (Azure AD) に統合されています。これは、Azure の既定の id およびアクセス管理サービスです。 

より高度な監視と分析のユースケースを実現するために、Azure AD 提供のユーザーログを Azure AD レポートなどのソリューションや、Azure Monitor、Azure Sentinel などの SIEM/監視ツールと共に表示します。 

これらは次のとおりです。 

-   サインインレポート-サインインレポートには、マネージアプリケーションとユーザーサインインアクティビティの使用状況に関する情報が表示されます。

-   監査ログ - Azure AD 内のさまざまな機能によって行われたすべての変更についてログによる追跡可能性を提供します。 監査ログの例には、ユーザー、アプリ、グループ、ロール、ポリシーの追加や削除など、Azure AD 内のリソースに対して行われた変更が含まれます。

-   リスクの高いサインイン-リスクの高いサインインは、ユーザーアカウントの正当な所有者ではないユーザーによって実行された可能性があるサインイン試行の指標です。

-   リスクのフラグ付きユーザー - リスクの高いユーザーは、侵害された可能性があるユーザー アカウントの指標です。

また Azure Security Center は、失敗した認証試行の数が多すぎるなど、特定の疑わしいアクティビティについてもアラートを表示し、サブスクリプションでは非推奨のアカウントを警告することもできます。 基本的なセキュリティの検疫の監視に加えて、Security Center の脅威保護モジュールは、個々の Azure コンピューティングリソース (仮想マシン、コンテナー、app service など)、データリソース (SQL DB やストレージなど)、Azure サービスレイヤーから、さらに詳細なセキュリティアラートを収集することもできます。 この機能を使用すると、個々のリソース内でアカウントの異常を確認できます。

- [Azure AD でアクティビティ レポートを監査する](/azure/active-directory/reports-monitoring/concept-audit-logs)

- [Azure Identity Protection を有効にする](/azure/active-directory/identity-protection/overview-identity-protection)

- [Azure Security Center での脅威の防止](/azure/security-center/threat-protection)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="lt-4-enable-logging-for-azure-resources"></a>LT-4:Azure リソースのログ記録を有効にする

**ガイダンス**: Azure Information Protection は、組織のドキュメントと電子メールのデータ保護と、各要求のログを提供します。  これらの要求には、ユーザーがドキュメントや電子メールを保護する場合、このコンテンツを使用する場合、このサービスの管理者によって実行される操作、および Azure Information Protection の展開をサポートするために Microsoft operators によって実行される操作が含まれます。

Azure Information Protection によって生成されるログの種類は次のとおりです。

- 管理者ログ-保護サービスの管理タスクをログに記録します。 たとえば、このサービスが非アクティブ化されていて、スーパー ユーザー機能が有効で、ユーザーがサービスに対する管理者権限を委任されている場合などです。

- ドキュメント追跡-ユーザーが Azure Information Protection クライアントで追跡したドキュメントを追跡したり取り消したりできるようにします。 ユーザーに代わって、グローバル管理者がこれらのドキュメントを追跡することもできます。

- クライアントイベントログ-Azure Information Protection クライアントの使用状況アクティビティ。ローカルの Windows アプリケーションとサービスのイベントログに記録され、Azure Information Protection ます。

- クライアントログファイル-Azure Information Protection クライアントのトラブルシューティングログ

保護の使用状況ログを使用して、保護されたデータにアクセスしているユーザー、' その ' デバイス、および ' where ' を識別できます。 ログでは、保護されたコンテンツを正常に読み取ることができるかどうか、および保護された重要なドキュメントを読んだ相手を特定することができます。 

- [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="lt-5-centralize-security-log-management-and-analysis"></a>LT-5:セキュリティ ログの管理と分析を一元化する

**ガイダンス**: サポート担当者は、潜在的なインシデントを調査する際に、多様なデータソースを照会して使用することによって、イベント中に発生した問題の完全なビューを構築できることを確認します。 

さまざまなログを収集し、それを Azure Sentinel などの中央の SIEM ソリューションに送信することで、ブラインドスポットを回避して、キルチェーン全体で潜在的な攻撃者のアクティビティを追跡します。 ログでは、保護されたコンテンツを正常に読み取ることができるかどうか、および保護されている重要なドキュメントを読んだ相手を特定できます。 Insights と学習が他のアナリスト用にキャプチャされ、将来の履歴参照用にキャプチャされていることを確認します。  

Azure Sentinel により、事実上すべてのログソースに対して広範な Data Analytics と、インシデントのライフサイクル全体を管理するためのケース管理ポータルが提供されます。 調査中のインテリジェンス情報を、追跡とレポートのためにインシデントに関連付けることができます。 

- [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)

- [Azure Sentinel でインシデントを調査します](/azure/sentinel/tutorial-investigate-cases)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="lt-6-configure-log-storage-retention"></a>LT-6:ログの保持期間を構成する

**ガイダンス**: Azure Information Protection 組織のドキュメントと電子メールのデータ保護を提供し、すべての要求のログを記録します。  これらの要求には、ユーザーがドキュメントや電子メールを保護する場合、このコンテンツを使用する場合、このサービスの管理者によって実行される操作、および Azure Information Protection の展開をサポートするために Microsoft operators によって実行される操作が含まれます。

Azure Information Protection ワークスペースに収集して格納されているデータの量とそのリテンション期間は、テナントごとに大きく異なります。これは、エンドポイント探索データを収集するかどうか、スキャナーを展開したかどうか、アクセスする保護されたドキュメントの数などの Azure Information Protection 要因によって異なります。

Azure Monitor ログの使用量と推定コスト機能を使用して、格納されているデータの量を見積もり、確認したり、Log Analytics ワークスペースのデータ保有期間を制御したりすることができます。 

- [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)

- [Azure Monitor ログで使用量とコストを管理する](/azure/azure-monitor/platform/manage-cost-storage)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="incident-response"></a>インシデント対応

*詳細については、[Azure セキュリティ ベンチマークの「インシデント対応](/azure/security/benchmarks/security-controls-v2-incident-response)」を参照してください。*

### <a name="ir-1-preparation--update-incident-response-process-for-azure"></a>IR-1: 準備 – インシデント対応プロセスを Azure 用に更新する

**ガイダンス**:組織において、セキュリティ インシデントに対応するためのプロセスが用意されていること、Azure のこれらのプロセスが更新されていること、それらのプロセスを定期的に使用して準備されていることを確認します。

- [企業環境全体にセキュリティを実装する](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [インシデント対応のリファレンス ガイド](/microsoft-365/downloads/IR-Reference-Guide.pdf)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="ir-2-preparation--setup-incident-notification"></a>IR-2: 準備 – インシデント通知をセットアップする

**ガイダンス**:Azure Security Center でセキュリティ インシデントの連絡先情報を設定します。 この連絡先情報は、Microsoft Security Response Center (MSRC) でユーザーのデータが違法または権限のないユーザーによってアクセスされたことが検出された場合に、Microsoft からの連絡先として使用されます。 また、インシデント対応のニーズに応じて、異なる Azure サービスでインシデント アラートと通知をカスタマイズするオプションもあります。 

- [Azure Security Center のセキュリティ連絡先を設定する方法](/azure/security-center/security-center-provide-security-contact-details)

**Azure Security Center の監視**: はい

**責任**: Customer

### <a name="ir-3-detection-and-analysis--create-incidents-based-on-high-quality-alerts"></a>IR-3: 検出と分析 – 高品質のアラートに基づいてインシデントを作成する

**ガイダンス**:高品質のアラートを作成し、アラートの品質を測定するプロセスがあることを確認します。 これにより、過去のインシデントから教訓を学び、アナリストに対するアラートに優先順位を付けることができるので、擬陽性に時間を無駄にすることがありません。 

高品質のアラートは、過去のインシデントからの経験、検証されたコミュニティ ソース、およびさまざまなシグナル ソースの融合と関連付けによってアラートを生成してクリーンアップするように設計されたツールに基づいて構築できます。 

Azure Security Center では、多数の Azure 資産について高品質のアラートが提供されます。 ASC データ コネクタを使用してアラートを Azure Sentinel にストリーミングできます。 Azure Sentinel を使用すると、高度なアラート ルールを作成し、調査のためにインシデントを自動的に生成できます。 

エクスポート機能を使用して Azure Security Center のアラートと推奨事項をエクスポートし、Azure リソースへのリスクを特定します。 アラートと推奨事項を手動で、または継続した連続的な方法でエクスポートします。

- [エクスポートを構成する方法](/azure/security-center/continuous-export)

- [Azure Sentinel にアラートをストリーミングする方法](/azure/sentinel/connect-azure-security-center)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

### <a name="ir-4-detection-and-analysis--investigate-an-incident"></a>IR-4: 検出と分析 – インシデントを調査する

**ガイダンス**: アナリストが、潜在的なインシデントを調査する際に、さまざまなデータソースを照会して使用することで、何が起こったかを完全に把握できるようにします。 さまざまなログを収集して、キルチェーン全体で潜在的な攻撃者のアクティビティを追跡することで、ブラインドスポットを回避します。 さらに、insights と学習が他のアナリストや今後の履歴参照用にキャプチャされていることを確認します。  

調査のためのデータ ソースには、スコープ内のサービスおよび実行中のシステムから既に収集されている一元化されたログ ソースが含まれますが、次のものも含まれます。

- ネットワーク データ - ネットワーク セキュリティ グループのフロー ログ、Azure Network Watcher、Azure Monitor を使用して、ネットワーク フロー ログやその他の分析情報をキャプチャします。 

- 実行中のシステムのスナップショット: 

    - Azure 仮想マシンのスナップショット機能を使用して、実行中のシステムのディスクのスナップショットを作成します。 

    - オペレーティングシステムの組み込みメモリダンプ機能を使用して、実行中のシステムのメモリのスナップショットを作成します。

    - Azure サービスのスナップショット機能またはソフトウェア独自の機能を使用して、実行中のシステムのスナップショットを作成します。

Azure Sentinel により、事実上すべてのログソースに対して広範な Data Analytics と、インシデントのライフサイクル全体を管理するためのケース管理ポータルが提供されます。 調査中のインテリジェンス情報を、追跡とレポートのためにインシデントに関連付けることができます。 

- [Windows マシンのディスクのスナップショットを作成する](/azure/virtual-machines/windows/snapshot-copy-managed-disk)

- [Linux マシンのディスクのスナップショットを作成する](/azure/virtual-machines/linux/snapshot-copy-managed-disk)

- [Microsoft Azure サポートの診断情報とメモリ ダンプ コレクション](https://azure.microsoft.com/support/legal/support-diagnostic-information-collection/) 

- [Azure Sentinel でインシデントを調査します](/azure/sentinel/tutorial-investigate-cases)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="ir-5-detection-and-analysis--prioritize-incidents"></a>IR-5: 検出と分析 – インシデントの優先順位を付ける

**ガイダンス**:アラートの重要度と資産の機密性に基づいて、最初に注目するインシデントについてのコンテキストをアナリストに提供します。 

Azure Security Center によって各アラートに重大度が割り当てられるため、最初に調査する必要があるアラートの優先順位付けに役立ちます。 重要度は、アラートの発行に使用された Security Center の信頼度と、アラートの原因となったアクティビティの背後に悪意のある意図があったかどうかの信頼レベルに基づいて決まります。

さらに、タグを使用してリソースをマークし、Azure リソース (特に、機密データを処理するもの) を識別して分類するための命名システムを作成します。  インシデントが発生した Azure リソースと環境の重要度に基づいて、アラートの修復に優先順位を付けることは、お客様の責任です。

- [Security alerts in Azure Security Center](/azure/security-center/security-center-alerts-overview)

- [タグを使用した Azure リソースの整理](/azure/azure-resource-manager/resource-group-using-tags)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

### <a name="ir-6-containment-eradication-and-recovery--automate-the-incident-handling"></a>IR-6: 包含、根絶、復旧 – インシデントの処理を自動化する

**ガイダンス**:手動による反復タスクを自動化して、応答時間を短縮し、アナリストの負担を軽減します。 手動タスクの実行には時間がかかり、各インシデントの速度が低下し、アナリストが処理できるインシデントの数が減少します。 手動タスクではアナリストの疲労も増加します。これにより、遅延が発生する人的エラーのリスクが増加し、複雑なタスクに効果的に焦点を当てるアナリストの能力が低下します。 Azure Security Center と Azure Sentinel のワークフロー自動化機能を使用して、自動的にアクションをトリガーしたり、プレイブックを実行して受信したセキュリティ アラートに応答したりします。 プレイブックにより、通知の送信、アカウントの無効化、問題のあるネットワークの特定などのアクションが実行されます。 

- [Security Center でワークフロー自動化を構成する](/azure/security-center/workflow-automation)

- [Azure Security Center で脅威への自動対応を設定する](/azure/security-center/tutorial-security-incident#triage-security-alerts)

- [Azure Sentinel で脅威への自動対応を設定します](/azure/sentinel/tutorial-respond-threats-playbook)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

## <a name="posture-and-vulnerability-management"></a>体制と脆弱性の管理

*詳細については、[Azure セキュリティ ベンチマークの「体制と脆弱性の管理](/azure/security/benchmarks/security-controls-v2-vulnerability-management)」を参照してください。*

### <a name="pv-1-establish-secure-configurations-for-azure-services"></a>PV-1: Azure サービスのセキュリティで保護された構成を確立する 

**ガイダンス**: Azure Information Protection は、セキュリティとコンプライアンスセンターまたは PowerShell を使用して構成できます。 

セキュリティとコンプライアンスセンターでは、管理者は、機密ラベルを作成し、各ラベルが実行できる内容を定義し、ラベルを発行できます。 

ラベルを作成します。さまざまな機密レベルのコンテンツに対する組織の分類の分類に従って、機密ラベルを作成して名前を付けます。 ユーザーにとって意味のある共通名または用語を使用してください。 まだ設定されていない分類がある場合は、個人用、パブリック、一般、社外秘、非常に機密性の高い社外秘などのラベル名から始めることを検討してください。 その後、サブラベルを使用して、類似したラベルをカテゴリ別にグループ化することができます。 ラベルを作成するときに、ユーザーが適切なラベルを選択できるように、ツールヒントのテキストを使用します。

各ラベルに対して実行できる操作を定義します。各ラベルに関連付けられている保護設定を構成します。 たとえば、低い感度のコンテンツ ("全般" ラベルなど) にヘッダーまたはフッターのみを適用し、より高い感度のコンテンツ ("社外秘" ラベルなど) には透かしと暗号化を設定することができます。

ラベルを発行する: 機密ラベルが構成されたら、ラベルポリシーを使用して公開します。 ラベルを持つユーザーとグループ、および使用するポリシー設定を決定します。 1つのラベルを再利用できます。一度定義すると、別のユーザーに割り当てられた複数のラベルポリシーに含めることができます。 たとえば、少数のユーザーにラベルポリシーを割り当てることによって、機密ラベルをパイロットにすることができます。 組織全体でラベルを展開する準備ができたら、ラベルの新しいラベルポリシーを作成し、今度は [すべてのユーザー] を指定します。

PowerShell を使用するには、AIPService PowerShell モジュールをインストールします。 PowerShell では、管理者は次のタスクを他のタスクと共に実行できます。 

- オンプレミスの Rights Management (AD RMS または Windows RMS) から Azure Information Protection への移行
- 独自のテナントキーを生成して管理する-独自のキーを持ち込む (BYOK) シナリオ
- 組織の Rights Management サービスをアクティブ化または非アクティブ化する
- Azure Rights Management サービスの段階的なデプロイのオンボードコントロールを構成する
- 組織の Rights Management テンプレートを作成および管理する
- 組織の Rights Management サービスを管理する権限を持つユーザーとグループを管理する
- Rights Management の使用状況をログに記録して分析する

詳細については、次のリファレンスを参照してください。

- [セキュリティとコンプライアンスセンターの機密ラベルを使ってみる](/microsoft-365/compliance/get-started-with-sensitivity-labels?amp;preserve-view=true&view=o365-worldwide)

- [秘密度ラベルの作成と発行](/microsoft-365/compliance/create-sensitivity-labels?amp;preserve-view=true&view=o365-worldwide)

- [機密ラベルに暗号化を適用する](/microsoft-365/compliance/encryption-sensitivity-labels?amp;preserve-view=true&view=o365-worldwide)

- [Azure Information Protection 用 PowerShell](./administer-powershell.md)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pv-8-conduct-regular-attack-simulation"></a>PV-8: 定期的に攻撃シミュレーションを実施する

**ガイダンス**:必要に応じて、Azure リソースの侵入テストまたはレッド チーム アクティビティを実施し、セキュリティに関するすべての重大な調査結果が確実に修復されるようにします。
お客様の侵入テストが Microsoft のポリシーに違反しないように、Microsoft クラウド侵入テストの実施ルールに従ってください。 Microsoft が管理しているクラウド インフラストラクチャ、サービス、アプリケーションに対する Red Teaming およびライブ サイト侵入テストに関する Microsoft の戦略と実施を活用してください。

- [Azure での侵入テスト](/azure/security/fundamentals/pen-testing)

- [侵入テストの実施ルール](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Microsoft Cloud Red Teaming](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Azure Security Center の監視**: 適用なし

**責任**: 共有

## <a name="backup-and-recovery"></a>バックアップと回復

*詳細については、[Azure セキュリティ ベンチマークの「バックアップと回復」](/azure/security/benchmarks/security-controls-v2-backup-recovery)を参照してください。*

### <a name="br-4-mitigate-risk-of-lost-keys"></a>BR-4:キー紛失のリスクを軽減する

**ガイダンス**: Azure Information Protection を使用すると、ユーザーは Bring Your Own Key (byok) を使用して独自のキーを使用してテナントを構成することができます。 ユーザーが生成したキーは、保護のために Azure Key Vault に保存する必要があります。 Azure Key Vault を使用すると、論理的な削除、役割の分離、および分離されたセキュリティドメインによってキーが失われるのを防ぐことができます。 

- [Azure Information Protection Bring Your Own Key と Azure Key Vault との統合](./byok-price-restrictions.md)
- [Key Vault での論理的な削除の有効化](/azure/storage/blobs/storage-blob-soft-delete?tabs=azure-portal)

**Azure Security Center の監視**: はい

**責任**: Customer

## <a name="governance-and-strategy"></a>ガバナンスと戦略

*詳細については、[Azure セキュリティ ベンチマークの「ガバナンスと戦略](/azure/security/benchmarks/security-controls-v2-governance-strategy)」を参照してください。*

### <a name="gs-1-define-asset-management-and-data-protection-strategy"></a>GS-1: 資産の管理とデータ保護の戦略を定義する 

**ガイダンス**:システムとデータを継続的に監視および保護するための明確な戦略が文書化および伝達されるようにします。 ビジネスに不可欠なデータとシステムの検出、評価、保護、監視の優先順位を決定します。 

この戦略には、次の要素に関する文書化されたガイダンス、ポリシー、標準が含まれている必要があります。 

-   ビジネス リスクに応じたデータ分類標準

-   リスクと資産のインベントリに対するセキュリティ組織の可視性 

-   Azure サービスを使用するためのセキュリティ組織の承認 

-   ライフサイクルを通じた資産のセキュリティ

-   組織のデータ分類に従った必要なアクセス制御戦略

-   Azure 組み込みおよびサードパーティのデータ保護機能の使用

-   転送中および保存中のユース ケースのデータ暗号化要件

-   適切な暗号化標準

詳細については、次のリファレンスを参照してください。

- [Azure セキュリティ アーキテクチャに関する推奨事項 - ストレージ、データ、暗号化](/azure/architecture/framework/security/storage-data-encryption?amp;bc=%2fsecurity%2fcompass%2fbreadcrumb%2ftoc.json&toc=%2fsecurity%2fcompass%2ftoc.json)

- [Azure のセキュリティの基礎 - Azure のデータ セキュリティ、暗号化、ストレージ](/azure/security/fundamentals/encryption-overview)

- [クラウド導入フレームワーク - Azure のデータ セキュリティと暗号化のベスト プラクティス](/azure/security/fundamentals/data-encryption-best-practices?amp;bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json)

- [Azure セキュリティ ベンチマーク - アセット管理](/azure/security/benchmarks/security-benchmark-v2-asset-management)

- [Azure セキュリティ ベンチマーク - データ保護](/azure/security/benchmarks/security-benchmark-v2-data-protection)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-2-define-enterprise-segmentation-strategy"></a>GS-2: 企業のセグメント化戦略を定義する 

**ガイダンス**:ID、ネットワーク、アプリケーション、サブスクリプション、管理グループ、その他のコントロールを利用し、アセットへのアクセスをセグメント化する企業規模の戦略を確立します。

セキュリティ分離の必要性と、互いと通信し、データにアクセスする必要があるシステムの日常的操作を有効にするという必要性のバランスを慎重に取ります。

セグメント化戦略は、ネットワーク セキュリティ、ID とアクセス モデル、アプリケーション アクセス許可とアクセス モデル、人的プロセスの制御など、あらゆるコントロールの種類を対象として確実に一貫性をもって実装します。

- [Azure のセグメント化戦略に関するガイド (動画)](/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151)

- [Azure のセグメント化戦略に関するガイド (ドキュメント)](/security/compass/governance#enterprise-segmentation-strategy)

- [ネットワークのセグメント化を企業のセグメント化戦略に合わせる](/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-3-define-security-posture-management-strategy"></a>GS-3: セキュリティ態勢管理の戦略を定義する

**ガイダンス**:個々の資産とそれらがホストされている環境に対するリスクを継続的に測定し、軽減します。 高い価値を持つ資産と、攻撃に晒される可能性の高い部分 (公開されたアプリケーション、ネットワークのイングレス ポイントとエグレス ポイント、ユーザーと管理者のエンドポイントなど) を優先します。

- [Azure セキュリティ ベンチマーク - 体制と脆弱性の管理](/azure/security/benchmarks/security-benchmark-v2-posture-vulnerability-management)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-4-align-organization-roles-responsibilities-and-accountabilities"></a>GS-4: 組織の役割、責任、責務を整合させる

**ガイダンス**:セキュリティ組織における役割と責任に関する明確な戦略が文書化されて伝えられるようにします。 セキュリティに関する決定についてわかりやすく説明すること、共有される責任モデルについて全員に教育すること、クラウドをセキュリティで保護するテクノロジについて技術チームに教育することを優先とします。

- [Azure のセキュリティのベスト プラクティス 1 – 人: クラウド セキュリティに関する取り組みについてチームを教育する](/azure/cloud-adoption-framework/security/security-top-10#1-people-educate-teams-about-the-cloud-security-journey)

- [Azure のセキュリティのベスト プラクティス 2 - 人: クラウド セキュリティ テクノロジについてチームを教育する](/azure/cloud-adoption-framework/security/security-top-10#2-people-educate-teams-on-cloud-security-technology)

- [Azure のセキュリティのベスト プラクティス 3 - プロセス: クラウドのセキュリティに関する意思決定のアカウンタビリティを割り当てる](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-5-define-network-security-strategy"></a>GS-5: ネットワーク セキュリティ戦略を定義する

**ガイダンス**:組織全体のセキュリティ アクセス制御戦略の一環として、Azure ネットワーク セキュリティ アプローチを確立します。  

この戦略には、次の要素に関する文書化されたガイダンス、ポリシー、標準が含まれている必要があります。 

-   一元的なネットワーク管理とセキュリティ責任

-   エンタープライズ セグメント化戦略と一致する仮想ネットワーク セグメント化モデル

-   さまざまな脅威と攻撃のシナリオにおける修復戦略

-   インターネット エッジとイングレスおよびエグレス戦略

-   クラウドとオンプレミスのハイブリッド相互依存戦略

-   最新のネットワーク セキュリティ成果物 (例: ネットワーク図、参照ネットワーク アーキテクチャ)

詳細については、次のリファレンスを参照してください。
- [Azure のセキュリティのベスト プラクティス 11 - アーキテクチャ。単一の統合セキュリティ戦略](/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Azure セキュリティ ベンチマーク - ネットワーク セキュリティ](/azure/security/benchmarks/security-benchmark-v2-network-security)

- [Azure のネットワーク セキュリティの概要](/azure/security/fundamentals/network-overview)

- [エンタープライズ ネットワーク アーキテクチャ戦略](/azure/cloud-adoption-framework/ready/enterprise-scale/architecture)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-6-define-identity-and-privileged-access-strategy"></a>GS-6: ID と特権アクセス戦略を定義する

**ガイダンス**:組織全体のセキュリティ アクセス制御戦略の一環として、Azure の ID と特権アクセス アプローチを確立します。  

この戦略には、次の要素に関する文書化されたガイダンス、ポリシー、標準が含まれている必要があります。 

-   一元化された ID と認証システム、および他の内部および外部 ID システムとのその相互接続

-   さまざまなユース ケースおよび条件における強力な認証方法

-   高い特権を持つユーザーの保護

-   異常なユーザー アクティビティの監視と処理  

-   ユーザー ID とアクセスの確認と調整のプロセス

詳細については、次のリファレンスを参照してください。

- [Azure セキュリティ ベンチマーク - ID 管理](/azure/security/benchmarks/security-benchmark-v2-identity-management)

- [Azure セキュリティ ベンチマーク - 特権アクセス](/azure/security/benchmarks/security-benchmark-v2-privileged-access)

- [Azure のセキュリティのベスト プラクティス 11 - アーキテクチャ。単一の統合セキュリティ戦略](/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Azure ID 管理のセキュリティの概要](/azure/security/fundamentals/identity-management-overview)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-7-define-logging-and-threat-response-strategy"></a>GS-7: ログ記録と脅威対応戦略を定義する

**ガイダンス**:コンプライアンス要件を満たしながら脅威を迅速に検出して修復するための、ログ記録と脅威対応戦略を確立します。 アナリストが、統合や手動による手順ではなく、脅威の対応に集中できるように、質の高いアラートとシームレスなエクスペリエンスを提供することを優先してください。 

この戦略には、次の要素に関する文書化されたガイダンス、ポリシー、標準が含まれている必要があります。 

-   セキュリティ運用 (SecOps) 組織の役割と責任 

-   NIST または他の業界フレームワークと一致する、明確に定義されたインシデント対応プロセス 

-   脅威の検出、インシデント対応、コンプライアンスのニーズに対応するためのログのキャプチャと保持

-   脅威、SIEM、組み込みの Azure 機能、およびその他のソースを使用した、脅威に関する情報の一元的な可視化 

-   顧客、サプライヤー、および関心を持つパブリック パーティに関するコミュニケーションと通知の計画

-   ログ記録と脅威の検出、フォレンジック、攻撃の修復などのインシデント処理に Azure 組み込みおよびサードパーティのプラットフォームを使用

-   インシデントとインシデント発生後のアクティビティを処理するためのプロセス (教訓や証拠の保持など)

詳細については、次のリファレンスを参照してください。

- [Azure セキュリティ ベンチマーク - ログと脅威検出](/azure/security/benchmarks/security-benchmark-v2-logging-threat-detection)

- [Azure セキュリティ ベンチマーク - インシデント対応](/azure/security/benchmarks/security-benchmark-v2-incident-response)

- [Azure のセキュリティのベスト プラクティス 4 - プロセス: クラウドのインシデント対応プロセスを更新する](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Azure 導入フレームワーク、ログ、およびレポートの決定ガイド](/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)

- [Azure のエンタープライズ スケーリング、管理、監視](/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="next-steps"></a>次のステップ

- 「[Azure セキュリティ ベンチマーク V2 の概要](/azure/security/benchmarks/overview)」を参照してください。
- [Azure セキュリティ ベースライン](/azure/security/benchmarks/security-baselines-overview)の詳細について学習する