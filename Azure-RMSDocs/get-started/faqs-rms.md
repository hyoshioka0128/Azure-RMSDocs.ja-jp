---
title: "Azure RMS に関してよく寄せられる質問 - AIP"
description: "Azure Information Protection のデータ保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問の一部"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/09/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9983b088b5856f8c2223d05624c3bee21b80fd15
ms.sourcegitcommit: db0c5185aab9ba4f71b9d2aa1dd87681dfe7c1b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2017
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Azure Information Protection のデータ保護に関してよく寄せられる質問

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection のデータ保護サービス、Azure Rights Management に関して質問がございますか。 ここで回答を探してみてください。 

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>ファイルを Azure Rights Management で保護するには、クラウドに置いておく必要があるのでしょうか。
よくある誤解ですが、そのようなことはありません。 Azure Rights Management サービス (と Microsoft) では、情報保護の一環としてユーザーのデータを閲覧したり、保存したりすることはありません。 ユーザーが保護した情報は、ユーザーが Azure に明示的に保存したり、Azure に情報を保存する別のクラウド サービスを使用しない限り、Azure に送信されたり保存されたりすることはありません。 

詳細については、「[Azure RMS の機能の詳細](../understand-explore/how-does-it-work.md)」を参照してください。(コーラのレシピのように) オンプレミスで作成および保管している機密性の高いデータを Azure Rights Management サービスで保護しながら、引き続きオンプレミスに置いておくことができるしくみについて説明しています。

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Azure Rights Management 暗号化と Microsoft のその他のクラウド サービスでの暗号化の違いは何ですか。

Microsoft はさまざまなシナリオでのデータ保護に合わせて多数の暗号化技術を提供していますが、多くの場合はデータ保護のシナリオが相互補完的です。 たとえば、Office 365 の暗号化は Office 365 に保存される静止状態のデータが対象ですが、Azure Information Protection の Azure Rights Management サービスは独立してユーザーのデータを暗号化するものであり、データは格納されている場所や伝送方法にかかわらず保護されます。

これらの暗号化技術は互いに補完するものであり、使用するには各技術を個別に有効化して構成する必要があります。 このときに、暗号化のキーを独自に用意するという選択が可能な場合があり、このようなシナリオは "BYOK" (Bring Your Own Key) とも呼ばれます。 暗号化技術の 1 つについて BYOK を有効にしても、それ以外の技術に影響することはありません。 たとえば、BYOK を Azure Information Protection に使用するが、それ以外の暗号化技術に対しては使用しないということも、その逆も可能です。 使用されるキーが暗号化技術ごとに異なるか同一であるかは、管理者が各サービスの暗号化オプションをどのように構成するかによって決まります。

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>BYOK と HYOK の違いは何ですか。また、どのような場合に使用すべきですか。

Azure Information Protection において**独自キーを持ち込む** (BYOK) のは、Azure Rights Management 保護の独自キーをオンプレミスで作成する場合です。 そのキーを Azure Key Vault のハードウェア セキュリティ モジュール (HSM) に転送し、そこでそのキーの所有と管理を続行します。 これを行わない場合、Azure Rights Management 保護では Azure 内で自動的に作成、管理されるキーが使用されます。 この既定の設定は、"顧客管理" ではなく "マイクロソフト管理" と呼ばれます (BYOK オプション)。

BYOK の詳細および組織でこのキー トポロジを選択すべきかについては、「[Azure Information Protection テナント キーの計画と実装](../plan-design/plan-implement-tenant-key.md)」を参照してください。 

Azure Information Protection において**独自キーを保持する** (HYOK) 機能は、クラウドに格納されているキーで保護することができないドキュメントや電子メールのサブセットを持つような、少数の組織のためのものです。 こうした組織では、BYOK を使用してキーを作成し管理する場合でも、この制限が適用されます。 この制限は多くの場合、規制やコンプライアンス上の理由によるもので、HYOK 構成は "最高機密" 情報のみに適用されます。すなわち、組織外には決して共有されず、内部ネットワークのみで利用され、モバイル デバイスからアクセスする必要のない情報です。 

これらの例外 (通常は、保護する必要のあるすべてのコンテンツの 10% 未満) については、組織は、オンプレミスのソリューションである Active Directory Rights Management サービスを使用して、オンプレミスのキーを作成することができます。 このソリューションでは、コンピューターはクラウドから Azure Information Protection ポリシーを取得しますが、この識別されたコンテンツはオンプレミスのキーを使用して保護することができます。

HYOK の詳細についてや、制限事項の正しい理解や使用するタイミングを確認するには、「[AD RMS 保護の Hold Your Own Key (HYOK) の要件と制限事項](../deploy-use/configure-adrms-restrictions.md)」を参照してください。

## <a name="can-i-now-use-byok-with-exchange-online"></a>現在、Exchange Online で BYOK を使用できますか?

はい。「[Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)」 (Azure Information Protection 上に構築される新しい Office 365 メッセージの暗号化機能の設定) の手順に従って、Exchange Online で BYOK を使用することができるようになりました。 これらの手順に従うことで、新しい Office 365 メッセージの暗号化と、Azure Information Protection の BYOK の使用をサポートする新しい機能を Exchange Online で使用できるようになります。

この変更の詳細については、[Office 365 メッセージの暗号化と新しい機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)に関するブログのお知らせを参照してください。

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>Azure RMS と統合するサード パーティのソリューションに関する情報はどこで入手できますか?

既に多くのソフトウェア ベンダーが、Azure Rights Management と統合するソリューションを持っているか、またはそのソリューションを実装しており、リストは急増し続けています。 [RMS 対応ソリューション](requirements-applications.md#rms-enlightened-solutions)の一覧に役立つ情報が掲載されています。また Twitter の [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) からも最新の情報を入手できます。 なお、具体的なご質問は、Information Protection チーム (askipteam@microsoft.com) までメールでメッセージをお送りください。

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>RMS コネクタには管理パックまたは同様の監視メカニズムがありますか?

Rights Management コネクタは情報、警告、およびエラー メッセージをイベント ログに記録しますが、これらのイベントの監視機能を備えた管理パックはありません。 ただし、イベントの一覧とその説明および修正の実施に役立つ詳細な情報については、「[Azure Rights Management コネクタを監視する](../deploy-use/monitor-rms-connector.md)」を参照してください。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>Azure RMS を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?

Office 365 テナントまたは Azure AD テナントのグローバル管理者は、Azure Rights Management サービスのすべての管理タスクを実行できます。 ただし、他のユーザーに管理者権限を割り当てる場合は、Azure RMS の PowerShell コマンドレット [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) を使用して行うことができます。 この管理ロールは、ユーザー アカウントまたはグループごとに割り当てることができます。 使用できるロールは、**グローバル管理者**と**コネクタ管理者**の 2 つです。 

ロールの名前からわかるように、1 番目のロールは Azure Rights Management のすべての管理タスクを実行する権限を付与します (他のクラウド サービスのグローバル管理者には付与しません)、2 番目のロールは Rights Management (RMS) コネクタのみを実行する権限を付与します。

注意事項:

- Office 365 のグローバル管理者と Azure AD のグローバル管理者のみが、Office 365 管理センターまたは Azure クラシック ポータルを使用して Azure RMS を構成できます。 Azure Information Protection に Azure Portal を利用する場合、セキュリティ管理者としてサインインすることもできます。

- Azure RMS のグローバル管理者ロールを割り当てられたユーザーは、Azure RMS の PowerShell コマンドを使用して Azure RMS を構成する必要があります。 特定のタスクを実行する正しいコマンドレットについては、「[Windows PowerShell を使用した Azure Rights Management の管理](../deploy-use/administer-powershell.md)」を参照してください。

- [オンボーディング コントロール](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成してある場合は、RMS コネクタを除き、Azure RMS を管理する機能に影響はありません。 たとえば、コンテンツを保護する機能を "IT department" グループに制限するようにオンボーディング コントロールが構成されている場合、RMS コネクタのインストールと構成に使用するアカウントは、そのグループのメンバーである必要があります。 

- Azure RMS の管理者 (テナントのグローバル管理者や Azure RMS のグローバル管理者など) は、Azure RMS によって保護されていたドキュメントまたは電子メールから保護を自動的に削除することはできません。 Azure RMS のスーパー ユーザーを割り当てられたユーザーだけが、スーパー ユーザー機能が有効になっているときにのみ、これを行うことができます。 ただし、テナントのグローバル管理者および Azure RMS のグローバル管理者は、ユーザーをスーパー ユーザーとして割り当てることができます (これには自分自身のアカウントも含まれます)。 また、スーパー ユーザー機能を有効にすることもできます。 これらのアクションは、Azure RMS の管理者ログに記録されます。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」のセキュリティのベスト プラクティスに関するセクションを参照してください。 

>[!NOTE]
> Azure Rights Management 保護を構成するためのテンプレートと新しいオプションは、Azure Portal に移動しました。Azure Portal はグローバル管理者のアクセスだけでなく、セキュリティ管理者をサポートします。 

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>Azure Portal で新しいカスタム テンプレートをどのように作成しますか?

カスタム テンプレートは、Azure Portal に移動しています。Azure Portal では、引き続きカスタムテンプレートをテンプレートとして管理したり、ラベルに変換することができます。 新しいテンプレートを作成するには、新しいラベルを作成し、Azure RMS 用のデータ保護設定を構成します。 その処理の裏では、Rights Management テンプレートと統合されるサービスとアプリケーションが次からアクセスできるようになる新しいテンプレートが作成されます。

Azure Portal のテンプレートの詳細については、「[Azure Information Protection のテンプレートを構成して管理する](../deploy-use/configure-policy-templates.md)」を参照してください。

## <a name="ive-protected-a-document-and-now-want-to-change-the-usage-rights-or-add-usersdo-i-need-to-reprotect-the-document"></a>保護されているドキュメントに対して、使用権限の変更またはユーザーの追加を行いたいのですが、ドキュメントを再保護する必要がありますか。

ドキュメントがラベルまたはテンプレートを使用して保護されている場合、ドキュメントを再保護する必要はありません。 使用権限に変更を加えるか、新しいグループ (またはユーザー) を追加することによってラベルまたはテンプレートを変更します。さらに変更内容を保存して発行します。

- 変更を加える前にユーザーがドキュメントにアクセスしていない場合、ユーザーがドキュメントを開くとすぐに変更が有効になります。 

- ユーザーが既にドキュメントにアクセスしている場合は、ユーザーの[使用ライセンス](../deploy-use/configure-usage-rights.md#rights-management-use-license)の有効期限が過ぎた時点で変更が有効になります。 使用ライセンスの有効期限が切れるまで待てない場合にのみ、ドキュメントを再保護します。 効果的に再保護を行うと、ドキュメントの新しいバージョンが作成され、ユーザーの使用ライセンスも新しくなります。

あるいは、必要なアクセス許可に対して既にグループを構成している場合、グループのメンバーシップを変更してユーザーの追加または除外を行うことができます。ラベルまたはテンプレートの変更は必要ありません。 Azure Rights Management サービスがグループ メンバーシップを[キャッシュ](../plan-design/prepare.md#group-membership-caching-by-azure-rights-management)に入れるため、変更が反映されるまでわずかな遅延が生じる可能性があります。

カスタム アクセス許可を使用してドキュメントが保護されている場合は、既存のドキュメントのアクセス許可を変更できません。 ドキュメントを再度保護し、この新しいバージョンのドキュメントに必要なすべてのユーザーとすべての使用権限を指定する必要があります。 保護されたドキュメントを再保護するには、"フル コントロール" 使用権限が必要です。 

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>一部のユーザーが Exchange Online 上の Exchange に、他のユーザーが Exchange Server 上の Exchange に登録されているハイブリッド デプロイメント構成です。この構成は、Azure RMS でサポートされていますか。
はい、サポートされています。また、2 つの Exchange デプロイメント間でシームレスに電子メールと添付ファイルを保護し、保護された電子メールと添付ファイルを使用できるようになることがメリットです。 この構成の場合、[Azure RMS をアクティブ化し](../deploy-use/activate-service.md)、[IRM for Exchange Online を有効にして](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)、[RMS コネクタをデプロイして](../deploy-use/deploy-rms-connector.md) Exchange Server 用に構成します。

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>運用環境にこの保護を利用すると、会社の環境が Azure RMS に固定されたり、Azure RMS で保護したコンテンツにアクセスできなくなる危険性が生じたりしますか。
いいえ。データを常に制御することができます。また、たとえ Azure Rights Management サービスの使用を停止したとしても、継続してデータにアクセスすることができます。 詳細については、「[Azure Rights Management の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」を参照してください。

ただし、Azure Rights Management サービスを停止される前に、お客様が使用を停止する理由を伺う機会をいただいています。 Azure Rights Management 保護がビジネス要件を満たしていない場合は、近い将来に新機能が計画されているか、代替案がないかをお問い合わせください。 お問い合わせの電子メールは [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) に送信してください。技術とビジネスの要件について説明いたします。

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>Azure RMS を使用してコンテンツを保護するユーザーを制御できますか。
はい。Azure Rights Management サービスには、このシナリオのためのユーザー オンボーディング コントロールがあります。 詳細については、記事「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」の「[段階的デプロイのオンボーディング コントロールの構成](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)」のセクションを参照してください。

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>ユーザーが、保護されたドキュメントを特定の組織と共有しないようにすることはできますか。
データ保護に Azure Rights Management サービスを使用する最大の利点の 1 つは、Azure AD が認証を自動的に処理するため、各パートナー組織に対して明示的な信頼を構成することなく、企業間のコラボレーションをサポートできることです。

ユーザーが特定の組織とのドキュメントの安全な共有を防止するような管理オプションはありません。 たとえば、信頼していない組織や、競合先の組織をブロックするとします。 Azure Rights Management サービスがこれらの組織のユーザーに保護されたドキュメントを送信しないようにしても意味がありません。その場合、ユーザーはドキュメントを保護されていないまま共有することになり、おそらくこれはこのシナリオにおいて最も望ましくない状況です。 たとえば、これらの組織のユーザーと社外秘ドキュメントを共有しているユーザーを識別することはできませんが、ドキュメント (または電子メール) が Azure Rights Management サービスで保護されていれば、これが可能になります。

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>保護されたドキュメントを社外のユーザーと共有する場合、そのユーザーはどのようにして認証されますか。

既定では、Azure Rights Management サービスは、ユーザー認証に Azure Active Directory アカウントと関連付けられた電子メール アドレスを使用します。これにより、管理者にとって企業間のコラボレーションがシームレスになります。 他の組織で Azure サービスを使用する場合は、アカウントがオンプレミスで作成、管理されてから Azure に同期される場合でも、ユーザーは既に Azure Active Directory にアカウントを持っています。 組織が内部的に Office 365 を所有している場合、このサービスはユーザー アカウント用に Azure Active Directory も使用します。 ユーザーの組織が Azure に管理アカウントを持っていない場合、ユーザーは[個人向け RMS](../understand-explore/rms-for-individuals.md) にサインアップできます。これは、管理されていない Azure テナントと組織用のディレクトリをユーザー用のアカウントを使用して作成するため、このユーザー (およびそれ以降のユーザー) は Azure Rights Management サービスに対して認証されます。

このようなアカウントの認証方法は、他の組織の管理者が Azure Active Directory アカウントを構成している方法によって異なります。 たとえば、これらのアカウント用に作成されたパスワード、多要素認証 (MFA)、フェデレーション、Active Directory Domain Services で作成されたパスワードを使用してから、Azure Active Directory に同期される場合があります。

Azure AD のアカウントを持っていないユーザー宛の Office ドキュメントが添付されている電子メールを保護する場合、認証方法が異なります。 Azure Rights Management サービスは、Gmail など、いくつかの一般的なソーシャル ID プロバイダーと統合されます。 ユーザーの電子メール プロバイダーがサポートされている場合、ユーザーはそのサービスにサインインでき、電子メール プロバイダーによって認証が行われます。 ユーザーの電子メール プロバイダーがサポートされていない場合、または基本設定として、ユーザーは認証を行い、Web ブラウザーで保護されたドキュメントを含む電子メールを表示するためのワンタイム パスワードを申請できます。

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>社外のユーザーをカスタム テンプレートに追加できますか?

はい。 Azure Portal でテンプレートをラベルに変換するときに、組織の外部からユーザーとグループや、別組織の全ユーザーに対しても、アクセス許可を追加する[保護設定](../deploy-use/configure-policy-protection.md)を構成できます。 あるいは、PowerShell を利用してこの構成を行うことができます。

カスタム テンプレートをラベルに変換して、外部ユーザーを簡単に追加できるようにする方法については、「[Azure Information Protection のテンプレートを構成して管理する](../deploy-use/configure-policy-templates.md)」を参照してください。

## <a name="what-type-of-groups-can-i-use-with-azure-rms"></a>Azure RMS では、どの種類のグループを使用できますか?
ほとんどのシナリオでは、電子メール アドレスを持つ、Azure AD 内の任意の種類のグループを使用できます。 この経験則は、使用権限を割り当てる際に常に適用されますが、Azure Rights Management サービスの管理の場合はいくつか例外があります。 詳細については、「[グループ アカウントに関する Azure Information Protection の要件](../plan-design/prepare.md#azure-information-protection-requirements-for-group-accounts)」を参照してください。

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>保護されたメールを Gmail または Hotmail のアカウントに送信するにはどうしますか。

Exchange Online と Azure Rights Management サービスを使用する場合は、保護メッセージとして電子メールを送信するだけです。 たとえば、Outlook on the web でコマンド バーの **[保護]** ボタンを選択し、[Outlook 転送不可] オプションを使用し、Azure Rights Management から保護を適用する Azure Information Protection ラベルを選択できます。あるいは保護を Exchange Online トランスポート ルールで適用できます。

受信者には Gmail、Yahoo、または Microsoft アカウントにサインインするためのオプションが表示され、保護された電子メールを読み取れるようになります。 また、ブラウザーで電子メールを読み取るためにワンタイム パスワードのオプションを選択することもできます。

このシナリオをサポートするには、Exchange Online を Azure Rights Management サービスおよび Office 365 のメッセージの暗号化の新しい機能で使用できるようにする必要があります。 この構成の詳細については、「[Exchange Online: IRM 構成](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」を参照してください。

すべてのデバイスですべての電子メール アカウントをサポートする新機能の詳細については、ブログの投稿「[Announcing new capabilities available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)」 (Office 365 のメッセージの暗号化で使用できる新機能のお知らせ) を参照してください。

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Azure RMS でサポートされているデバイスとファイルの種類を教えてください。
Azure Rights Management サービスをサポートするデバイスの一覧については、「[Azure Rights Management データ保護をサポートするクライアント デバイス](../get-started/requirements-client-devices.md)」をご覧ください。 サポートされているデバイスによっては一部の Rights Management 機能がサポートされていないため、[RMS 対応のアプリケーション](../get-started/requirements-applications.md#rms-enlightened-applications)の表も確認してください。

Azure Rights Management サービスはあらゆる種類のファイルに対応しています。 テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、他のいくつかのアプリケーションのファイルの種類については、Azure Rights Management は暗号化と権限の適用 (アクセス許可) の両方を含むネイティブな保護を提供します。 他のすべてのアプリケーションとファイルの種類については、ファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証という一般的な保護機能が提供されます。

Azure Rights Management でネイティブでサポートされているファイル名拡張子の一覧については、「[File types supported by the Azure Information Protection client](../rms-client/client-admin-guide-file-types.md)」(Azure Information Protection クライアントでサポートされるファイルの種類) を参照してください。 一覧に含まれないファイル名拡張子は、汎用的な保護をこれらのファイルに自動的に適用する Azure Information Protection クライアントを使用することによってサポートされます。

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>ドキュメントを保護および追跡するように Mac コンピューターを設定するにはどうすればよいのですか?

まず、ソフトウェア インストール リンクを使用して https://portal.office.com から Office for Mac をインストールしたことを確認します。手順については、「[Office 365 または Office 2016 を PC または Mac にダウンロードしてインストールまたは再インストールする](https://support.office.com/en-us/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658)」を参照してください。

Office 365 の職場または学校のアカウントを使用して、Outlook を開き、プロファイルを作成します。 次に新しいメッセージを作成し、次の操作を行って、Azure Rights Management サービスを使用してドキュメントや電子メールを保護できるように Office を構成します。

1. 新規のメッセージで、**[オプション]** タブで、**[アクセス許可]** をクリックし、**[資格情報の確認]** をクリックします。

2. 入力要求が表示されたら、Office 365 の職場または学校のアカウントの詳細をもう一度指定し、**[サインイン]** を選択します。 
    
    これによって Azure Rights Management テンプレートがダウンロードされ、**資格情報の確認**が、**無制限**、**転送不可**、およびユーザーのテナント用に公開されたすべての Azure Rights Management テンプレートを含むオプションで置換されます。 この新しいメッセージを今すぐ取り消すことができます。

電子メール メッセージやドキュメントを保護するには、**[オプション]** タブで、**[アクセス許可]** をクリックして、電子メールやドキュメントを保護するオプションまたはテンプレートを選択します。

ドキュメントを保護した後、ドキュメントを追跡するには、Azure Information Protection クライアントをインストールした Windows コンピューターから、Office アプリケーションまたはエクスプローラーを使用して、ドキュメントをドキュメント追跡サイトに登録します。 手順については、[ドキュメントの追跡と取り消し](../rms-client/client-track-revoke.md)に関する記事を参照してください。 Mac コンピューターからは、現在、Web ブラウザーを使用してドキュメント追跡サイト (https://track.azurerms.com) に移動し、このドキュメントを追跡して取り消すことができます。

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>RMS で保護されている Office ドキュメントを開いた場合、関連付けられた一時ファイルも RMS で保護されたものになりますか。
いいえ。 このシナリオでは、関連付けられている一時ファイルには元のドキュメントのデータは含まれず、ユーザーがファイルを開いているときに入力したもののみが含まれます。 元のファイルとは異なり、一時ファイルは明らかに共有用に設計されておらず、BitLocker や EFS などのローカル セキュリティ コントロールによって保護されデバイス上に残ります。

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>必要な機能があるのですが、SharePoint で保護されたライブラリには使用できないようです。この機能のサポートは予定されていますか。
現在のところ、SharePoint は、IRM で保護されたライブラリを使用して、RMS で保護されたドキュメントをサポートしています。IRM で保護されたライブラリは、Rights Management テンプレートやドキュメントの追跡などの機能をサポートしていません。 詳細については、記事「[Office アプリケーションおよびサービス](../understand-explore/office-apps-services-support.md)」の「[SharePoint Online と SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server)」セクションを参照してください。

まだサポートされていない機能に関する情報については、[Enterprise Mobility and Security チーム ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)のお知らせに注意してください。

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>ユーザーが社内や社外の人間とファイルを安全に共有できるように SharePoint Online で OneDrive for Business を構成するには、どうすればよいですか。
既定では、Office 365 管理者は構成しません。ユーザーが構成します。

SharePoint サイト管理者が、所有する SharePoint ライブラリの IRM を有効にして構成するのと同じように、OneDrive for Business は、ユーザーが自身の OneDrive for Business ライブラリの IRM を有効にして構成するように設計されています。 ただし、PowerShell を使用して、ユーザーに代わってこの処理を行うことができます。 手順については、記事「[Office 365: クライアントとオンライン サービスの構成](../deploy-use/configure-office365.md)」の「[SharePoint Online と OneDrive for Business:IRM 構成](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)」セクションを参照してください。

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>正常にデプロイするためのヒントやコツがあれば教えてください。

これまでに多数のデプロイをサポートし、顧客、パートナー、コンサルタント、サポート エンジニアから話を聞いてきた経験から言える一番のヒントは、**シンプルなポリシーを設計してデプロイすること**です。

Azure Information Protection では、他のユーザーと情報を安全に共有できるため、データ保護の範囲を詳細に指定することができます。 使用権限の制限の構成は慎重に行ってください。 多くの組織にとって、業務上最も重要な利点は、組織内のユーザーのアクセス許可を制限して、データ漏えいを防止できることです。 もちろん、印刷や編集などの操作を制限する必要があれば、より詳細なポリシーを作成することもできます。ただし、そのような細かい制限は、高レベルのセキュリティが本当に必要なドキュメントに限定してください。最初から制限の厳しい使用権限を実装するのではなく、より段階的な方法を計画することをお勧めします。

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>退職した従業員が保護していたファイルにアクセスするには、どうすればよいですか。
[スーパー ユーザー機能](../deploy-use/configure-super-users.md)を使用してください。この機能により、テナントで保護されているすべてのドキュメントと電子メールに対して承認されたユーザーにフル コントロール使用権限が与えられます。 スーパー ユーザーは常にこの保護されたコンテンツを読み取ることができ、必要に応じて、保護を解除したり、別のユーザーのために再度保護したりすることができます。 また必要に応じて、スーパー ユーザー機能を使用すると、権限を持つサービスのインデックス化とファイルの検証を行うことができます。

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>ドキュメント追跡サイトで失効をテストすると、最大 30 日間はドキュメントにアクセスできるというメッセージが表示されます。この期間を構成することはできますか。

はい。 このメッセージは、その特定のファイルの[使用ライセンス](../deploy-use/configure-usage-rights.md#rights-management-use-license)を反映します。 

ファイルを取り消すと、そのアクションは、Azure Rights Management サービスにユーザーを認証する場合にのみ適用できます。 そのため、ファイルに 30 日間の使用ライセンス有効期間があり、ユーザーが既にそのドキュメントを開いている場合、ユーザーは引き続きその使用ライセンスの期間中はドキュメントにアクセスすることができます。 使用ライセンスの期限が切れた後は、ドキュメントが取り消されているため、ユーザーのアクセスが拒否される時点で、ユーザーの再認証が必要になります。

ドキュメントを保護したユーザーである [Rights Management 発行者](../deploy-use/configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)は、この取り消しから除外されており、常に自分のドキュメントにアクセスできます。 

テナントに適用される使用ライセンスの有効期間の既定値は 30 日間です。ラベルまたはテンプレートで、この設定をより制限の厳しい値でオーバーライドできます。 使用ライセンスの詳細および使用ライセンスの構成方法については、[Rights Management の使用ライセンス](../deploy-use/configure-usage-rights.md#rights-management-use-license)に関するページを参照してください。

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management は画面キャプチャを防止できますか。
Windows プラットフォーム (Windows 7、Windows 8.1、Windows 10、Windows Phone) および Android で広く使われているさまざまな画面キャプチャ ツールについては、**コピーの**[使用権限](../deploy-use/configure-usage-rights.md)を付与しなければ、Rights Management で画面キャプチャを防止できます。 これに対して、iOS や Mac のデバイスでは、画面キャプチャを禁止するアプリが認められていません。また、(Outlook Web App や Office Online を使用しているなどの場合に) ブラウザーでの画面キャプチャを禁止することも不可能です。

画面のキャプチャを禁止しておくと、不注意や不測の出来事により機密性の高い情報が漏洩してしまう事態を避けることができます。 ただし、画面に表示されるデータをユーザーが共有するにはさまざまな方法があり、スクリーン ショットを保存する方法はその 1 つにすぎません。 たとえば、表示される情報を共有しようとするユーザーは、カメラ付き携帯電話を使用して写真を撮影したり、データを再入力したり、単に口頭で他者に伝達することができます。

このように、あらゆるプラットフォームとソフトウェアが Rights Management API をサポートしており、かつ画面キャプチャをブロックできたとしても、テクノロジだけでデータの漏洩を防ぐことができるわけではありません。 Rights Management は、承認および使用ポリシーを使用して重要なデータを保護するのに役立つものの、このエンタープライズ権限管理ソリューションは、他の管理手段と共に使用する必要があります。 たとえば、物理的なセキュリティを実装したり、組織のデータへのアクセスが承認されているユーザーを慎重に検査および監視したり、共有してはならないデータを理解できるようにユーザーの教育に投資したりすることです。

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>電子メールをユーザー保護する方法として、[転送不可] と転送権限のないテンプレートにはどのような違いがありますか。

名前や外観に反して、**[転送不可]** は転送権限の反対ではなく、テンプレートでもありません。 実際には、コピー、印刷、添付ファイルの保存の制限を含む権限の集まりであり、それらに加え、電子メールの転送が制限されます。 権限は、選択した受信者に基づき、ユーザーに動的に適用されます。管理者によって静的に割り当てられるものではありません。 詳細については、「[Azure Rights Management の使用権限を構成する](../deploy-use/configure-usage-rights.md)」の「[電子メールの [転送不可] オプション](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails)」セクションを参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


