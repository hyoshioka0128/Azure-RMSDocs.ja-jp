---
title: "Azure Rights Management に関してよく寄せられる質問 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b73c83b91a6b00e44ff6c8fe7f8e954bd9713e34
ms.openlocfilehash: a3ed9e8de496741fae8904481edb1177762a12c0


---

# Azure Rights Management に関してよく寄せられる質問

*適用対象: Azure Rights Management、Office 365*

Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) に関してよく寄せられる質問をいくつか紹介します。

## Azure RMS のデプロイの要件と、デプロイを開始する方法について教えてください。
最初に「[Azure Rights Management の要件](requirements-azure-rms.md)」を確認してください。使用可能なクラウド サブスクリプション、オンプレミス サーバーで Azure RMS を使用する方法、現時点でサポートされていないデプロイ シナリオ、Azure RMS をサポートするデバイスとアプリケーションについての情報と、ファイアウォールまたはプロキシ サーバーの IP アドレスとドメイン名の一覧へのリンクが記載されています。 

また、この「**作業の開始**」セクションに含まれる他の記事および「**理解と調査**」セクションを確認すると、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] による組織のデータ保護とアプリケーション連携のしくみや、オンプレミス バージョンの Active Directory Rights Management との比較結果について基本的な知識を得ることができ、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] に固有の用語と略語について理解することができます。

その後については、「[Azure Rights Management のデプロイ ロードマップ](../plan-design/deployment-roadmap.md)」を参照してください。

## ファイルを Azure RMS で保護するには、クラウドに置いておく必要があるのでしょうか?
よくある誤解ですが、そのようなことはありません。 Azure Rights Management サービス (および Microsoft) では、情報保護の一環としてユーザーのデータを閲覧したり、保存したりすることはありません。 ユーザーが保護した情報は、ユーザーが Azure に明示的に保存したり、Azure に情報を保存する別のクラウド サービスを使用しない限り、Azure に送信されたり保存されたりすることはありません。 

詳細については、「[Azure RMS の機能の詳細](../understand-explore/how-does-it-work.md)」を参照してください。(コーラのレシピのように) オンプレミスで作成および保管している機密性の高いデータを Azure RMS で保護しながら、引き続きオンプレミスに置いておくことができるしくみについて説明しています。

## Azure RMS はオンプレミス サーバーと統合できますか。
はい。 Azure RMS は、Exchange Server、SharePoint、Windows ファイル サーバーなどのオンプレミス サーバーと統合できます。 統合するには、[Rights Management コネクタ](../deploy-use/deploy-rms-connector.md)を使用します。 または、Windows Server でファイル分類インフラストラクチャ (FCI) を使用することのみを目的とされている場合は、[RMS 保護コマンドレット](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx)を使用できます。 また、Active Directory ドメイン コントローラーを Azure AD と同期し、連携することで、たとえば [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)を使用して、よりシームレスな認証方法をユーザーに提供できます。

必要に応じて、Azure RMS で XrML 証明書の生成と管理が自動的に行われるので、オンプレミスの PKI は使用されません。 Azure RMS での証明書の使用方法については、記事「[Azure RMS の機能の詳細](../understand-explore/how-does-it-work.md)」の「[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」セクションを参照してください。

## Azure RMS と統合するサード パーティのソリューションに関する情報はどこで入手できますか?

既に多くのソフトウェア ベンダーが、Azure RMS と統合するソリューションを持っているか、またはそのソリューションを実装しており、リストは急増し続けています。 [Enterprise Mobility and Security のブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)に役立つ情報が掲載されています。また Twitter の [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) からも最新の情報が入手できます。 なお、具体的なご質問は、Information Protection チーム (askipteam@microsoft.com) までメールでメッセージをお送りください。

## RMS コネクタには管理パックまたは同様の監視メカニズムがありますか?

Rights Management コネクタは情報、警告、およびエラー メッセージをイベント ログに記録しますが、これらのイベントの監視機能を備えた管理パックはありません。 ただし、イベントの一覧とその説明および修正の実施に役立つ詳細な情報については、「[Azure Rights Management コネクタを監視する](../deploy-use/monitor-rms-connector.md)」を参照してください。

## Azure RMS を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?

Office 365 テナントまたは Azure AD テナントのグローバル管理者は、Azure RMS のすべての管理タスクを実行できます。 ただし、他のユーザーに管理者権限を割り当てる場合は、Azure RMS の PowerShell コマンドレット [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) を使用して行うことができます。 この管理ロールは、ユーザー アカウントまたはグループごとに割り当てることができます。 使用できるロールは、**グローバル管理者**と**コネクタ管理者**の 2 つです。 

ロールの名前からわかるように、1 番目のロールは Azure Rights Management のすべての管理タスクを実行する権限を付与します (他のクラウド サービスのグローバル管理者には付与しません)、2 番目のロールは Rights Management (RMS) コネクタのみを実行する権限を付与します。

注意事項:

- Office 365 のグローバル管理者と Azure AD のグローバル管理者のみが、管理ポータル (Office 365 管理センターまたは Azure クラシック ポータル) を使用して Azure RMS を構成できます。 Azure RMS のグローバル管理者ロールを割り当てられたユーザーは、Azure RMS の PowerShell コマンドを使用して Azure RMS を構成する必要があります。 特定のタスクを実行する正しいコマンドレットについては、「[Windows PowerShell を使用した Azure Rights Management の管理](../deploy-use/administer-powershell.md)」を参照してください。

- [オンボーディング コントロール](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成してある場合は、RMS コネクタを除き、Azure RMS を管理する機能に影響はありません。 たとえば、コンテンツを保護する機能を "IT department" グループに制限するようにオンボーディング コントロールが構成されている場合、RMS コネクタのインストールと構成に使用するアカウントは、そのグループのメンバーである必要があります。 

- Azure RMS の管理者 (テナントのグローバル管理者または Azure RMS のグローバル管理者) は、Azure RMS によって保護されていたドキュメントまたは電子メールから保護を自動的に削除することはできません。 Azure RMS のスーパー ユーザーを割り当てられたユーザーだけが、スーパー ユーザー機能が有効になっているときにのみ、これを行うことができます。 ただし、テナントのグローバル管理者および Azure RMS のグローバル管理者は、ユーザーをスーパー ユーザーとして割り当てることができます (これには自分自身のアカウントも含まれます)。 また、スーパー ユーザー機能を有効にすることもできます。 これらのアクションは、Azure RMS の管理者ログに記録されます。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」のセキュリティのベスト プラクティスに関するセクションを参照してください。 


## 一部のユーザーが Exchange Online 上の Exchange に、他のユーザーが Exchange Server 上の Exchange に登録されているハイブリッド デプロイメント構成です。この構成は、Azure RMS でサポートされていますか。
はい、サポートされています。また、2 つの Exchange デプロイメント間でシームレスに電子メールと添付ファイルを保護し、保護された電子メールと添付ファイルを使用できるようになることがメリットです。 この構成の場合、[Azure RMS をアクティブ化し](../deploy-use/activate-service.md)、[IRM for Exchange Online を有効にして](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)、[RMS コネクタをデプロイして](../deploy-use/deploy-rms-connector.md) Exchange Server 用に構成します。

## Exchange Online で Azure RMS を使うための構成について詳しい手順を説明した資料はありますか?

はい。 「[Exchange Online: IRM 構成](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」を参照すると、Exchange Online で Azure RMS の使用を開始するにあたってよく使われるコマンド、Outlook Web App で **[権限の設定]** メニューのオプションがすぐに表示されない理由、Azure RMS テンプレートを変更または更新した場合に実行が必要なコマンドを確認できます。 

## 運用環境に Azure RMS をデプロイすると、会社の環境が Azure RMS に固定されたり、Azure RMS で保護したコンテンツにアクセスできなくなる危険性が生じたりしますか。
いいえ。データを常に制御することができます。また、たとえ Azure RMS の使用を停止したとしても、継続してデータにアクセスすることができます。 詳細については、「[Azure Rights Management の使用停止と非アクティブ化](../deploy-use/decommission-deactivate.md)」を参照してください。

ただし、Azure RMS のデプロイメントを停止される前に、お客様が使用を停止する理由を伺う機会をいただいています。 Azure RMS がビジネス要件を満たしていない場合は、近い将来に新機能が計画されているか、代替案がないかをお問い合わせください。 お問い合わせの電子メールは [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) に送信してください。技術とビジネスの要件について説明いたします。

## Azure RMS を使用してコンテンツを保護するユーザーを制御できますか。
はい。Azure RMS には、このシナリオ用のユーザーのオンボーディング コントロールがあります。 詳細については、記事「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」の「[段階的デプロイのオンボーディング コントロールの構成](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)」のセクションを参照してください。

## ユーザーが、保護されたドキュメントを特定の組織と共有しないようにすることはできますか。
Azure RMS の最大の利点の 1 つは、Azure AD が認証を自動的に処理するため、各パートナー組織に対して明示的な信頼を構成することなく、企業間のコラボレーションをサポートできることです。

ユーザーが特定の組織とのドキュメントの安全な共有を防止するような管理オプションはありません。 たとえば、信頼していない組織や、競合先の組織をブロックするとします。 Azure RMS がこれらの組織のユーザーに保護されたドキュメントを送信しないようにしても意味がありません。その場合、ユーザーはドキュメントを保護されていないまま共有することになり、おそらくこれはこのシナリオにおいて最も望ましくない状況です。 たとえば、これらの組織のユーザーと社外秘ドキュメントを共有しているユーザーを識別することはできませんが、ドキュメント (または電子メール) が Azure RMS で保護されていれば、これが可能になります。

## 保護されたドキュメントを社外のユーザーと共有する場合、そのユーザーはどのようにして認証されますか。
Azure RMS は、常にユーザー認証に Azure Active Directory アカウントと関連付けられた電子メール アドレスを使用します。これは、管理者にとって企業間のコラボレーションをシームレスにします。 他の組織で Azure サービスを使用する場合は、アカウントがオンプレミスで作成、管理されてから Azure に同期される場合でも、ユーザーは既に Azure Active Directory にアカウントを持っています。 組織が内部的に Office 365 を所有している場合、このサービスはユーザー アカウント用に Azure Active Directory も使用します。 ユーザーの組織が Azure に管理アカウントを持っていない場合、ユーザーは[個人向け RMS](../understand-explore/rms-for-individuals.md) にサインアップできます。これは、管理されていない Azure テナントと組織用のディレクトリをユーザー用のアカウントを使用して作成するため、このユーザー (およびそれ以降のユーザー) は Azure RMS に対して認証されます。

このようなアカウントの認証方法は、他の組織の管理者が Azure Active Directory アカウントを構成している方法によって異なります。 たとえば、これらのアカウント用に作成されたパスワード、多要素認証 (MFA)、フェデレーション、Active Directory ドメイン サービスで作成されたパスワードを使用してから、Azure Active Directory に同期される場合があります。

## 社外のユーザーをカスタム テンプレートに追加できますか。
はい。 エンドユーザー (と管理者) がアプリケーションから選択できるカスタム テンプレートを作成すると、指定した定義済みのポリシーを使用して、すばやく簡単に情報保護を適用できます。 テンプレートの設定の 1 つに、コンテンツにアクセス可能なユーザーの設定があります。組織内のグループとユーザー、および組織外のユーザーを指定できます。

組織外のユーザーを指定するには、テンプレートを構成するとき、Azure クラシック ポータルで選択したグループに連絡先として追加します。 あるいは、[Azure Rights Management 用 Windows PowerShell モジュール](../deploy-use/install-powershell.md)を使用します。

-   **権限定義オブジェクトを使用してテンプレートを作成または更新する**。    権限定義オブジェクトで外部電子メール アドレスおよびその権限を指定し、これを使用してテンプレートを作成または更新します。 [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) コマンドレットを使用して権限定義オブジェクト指定し、変数を作成してから、[Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) コマンドレット (新しいテンプレート用) または [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) コマンドレット (既存のテンプレートを変更する場合) を使用して、この変数を -RightsDefinition パラメーターに指定します。 ただし、これらのユーザーを既存のテンプレートに追加する場合は、外部ユーザーだけでなく、テンプレートに既存のグループの権限定義オブジェクトを定義する必要があります。

カスタム テンプレートの詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

## Azure RMS で Azure AD の動的なグループを使用できますか。
Azure AD Premium の機能では、[属性ベースのルール](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/)を指定することによってグループの動的メンバーシップを構成できます。 Azure AD でセキュリティ グループを作成する場合、このグループの種類では動的メンバーシップがサポートされますが、電子メール アドレスはサポートされないため、Azure RMS で使用することはできません。 ただし、動的メンバーシップをサポートし、メールが有効な新しいグループの種類を Azure AD で作成できるようになりました。 Azure クラシック ポータルで新しいグループを追加する場合は、**グループの種類**として **Office 365 の "プレビュー"** を選択できます。 このグループではメールが有効なため、Azure RMS で使用できます。

オプション名が明確に表示されているため、この新しいグループの種類は、必要な追加機能および使用する新しいドキュメントと共にプレビュー段階のままです。 その間に、Azure RMS でこの新しいグループの種類を使用できることを確認する必要があります。


## Azure RMS でサポートされているデバイスとファイルの種類を教えてください。
サポートされるデバイスの一覧については、「[Azure RMS の要件: Azure RMS をサポートするクライアント デバイス](../get-started/requirements-client-devices.md)」を参照してください。 サポートされるデバイスによっては一部の RMS 機能がサポートされていないため、「[Azure RMS の要件: アプリケーション](../get-started/requirements-applications.md)」の表も確認してください。

Azure RMS はすべてのファイルの種類をサポートできます。 テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、他のいくつかのアプリケーションのファイルの種類については、Azure RMS は暗号化と権限の適用 (アクセス許可) の両方を含むネイティブな保護を提供します。 他のすべてのアプリケーションとファイルの種類については、ファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証という一般的な保護機能が提供されます。

Azure RMS でネイティブでサポートされるファイル名拡張子の一覧については、「[Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)」の「[サポートされているファイルの種類とファイル名拡張子](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)」セクションを参照してください。 一覧に含まれないファイル名拡張子は、一般保護をこれらのファイルに自動的に適用する RMS 共有アプリケーションを使用することによってサポートされます。

## RMS で保護されている Office ドキュメントを開いた場合、関連付けられた一時ファイルも RMS で保護されたものになりますか。

いいえ。 このシナリオでは、関連付けられている一時ファイルには元のドキュメントのデータは含まれず、ユーザーがファイルを開いているときに入力したもののみが含まれます。 元のファイルとは異なり、一時ファイルは明らかに共有用に設計されておらず、BitLocker や EFS などのローカル セキュリティ コントロールによって保護されデバイス上に残ります。

## AD RMS からの移行はいつサポートされますか。
当初、Azure RMS は AD RMS などの Rights Management のオンプレミス デプロイからの移行をサポートしていませんでした。 ただし、現在ではサポートしています。

詳細については、「[AD RMS から Azure Rights Management への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

## BYOK と Azure RMS を併用したいのですが、BYOK は Exchange Online と互換性がないと知りました。何かアドバイスはありますか。
現在のこの制限で、Azure RMS のデプロイメントを延期しないでください。 Exchange Online をお持ちで、Bring Your Own Key (BYOK) を使用する場合は、当面 Azure RMS を既定のキー管理モード (キーの生成と管理を Microsoft で行う) でデプロイすることをお勧めします。 この方法を採用すると、重要なファイルと電子メールを保護する機能をすぐに活用し、後で (たとえば Exchange Online が BYOK をサポートするようになったときなどに) BYOK に移行することができます。

ただし、会社のポリシーでハードウェア セキュリティ モジュール (HSM) を使用する必要があり、そのために Azure RMS をデプロイできない場合は、Azure RMS をデプロイし、Exchange の RMS 機能を減らして BYOK を併用する方法があります。 詳細については、「[Azure Rights Management テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」の「[BYOK の料金と制限事項](../plan-design/byok-price-restrictions.md)」を参照してください。

## 必要な機能があるのですが、SharePoint で保護されたライブラリには使用できないようです。この機能のサポートは予定されていますか。
現在のところ、SharePoint は、IRM で保護されたライブラリを使用して、RMS で保護されたドキュメントをサポートしています。IRM で保護されたライブラリは、カスタム テンプレート、ドキュメントの追跡などの機能をサポートしていません。 詳細については、記事「[Office applications and services (Office アプリケーションとサービス)](../understand-explore/office-apps-services-support.md)」の「[SharePoint Online and SharePoint Server (SharePoint Online と SharePoint Server)](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server)」セクションを参照してください。

まだサポートされていない機能に関する情報については、[Enterprise Mobility and Security チーム ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)のお知らせに注意してください。

## ユーザーが社内や社外の人間とファイルを安全に共有できるように SharePoint Online で OneDrive for Business を構成するには、どうすればよいですか。
既定では、Office 365 管理者は構成しません。ユーザーが構成します。

SharePoint サイト管理者が、所有する SharePoint ライブラリの IRM を有効にして構成するのと同じように、OneDrive for Business は、ユーザーが自身の OneDrive for Business ライブラリの IRM を有効にして構成するように設計されています。  ただし、PowerShell を使用して、ユーザーに代わってこの処理を行うことができます。 手順については、記事「[Office 365: クライアントとオンライン サービスの構成](../deploy-use/configure-office365.md)」の「[SharePoint Online と OneDrive for Business:IRM 構成](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)」セクションを参照してください。

## RMS を正常にデプロイするためのヒントやコツがあれば教えてください。
これまでに多数のデプロイをサポートし、顧客、パートナー、コンサルタント、サポート エンジニアから話を聞いてきた経験から言える一番のヒントは、**シンプルな権限ポリシーを設計してデプロイすること**です。

Azure RMS では、他のユーザーと情報を安全に共有できるため、情報保護の範囲を詳細に指定することができます。 しかし、権限ポリシーはできるだけシンプルにしてください。 多くの組織にとって、Azure RMS の導入による業務上最も重要な利点は、既定の権限ポリシー テンプレートを適用して組織内のユーザーのアクセス許可を制限し、データ漏えいを防止できることです。 もちろん、印刷や編集などの操作を制限する必要があれば、より詳細なポリシーを作成することもできます。ただし、そのような細かい制限は、高レベルのセキュリティが必要なドキュメントに限定してください。最初から制限の厳しいポリシーを作成するのではなく、段階的に計画して作成していくことをお勧めします。

## Azure RMS の各サブスクリプションで使用できる機能と使用できない機能を教えてください。
Azure RMS (Office 365、Azure RMS Premium、および Enterprise Mobility Suite) をサポートする有料サブスクリプションの場合、サポートされる RMS 機能の一部に違いがあります。 機能の一覧については、「 [Rights Management サービス (RMS) オファリングの比較](http://technet.microsoft.com/dn858608)」を参照してください。

Azure RMS (個人用の RMS) をサポートする無料サブスクリプションは、Azure RMS で保護されているコンテンツの使用をサポートしています。 詳細については、「[個人用 RMS と Azure Rights Management](../understand-explore/rms-for-individuals.md)」を参照してください。

## 無料の Azure RMS サブスクリプション (個人用 RMS) に関する技術情報 (たとえば、そのしくみ、アカウントを制御する方法、使用できないドメイン) はどこで入手できますか。
これらの質問に対する回答については、「[個人用 RMS と Azure Rights Management](../understand-explore/rms-for-individuals.md)」および関連する記事を参照してください。

## 退職した従業員が保護していたファイルにアクセスするには、どうすればよいですか。
Azure RMS のスーパー ユーザー機能を使用してください。スーパー ユーザー権限を持つユーザーは、組織の RMS テナントから付与されたすべての使用ライセンスについて、完全な所有者権限を持ちます。 また必要に応じて、スーパー ユーザー機能を使用すると、権限を持つサービスのインデックス化とファイルの検証を行うことができます。

詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」を参照してください。

## Rights Management は画面キャプチャを防止できますか。
Windows プラットフォーム (Windows 7、Windows 8.1、Windows 10、Windows Phone) および Android で広く使われているさまざまな画面キャプチャ ツールについては、**コピー**の[使用権限](../deploy-use/configure-usage-rights.md)を付与しなければ、Rights Management で画面キャプチャを防止できます。 これに対して、iOS や Mac のデバイスでは、画面キャプチャを禁止するアプリが認められていません。また、(Outlook Web App や Office Online を使用しているなどの場合に) ブラウザーでの画面キャプチャを禁止することも不可能です。

画面のキャプチャを禁止しておくと、不注意や不測の出来事により機密性の高い情報が漏洩してしまう事態を避けることができます。 ただし、画面に表示されるデータをユーザーが共有するにはさまざまな方法があり、スクリーン ショットを保存する方法はその 1 つにすぎません。 たとえば、表示される情報を共有しようとするユーザーは、カメラ付き携帯電話を使用して写真を撮影したり、データを再入力したり、単に口頭で他者に伝達することができます。

このように、あらゆるプラットフォームとソフトウェアが Rights Management API をサポートしており、かつ画面キャプチャをブロックできたとしても、テクノロジだけでデータの漏洩を防ぐことができるわけではありません。 Rights Management は、承認および使用ポリシーを使用して重要なデータを保護するのに役立つものの、このエンタープライズ権限管理ソリューションは、他の管理手段と共に使用する必要があります。 たとえば、物理的なセキュリティを実装したり、組織のデータへのアクセスが承認されているユーザーを慎重に検査および監視したり、共有してはならないデータを理解できるようにユーザーの教育に投資したりすることです。

## 電子メールをユーザー保護する方法として、[転送不可] と転送権限のないテンプレートにはどのような違いがありますか。

名前や外観に反して、**[転送不可]** は転送権限の反対ではなく、テンプレートでもありません。 実際には、コピー、印刷、添付ファイルの保存の制限を含む権限の集まりであり、それらに加え、電子メールの転送が制限されます。 権限は、選択した受信者に基づき、ユーザーに動的に適用されます。管理者によって静的に割り当てられるものではありません。 詳細については、「[Azure Rights Management の使用権限を構成する](../deploy-use/configure-usage-rights.md)」の「[電子メールの [転送不可] オプション](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails)」セクションを参照してください。

## 法律、法令遵守、SLA など、Azure RMS に関するサポート情報はどこで入手できますか。
Azure RMS は他のサービスをサポートし、また、他のサービスに依存しています。 Azure RMS サービスの使用方法以外で、Azure RMS の関連情報をお探しの場合は、以下のリソースを参照してください。

**法律およびプライバシー:**

-   Microsoft Azure の契約情報について: [Microsoft Azure の契約](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Microsoft Azure のプライバシー情報について: [Microsoft Azure のプライバシーに関する声明](http://azure.microsoft.com/support/legal/privacy-statement/)

**セキュリティ、コンプライアンス、監査:**

記事「[Azure RMS が解決する問題の種類](../understand-explore/azure-rms-problems-it-solves.md)」の「[セキュリティ、コンプライアンス、および規制の要件](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements)」のセクションを参照してください。 さらに

-   Azure RMS の外部認証について: [Microsoft Azure セキュリティ センター](http://azure.microsoft.com/support/trust-center/)

-   FIPS 140 について: [FIPS 140 検証](https://technet.microsoft.com/library/security/cc750357.aspx)

**サービス レベル アグリーメント:**

-   主なリージョンごとの Azure RMS のサービス レベル アグリーメント: [製品ライセンスの検索ページからダウンロード](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

    - たとえば、北米向けの 2016 年 3 月のサービス レベル アグリーメントをダウンロードするには、**[OnlineSvcsConsolidatedSLA(WW)(English)(March2016)]** をクリックします。

-   Azure Active Directory のサービス レベル アグリーメント: [サービス レベル アグリーメント](http://azure.microsoft.com/support/legal/sla/)

**ドキュメント:**

-   Azure Active Directory のドキュメント サイト: [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Azure Active Directory ライブラリ: [Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx)

-   Office 365 ライブラリ: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## 新しいリリースが Azure RMS ですぐに利用できるようになると聞きました。いつリリースされますか?

技術文書には今後のリリースに関する情報は含まれません。 この種の情報およびリリースの通知については、[Enterprise Mobility and Security のブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)を参照し、Twitter の [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) から最新の情報を入手してください。 Office のリリースにご興味がある場合は、[Office ブログ](https://blogs.office.com/)も確認してください。

## 質問がここに含まれていない場合は、どうすればよいですか
「[Azure Rights Management の情報とサポート](information-support.md)」に一覧表示されているリンクとリソースを使用します。

さらに、FAQ がエンドユーザー向けに用意されています。

-   [Windows 用 Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn467883)

-   [モバイル プラットフォームと Mac プラットフォームのための Rights Management 共有アプリケーションの FAQ](https://technet.microsoft.com/dn451248)

-   [ドキュメント追跡の FAQ](http://go.microsoft.com/fwlink/?LinkId=523977)

この FAQ ページは定期的に更新されます。新しい情報は [Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)上の月次のドキュメント更新発表に一覧表示されます。





<!--HONumber=Jul16_HO1-->


