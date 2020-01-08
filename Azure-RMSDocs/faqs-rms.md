---
title: Azure RMS に関してよく寄せられる質問 - AIP
description: Azure Information Protection のデータ保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問の一部
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 56f8a89753660db66581822b5928f5340328918a
ms.sourcegitcommit: d0012de76c9156dd9239f7ba09c044a4b42ffc71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/06/2020
ms.locfileid: "75674226"
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Azure Information Protection のデータ保護に関してよく寄せられる質問

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE] 
> 統合された効率的なカスタマーエクスペリエンスを提供するために、Azure Portal での**Azure Information Protection クライアント (クラシック)** と**ラベル管理**は **、2021年3月31日**に**非推奨**とされる予定です。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection の統一されたラベル付けプラットフォームを使用して、統一されたラベル付けソリューションに移行できます。 詳細については、非[推奨の通知](https://aka.ms/aipclassicsunset)を参照してください。

Azure Information Protection のデータ保護サービス、Azure Rights Management に関して質問がございますか。 ここで回答を探してみてください。

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>ファイルを Azure Rights Management で保護するには、クラウドに置いておく必要があるのでしょうか。
よくある誤解ですが、そのようなことはありません。 Azure Rights Management サービス (と Microsoft) では、情報保護の一環としてユーザーのデータを閲覧したり、保存したりすることはありません。 ユーザーが保護した情報は、ユーザーが Azure に明示的に保存したり、Azure に情報を保存する別のクラウド サービスを使用しない限り、Azure に送信されたり保存されたりすることはありません。

詳細については、「Azure RMS のしくみ」を参照してください[。内部](./how-does-it-work.md)設置型で格納され、オンプレミスに格納されている secret cola 式が Azure Rights Management サービスによって保護されていても、オンプレミスのままになっていることを理解するためのものです。

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Azure Rights Management 暗号化と Microsoft のその他のクラウド サービスでの暗号化の違いは何ですか。

Microsoft はさまざまなシナリオでのデータ保護に合わせて多数の暗号化技術を提供していますが、多くの場合はデータ保護のシナリオが相互補完的です。 たとえば、Office 365 の暗号化は Office 365 に保存される静止状態のデータが対象ですが、Azure Information Protection の Azure Rights Management サービスは独立してユーザーのデータを暗号化するものであり、データは格納されている場所や伝送方法にかかわらず保護されます。

これらの暗号化技術は互いに補完するものであり、使用するには各技術を個別に有効化して構成する必要があります。 このときに、暗号化のキーを独自に用意するという選択が可能な場合があり、このようなシナリオは "BYOK" (Bring Your Own Key) とも呼ばれます。 暗号化技術の 1 つについて BYOK を有効にしても、それ以外の技術に影響することはありません。 たとえば、BYOK を Azure Information Protection に使用するが、それ以外の暗号化技術に対しては使用しないということも、その逆も可能です。 使用されるキーが暗号化技術ごとに異なるか同一であるかは、管理者が各サービスの暗号化オプションをどのように構成するかによって決まります。

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>BYOK と HYOK の違いは何ですか。また、どのような場合に使用すべきですか。

Azure Information Protection において**独自キーを持ち込む** (BYOK) のは、Azure Rights Management 保護の独自キーをオンプレミスで作成する場合です。 そのキーを Azure Key Vault のハードウェア セキュリティ モジュール (HSM) に転送し、そこでそのキーの所有と管理を続行します。 これを行わない場合、Azure Rights Management 保護では Azure 内で自動的に作成、管理されるキーが使用されます。 この既定の設定は、"顧客管理" ではなく "マイクロソフト管理" と呼ばれます (BYOK オプション)。

BYOK の詳細および組織でこのキー トポロジを選択すべきかについては、「[Azure Information Protection テナント キーの計画と実装](plan-implement-tenant-key.md)」を参照してください。

Azure Information Protection において**独自キーを保持する** (HYOK) 機能は、クラウドに格納されているキーで保護することができないドキュメントや電子メールのサブセットを持つような、少数の組織のためのものです。 こうした組織では、BYOK を使用してキーを作成し管理する場合でも、この制限が適用されます。 この制限は多くの場合、規制やコンプライアンス上の理由によるもので、HYOK 構成は "最高機密" 情報のみに適用されます。すなわち、組織外には決して共有されず、内部ネットワークのみで利用され、モバイル デバイスからアクセスする必要のない情報です。

これらの例外 (通常は、保護する必要のあるすべてのコンテンツの 10% 未満) については、組織は、オンプレミスのソリューションである Active Directory Rights Management サービスを使用して、オンプレミスのキーを作成することができます。 このソリューションでは、コンピューターはクラウドから Azure Information Protection ポリシーを取得しますが、この識別されたコンテンツはオンプレミスのキーを使用して保護することができます。

HYOK の詳細についてや、制限事項の正しい理解や使用するタイミングを確認するには、「[AD RMS 保護の Hold Your Own Key (HYOK) の要件と制限事項](configure-adrms-restrictions.md)」を参照してください。

## <a name="can-i-now-use-byok-with-exchange-online"></a>現在、Exchange Online で BYOK を使用できますか?

はい。「[Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)」 (Azure Information Protection 上に構築される新しい Office 365 メッセージの暗号化機能の設定) の手順に従って、Exchange Online で BYOK を使用することができるようになりました。 これらの手順に従うことで、新しい Office 365 メッセージの暗号化と、Azure Information Protection の BYOK の使用をサポートする新しい機能を Exchange Online で使用できるようになります。

この変更の詳細については、[Office 365 メッセージの暗号化と新しい機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)に関するブログのお知らせを参照してください。

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>Azure RMS と統合するサード パーティのソリューションに関する情報はどこで入手できますか?

既に多くのソフトウェア ベンダーが、Azure Rights Management と統合するソリューションを持っているか、またはそのソリューションを実装しており、リストは急増し続けています。 [RMS 対応ソリューション](requirements-applications.md#rms-enlightened-solutions)の一覧に役立つ情報が掲載されています。また Twitter の [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) からも最新の情報を入手できます。 さらに、[開発者ガイド](./develop/developers-guide.md)を確認し、Azure Information Protection の [Yammer サイト](https://www.yammer.com/AskIPTeam)に特定の統合の質問を投稿します。

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>RMS コネクタには管理パックまたは同様の監視メカニズムがありますか?

Rights Management コネクタは情報、警告、およびエラー メッセージをイベント ログに記録しますが、これらのイベントの監視機能を備えた管理パックはありません。 ただし、イベントの一覧とその説明および修正の実施に役立つ詳細な情報については、「[Azure Rights Management コネクタを監視する](monitor-rms-connector.md)」を参照してください。

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>Azure Portal で新しいカスタム テンプレートをどのように作成しますか?

カスタム テンプレートは、Azure Portal に移動しています。Azure Portal では、引き続きカスタムテンプレートをテンプレートとして管理したり、ラベルに変換することができます。 新しいテンプレートを作成するには、新しいラベルを作成し、Azure RMS 用のデータ保護設定を構成します。 その処理の裏では、Rights Management テンプレートと統合されるサービスとアプリケーションが次からアクセスできるようになる新しいテンプレートが作成されます。

Azure Portal のテンプレートの詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

## <a name="ive-protected-a-document-and-now-want-to-change-the-usage-rights-or-add-usersdo-i-need-to-reprotect-the-document"></a>保護されているドキュメントに対して、使用権限の変更またはユーザーの追加を行いたいのですが、ドキュメントを再保護する必要がありますか。

ドキュメントがラベルまたはテンプレートを使用して保護されている場合、ドキュメントを再保護する必要はありません。 使用権限に変更を加えるか、新しいグループ (またはユーザー) を追加することによって、ラベルまたはテンプレートを変更した後、変更内容を保存します。

- 変更を加える前にユーザーがドキュメントにアクセスしていない場合、ユーザーがドキュメントを開くとすぐに変更が有効になります。

- ユーザーが既にドキュメントにアクセスしている場合は、ユーザーの[使用ライセンス](configure-usage-rights.md#rights-management-use-license)の有効期限が過ぎた時点で変更が有効になります。 使用ライセンスの有効期限が切れるまで待てない場合にのみ、ドキュメントを再保護します。 効果的に再保護を行うと、ドキュメントの新しいバージョンが作成され、ユーザーの使用ライセンスも新しくなります。

あるいは、必要なアクセス許可に対して既にグループを構成している場合、グループのメンバーシップを変更してユーザーの追加または除外を行うことができます。ラベルまたはテンプレートの変更は必要ありません。 Azure Rights Management サービスがグループ メンバーシップを[キャッシュ](prepare.md#group-membership-caching-by-azure-information-protection)に入れるため、変更が反映されるまでわずかな遅延が生じる可能性があります。

カスタム アクセス許可を使用してドキュメントが保護されている場合は、既存のドキュメントのアクセス許可を変更できません。 ドキュメントを再度保護し、この新しいバージョンのドキュメントに必要なすべてのユーザーとすべての使用権限を指定する必要があります。 保護されたドキュメントを再保護するには、"フル コントロール" 使用権限が必要です。

ヒント: ドキュメントがテンプレートで保護されているのか、それともカスタム アクセス許可を使用して保護されているのかを確認するには、[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell コマンドレットを使用してください。 [Get-RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate) を実行したときに一意のテンプレート ID が表示されない場合は、カスタム アクセス許可の **[制限されたアクセス]** に関するテンプレートの説明を必ず確認してください。

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>一部のユーザーが Exchange Online 上の Exchange に、他のユーザーが Exchange Server 上の Exchange に登録されているハイブリッド デプロイメント構成です。この構成は、Azure RMS でサポートされていますか。
はい、サポートされています。また、2 つの Exchange デプロイメント間でシームレスに電子メールと添付ファイルを保護し、保護された電子メールと添付ファイルを使用できることがメリットです。 この構成の場合、[Azure RMS をアクティブ化し](activate-service.md)、[IRM for Exchange Online を有効にして](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)、[RMS コネクタをデプロイして](deploy-rms-connector.md) Exchange Server 用に構成します。

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azurerms"></a>運用環境にこの保護を利用すると、会社の環境がこのソリューションに固定されたり、Azure RMS で保護したコンテンツにアクセスできなくなる危険性が生じたりしますか。
いいえ。データを常に制御することができます。また、たとえ Azure Rights Management サービスの使用を停止したとしても、継続してデータにアクセスすることができます。 詳細については、「[Azure Rights Management の使用停止と非アクティブ化](decommission-deactivate.md)」を参照してください。

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>Azure RMS を使用してコンテンツを保護するユーザーを制御できますか。
はい。Azure Rights Management サービスには、このシナリオのためのユーザー オンボーディング コントロールがあります。 詳細については、「 [Azure Information Protection からの保護サービスのアクティブ化](activate-service.md)」の記事の「[段階的な展開のオンボードコントロールの構成](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>ユーザーが、保護されたドキュメントを特定の組織と共有しないようにすることはできますか。
データ保護に Azure Rights Management サービスを使用する最大の利点の 1 つは、Azure AD が認証を自動的に処理するため、各パートナー組織に対して明示的な信頼を構成することなく、企業間のコラボレーションをサポートできることです。

ユーザーが特定の組織とのドキュメントの安全な共有を防止するような管理オプションはありません。 たとえば、信頼していない組織や、競合先の組織をブロックするとします。 Azure Rights Management サービスがこれらの組織のユーザーに保護されたドキュメントを送信しないようにしても意味がありません。その場合、ユーザーはドキュメントを保護されていないまま共有することになり、おそらくこれはこのシナリオにおいて最も望ましくない状況です。 たとえば、これらの組織のユーザーと社外秘ドキュメントを共有しているユーザーを識別することはできませんが、ドキュメント (または電子メール) が Azure Rights Management サービスで保護されていれば、これが可能になります。

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>保護されたドキュメントを社外のユーザーと共有する場合、そのユーザーはどのようにして認証されますか。

既定では、Azure Rights Management サービスは、ユーザー認証に Azure Active Directory アカウントと関連付けられた電子メール アドレスを使用します。これにより、管理者にとって企業間のコラボレーションがシームレスになります。 他の組織で Azure サービスを使用する場合は、アカウントがオンプレミスで作成、管理されてから Azure に同期される場合でも、ユーザーは既に Azure Active Directory にアカウントを持っています。 組織が内部的に Office 365 を所有している場合、このサービスはユーザー アカウント用に Azure Active Directory も使用します。 ユーザーの組織が Azure に管理アカウントを持っていない場合、ユーザーは[個人向け RMS](./rms-for-individuals.md) にサインアップできます。これは、アンマネージド Azure テナントと組織用のディレクトリをユーザー用のアカウントを使用して作成するため、このユーザー (およびそれ以降のユーザー) は Azure Rights Management サービスに対して認証されます。

このようなアカウントの認証方法は、他の組織の管理者が Azure Active Directory アカウントを構成している方法によって異なります。 たとえば、これらのアカウント用に作成したパスワード、フェデレーション、Active Directory Domain Services で作成した後 Azure Active Directory に同期したパスワードを使用できます。

その他の認証方法:

- Azure AD のアカウントを持っていないユーザー宛の Office ドキュメントが添付されている電子メールを保護する場合、認証方法が異なります。 Azure Rights Management サービスは、Gmail など、いくつかの一般的なソーシャル ID プロバイダーと統合されます。 ユーザーの電子メール プロバイダーがサポートされている場合、ユーザーはそのサービスにサインインでき、電子メール プロバイダーによって認証が行われます。 ユーザーの電子メール プロバイダーがサポートされていない場合、または基本設定として、ユーザーは認証を行い、Web ブラウザーで保護されたドキュメントを含む電子メールを表示するためのワンタイム パスワードを申請できます。

- Azure Information Protection では、サポートされているアプリケーションの Microsoft アカウントを使用できます。 現在、Microsoft アカウントが認証に使用されている場合、アプリケーションによっては、保護されたコンテンツを開けない場合があます。 [詳細情報](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>社外のユーザーをカスタム テンプレートに追加できますか?

対応 Azure Portal で構成できる[保護設定](configure-policy-protection.md)では、組織の外部からユーザーとグループや、別組織の全ユーザーに対しても、アクセス許可を追加することができます。 これについては、必要に応じて「[Azure Information Protection を使用したセキュアなドキュメント コラボレーション](secure-collaboration-documents.md)」をご覧ください。 

Azure Information Protection ラベルがある場合は、最初にカスタム テンプレートをラベルに変換してから、Azure Potal でこれらの保護設定を構成する必要があります。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

または、PowerShell を使用して、カスタム テンプレート (およびラベル) に外部ユーザーを追加できます。 この構成では、テンプレートを更新するために使用する権限定義オブジェクトを使用する必要があります。

1. [AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)コマンドレットを使用して変数を作成することにより、権限定義オブジェクトで外部電子メールアドレスとその権限を指定します。

2. RightsDefinition パラメーターにこの変数を指定します。これには、 [Set AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)コマンドレットを使用します。

    ユーザーを既存のテンプレートを追加するときに、新しいユーザーに加え、テンプレート内の既存のユーザーに対して、権限定義オブジェクトを定義する必要があります。 このシナリオでは、コマンドレットの「[例](/powershell/module/aipservice/set-aipservicetemplateproperty#examples)」セクションの「**Example 3: Add new users and rights to a custom template**」 (例 3: カスタム テンプレートへの新しいユーザーと権利の追加) が役に立ちます。

## <a name="what-type-of-groups-can-i-use-with-azure-rms"></a>Azure RMS では、どの種類のグループを使用できますか?
ほとんどのシナリオでは、電子メール アドレスを持つ、Azure AD 内の任意の種類のグループを使用できます。 この経験則は、使用権限を割り当てる際に常に適用されますが、Azure Rights Management サービスの管理の場合はいくつか例外があります。 詳細については、「[グループ アカウントに関する Azure Information Protection の要件](prepare.md#azure-information-protection-requirements-for-group-accounts)」を参照してください。

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>保護されたメールを Gmail または Hotmail のアカウントに送信するにはどうしますか。

Exchange Online と Azure Rights Management サービスを使用する場合は、保護メッセージとしてユーザーに電子メールを送信するだけです。 たとえば、Outlook on the Web のコマンド バーにある新しい **[保護]** ボタンを選択するか、Outlook の **[転送不可]** ボタンまたはメニュー オプションを選択できます。 または、自動的に転送不可を適用する Azure Information Protection ラベルを選択して、電子メールを分類することができます。

受信者には Gmail、Yahoo、または Microsoft アカウントにサインインするためのオプションが表示され、保護された電子メールを読むことができます。 また、ブラウザーで電子メールを読み取るためにワンタイム パスワードのオプションを選択することもできます。

このシナリオをサポートするには、Exchange Online を Azure Rights Management サービスおよび Office 365 のメッセージの暗号化の新しい機能で使用できるようにする必要があります。 この構成の詳細については、「[Exchange Online: IRM 構成](configure-office365.md#exchangeonline-irm-configuration)」をご覧ください。

すべてのデバイスですべての電子メール アカウントをサポートする新機能の詳細については、ブログの投稿「[Announcing new capabilities available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)」 (Office 365 のメッセージの暗号化で使用できる新機能のお知らせ) を参照してください。

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Azure RMS でサポートされているデバイスとファイルの種類を教えてください。
Azure Rights Management サービスをサポートするデバイスの一覧については、「[Azure Rights Management データ保護をサポートするクライアント デバイス](./requirements-client-devices.md)」をご覧ください。 サポートされているデバイスによっては一部の Rights Management 機能がサポートされていないため、[RMS 対応のアプリケーション](./requirements-applications.md#rms-enlightened-applications)の表も確認してください。

Azure Rights Management サービスはあらゆる種類のファイルに対応しています。 テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、他のいくつかのアプリケーションのファイルの種類については、Azure Rights Management は暗号化と権限の適用 (アクセス許可) の両方を含むネイティブな保護を提供します。 他のすべてのアプリケーションとファイルの種類については、ファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証という一般的な保護機能が提供されます。

Azure Rights Management でネイティブでサポートされているファイル名拡張子の一覧については、「[File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)」(Azure Information Protection クライアントでサポートされるファイルの種類) を参照してください。 一覧に含まれないファイル名拡張子は、汎用的な保護をこれらのファイルに自動的に適用する Azure Information Protection クライアントを使用することによってサポートされます。

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>ドキュメントを保護および追跡するように Mac コンピューターを設定するにはどうすればよいのですか?

まず、 https://admin.microsoft.com のソフトウェア インストール リンクから Office for Mac がインストールされていることを確認します。 手順については、「[Office 365 または Office 2019 を PC または Mac にダウンロードしてインストールまたは再インストールします](https://support.office.com/en-us/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658)」を参照してください。

Office 365 の職場または学校のアカウントを使用して、Outlook を開き、プロファイルを作成します。 次に新しいメッセージを作成し、次の操作を行って、Azure Rights Management サービスを使用してドキュメントや電子メールを保護できるように Office を構成します。

1. 新規のメッセージで、 **[オプション]** タブで、 **[アクセス許可]** をクリックし、 **[資格情報の確認]** をクリックします。

2. 入力要求が表示されたら、Office 365 の職場または学校のアカウントの詳細をもう一度指定し、 **[サインイン]** を選択します。

    これによって Azure Rights Management テンプレートがダウンロードされ、**資格情報の確認**が、**無制限**、**転送不可**、およびユーザーのテナント用に公開されたすべての Azure Rights Management テンプレートを含むオプションで置換されます。 この新しいメッセージを今すぐ取り消すことができます。

電子メール メッセージやドキュメントを保護するには、 **[オプション]** タブで、 **[アクセス許可]** をクリックして、電子メールやドキュメントを保護するオプションまたはテンプレートを選択します。

ドキュメントを保護した後、ドキュメントを追跡するには、Azure Information Protection クライアントをインストールした Windows コンピューターから、Office アプリケーションまたはエクスプローラーを使用して、ドキュメントをドキュメント追跡サイトに登録します。 手順については、[ドキュメントの追跡と取り消し](./rms-client/client-track-revoke.md)に関する記事を参照してください。 Mac コンピューターからは、現在、Web ブラウザーを使用してドキュメント追跡サイト (https://track.azurerms.com) ) に移動し、このドキュメントを追跡して取り消すことができます。

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>RMS で保護されている Office ドキュメントを開いた場合、関連付けられた一時ファイルも RMS で保護されたものになりますか。
いいえ。 このシナリオでは、関連付けられている一時ファイルには元のドキュメントのデータは含まれず、ユーザーがファイルを開いているときに入力したもののみが含まれます。 元のファイルとは異なり、一時ファイルは明らかに共有用に設計されておらず、BitLocker や EFS などのローカル セキュリティ コントロールによって保護されデバイス上に残ります。

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>必要な機能があるのですが、SharePoint で保護されたライブラリには使用できないようです。この機能のサポートは予定されていますか。
現在のところ、SharePoint は、IRM で保護されたライブラリを使用して、RMS で保護されたドキュメントをサポートしています。IRM で保護されたライブラリは、Rights Management テンプレートやドキュメントの追跡などの機能をサポートしていません。 詳細については、記事「[Office アプリケーションおよびサービス](./office-apps-services-support.md)」の「[SharePoint Online と SharePoint Server](./office-apps-services-support.md#sharepoint-online-and-sharepoint-server)」セクションを参照してください。

まだサポートされていない機能に関する情報については、[Enterprise Mobility and Security チーム ブログ](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-rights-management-services)のお知らせに注意してください。

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>ユーザーが社内や社外の人間とファイルを安全に共有できるように SharePoint Online で OneDrive for Business を構成するには、どうすればよいですか。
既定では、Office 365 管理者は構成しません。ユーザーが構成します。

SharePoint サイト管理者が、所有する SharePoint ライブラリの IRM を有効にして構成するのと同じように、OneDrive for Business は、ユーザーが自身の OneDrive for Business ライブラリの IRM を有効にして構成するように設計されています。 ただし、PowerShell を使用して、ユーザーに代わってこの処理を行うことができます。 手順については、記事「[Office 365: クライアントとオンライン サービスの構成](configure-office365.md)」の「[SharePoint Online と OneDrive for Business:IRM 構成](configure-office365.md#sharepointonline-and-onedrive-for-business-irm-configuration)」セクションをご覧ください。

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>正常にデプロイするためのヒントやコツがあれば教えてください。

これまでに多数のデプロイをサポートし、顧客、パートナー、コンサルタント、サポート エンジニアから話を聞いてきた経験から言える一番のヒントは、**シンプルなポリシーを設計してデプロイすること**です。

Azure Information Protection では、他のユーザーと情報を安全に共有できるため、データ保護の範囲を詳細に指定することができます。 使用権限の制限の構成は慎重に行ってください。 多くの組織にとって、業務上最も重要な利点は、組織内のユーザーのアクセス許可を制限して、データ漏えいを防止できることです。 もちろん、印刷や編集などを防ぐ必要がある場合に比べて、はるかに詳細な情報を得ることができます。ただし、高レベルのセキュリティが本当に必要なドキュメントについては、例外としてより細かい制限を設け、1日に制限の厳しい使用権限を実装するのではなく、より段階的なアプローチを計画することをお勧めします。

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>退職した従業員が保護していたファイルにアクセスするには、どうすればよいですか。
[スーパー ユーザー機能](configure-super-users.md)を使用してください。この機能により、テナントで保護されているすべてのドキュメントと電子メールに対して承認されたユーザーにフル コントロール使用権限が与えられます。 スーパー ユーザーは常にこの保護されたコンテンツを読み取ることができ、必要に応じて、保護を解除したり、別のユーザーのために再度保護したりすることができます。 また必要に応じて、スーパー ユーザー機能を使用すると、権限を持つサービスのインデックス化とファイルの検証を行うことができます。

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>ドキュメント追跡サイトで失効をテストすると、最大 30 日間はドキュメントにアクセスできるというメッセージが表示されます。この期間を構成することはできますか。

対応 このメッセージは、その特定のファイルの[使用ライセンス](configure-usage-rights.md#rights-management-use-license)を反映します。

ファイルを取り消すと、そのアクションは、Azure Rights Management サービスにユーザーを認証する場合にのみ適用できます。 そのため、ファイルに 30 日間の使用ライセンス有効期間があり、ユーザーが既にそのドキュメントを開いている場合、ユーザーは引き続きその使用ライセンスの期間中はドキュメントにアクセスすることができます。 使用ライセンスの期限が切れた後は、ドキュメントが取り消されているため、ユーザーのアクセスが拒否される時点で、ユーザーの再認証が必要になります。

ドキュメントを保護したユーザーである [Rights Management 発行者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)は、この取り消しから除外されており、常に自分のドキュメントにアクセスできます。

テナントに適用される使用ライセンスの有効期間の既定値は 30 日間です。ラベルまたはテンプレートで、この設定をより制限の厳しい値でオーバーライドできます。 使用ライセンスの詳細および使用ライセンスの構成方法については、[Rights Management の使用ライセンス](configure-usage-rights.md#rights-management-use-license)に関するページを参照してください。

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management は画面キャプチャを防止できますか。
**コピー** [使用権限](configure-usage-rights.md)を付与しないことにより、Rights Management は、windows プラットフォーム (windows 7、Windows 8.1、windows 10、windows 10 Mobile) および Android で一般的に使用されているさまざまな画面キャプチャツールから画面キャプチャを防ぐことができます。 ただし、iOS および Mac デバイスでは、いかなるアプリも画面キャプチャを防止することができません。 さらに、すべてのデバイス上のブラウザーは画面キャプチャを防止することができません。 ブラウザーでは、web 用に Outlook と Office を使用します。

画面のキャプチャを禁止しておくと、不注意や不測の出来事により機密性の高い情報が漏洩してしまう事態を避けることができます。 ただし、画面に表示されるデータをユーザーが共有する方法は多数あります。スクリーンショットを撮影する方法は、1つの方法にすぎません。 たとえば、表示される情報を共有しようとするユーザーは、カメラ付き携帯電話を使用して写真を撮影したり、データを再入力したり、単に口頭で他者に伝達することができます。

このように、あらゆるプラットフォームとソフトウェアが Rights Management API をサポートしており、かつ画面キャプチャをブロックできたとしても、テクノロジだけでデータの漏洩を防ぐことができるわけではありません。 Rights Management は、承認および使用ポリシーを使用して重要なデータを保護するのに役立つものの、このエンタープライズ権限管理ソリューションは、他の管理手段と共に使用する必要があります。 たとえば、物理的なセキュリティを実装したり、組織のデータへのアクセスが承認されているユーザーを慎重に検査および監視したり、共有してはならないデータを理解できるようにユーザーの教育に投資したりすることです。

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>電子メールをユーザー保護する方法として、[転送不可] と転送権限のないテンプレートにはどのような違いがありますか。

名前や外観に反して、 **[転送不可]** は転送権限の反対ではなく、テンプレートでもありません。 実際には、コピー、印刷、添付ファイルの保存の制限を含む権限の集まりであり、それらに加え、電子メールの転送が制限されます。 権限は、選択した受信者に基づき、ユーザーに動的に適用されます。管理者によって静的に割り当てられるものではありません。 詳細については、「 [Azure Information Protection の使用権限を構成する](configure-usage-rights.md)」の「[電子メールの [転送不可] オプション](configure-usage-rights.md#do-not-forward-option-for-emails)」セクションを参照してください。

