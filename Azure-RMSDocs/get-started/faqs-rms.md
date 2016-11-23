---
title: "Azure Information Protection のデータ保護サービス、Azure Rights Management に関してよく寄せられる質問 | Azure Information Protection"
description: "Azure Information Protection のデータ保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問の一部"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: eb9b9c1308abe6b1b5803cba7ba254d54cbac812
ms.openlocfilehash: d3d11dba936ca8901b701008e55df8d73be8bded


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

## <a name="can-i-integrate-the-azure-rights-management-service-with-my-on-premises-servers"></a>Azure Rights Management サービスとオンプレミス サービスを統合できますか。
はい。 Azure Rights Management は、Exchange Server、SharePoint、Windows ファイル サーバーなどのオンプレミス サーバーと統合できます。 統合するには、[Rights Management コネクタ](../deploy-use/deploy-rms-connector.md)を使用します。 または、Windows Server でファイル分類インフラストラクチャ (FCI) を使用することのみを目的とされている場合は、[RMS 保護コマンドレット](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx)を使用できます。 また、Active Directory ドメイン コントローラーを Azure AD と同期し、連携することで、たとえば [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)を使用して、よりシームレスな認証方法をユーザーに提供できます。

必要に応じて、Azure Rights Management で XrML 証明書の生成と管理が自動的に行われるので、オンプレミスの PKI は使用されません。 Azure Rights Management での証明書の使用方法については、記事「[Azure RMS の機能の詳細](../understand-explore/how-does-it-work.md)」の「[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」セクションを参照してください。

## <a name="where-can-i-find-information-about-3rd-party-solutions-that-integrate-with-azure-rms"></a>Azure RMS と統合するサード パーティのソリューションに関する情報はどこで入手できますか?

既に多くのソフトウェア ベンダーが、Azure Rights Management と統合するソリューションを持っているか、またはそのソリューションを実装しており、リストは急増し続けています。 [Enterprise Mobility and Security のブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)に役立つ情報が掲載されています。また Twitter の [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) からも最新の情報が入手できます。 なお、具体的なご質問は、Information Protection チーム (askipteam@microsoft.com.) までメールでメッセージをお送りください。

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>RMS コネクタには管理パックまたは同様の監視メカニズムがありますか?

Rights Management コネクタは情報、警告、およびエラー メッセージをイベント ログに記録しますが、これらのイベントの監視機能を備えた管理パックはありません。 ただし、イベントの一覧とその説明および修正の実施に役立つ詳細な情報については、「[Azure Rights Management コネクタを監視する](../deploy-use/monitor-rms-connector.md)」を参照してください。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>Azure RMS を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?

Office 365 テナントまたは Azure AD テナントのグローバル管理者は、Azure Rights Management サービスのすべての管理タスクを実行できます。 ただし、他のユーザーに管理者権限を割り当てる場合は、Azure RMS の PowerShell コマンドレット [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) を使用して行うことができます。 この管理ロールは、ユーザー アカウントまたはグループごとに割り当てることができます。 使用できるロールは、**グローバル管理者**と**コネクタ管理者**の 2 つです。 

ロールの名前からわかるように、1 番目のロールは Azure Rights Management のすべての管理タスクを実行する権限を付与します (他のクラウド サービスのグローバル管理者には付与しません)、2 番目のロールは Rights Management (RMS) コネクタのみを実行する権限を付与します。

注意事項:

- Office 365 のグローバル管理者と Azure AD のグローバル管理者のみが、管理ポータル (Office 365 管理センターまたは Azure クラシック ポータル) を使用して Azure RMS を構成できます。 Azure RMS のグローバル管理者ロールを割り当てられたユーザーは、Azure RMS の PowerShell コマンドを使用して Azure RMS を構成する必要があります。 特定のタスクを実行する正しいコマンドレットについては、「[Windows PowerShell を使用した Azure Rights Management の管理](../deploy-use/administer-powershell.md)」を参照してください。

- [オンボーディング コントロール](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成してある場合は、RMS コネクタを除き、Azure RMS を管理する機能に影響はありません。 たとえば、コンテンツを保護する機能を "IT department" グループに制限するようにオンボーディング コントロールが構成されている場合、RMS コネクタのインストールと構成に使用するアカウントは、そのグループのメンバーである必要があります。 

- Azure RMS の管理者 (テナントのグローバル管理者または Azure RMS のグローバル管理者) は、Azure RMS によって保護されていたドキュメントまたは電子メールから保護を自動的に削除することはできません。 Azure RMS のスーパー ユーザーを割り当てられたユーザーだけが、スーパー ユーザー機能が有効になっているときにのみ、これを行うことができます。 ただし、テナントのグローバル管理者および Azure RMS のグローバル管理者は、ユーザーをスーパー ユーザーとして割り当てることができます (これには自分自身のアカウントも含まれます)。 また、スーパー ユーザー機能を有効にすることもできます。 これらのアクションは、Azure RMS の管理者ログに記録されます。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」のセキュリティのベスト プラクティスに関するセクションを参照してください。 


## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>一部のユーザーが Exchange Online 上の Exchange に、他のユーザーが Exchange Server 上の Exchange に登録されているハイブリッド デプロイメント構成です。この構成は、Azure RMS でサポートされていますか。
はい、サポートされています。また、2 つの Exchange デプロイメント間でシームレスに電子メールと添付ファイルを保護し、保護された電子メールと添付ファイルを使用できるようになることがメリットです。 この構成の場合、[Azure RMS をアクティブ化し](../deploy-use/activate-service.md)、[IRM for Exchange Online を有効にして](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)、[RMS コネクタをデプロイして](../deploy-use/deploy-rms-connector.md) Exchange Server 用に構成します。

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>運用環境にこの保護を利用すると、会社の環境が Azure RMS に固定されたり、Azure RMS で保護したコンテンツにアクセスできなくなる危険性が生じたりしますか。
いいえ。データを常に制御することができます。また、たとえ Azure Rights Management サービスの使用を停止したとしても、継続してデータにアクセスすることができます。 詳細については、「[Azure Rights Management の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」を参照してください。

ただし、Azure RMS のデプロイメントを停止される前に、お客様が使用を停止する理由を伺う機会をいただいています。 Azure Rights Management 保護がビジネス要件を満たしていない場合は、近い将来に新機能が計画されているか、代替案がないかをお問い合わせください。 お問い合わせの電子メールは [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) に送信してください。技術とビジネスの要件について説明いたします。

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>Azure RMS を使用してコンテンツを保護するユーザーを制御できますか。
はい。Azure Rights Management サービスには、このシナリオのためのユーザー オンボーディング コントロールがあります。 詳細については、記事「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」の「[段階的デプロイのオンボーディング コントロールの構成](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)」のセクションを参照してください。

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>ユーザーが、保護されたドキュメントを特定の組織と共有しないようにすることはできますか。
データ保護に Azure Rights Management サービスを使用する最大の利点の 1 つは、Azure AD が認証を自動的に処理するため、各パートナー組織に対して明示的な信頼を構成することなく、企業間のコラボレーションをサポートできることです。

ユーザーが特定の組織とのドキュメントの安全な共有を防止するような管理オプションはありません。 たとえば、信頼していない組織や、競合先の組織をブロックするとします。 Azure Rights Management サービスがこれらの組織のユーザーに保護されたドキュメントを送信しないようにしても意味がありません。その場合、ユーザーはドキュメントを保護されていないまま共有することになり、おそらくこれはこのシナリオにおいて最も望ましくない状況です。 たとえば、これらの組織のユーザーと社外秘ドキュメントを共有しているユーザーを識別することはできませんが、ドキュメント (または電子メール) が Azure Rights Management サービスで保護されていれば、これが可能になります。

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>保護されたドキュメントを社外のユーザーと共有する場合、そのユーザーはどのようにして認証されますか。
Azure Rights Management サービスは、常にユーザー認証に Azure Active Directory アカウントと関連付けられた電子メール アドレスを使用します。これは、管理者にとって企業間のコラボレーションをシームレスにします。 他の組織で Azure サービスを使用する場合は、アカウントがオンプレミスで作成、管理されてから Azure に同期される場合でも、ユーザーは既に Azure Active Directory にアカウントを持っています。 組織が内部的に Office 365 を所有している場合、このサービスはユーザー アカウント用に Azure Active Directory も使用します。 ユーザーの組織が Azure に管理アカウントを持っていない場合、ユーザーは[個人向け RMS](../understand-explore/rms-for-individuals.md) にサインアップできます。これは、管理されていない Azure テナントと組織用のディレクトリをユーザー用のアカウントを使用して作成するため、このユーザー (およびそれ以降のユーザー) は Azure Rights Management サービスに対して認証されます。

このようなアカウントの認証方法は、他の組織の管理者が Azure Active Directory アカウントを構成している方法によって異なります。 たとえば、これらのアカウント用に作成されたパスワード、多要素認証 (MFA)、フェデレーション、Active Directory Domain Services で作成されたパスワードを使用してから、Azure Active Directory に同期される場合があります。

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>社外のユーザーをカスタム テンプレートに追加できますか?
はい。 エンドユーザー (と管理者) がアプリケーションから選択できるカスタム テンプレートを作成すると、指定した定義済みのポリシーを使用して、すばやく簡単に情報保護を適用できます。 テンプレートの設定の 1 つに、コンテンツにアクセス可能なユーザーの設定があります。組織内のグループとユーザー、および組織外のユーザーを指定できます。

組織外のユーザーを指定するには、テンプレートを構成するとき、Azure クラシック ポータルで選択したグループに連絡先として追加します。 あるいは、[Azure Rights Management 用 Windows PowerShell モジュール](../deploy-use/install-powershell.md)を使用します。

-   **権限定義オブジェクトを使用してテンプレートを作成または更新する**。    権限定義オブジェクトで外部電子メール アドレスおよびその権限を指定し、これを使用してテンプレートを作成または更新します。 [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) コマンドレットを使用して権限定義オブジェクト指定し、変数を作成してから、[Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) コマンドレット (新しいテンプレート用) または [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) コマンドレット (既存のテンプレートを変更する場合) を使用して、この変数を -RightsDefinition パラメーターに指定します。 ただし、これらのユーザーを既存のテンプレートに追加する場合は、外部ユーザーだけでなく、テンプレートに既存のグループの権限定義オブジェクトを定義する必要があります。

カスタム テンプレートの詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

## <a name="does-azure-rms-work-with-dynamic-groups-in-azure-ad"></a>Azure RMS で Azure AD の動的なグループを使用できますか。
Azure AD Premium の機能では、[属性ベースのルール](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/)を指定することによってグループの動的メンバーシップを構成できます。 Azure AD でセキュリティ グループを作成する場合、このグループの種類では動的メンバーシップがサポートされますが、電子メール アドレスはサポートされないため、Azure Rights Management サービスで使用することはできません。 ただし、動的メンバーシップをサポートし、メールが有効な新しいグループの種類を Azure AD で作成できるようになりました。 Azure クラシック ポータルで新しいグループを追加する場合は、**グループの種類**として **Office 365 の "プレビュー"** を選択できます。 このグループではメールが有効なため、Azure Rights Management 保護で使用できます。

オプション名が明確に表示されているため、この新しいグループの種類は、必要な追加機能および使用する新しいドキュメントと共にプレビュー段階のままです。 その間に、Azure Rights Management 保護でこの新しいグループの種類を使用できることを確認する必要があります。


## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Azure RMS でサポートされているデバイスとファイルの種類を教えてください。
Azure Rights Management サービスをサポートするデバイスの一覧については、「[Azure Rights Management データ保護をサポートするクライアント デバイス](../get-started/requirements-client-devices.md)」をご覧ください。 サポートされるデバイスによっては一部の Rights Management 機能がサポートされていないため、「[Azure Rights Management データ保護をサポートするアプリケーション](../get-started/requirements-applications.md)」の表も確認してください。

Azure Rights Management サービスはあらゆる種類のファイルに対応しています。 テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、他のいくつかのアプリケーションのファイルの種類については、Azure Rights Management は暗号化と権限の適用 (アクセス許可) の両方を含むネイティブな保護を提供します。 他のすべてのアプリケーションとファイルの種類については、ファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証という一般的な保護機能が提供されます。

Azure Rights Management でネイティブでサポートされるファイル名拡張子の一覧については、「[Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)」の「[サポートされているファイルの種類とファイル名拡張子](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)」セクションを参照してください。 一覧に含まれないファイル名拡張子は、一般保護をこれらのファイルに自動的に適用する RMS 共有アプリケーションを使用することによってサポートされます。

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>RMS で保護されている Office ドキュメントを開いた場合、関連付けられた一時ファイルも RMS で保護されたものになりますか。

いいえ。 このシナリオでは、関連付けられている一時ファイルには元のドキュメントのデータは含まれず、ユーザーがファイルを開いているときに入力したもののみが含まれます。 元のファイルとは異なり、一時ファイルは明らかに共有用に設計されておらず、BitLocker や EFS などのローカル セキュリティ コントロールによって保護されデバイス上に残ります。

## <a name="we-really-want-to-use-byok-with-azure-information-protection-but-learned-that-this-isnt-compatible-with-exchange-onlinewhats-your-advice"></a>BYOK と Azure Information Protection を併用したいのですが、BYOK は Exchange Online と互換性がないと知りました。何かアドバイスはありますか。
現在の制限を理由に、Azure Information Protection の Azure Rights Management の利用を遅らせる必要はありません。 Exchange Online をお持ちで、Bring Your Own Key (BYOK) を使用する場合は、当面 Azure Information Protection を既定のキー管理モード (キーの生成と管理を Microsoft で行う) でデプロイすることをお勧めします。 この方法を採用すると、重要なファイルと電子メールを保護する機能をすぐに活用し、後で (たとえば Exchange Online が BYOK をサポートするようになったときなどに) BYOK に移行することができます。 BYOK に移行した後も、前に保護したドキュメントや電子メールには、アーカイブされたキーを使用して引き続きアクセスできます。

ただし、会社のポリシーでハードウェア セキュリティ モジュール (HSM) を使用する必要があり、そのために Azure Information Protection をデプロイできない場合は、Azure Information Protection をデプロイし、Exchange の Rights Management の制限付き保護機能と BYOK を併用する方法があります。 詳細については、「[Azure Rights Management テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」の「[BYOK の料金と制限事項](../plan-design/byok-price-restrictions.md)」を参照してください。

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>必要な機能があるのですが、SharePoint で保護されたライブラリには使用できないようです。この機能のサポートは予定されていますか。
現在のところ、SharePoint は、IRM で保護されたライブラリを使用して、Rights Management で保護されたドキュメントをサポートしています。IRM で保護されたライブラリは、カスタム テンプレート、ドキュメントの追跡などの機能をサポートしていません。 詳細については、記事「[Office アプリケーションおよびサービス](../understand-explore/office-apps-services-support.md)」の「[SharePoint Online と SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server)」セクションを参照してください。

まだサポートされていない機能に関する情報については、[Enterprise Mobility and Security チーム ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)のお知らせに注意してください。

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>ユーザーが社内や社外の人間とファイルを安全に共有できるように SharePoint Online で OneDrive for Business を構成するには、どうすればよいですか。
既定では、Office 365 管理者は構成しません。ユーザーが構成します。

SharePoint サイト管理者が、所有する SharePoint ライブラリの IRM を有効にして構成するのと同じように、OneDrive for Business は、ユーザーが自身の OneDrive for Business ライブラリの IRM を有効にして構成するように設計されています。  ただし、PowerShell を使用して、ユーザーに代わってこの処理を行うことができます。 手順については、記事「[Office 365: クライアントとオンライン サービスの構成](../deploy-use/configure-office365.md)」の「[SharePoint Online と OneDrive for Business:IRM 構成](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)」セクションを参照してください。

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>正常にデプロイするためのヒントやコツがあれば教えてください。
これまでに多数のデプロイをサポートし、顧客、パートナー、コンサルタント、サポート エンジニアから話を聞いてきた経験から言える一番のヒントは、**シンプルな権限ポリシーを設計してデプロイすること**です。

Azure Information Protection では、他のユーザーと情報を安全に共有できるため、データ保護の範囲を詳細に指定することができます。 しかし、権限ポリシーはできるだけシンプルにしてください。 多くの組織にとって、Azure RMS の導入による業務上最も重要な利点は、既定の権限ポリシー テンプレートを適用して組織内のユーザーのアクセス許可を制限し、データ漏えいを防止できることです。 もちろん、印刷や編集などの操作を制限する必要があれば、より詳細なポリシーを作成することもできます。ただし、そのような細かい制限は、高レベルのセキュリティが必要なドキュメントに限定してください。最初から制限の厳しいポリシーを作成するのではなく、段階的に計画して作成していくことをお勧めします。

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>退職した従業員が保護していたファイルにアクセスするには、どうすればよいですか。
Azure RMS のスーパー ユーザー機能を使用してください。スーパー ユーザー権限を持つユーザーは、組織の RMS テナントから付与されたすべての使用ライセンスについて、完全な所有者権限を持ちます。 また必要に応じて、スーパー ユーザー機能を使用すると、権限を持つサービスのインデックス化とファイルの検証を行うことができます。

詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」を参照してください。

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>ドキュメント追跡サイトで失効をテストすると、最大 30 日間はドキュメントにアクセスできるというメッセージが表示されます。この期間を構成することはできますか。

はい。 このメッセージは、その特定のファイルの使用ライセンスを反映します。 使用ライセンスは、保護されたファイルや電子メール メッセージを開くユーザーに付与されるドキュメントごとの証明書です。 この証明書は、ファイルや電子メール メッセージに対するユーザーの権限のほか、コンテンツを暗号化する際に使用される暗号化キー、ドキュメントのポリシー内で別途定義されるアクセス制限を含んでいます。 使用ライセンスの有効期間が切れた場合に、そのファイルまたは電子メール メッセージを開くには、Azure Rights Management サービスに再度、ユーザーの資格情報を送信する必要があります。 

ファイルを取り消すと、そのアクションは、Azure Rights Management サービスにユーザーを認証する場合にのみ適用できます。 そのため、ファイルに 30 日間の使用ライセンス有効期間があり、ユーザーが既にそのドキュメントを開いている場合、ユーザーは引き続きその使用ライセンスの期間中はドキュメントにアクセスすることができます。 使用ライセンスの期限が切れた後は、ドキュメントが取り消されているため、ユーザーのアクセスが拒否される時点で、ユーザーの再認証が必要になります。

テナントの使用ライセンス有効期間の既定値は 30 日間であり、この値は PowerShell のコマンドレット [Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx) を使用することで構成できます。 この設定は、カスタム テンプレートでより制限の厳しい設定によって上書きできます。 

テナント設定およびテンプレート設定は、ユーザーが RMS 共有アプリケーションを使用して、オプション **[これらのドキュメントへのアクセスをすぐに取り消せるようにする]** を選択すると上書きできます。 この設定により、実際には使用ライセンスの有効期間が 0 に設定されます。 

使用ライセンスのしくみの情報および例については、[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx) の詳細な説明を参照してください。

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management は画面キャプチャを防止できますか。
Windows プラットフォーム (Windows 7、Windows 8.1、Windows 10、Windows Phone) および Android で広く使われているさまざまな画面キャプチャ ツールについては、**コピー**の[使用権限](../deploy-use/configure-usage-rights.md)を付与しなければ、Rights Management で画面キャプチャを防止できます。 これに対して、iOS や Mac のデバイスでは、画面キャプチャを禁止するアプリが認められていません。また、(Outlook Web App や Office Online を使用しているなどの場合に) ブラウザーでの画面キャプチャを禁止することも不可能です。

画面のキャプチャを禁止しておくと、不注意や不測の出来事により機密性の高い情報が漏洩してしまう事態を避けることができます。 ただし、画面に表示されるデータをユーザーが共有するにはさまざまな方法があり、スクリーン ショットを保存する方法はその 1 つにすぎません。 たとえば、表示される情報を共有しようとするユーザーは、カメラ付き携帯電話を使用して写真を撮影したり、データを再入力したり、単に口頭で他者に伝達することができます。

このように、あらゆるプラットフォームとソフトウェアが Rights Management API をサポートしており、かつ画面キャプチャをブロックできたとしても、テクノロジだけでデータの漏洩を防ぐことができるわけではありません。 Rights Management は、承認および使用ポリシーを使用して重要なデータを保護するのに役立つものの、このエンタープライズ権限管理ソリューションは、他の管理手段と共に使用する必要があります。 たとえば、物理的なセキュリティを実装したり、組織のデータへのアクセスが承認されているユーザーを慎重に検査および監視したり、共有してはならないデータを理解できるようにユーザーの教育に投資したりすることです。

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>電子メールをユーザー保護する方法として、[転送不可] と転送権限のないテンプレートにはどのような違いがありますか。

名前や外観に反して、**[転送不可]** は転送権限の反対ではなく、テンプレートでもありません。 実際には、コピー、印刷、添付ファイルの保存の制限を含む権限の集まりであり、それらに加え、電子メールの転送が制限されます。 権限は、選択した受信者に基づき、ユーザーに動的に適用されます。管理者によって静的に割り当てられるものではありません。 詳細については、「[Azure Rights Management の使用権限を構成する](../deploy-use/configure-usage-rights.md)」の「[電子メールの [転送不可] オプション](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails)」セクションを参照してください。






<!--HONumber=Nov16_HO3-->


