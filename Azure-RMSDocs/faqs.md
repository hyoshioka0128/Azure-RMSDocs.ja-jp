---
title: Azure Information Protection に関してよく寄せられる質問
description: Azure Information Protection とその保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問をいくつか示します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 0ba1046b18c8500130572e054e2bdd6e3a90fc5c
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73561404"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure Information Protection に関してよく寄せられる質問

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection、または Azure Rights Management サービス (Azure RMS) に関して質問がございますか。 ここで回答を探してみてください。

これらの FAQ ページは定期的に更新されます。新しい情報は [Azure Information Protection 技術ブログ](https://aka.ms/AIPblog)上の月次のドキュメント更新発表に一覧表示されます。

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Azure Information Protection と Microsoft Information Protection の違いは何ですか。

Azure Information Protection とは異なり、Microsoft Information Protection は購入できるサブスクリプションや製品ではありません。 そうではなく、これは組織の機密情報を保護するのに役立つ製品および統合された機能のフレームワークです。

- このフレームワークに含まれる個々の製品には、Azure Information Protection、Office 365 Information Protection (たとえば Office 365 DLP)、Windows Information Protection、Microsoft Cloud App Security などがあります。 

- このフレームワークに含まれる統合された機能としては、統合ラベルの管理、Office アプリに組み込みのエンド ユーザーのラベル付けエクスペリエンス、Windows で統合ラベルを使用したりデータに保護を適用したりする機能、Microsoft Information Protection SDK、ラベル付けされた PDF と保護された PDF を表示する Adobe Acrobat Reader の新機能などがあります。

詳細については、「[Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)」(機密データを保護するために使用できる情報保護機能の発表) をご覧ください。

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Azure Information Protection のラベルと Office 365 のラベルにはどのような違いがありますか。

当初は、Office 365 には[保有期間ラベル](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30)のみがあり、ドキュメントおよび電子メールのコンテンツが Office 365 サービス内にある場合に、それらを分類して監査および保持することができました。 これに対して、Azure Information Protection のラベルでは、ドキュメントおよび電子メールがオンプレミスのものであるかクラウド内のものであるかに関係なく、ドキュメントと電子メールに対して一貫性のある分類および保護ポリシーを適用できます。

州オーランドの Microsoft Ignite 2018 で発表された管理センターの1つで、リテンション期間のラベルに加えて、[機密ラベル](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)を作成して構成できるようになりました。 Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security Centerまたは Microsoft 365 コンプライアンスセンター。 Office アプリでは、既存の Azure Information Protection ラベルを新しい統合ラベルストアに移行して、機密ラベルとして使用することができます。 

統合ラベル付けの管理と各ラベルのサポート方法について詳しくは、ブログ記事「[Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)」 (機密データの保護に役立つ情報保護機能の可用性の発表) をご覧ください。

既存のラベルの移行の詳細については、「 [Azure Information Protection ラベルを統合秘密度ラベルに移行する方法](configure-policy-migrate-labels.md)」を参照してください。

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>テナントが統一されたラベル付けプラットフォームにあるかどうかを確認する方法はありますか

テナントが統一されたラベル付けプラットフォームにある場合、[統一ラベル付けをサポートするクライアントとサービス](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)は、秘密度ラベルを使用できます。 2019年6月以降に Azure Information Protection のサブスクリプションを取得した場合、テナントは自動的に統合されたラベル付けプラットフォームになり、それ以上の操作は必要ありません。 また、ユーザーが Azure Information Protection ラベルを移行したため、テナントがこのプラットフォーム上に存在する場合もあります。

状態を確認するには、Azure portal で  **Azure Information Protection**にアクセスして > の**統合**されたラベルを**管理** > 、**統合ラベル**の状態を表示します。

- **アクティブ**になっている場合は、テナントは統一されたラベル付けプラットフォームにあります。

- **アクティブ化されてい**ない場合、テナントは統一されたラベル付けプラットフォーム上にありません。 移行手順については、「 [Azure Information Protection ラベルを統合秘密度ラベルに移行する方法](configure-policy-migrate-labels.md)」を参照してください。

## <a name="whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection クライアントと Azure Information Protection の統一されたラベル付けクライアントの違いは何ですか。

**Azure Information Protection クライアント (クラシック)** は、ファイルと電子メールを分類して保護するための新しいサービスとして Azure Information Protection が最初に発表されたため、利用可能になりました。 このクライアントは、Azure からラベルとポリシー設定をダウンロードし、Azure portal から Azure Information Protection ポリシーを構成します。 詳細については、「 [Azure Information Protection ポリシーの概要](overview-policy.md)」を参照してください。 

Azure Information Protection の統一された**ラベル付けクライアント**は、複数のアプリケーションやサービスがサポートする、統一されたラベル付けストアをサポートするために、より新しい追加機能です。 このクライアントは、Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、および Microsoft 365 コンプライアンスセンターの管理センターから、機密ラベルとポリシー設定をダウンロードします。 詳細については、「[秘密度ラベルの概要](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)」を参照してください。

使用するクライアントがわからない場合は、「[使用する Azure Information Protection クライアントを選択](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers)する」を参照してください。

### <a name="identify-which-client-you-have-installed"></a>インストールしたクライアントを特定する

両方のクライアントがインストールされると、 **Azure Information Protection**が表示されます。 インストールしたクライアントを識別できるように、 **[ヘルプとフィードバック]** オプションを使用して **[Microsoft Azure Information Protection]** ダイアログボックスを開きます。

- エクスプローラーから単一ファイル、複数ファイル、またはフォルダーを右クリックで選択し、 **[分類して保護する]** 、 **[ヘルプとフィードバック]** の順に選択します。

- Office アプリケーションから: **[保護]** ボタン (クラシッククライアント) または **[秘密度]** ボタン (統一されたラベル付けクライアント) から、 **[ヘルプとフィードバック]** を選択します。

表示された**バージョン**番号を使用して、クライアントを識別します。

- バージョン**1**(たとえば、 **1.53.10.0**) は、Azure Information Protection クライアント (クラシック) を識別します。

- バージョン**2**(たとえば、 **2.2.14.0**) は、Azure Information Protection 統合されたラベル付けクライアントを識別します。

## <a name="when-is-the-right-time-to-migrate-my-labels"></a>ラベルを移行するのに最適なタイミング

Azure portal のラベルを移行するオプションが一般に利用できるようになったので、移行をアクティブ化することをお勧めします。これにより、ラベルを、統一されたラベル[付けをサポートするクライアントとサービス](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)の秘密ラベルとして使用できるようになります。

詳細および手順については、「 [Azure Information Protection ラベルを統合秘密度ラベルに移行する方法](configure-policy-migrate-labels.md)」を参照してください。

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>ラベルを移行した後に使用する管理ポータルはどれですか。

Azure portal でラベルを移行した場合:

- [クライアントとサービスを統一](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)したラベルを作成している場合は、管理センター (Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、または Microsoft 365 コンプライアンスセンター) のいずれかにアクセスして、これらのラベルを公開し、ポリシーを構成します。設定。 転送されるラベル変更には、いずれかの管理センターを使用します。 統合ラベル付けのクライアントは、これらの管理センターからラベルとポリシー設定をダウンロードします。

- [Azure Information Protection クライアント (クラシック)](./rms-client/aip-client.md)を使用している場合は、引き続き Azure portal を使用してラベルとポリシー設定を編集します。 クラシッククライアントは、Azure からラベルとポリシー設定を引き続きダウンロードします。

- 統一されたラベル[付けクライアント](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)と[従来のクライアント](./rms-client/aip-client.md)の両方がある場合は、管理センターまたは Azure portal を使用してラベルを変更できます。 ただし、クラシッククライアントで管理センターで行ったラベルの変更を取得するには、Azure portal の **[Azure Information Protection 統合ラベル]** ウィンドウにある Azure portal: **[発行]** オプションを使用する必要があります。 

[中央レポート機能](reports-aip.md)と[スキャナー](deploy-aip-scanner.md)には、引き続き Azure portal を使用します。

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure Information Protection と Azure Rights Management の違いは何ですか。

Azure Information Protection では、組織の文書や電子メールを分類、ラベル付け、保護できます。 保護テクノロジでは、Azure Information Protection のコンポーネントになった、Azure Rights Management サービスが利用されます。

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>Azure Information Protection の id 管理の役割は何ですか。

Azure Information Protection で保護されたコンテンツにアクセスするには、有効なユーザー名とパスワードが必要です。 Azure Information Protection でデータを保護するしくみについての詳細は、「[データのセキュリティ保護における Azure Information Protection の役割](/enterprise-mobility-security/solutions/azure-information-protection-securing-data)」をご覧ください。 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。

「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)」ページのサブスクリプション情報と機能一覧を参照してください。

Azure Rights Management データ保護を含む Office 365 サブスクリプションをお持ちの場合は、[Azure Information Protection ライセンス データシート](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)をダウンロードしてください。

ライセンスについてまだご質問がありますか。 [ライセンスについてよく寄せられる質問](https://azure.microsoft.com/pricing/details/information-protection#faq)のセクションで回答されているかどうかを確認してください。

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Azure Information Protection client は分類とラベル付けを含むサブスクリプション用のみでしょうか。

いいえ。 Azure Information Protection クライアント (クラシック) は、データを保護するために Azure Rights Management サービスだけを含むサブスクリプションでも使用できます。

クラシッククライアントがインストールされていて、Azure Information Protection ポリシーがない場合、このクライアントは自動的に[保護のみモード](./rms-client/client-protection-only-mode.md)で動作します。 このモードでは、ユーザーは Rights Management テンプレートとカスタム アクセス許可に簡単に適用できます。 分類とラベル付けを含むサブスクリプションを後で購入した場合、Azure Information Protection ポリシーをダウンロードする際に、クライアントは自動的に標準モードへと切り替わります。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Azure Information Protection を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?

Office 365 テナントまたは Azure AD テナントのグローバル管理者は、Azure Information Protection のすべての管理タスクを実行できます。 ただし、管理アクセス許可を他のユーザーに割り当てる場合は、次のオプションがあります。

- **Azure Information Protection 管理**者: この Azure Active Directory 管理者ロールを使用すると、管理者は Azure Information Protection を構成できますが、他のサービスは構成できません。 この役割を持つ管理者は、Azure Rights Management 保護サービスのアクティブ化と非アクティブ化、保護設定とラベルの構成、Azure Information Protection ポリシーの構成を行うことができます。 さらに、この役割を持つ管理者は、 [Azure Information Protection クライアント](./rms-client/client-admin-guide-powershell.md)および[aipservice モジュール](administer-powershell.md)から、すべての PowerShell コマンドレットを実行できます。 ただし、このロールは、ユーザーのドキュメントの追跡と取り消しをサポートしていません。
    
    > [!NOTE]
    > テナントが統一された[ラベル付けプラットフォーム](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)にある場合、このロールは Azure portal ではサポートされません。
    
    ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。

- **コンプライアンス管理者**または**コンプライアンスデータ管理者**: これらの Azure Active Directory 管理者ロールでは、管理者が Azure Information Protection を構成できます。これには、Azure の権限のアクティブ化と非アクティブ化が含まれます。管理保護サービス、保護設定とラベルの構成、および Azure Information Protection ポリシーの構成を行います。 さらに、これらのロールのいずれかを持つ管理者は、 [Azure Information Protection クライアント](./rms-client/client-admin-guide-powershell.md)および[aipservice モジュール](administer-powershell.md)のすべての PowerShell コマンドレットを実行できます。 ただし、これらのロールでは、ユーザーのドキュメントの追跡と取り消しはサポートされていません。
    
    これらのいずれかの管理者ロールにユーザーを割り当てるには、「 [Azure Active Directory で管理者ロールにユーザーを割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。 これらのロールが割り当てられているユーザーの他のアクセス許可については、Azure Active Directory のドキュメントの「[利用可能な役割](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles)」セクションを参照してください。

- **セキュリティ閲覧**者または**グローバルリーダー**: [Azure Information Protection analytics](reports-aip.md)のみ。 この Azure Active Directory の管理者ロールを持っている管理者は、ご自身のラベルの使用方法を確認したり、ラベル付きのドキュメントやメールに対するユーザー アクセスや、各分類への変更を監視したり、保護する必要がある機密情報を含んでいるドキュメントを識別したりできます。 この機能は Azure Monitor を使用するため、サポート[RBAC ロール](reports-aip.md#permissions-required-for-azure-information-protection-analytics)も必要です。
    
    > [!NOTE]
    > テナントが統一された[ラベル付けプラットフォーム](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)上にある場合、グローバル閲覧者ロールはサポートされません。

- **セキュリティ管理者**: 管理者は、この Azure Active Directory 管理者ロールを使用して、他の Azure サービスの一部を構成するだけでなく、Azure portal の Azure Information Protection を構成することができます。 このロールの管理者は、 [AIPService モジュールから PowerShell コマンドレット](administer-powershell.md)を実行したり、ユーザーのドキュメントを追跡したり取り消したりすることはできません。
    
    ユーザーに管理者ロールを割り当てるには、「[Azure Active Directory でユーザーを管理者ロールに割り当てる](/azure/active-directory/active-directory-users-assign-role-azure-portal)」を参照してください。 この役割のユーザーが持つその他のアクセス許可を確認するには、Azure Active Directory ドキュメントの「[使用可能なロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles)」セクションを参照してください。

- Azure Rights Management**全体管理**者と**コネクタ管理者**: これらの azure Rights Management 管理者ロールについては、最初に[aipservice モジュールからすべての PowerShell コマンドレット](administer-powershell.md)を実行するアクセス許可がユーザーに付与されます。他のクラウドサービスのグローバル管理者になる必要はありません。2つ目のロールは、Rights Management (RMS) コネクタのみを実行するアクセス許可を付与します。 これらの管理者ロールは、管理コンソールにアクセス許可を付与したり、ユーザーのドキュメントを追跡したり取り消したりすることはありません。
    
    これらの管理者ロールのいずれかを割り当てるには、AIPService PowerShell コマンドレットを使用し[ます。](/powershell/module/aipservice/add-aipservicerolebasedadministrator)

注意事項:

- Microsoft アカウントは、一覧表示されているいずれかの管理者ロールにアカウントが割り当てられている場合でも、Azure Information Protection の代理管理ではサポートされません。 

- [オンボーディング コントロール](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成してある場合は、RMS コネクタを除き、Azure Information Protection を管理する機能に影響はありません。 たとえば、コンテンツを保護する機能を "IT department" グループに制限するようにオンボーディング コントロールが構成されている場合、RMS コネクタのインストールと構成に使用するアカウントは、そのグループのメンバーである必要があります。 

- 管理者ロールが割り当てられているユーザーは、Azure Information Protection によって保護されたドキュメントやメールから保護を自動的に削除することはできません。 スーパー ユーザーを割り当てられたユーザーだけが、スーパー ユーザー機能が有効になっているときにのみ、この操作を行うことができます。 ただし、Azure Information Protection への管理アクセス許可を割り当てたすべてのユーザーが、各自のアカウントなど、ユーザーにスーパー ユーザーを割り当てることができます。 また、スーパー ユーザー機能を有効にすることもできます。 これらのアクションは、管理者ログに記録されます。 詳細については、「 [Azure Information Protection および探索サービスまたはデータ回復用のスーパーユーザーの構成](configure-super-users.md)」のセキュリティのベストプラクティスに関するセクションを参照してください。 

- Azure Information Protection ラベルを統合ラベルストアに移行する場合は、「移行に関するドキュメント: 統一されたラベル[付けプラットフォームをサポートする管理者ロール](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform)」の「」のセクションを必ず参照してください。

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection はオンプレミスおよびハイブリッドのシナリオをサポートしますか?

○ Azure Information Protection はクラウドベースのソリューションですが、クラウドだけでなく、オンプレミスに保存されているドキュメントや電子メールの分類、ラベル付け、および保護が可能です。

Exchange Server、SharePoint Server、および Windows ファイル サーバーがある場合は、これらのオンプレミス サーバーで Azure Rights Management サービスを使用して電子メールやドキュメントを保護できるように、[Rights Management コネクタ](deploy-rms-connector.md)をデプロイすることができます。 また、Active Directory ドメイン コントローラーを Azure AD と同期し、連携することで、たとえば [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect) を使用して、よりシームレスな認証方法をユーザーに提供できます。

必要に応じて、Azure Rights Management サービスで XrML 証明書の生成と管理が自動的に行われるので、オンプレミスの PKI は使用されません。 Azure Rights Management での証明書の使用方法については、記事「[Azure RMS の機能の詳細](./how-does-it-work.md)」の「[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」セクションを参照してください。

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Azure Information Protection ではどのようなデータの種類を分類し、保護できますか?

Azure Information Protection では、メール メッセージやドキュメントがオンプレミスまたはクラウドのどちらに配置されていても、それらを分類し、管理することができます。 これらのドキュメントには、Word ドキュメント、Excel スプレッドシート、PowerPoint プレゼンテーション、PDF ドキュメント、テキストベースのファイル、および画像ファイルが含まれます。 サポートされるドキュメントの種類の一覧については、管理者ガイドの[サポートされているファイルの種類](./rms-client/clientv2-admin-guide-file-types.md)の一覧を参照してください。

Azure Information Protection では、データベースファイル、予定表アイテム、Yammer の投稿、Sway コンテンツ、OneNote ノートブックなどの構造化データを分類して保護することはできません。

**新しく発表**されたプレビュー: Power BI では、機密ラベルを使用した分類がサポートされるようになり、次のファイル形式 (.pdf、.xls、.ppt) にエクスポートされたデータに、これらのラベルからの保護を適用できます。 詳細については、「 [Power BI でのデータ保護 (プレビュー)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview)」を参照してください。

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>条件付きアクセスに利用できるクラウド アプリとして Azure Information Protection が一覧に記載されています。これはどのように動作しますか。

はい。プレビュー オファリングとして、Azure Information Protection に Azure AD 条件付きアクセスを構成できるようになりました。

Azure Information Protection で保護されているドキュメントをユーザーが開くとき、標準的な条件付きアクセス コントロールに基づき、管理者は自分のテナントでユーザーをブロックするか、アクセス許可を与えることができるようになりました。 最も一般的に要求される条件の 1 つが多要素認証 (MFA) を要求することです。 もう 1 つは、デバイスが [Intune ポリシーに準拠する](/intune/conditional-access-intune-common-ways-use)必要があるということです (たとえば、モバイル デバイスがパスワード要件やオペレーティング システムの最小バージョンを満たすようにする)。また、コンピューターはドメインに参加する必要があります。

チュートリアル形式の例が必要であれば、ブログ投稿の「[Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/)」 (Azure Information Protection の条件付きアクセス ポリシー) を参照してください。

追加情報:

- Windows コンピューターの場合: 現行プレビュー リリースの場合、[ユーザー環境が初期化](./how-does-it-work.md#initializing-the-user-environment) (このプロセスはブートストラップとも呼ばれています) されたときに Azure Information Protection の条件付きアクセス ポリシーが評価され、その後、30 日おきに評価されます。

- 条件付きアクセス ポリシーの評価頻度を微調整することもできます。 この微調整は、トークンの有効期間を構成することで実行できます。 詳細については、「[Azure Active Directory における構成可能なトークンの有効期間](/azure/active-directory/active-directory-configurable-token-lifetimes)」を参照してください。

- 条件付きアクセスポリシーに管理者アカウントを追加しないことをお勧めします。これらのアカウントは、Azure portal の [Azure Information Protection] ウィンドウにアクセスできないためです。

- 他の組織とのコラボレーション (B2B) のための条件付きアクセス ポリシーで MFA を使用する場合は、[Azure AD B2B コラボレーション](/azure/active-directory/b2b/what-is-b2b)を使用して、他の組織と共有するユーザーのためのゲスト アカウントを作成する必要があります。

- 2018 年 12 月の Azure AD プレビュー リリースでは、ユーザーが保護されたドキュメントを初めて開く前に、ユーザーに使用条件への同意を求めることができるようになりました。 詳細については、次のブログ投稿のお知らせを参照してください。[条件付きアクセスでの Azure AD の使用条件の更新](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822)

- 多くのクラウド アプリで条件付きアクセスを使用する場合、選択対象の一覧に **Microsoft Azure Information Protection** が表示されないことがあります。 その場合、一覧の上にある検索ボックスを使用します。 「Microsoft Azure Information Protection」と入力し、利用可能アプリを絞り込みます。 サポートされているサブスクリプションがある場合、選択対象として **Microsoft Azure Information Protection** が表示されます。 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Azure Information Protection が Microsoft Graph Security のセキュリティ プロバイダーとして記載されています。これはどのように動作しますか? また、どのようなアラートを受信できますか?

はい。公共プレビュー サービスとして、**Azure Information Protection の異常なデータ アクセス**に対するアラートを受信できるようになりました。 Azure Information Protection によって保護されているデータに対する異常なアクセスの試行があると、このアラートがトリガーされます。 たとえば、異常に大量のデータへのアクセス、不自然な時間帯でのアクセス、または不明な場所からのアクセスなどです。

このようなアラートは、データ関連の高度な攻撃や、環境内部の脅威を検出するのに役立ちます。 これらのアラートでは、保護されたデータにアクセスするユーザーの動作をプロファイルするために機械学習が使用されます。 

Azure Information Protection のアラートにアクセスするには、[Microsoft Graph Security API を使用します](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/security-api-overview)。または、Azure Monitor を使用して、Splunk や IBM Qradar などの SIEM ソリューションに[アラートをストリームする](https://developer.microsoft.com/graph/docs/concepts/security_siemintegration)ことができます。

Microsoft Graph Security API について詳しくは、「[Microsoft Graph Security API の概要](https://developer.microsoft.com/graph/docs/concepts/security-concept-overview)」をご覧ください。

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Windows Server FCI と Azure Information Protection スキャナーの違い

[Rights Management コネクタ](deploy-rms-connector.md) (Office ドキュメントのみ) や [PowerShell スクリプト](./rms-client/configure-fci.md) (すべてのファイルの種類) を使用してドキュメントを分類して保護するために、これまでは Windows Server ファイル分類インフラストラクチャが選択されてきました。 

これからは、[Azure Information Protection スキャナー](deploy-aip-scanner.md)の使用をお勧めします。 スキャナーは Azure Information Protection クライアントと Azure Information Protection ポリシーを使用して、ドキュメント (すべてのファイルの種類) にラベルを付けるため、これらのドキュメントは分類され、必要に応じて保護されます。

この 2 つのトポロジの主な違いを次に示します。

|Windows Server FCI|Azure Information Protection スキャナー|
|--------------------------------|-------------------------------------|
|サポートされるデータ ストア: <br /><br />- Windows Server のローカル フォルダー|サポートされるデータ ストア: <br /><br />- Windows Server のローカル フォルダー<br /><br />- Windows ファイル共有とネットワーク接続ストレージ<br /><br />- SharePoint Server 2016 と SharePoint Server 2013。 [このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様向けに SharePoint Server 2010 もサポートされています。|
|操作モード: <br /><br />- リアルタイム|操作モード: <br /><br />- 体系的にデータ ストアをクロールします。このサイクルは 1 回のみまたは繰り返し実行できます|
|ファイルの種類ごとのサポート: <br /><br />- すべてのファイルの種類が既定で保護されます <br /><br />- レジストリを編集することで、特定のファイルの種類を保護から除外できます|ファイルの種類ごとのサポート: <br /><br />- Office ファイルの種類と PDF ドキュメントは既定で保護されます <br /><br />- レジストリを編集することで、保護に含めるファイルの種類を追加できます|

ローカルフォルダーまたはネットワーク共有で保護されているファイルの[Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)の設定には違いがあります。 既定では、どちらのソリューションでも、Rights Management の所有者は、ファイルを保護するアカウントに設定されますが、この設定をオーバーライドすることができます。

- Windows Server FCI の場合: すべてのファイルに対して単一アカウントとなるように Rights Management 所有者を設定したり、各ファイルの Rights Management 所有者を動的に設定したりすることができます。 Rights Management 所有者を動的に設定するには、 **-OwnerMail [ソース ファイルの所有者の電子メール]** パラメーターと値を使用します。 この構成では、ファイルの所有者プロパティのユーザー アカウント名を使用して、Active Directory からユーザーのメール アドレスを取得します。

- Azure Information Protection スキャナーの場合: 新しく保護されたファイルの場合、Rights Management 所有者を、指定したデータストアのすべてのファイルに対して1つのアカウントに設定できますが、各ファイルに対して Rights Management 所有者を動的に設定することはできません。 以前から保護されていたファイルについては、Rights Management 所有者は変更されません。 新しく保護されるファイルに対してアカウントを設定するには、スキャナー プロファイルで **-Default owner** 設定を指定します。 

スキャナーで SharePoint サイトおよびライブラリのファイルを保護する場合、Rights Management 所有者は SharePoint エディターの値を使用して、ファイルごとに動的に設定されます。

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>新しいリリースが Azure Information Protection ですぐに利用できるようになると聞きました。いつリリースされますか?

技術文書には今後のリリースに関する情報は含まれません。 この種類の情報については、 [Microsoft 365 ロードマップ](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent)を使用して、 [Enterprise Mobility + Security ブログ](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services)を確認してください。

## <a name="is-azure-information-protection-suitable-for-my-country"></a>自分の国に Azure Information Protection は適していますか?

国によって、さまざまな要件と規制があります。 組織のこの質問に対する回答は、[国ごとの適合性](./compliance.md#suitability-for-different-countries)に関する記事が役立ちます。

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Azure Information Protection は GDPR にどのように役立ちますか?

一般データ保護規則 (GDPR) に準拠するために Azure Information Protection がどのように役立つかを確認するには、ブログ投稿「[Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr)」(Microsoft 365 が GDPR で役立つ情報保護戦略を提供) のお知らせとビデオをご覧ください。

## <a name="where-can-i-find-supporting-information-for-azureinformation-protectionsuch-as-legal-compliance-and-slas"></a>法律、法令遵守、SLA など、Azure Information Protection に関するサポート情報はどこで入手できますか。
「[Azure Information Protection のコンプライアンスとサポート情報](./compliance.md)」を参照してください。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Azure Information Protection の問題を報告またはフィードバックを送信するにはどうすればよいですか。

テクニカル サポートの場合は、標準のサポート チャネルを使用するか、[Microsoft サポートに問い合わせ](information-support.md#to-contact-microsoft-support)てください。

[Azure Information Protection の Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>質問がここに含まれていない場合は、どうすればよいですか

最初に、分類、ラベル付け、データ保護に関する次の FAQ を確認してください。 Azure Rights Management サービス (Azure RMS) は、Azure Information Protection のデータ保護テクノロジを提供します。 Azure RMS は分類およびラベル付けと併用するか、単体で使用できます。 

- [分類とラベル付けに関してよく寄せられる質問](faqs-infoprotect.md)

- [データ保護に関してよく寄せられる質問](faqs-rms.md)

回答が得られない場合、「[Azure Information Protection の情報とサポート](information-support.md)」に一覧表示されているリンクとリソースを使用します。

さらに、エンドユーザー向けの FAQ が用意されています。

- [iOS 用と Android 用の Azure Information Protection の FAQ](./rms-client/mobile-app-faq.md)

- [Mac コンピューター用 RMS 共有アプリの FAQ](https://technet.microsoft.com/dn451248)

