---
title: Azure Information Protection に関してよく寄せられる質問
description: Azure Information Protection とその保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問をいくつか示します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: c42f2459861b7b7167469ddadd7c3ff399d47f48
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97381964"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure Information Protection に関してよく寄せられる質問

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection、または Azure Rights Management サービス (Azure RMS) に関して質問がございますか。 ここで回答を探してみてください。

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Azure Information Protection と Microsoft Information Protection の違いは何ですか。

Azure Information Protection とは異なり、 [Microsoft Information Protection](https://www.microsoft.com/security/business/information-protection) は購入できるサブスクリプションや製品ではありません。 代わりに、組織の機密情報を保護するのに役立つ製品と統合された機能のフレームワークです。

**Microsoft Information Protection 製品には次のものが含ま** れます。
- Azure Information Protection
- Microsoft 365 Information Protection (Microsoft 365 DLP など)
- Windows Information Protection
- Microsoft Cloud App Security

**Microsoft Information Protection の機能は** 次のとおりです。
- 統一されたラベルの管理
- Office アプリに組み込まれているエンドユーザーのラベル付けエクスペリエンス
- Windows が統合ラベルを理解し、データに保護を適用する機能
- Microsoft Information Protection SDK
- ラベル付きで保護された Pdf を表示するための Adobe Acrobat Reader の機能

詳細については、「 [機密データを保護するための情報保護機能](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)」を参照してください。

## <a name="whats-the-difference-between-labels-in-microsoft-365-and-labels-in-azure-information-protection"></a>Microsoft 365 のラベルと Azure Information Protection のラベルの違いは何ですか。

もともと、Microsoft 365 保持されているのは、そのコンテンツが Microsoft 365 services に格納されている場合に、監査と保持のためにドキュメントと電子メールを分類できるようにする、 [保持ラベル](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30)のみでした。 

これに対し、Azure Information Protection ラベルは、Azure portal の AIP クラシッククライアントを使用して構成されており、オンプレミスまたはクラウドのどちらに保存されたかにかかわらず、ドキュメントと電子メールに一貫した分類と保護ポリシーを適用できます。

Microsoft 365 では、保有期間のラベルに加えて、 [機密ラベル](/microsoft-365/compliance/sensitivity-labels) もサポートされるようになりました。 機密ラベルは、次の管理センターで作成および構成できます。

- Office 365 セキュリティ/コンプアライアンス センター
- Microsoft 365 セキュリティ センター
- Microsoft 365 コンプライアンス センター

Azure portal に従来の AIP ラベルが構成されている場合は、それらを機密ラベルと統合ラベル付けクライアントに移行することをお勧めします。 詳細については、「[チュートリアル:  Azure Information Protection (AIP) クラシック クライアントから、統合ラベル付けクライアントへの移行](tutorial-migrating-to-ul.md)」を参照してください。

詳細については、「[Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)」(機密データを保護するために使用できる情報保護機能の発表) をご覧ください。

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>テナントが統一されたラベル付けプラットフォームにあるかどうかを確認する方法はありますか

テナントが統一されたラベル付けプラットフォームにある場合、統一されたラベル [付けをサポートするクライアントとサービス](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)が使用できる機密ラベルをサポートします。 2019年6月以降に Azure Information Protection のサブスクリプションを取得した場合、テナントは自動的に統合されたラベル付けプラットフォームになり、それ以上の操作は必要ありません。 また、ユーザーが Azure Information Protection ラベルを移行したため、テナントがこのプラットフォーム上に存在する場合もあります。

テナントが統一されたラベル付けプラットフォームにない場合は、Azure portal の **Azure Information Protection** ペインに次の情報バナーが表示されます。

![移行情報バナー](media/migration-status-banner.png)

また、[ **Azure Information Protection** の  >  統合ラベルの **管理**] に移動して、統一さ  >  れた **ラベル** の状態を確認することもできます。

|Status |説明  |
|---------|---------|
|**アクティブ**     |  テナントは、統一されたラベル付けプラットフォーム上にあります。 <br />Microsoft 365 コンプライアンスセンターで [ラベルを作成、構成、および発行](/microsoft-365/compliance/create-sensitivity-labels) することができます。       |
|**非アクティブ化**    |  テナントは、統一されたラベル付けプラットフォーム上にありません。 <br />移行の手順とガイダンスについては、「 [Azure Information Protection ラベルを統合秘密度ラベルに移行する方法](configure-policy-migrate-labels.md)」を参照してください。       |
| | |

## <a name="whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients"></a>Azure Information Protection クラシックと統合されたラベル付けクライアントの違いは何ですか。

*クラシック* クライアントと呼ばれるレガシ Azure Information Protection クライアントは、Azure からラベルとポリシー設定をダウンロードし、Azure portal から [AIP ポリシー](overview-policy.md)を構成できます。

統一された *ラベル付けクライアント* は最新の更新プログラムが適用された最新のクライアントであり、複数のアプリケーションやサービスで使用される統一されたラベル付けプラットフォームをサポートします。 統一されたラベル付けクライアントは、次の管理センターから [機密ラベル](/microsoft-365/compliance/sensitivity-labels) とポリシー設定をダウンロードします。

- Office 365 セキュリティ/コンプアライアンス センター
- Microsoft 365 セキュリティ センター
- Microsoft 365 コンプライアンス センター

管理者の方は、 [「Windows のラベル付けソリューションを選択](rms-client/use-client.md#choose-your-windows-labeling-solution)する」で詳細を確認してください。

### <a name="classic-client-deprecation"></a>従来のクライアントの非推奨

統一された効率的なカスタマーエクスペリエンスを提供するために、Azure Portal での **Azure Information Protection クラシッククライアント** および **ラベル管理** は、 **2021 年3月31日** に **非推奨** となる予定です。 

非推奨になった後も、クライアントは引き続き正常に動作します。 ただし、管理者はポータルでポリシーを更新することはできません。また、従来のクライアントに対して修正や変更は提供されません。

このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

現在、クラシッククライアントが展開されている場合は、統合されたラベル付けクライアントにアップグレードすることをお勧めします。 詳細については、「」を参照してください。

- [チュートリアル: クラシッククライアントから統合ラベル付けクライアントへの移行](tutorial-migrating-to-ul.md)
- [Azure Information Protection ラベルを統合秘密度ラベルに移行する方法](configure-policy-migrate-labels.md)
### <a name="identify-the-client-you-have-installed"></a>インストールしたクライアントを特定する

クラシックまたは統合ラベルクライアントがインストールされているかどうかを理解する必要があるユーザーは、次のいずれかを実行できます。

- Office アプリで、[ **秘密度** ] または [ **保護** ] ツールバーボタンを確認します。 統一されたラベル付けクライアントは、[ **秘密度** :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: ] ボタンを表示し、クラシッククライアントは [ **保護** ] ボタンを表示します。 

- インストールされている Azure Information Protection アプリケーションのバージョン番号を確認します。

    - バージョン1.x は、クラシッククライアントがあることを示し **ています** 。 例: **1.54.59.0**
    - バージョン **2.x** は、統一されたラベル付けクライアントがあることを示しています。 例: **2.8.85.0**

    たとえば、[Windows の **設定] > [アプリと機能** ] 領域で、[ **Microsoft Azure Information Protection** アプリケーション] までスクロールし、バージョン番号を確認します。

    :::image type="content" source="media/client-about.png" alt-text="Azure Information Protection クライアントのバージョンを確認する":::

## <a name="when-is-the-right-time-to-migrate-my-labels"></a>ラベルを移行するのに最適なタイミング

Azure Information Protection ラベルを統一されたラベル付けプラットフォームに移行することをお勧めします。これにより、統一されたラベル付けを [サポートする他のクライアントおよびサービス](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)との感度ラベルとして使用できるようになります。

詳細および手順については、「 [Azure Information Protection ラベルを統合秘密度ラベルに移行する方法](configure-policy-migrate-labels.md)」を参照してください。

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>ラベルを移行した後に使用する管理ポータルはどれですか。

Azure portal でラベルを移行したら、インストールしたクライアントに応じて、次のいずれかの場所で管理を続行します。

|クライアント  |説明  |
|---------|---------|
|[クライアントとサービスのみの統一](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) されたラベル付け    |  統一されたラベル付けクライアントがインストールされている場合は、管理センターの1つでラベルを管理します。 Office 365 セキュリティ & コンプライアンスセンター、Microsoft 365 security center、または Microsoft 365 コンプライアンスセンターです。 統合ラベル付けのクライアントは、これらの管理センターからラベルとポリシー設定をダウンロードします。 <br /><br />手順については、「 [秘密度ラベルとそのポリシーを作成して構成する](/microsoft-365/compliance/create-sensitivity-labels)」を参照してください。     |
|[従来のクライアント](./rms-client/aip-client.md) のみ  | ラベルを移行した後も従来のクライアントがインストールされている場合は、引き続き Azure portal を使用してラベルとポリシー設定を編集します。 クラシッククライアントは、Azure からラベルとポリシー設定を引き続きダウンロードします。
|AIP [クラシッククライアント](./rms-client/aip-client.md) と統一された [ラベル付け](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) クライアントの両方     | 両方のクライアントがインストールされている場合は、管理センターまたは Azure portal を使用してラベルを変更します。 <br /><br />クラシッククライアントが管理センターで行われたラベルの変更を取得するには、Azure portal に戻り、発行します。 [Azure portal > **Azure Information Protection-統合ラベル** ] ウィンドウで、[ **発行**] を選択します。  <br /><br /> [中央レポート機能](reports-aip.md)と[スキャナー](deploy-aip-scanner.md)には、引き続き Azure portal を使用します。     |
| | |

## <a name="do-i-need-to-re-encrypt-my-files-after-moving-to-sensitivity-labels-and-the-unified-labeling-platform"></a>機密ラベルと統合されたラベル付けプラットフォームに移行した後、ファイルを再暗号化する必要がありますか。

いいえ。 AIP クラシッククライアントからの移行後、および Azure portal で管理されているラベルを使用して、機密ラベルと統一されたラベル付けプラットフォームに移行した後、ファイルを再暗号化する必要はありません。

移行した後、ラベル管理センター (Microsoft security center、Microsoft コンプライアンスセンター、Microsoft セキュリティ & コンプライアンスセンターなど) からラベルとラベル付けポリシーを管理します。 

詳細については、Microsoft 365 のドキュメントの「 [機密ラベルについ](/microsoft-365/compliance/sensitivity-labels) て」および「 [統合ラベルの移行](https://techcommunity.microsoft.com/t5/microsoft-security-and/understanding-unified-labeling-migration/ba-p/783185) に関するブログ」を参照してください。


## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure Information Protection と Azure Rights Management の違いは何ですか。

Azure Information Protection (AIP) は、組織のドキュメントや電子メールの分類、ラベル付け、保護を提供します。

コンテンツは、AIP のコンポーネントである Azure Rights Management サービスを使用して保護されます。 

詳細については、「 [AIP によるデータの保護](aip-classification-and-protection.md#how-aip-protects-your-data) 」および「 [Azure Rights Management とは](what-is-azure-rms.md)」を参照してください。

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>Azure Information Protection の id 管理の役割は何ですか。

Id 管理は、保護されたコンテンツにアクセスするためにユーザーが有効なユーザー名とパスワードを持っている必要があるため、AIP の重要なコンポーネントです。

Azure Information Protection でデータを保護するしくみについての詳細は、「[データのセキュリティ保護における Azure Information Protection の役割](/enterprise-mobility-security/solutions/azure-information-protection-securing-data)」をご覧ください。 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。

AIP サブスクリプションの詳細については、「 [Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection) 」ページのサブスクリプション情報と機能一覧を参照してください。

Azure Rights Management data protection を含む Microsoft 365 サブスクリプションがある場合は、AIP との統合の詳細について [Azure Information Protection ライセンスデータシート](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) をダウンロードしてください。

ライセンスについてまだご質問がありますか。 [ライセンスについてよく寄せられる質問](https://azure.microsoft.com/pricing/details/information-protection#faq)のセクションで回答されているかどうかを確認してください。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Azure Information Protection を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?

Microsoft 365 テナントまたは Azure AD テナントのグローバル管理者は、Azure Information Protection のすべての管理タスクを明らかに実行できます。 

ただし、管理アクセス許可を他のユーザーに割り当てる場合は、次の役割を使用します。

- [Azure Information Protection 管理者](#azure-information-protection-administrator)
- [コンプライアンス管理者またはコンプライアンスデータ管理者](#compliance-administrator-or-compliance-data-administrator)
- [セキュリティ閲覧者またはグローバルリーダー](#security-reader-or-global-reader)
- [セキュリティ管理者](#security-administrator)
- [Azure Rights Management 全体管理者とコネクタ管理者](#azure-rights-management-global-administrator-and-connector-administrator)

また、管理タスクと役割を管理する際には、次の点に注意してください。

|トピック  |詳細  |
|---------|---------|
|**サポートされているアカウントの種類**     | Microsoft アカウントは、一覧表示されているいずれかの管理者ロールにアカウントが割り当てられている場合でも、Azure Information Protection の代理管理ではサポートされません。         |
|**オンボードコントロール**     |[オンボーディング コントロール](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成してある場合は、RMS コネクタを除き、Azure Information Protection を管理する機能に影響はありません。 <br /><br />たとえば、オンボードコントロールを構成して、コンテンツを保護する機能が *IT 部門* のグループに限定されるようにした場合、RMS コネクタのインストールと構成に使用するアカウントは、そのグループのメンバーである必要があります。          |
|**保護の削除**     |  管理者は、Azure Information Protection によって保護されたドキュメントまたは電子メールから保護を自動的に削除することはできません。 <br /><br />スーパーユーザーとして割り当てられているユーザーのみが保護を削除でき、スーパーユーザー機能が有効になっている場合のみです。 <br /><br />Azure Information Protection に対する管理アクセス許可を持つすべてのユーザーは、スーパーユーザー機能を有効にし、自分のアカウントを含むスーパーユーザーとしてユーザーを割り当てることができます。<br /><br />これらのアクションは、管理者ログに記録されます。 <br /><br />詳細については、「 [Azure Information Protection および探索サービスまたはデータ回復用のスーパーユーザーの構成](configure-super-users.md)」のセキュリティのベストプラクティスに関するセクションを参照してください。 <br><br>**ヒント**: コンテンツが SharePoint または OneDrive に保存されている場合、管理者は [SensitivityLabelEncryptedFile](/powershell/module/sharepoint-online/unlock-sposensitivitylabelencryptedfile) コマンドレットを実行して、秘密度ラベルと暗号化の両方を削除できます。 詳細については、[Microsoft 365 のドキュメント](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files#remove-encryption-for-a-labeled-document)を参照してください。 |
|**統一されたラベル付けストアへの移行**      |  Azure Information Protection ラベルを統合ラベルストアに移行する場合は、「移行に関するドキュメント」の次のセクションを必ず参照してください。 <br />[統一されたラベル付けプラットフォームをサポートする管理ロール](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform)。 |
| | |
### <a name="azure-information-protection-administrator"></a>Azure Information Protection 管理者

管理者はこの Azure Active Directory 管理者ロールを使用して Azure Information Protection を構成できますが、他のサービスは構成できません。 

この役割を持つ管理者は、次のことができます。

- Azure Rights Management protection サービスのアクティブ化と非アクティブ化
- 保護設定とラベルを構成する
- Azure Information Protection ポリシーを構成する
- [Azure Information Protection クライアント](./rms-client/clientv2-admin-guide-powershell.md)と[aipservice モジュール](administer-powershell.md)のすべての PowerShell コマンドレットを実行します。
    
ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。

> [!NOTE]
> このロールは、ユーザーのドキュメントの追跡と取り消しをサポートしていません。テナントが統一された [ラベル付けプラットフォーム](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)にある場合、Azure portal ではサポートされません。
    
### <a name="compliance-administrator-or-compliance-data-administrator"></a>コンプライアンス管理者またはコンプライアンスデータ管理者

これらの Azure Active Directory 管理者ロールにより、管理者は次のことができます。

- Azure Rights Management Protection サービスのアクティブ化と非アクティブ化を含む Azure Information Protection の構成
- 保護設定とラベルを構成する
- Azure Information Protection ポリシーを構成する
- [Azure Information Protection クライアント](./rms-client/clientv2-admin-guide-powershell.md)および[aipservice モジュール](administer-powershell.md)から、すべての PowerShell コマンドレットを実行します。 

ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。 

これらのロールが割り当てられているユーザーの他のアクセス許可については、Azure Active Directory のドキュメントの「 [利用可能な役割](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) 」セクションを参照してください。

> [!NOTE]
> これらのロールは、ユーザーのドキュメントの追跡と取り消しをサポートしていません。
>     
    
### <a name="security-reader-or-global-reader"></a>セキュリティ閲覧者またはグローバルリーダー

これらのロールは [Azure Information Protection analytics](reports-aip.md) にのみ使用され、管理者は次のことを行うことができます。

- ラベルがどのように使用されているかを表示する
- ラベル付きドキュメントと電子メールへのユーザーアクセスを監視する
- 分類に加えられた変更の表示
- 保護する必要がある機密情報が含まれているドキュメントを識別する 

この機能は Azure Monitor を使用するため、サポート [RBAC ロール](reports-aip.md#permissions-required-for-azure-information-protection-analytics)も必要です。

### <a name="security-administrator"></a>セキュリティ管理者

この Azure Active Directory 管理者ロールを使用すると、管理者は Azure portal の Azure Information Protection と、他の Azure サービスのいくつかの側面を構成できます。 

このロールを持つ管理者は、 [AIPService モジュールから PowerShell コマンドレット](administer-powershell.md)を実行したり、ユーザーのドキュメントを追跡したり取り消したりすることはできません。
    
ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。 

この役割のユーザーが持つその他のアクセス許可を確認するには、Azure Active Directory ドキュメントの「[使用可能なロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles)」セクションを参照してください。

### <a name="azure-rights-management-global-administrator-and-connector-administrator"></a>Azure Rights Management 全体管理者とコネクタ管理者

グローバル管理者ロールを使用すると、ユーザーは、他のクラウドサービスのグローバル管理者になることなく、 [AIPService モジュールからすべての PowerShell コマンドレット](administer-powershell.md) を実行できます。

コネクタ管理者ロールは、ユーザーが Rights Management (RMS) コネクタのみを実行できるようにします。 

これらの管理者ロールは、管理コンソールにアクセス許可を付与したり、ユーザーのドキュメントの追跡と取り消しをサポートしたりすることはありません。
    
これらの管理者ロールのいずれかを割り当てるには、AIPService PowerShell コマンドレットを使用し[ます。](/powershell/module/aipservice/add-aipservicerolebasedadministrator)

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection はオンプレミスおよびハイブリッドのシナリオをサポートしますか?

はい。 Azure Information Protection はクラウドベースのソリューションですが、クラウドだけでなく、オンプレミスに保存されているドキュメントや電子メールの分類、ラベル付け、および保護が可能です。

Exchange Server、SharePoint Server、および Windows ファイルサーバーがある場合は、次のいずれかまたは両方の方法を使用します。

- これらのオンプレミスサーバーが Azure Rights Management サービスを使用して電子メールとドキュメントを保護できるように、 [Rights Management コネクタ](deploy-rms-connector.md) をデプロイします。
- Active Directory ドメインコントローラーを Azure AD と同期してフェデレーションし、ユーザーにとってシームレスな認証エクスペリエンスを実現します。 たとえば、 [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect)を使用します。

Azure Rights Management サービスは、必要に応じて XrML 証明書を自動的に生成して管理するため、オンプレミスの PKI は使用しません。 

Azure Rights Management での証明書の使用方法の詳細については、「 [Azure RMS の使用方法: 初めての使用、コンテンツ保護、コンテンツ消費」のチュートリアル](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)を参照してください。

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Azure Information Protection ではどのようなデータの種類を分類し、保護できますか?

Azure Information Protection では、メール メッセージやドキュメントがオンプレミスまたはクラウドのどちらに配置されていても、それらを分類し、管理することができます。 これらのドキュメントには、Word ドキュメント、Excel スプレッドシート、PowerPoint プレゼンテーション、PDF ドキュメント、テキストベースのファイル、および画像ファイルが含まれます。 

詳細については、「 [サポートされているファイルの種類](./rms-client/clientv2-admin-guide-file-types.md)の一覧」を参照してください。

> [!NOTE]
> Azure Information Protection では、データベースファイル、予定表アイテム、Yammer の投稿、Sway コンテンツ、OneNote ノートブックなどの構造化データを分類して保護することはできません。
> 

> [!TIP]
> Power BI では、機密ラベルを使用した分類がサポートされており、これらのラベルから、.pdf、.xls、.ppt というファイル形式にエクスポートされたデータに保護を適用できます。 詳細については、「[Power BI におけるデータ保護](/power-bi/admin/service-security-data-protection-overview)」を参照してください。
> 
## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>条件付きアクセスに利用できるクラウド アプリとして Azure Information Protection が一覧に記載されています。これはどのように動作しますか。

はい。プレビューサービスとして、Azure Information Protection の条件付きアクセスを構成 Azure AD ことができます。

Azure Information Protection で保護されているドキュメントをユーザーが開くとき、標準的な条件付きアクセス コントロールに基づき、管理者は自分のテナントでユーザーをブロックするか、アクセス許可を与えることができるようになりました。 最も一般的に要求される条件の 1 つが多要素認証 (MFA) を要求することです。 もう 1 つは、デバイスが [Intune ポリシーに準拠する](/intune/protect/conditional-access-intune-common-ways-use)必要があるということです (たとえば、モバイル デバイスがパスワード要件やオペレーティング システムの最小バージョンを満たすようにする)。また、コンピューターはドメインに参加する必要があります。

チュートリアル形式の例が必要であれば、ブログ投稿の「[Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/)」 (Azure Information Protection の条件付きアクセス ポリシー) を参照してください。

追加情報:

|トピック  |詳細  |
|---------|---------|
|**評価の頻度**    | Windows コンピューターと現在のプレビューリリースでは、 [ユーザー環境が初期化さ](./how-does-it-work.md#initializing-the-user-environment) れると (このプロセスはブートストラップとも呼ばれます)、その後30日ごとに、Azure Information Protection の条件付きアクセスポリシーが評価されます。<br /><br />条件付きアクセスポリシーが評価される頻度を微調整するには、 [トークンの有効期間を構成](/azure/active-directory/active-directory-configurable-token-lifetimes)します。       |
|**管理者アカウント**     |条件付きアクセスポリシーに管理者アカウントを追加しないことをお勧めします。これらのアカウントは、Azure portal の [Azure Information Protection] ウィンドウにアクセスできないためです。         |
|**MFA と B2B コラボレーション**     | 他の組織とのコラボレーション (B2B) のための条件付きアクセス ポリシーで MFA を使用する場合は、[Azure AD B2B コラボレーション](/azure/active-directory/b2b/what-is-b2b)を使用して、他の組織と共有するユーザーのためのゲスト アカウントを作成する必要があります。        |
|**使用条件のプロンプト**     |  Azure AD 12 月2018プレビューリリースでは、保護されたドキュメントを初めて開く前に、 [使用条件に同意するようにユーザーに求める](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822) ことができるようになりました。       |
|**クラウド アプリ**     |  多くのクラウド アプリで条件付きアクセスを使用する場合、選択対象の一覧に **Microsoft Azure Information Protection** が表示されないことがあります。 <br /><br />その場合、一覧の上にある検索ボックスを使用します。 「Microsoft Azure Information Protection」と入力し、利用可能アプリを絞り込みます。 サポートされているサブスクリプションがある場合、選択対象として **Microsoft Azure Information Protection** が表示されます。        |
| | |

> [!NOTE]
> 条件付きアクセスの Azure Information Protection サポートは、現在プレビューの段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 
> 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Azure Information Protection が Microsoft Graph Security のセキュリティ プロバイダーとして記載されています。これはどのように動作しますか? また、どのようなアラートを受信できますか?

はい。公共プレビュー サービスとして、**Azure Information Protection の異常なデータ アクセス** に対するアラートを受信できるようになりました。 Azure Information Protection によって保護されているデータに対する異常なアクセスの試行があると、このアラートがトリガーされます。 たとえば、異常に大量のデータへのアクセス、不自然な時間帯でのアクセス、または不明な場所からのアクセスなどです。

このようなアラートは、データ関連の高度な攻撃や、環境内部の脅威を検出するのに役立ちます。 これらのアラートでは、保護されたデータにアクセスするユーザーの動作をプロファイルするために機械学習が使用されます。 

Azure Information Protection のアラートにアクセスするには、[Microsoft Graph Security API を使用します](/graph/api/resources/security-api-overview)。または、Azure Monitor を使用して、Splunk や IBM Qradar などの SIEM ソリューションに[アラートをストリームする](/graph/security-integration)ことができます。

Microsoft Graph Security API について詳しくは、「[Microsoft Graph Security API の概要](/graph/security-concept-overview)」をご覧ください。

> [!NOTE]
> Microsoft Graph セキュリティの Azure Information Protection サポートは、現在プレビューの段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 
> 

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>新しいリリースは、Azure Information Protection について間もなく提供される予定です。いつリリースされますか?

技術文書には今後のリリースに関する情報は含まれません。 この種類の情報については、 [Microsoft 365 ロードマップ](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent)を使用して、 [Enterprise Mobility + Security ブログ](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services)を確認してください。

## <a name="is-azure-information-protection-suitable-for-my-country"></a>自分の国に Azure Information Protection は適していますか?

国によって、さまざまな要件と規制があります。 組織のこの質問に対する回答は、[国ごとの適合性](./compliance.md#suitability-for-different-countries)に関する記事が役立ちます。

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Azure Information Protection は GDPR にどのように役立ちますか?

[!INCLUDE [gdpr-hybrid-note](includes/gdpr-hybrid-note.md)]

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>法律、法令遵守、SLA など、Azure Information Protection に関するサポート情報はどこで入手できますか。
「[Azure Information Protection のコンプライアンスとサポート情報](./compliance.md)」を参照してください。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Azure Information Protection の問題を報告またはフィードバックを送信するにはどうすればよいですか。

テクニカル サポートの場合は、標準のサポート チャネルを使用するか、[Microsoft サポートに問い合わせ](information-support.md#to-contact-microsoft-support)てください。

[Azure Information Protection の Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>質問がここにない場合はどうすればよいですか。

まず、分類とラベル付け、またはデータ保護に固有のよく寄せられる質問を確認してください。 [Azure Rights Management サービス (Azure RMS)](what-is-azure-rms.md)は、Azure Information Protection のデータ保護テクノロジを提供します。 Azure RMS は分類およびラベル付けと併用するか、単体で使用できます。 

- [分類とラベル付けに関してよく寄せられる質問](faqs-infoprotect.md)

- [データ保護に関してよく寄せられる質問](faqs-rms.md)

- [クラシッククライアントのみに関する Faq](faqs-classic.md)

質問に答えがない場合は、「 [Azure Information Protection の情報とサポート](information-support.md)」に記載されているリンクとリソースを参照してください。
