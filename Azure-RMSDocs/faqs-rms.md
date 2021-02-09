---
title: Azure RMS に関してよく寄せられる質問 - AIP
description: Azure Information Protection のデータ保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問の一部。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 31202876b035f7b5266abd006cfcd943e8eb6690
ms.sourcegitcommit: ee20112ada09165b185d9c0c9e7f1179fc39e7cf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/21/2021
ms.locfileid: "98659019"
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Azure Information Protection のデータ保護に関してよく寄せられる質問

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)です。 詳細については、「 [クラシッククライアントの faq](faqs-classic.md)」も参照してください。 *

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure Portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection のデータ保護サービス、Azure Rights Management に関して質問がありますか。 ここで回答を探してみてください。

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>ファイルを Azure Rights Management で保護するには、クラウドに置いておく必要があるのでしょうか。

よくある誤解ですが、そのようなことはありません。 Azure Rights Management サービス (と Microsoft) では、情報保護の一環としてユーザーのデータを閲覧したり、保存したりすることはありません。 ユーザーが保護した情報は、ユーザーが Azure に明示的に保存したり、Azure に情報を保存する別のクラウド サービスを使用しない限り、Azure に送信されたり保存されたりすることはありません。

詳細については、「Azure RMS のしくみ」を参照してください [。内部](./how-does-it-work.md) 設置型で格納され、オンプレミスに格納されている secret cola 式が Azure Rights Management サービスによって保護されていても、オンプレミスのままになっていることを理解するためのものです。

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>他の Microsoft クラウドサービスでの Azure Rights Management の暗号化と暗号化の違いは何ですか。

Microsoft はさまざまなシナリオでのデータ保護に合わせて多数の暗号化技術を提供していますが、多くの場合はデータ保護のシナリオが相互補完的です。 たとえば、Microsoft 365 に格納されているデータの保存データの暗号化は、Microsoft 365 によって提供されますが、Azure Information Protection の Azure Rights Management サービスはデータを独立して暗号化し、そのデータがどこに置かれているかまたは送信方法に関係なく保護されるようにします。

これらの暗号化技術は互いに補完するものであり、使用するには各技術を個別に有効にして構成する必要があります。 このときに、暗号化のキーを独自に用意するという選択が可能な場合があり、このようなシナリオは "BYOK" (Bring Your Own Key) とも呼ばれます。 暗号化技術の 1 つについて BYOK を有効にしても、それ以外の技術に影響することはありません。 たとえば、BYOK を Azure Information Protection に使用し、それ以外の暗号化技術には使用しないことも、その逆も可能です。 使用されるキーが暗号化技術ごとに異なるか同一であるかは、管理者が各サービスの暗号化オプションをどのように構成するかによって決まります。

## <a name="can-i-now-use-byok-with-exchange-online"></a>現在、Exchange Online で BYOK を使用できますか。

はい。 [Azure Information Protection の上に構築された新しい Microsoft 365 メッセージの暗号化機能のセットアップ](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)に関するページの手順に従って、Exchange ONLINE で byok を使用できるようになりました。 これらの手順に従うことで、新しい Office 365 Message Encryption と、Azure Information Protection での BYOK の使用をサポートする Exchange Online の新しい機能を使用できるようになります。

この変更の詳細については、[Office 365 Message Encryption と新しい機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)に関するブログのお知らせを参照してください。

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>Azure RMS と統合するサード パーティのソリューションに関する情報はどこで入手できますか。

既に多くのソフトウェア ベンダーが、Azure Rights Management と統合するソリューションを持っているか、そのソリューションを実装中であり、そのようなベンダーが増え続けています。 [対応アプリケーション](requirements-applications.md#)の一覧を確認し、Twitter の[Microsoft Mobility@MSFTMobility ](https://twitter.com/MSFTMobility)から最新の更新プログラムを入手すると便利な場合があります。 Azure Information Protection [Yammer サイト](https://www.yammer.com/AskIPTeam)では、特定の統合に関する質問を投稿できます。

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>RMS コネクタには管理パックまたは同様の監視メカニズムがありますか。

Rights Management コネクタは、情報、警告、およびエラーメッセージをイベントログに記録しますが、これらのイベントの監視を含む管理パックはありません。 イベントとその説明の一覧および対処に役立つ詳細な情報については、「[Azure Rights Management コネクタを監視する](monitor-rms-connector.md)」を参照してください。

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>Azure Portal では、新しいカスタム テンプレートをどのように作成しますか。

カスタム テンプレートは、Azure Portal に移動しています。Azure Portal では、引き続きカスタム テンプレートをテンプレートとして管理したり、ラベルに変換したりすることができます。 新しいテンプレートを作成するには、新しいラベルを作成し、Azure RMS 用のデータ保護設定を構成します。 それによって、内部的には新しいテンプレートが作成され、Rights Management テンプレートと統合されるサービスとアプリケーションがアクセスできるようになります。

Azure Portal のテンプレートの詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

## <a name="ive-protected-a-document-and-now-want-to-change-the-usage-rights-or-add-usersdo-i-need-to-reprotect-the-document"></a>保護されているドキュメントに対して、使用権限の変更またはユーザーの追加を行いたいのですが、ドキュメントを再保護する必要がありますか。

ドキュメントがラベルまたはテンプレートを使用して保護されている場合、ドキュメントを再保護する必要はありません。 使用権限に変更を加えるか、新しいグループ (またはユーザー) を追加することによって、ラベルまたはテンプレートを変更した後、変更内容を保存します。

- 変更する前にユーザーがドキュメントにアクセスしていない場合、ユーザーがドキュメントを開くとすぐに変更が有効になります。

- ユーザーが既にドキュメントにアクセスしている場合は、ユーザーの[使用ライセンス](configure-usage-rights.md#rights-management-use-license)の有効期限が過ぎた時点で変更が有効になります。 使用ライセンスの有効期限が切れるまで待てない場合にのみ、ドキュメントを再保護します。 再保護を行うと、実際にはドキュメントの新しいバージョンが作成されるため、ユーザーの使用ライセンスも新しくなります。

あるいは、必要なアクセス許可に対して既にグループを構成している場合、グループのメンバーシップを変更してユーザーの追加または除外を行うことができます。ラベルまたはテンプレートの変更は必要ありません。 グループ メンバーシップが Azure Rights Management サービスによって[キャッシュ](prepare.md#group-membership-caching-by-azure-information-protection)に入れられるため、変更が反映されるまでにわずかな遅延が生じる可能性があります。

カスタム アクセス許可を使用してドキュメントが保護されている場合は、既存のドキュメントのアクセス許可を変更できません。 ドキュメントを再度保護し、この新しいバージョンのドキュメントに必要なすべてのユーザーとすべての使用権限を指定する必要があります。 保護されたドキュメントを再保護するには、"フル コントロール" 使用権限が必要です。

ヒント: ドキュメントがテンプレートで保護されているのか、カスタム アクセス許可を使用して保護されているのかを確認するには、[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell コマンドレットを使用します。 カスタム アクセス許可の場合、**[制限されたアクセス]** のテンプレートの説明と、[Get-RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate) を実行した場合には表示されない一意のテンプレート ID が常に表示されます。

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>一部のユーザーは Exchange Online に登録され、他のユーザーは Exchange Server に登録されている、Exchange のハイブリッド デプロイ構成は、Azure RMS でサポートされていますか。
はい、サポートされています。また、2 つの Exchange デプロイメント間でシームレスに電子メールと添付ファイルを保護し、保護された電子メールと添付ファイルを使用できることがメリットです。 この構成の場合、[Azure RMS をアクティブ](activate-service.md)にし、[IRM for Exchange Online を有効](/microsoft-365/enterprise/activate-rms-in-microsoft-365)にします。次に、[RMS コネクタをデプロイ](deploy-rms-connector.md)して、Exchange Server 用に構成します。

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>運用環境にこの保護を利用すると、会社の環境が Azure RMS に固定されたり、Azure RMS で保護したコンテンツにアクセスできなくなる危険性が生じたりしますか。
いいえ。データを常に制御することができます。また、Azure Rights Management サービスの使用を停止したとしても、継続してデータにアクセスすることができます。 詳細については、「 [Azure Rights Management の使用停止と非アクティブ](decommission-deactivate.md)化」を参照してください。

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>Azure RMS を使用してコンテンツを保護するユーザーを制御できますか。
はい。Azure Rights Management サービスには、このシナリオのためのユーザー オンボーディング コントロールがあります。 詳細については、「 [Azure Information Protection からの保護サービスのアクティブ化](activate-service.md)」の記事の「[段階的な展開のオンボードコントロールの構成](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>保護されたドキュメントをユーザーが特定の組織と共有しないようにすることはできますか。
データ保護に Azure Rights Management サービスを使用する最大の利点の 1 つは、Azure AD が認証を自動的に処理するため、各パートナー組織に対して明示的な信頼を構成することなく、企業間のコラボレーションをサポートできることです。

ユーザーが特定の組織とドキュメントを安全に共有することを防止するような管理オプションはありません。 たとえば、信頼されていない組織や、競合が発生している組織をブロックするとします。 Azure Rights Management サービスが保護されたドキュメントをこれらの組織のユーザーに送信できないようにすることは意味がありません。これは、ユーザーがドキュメントを保護されていない状態で共有するためです。このシナリオでは、おそらく最後に実行しようとしている可能性があります。 たとえば、社外秘ドキュメントを共有しているユーザーを特定することはできません。このような組織では、ドキュメント (または電子メール) が Azure Rights Management サービスによって保護されている場合に実行できます。

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>保護されたドキュメントを社外のユーザーと共有する場合、そのユーザーはどのようにして認証されますか。

既定では、Azure Rights Management サービスは、ユーザー認証に Azure Active Directory アカウントと関連付けられた電子メール アドレスを使用します。これにより、管理者にとって企業間のコラボレーションがシームレスになります。 他の組織で Azure サービスを使用する場合は、アカウントがオンプレミスで作成、管理されてから Azure に同期される場合でも、ユーザーは既に Azure Active Directory にアカウントを持っています。 組織に Microsoft 365 がある場合、このサービスでは、ユーザーアカウントに Azure Active Directory も使用します。 ユーザーの組織が Azure に管理アカウントを持っていない場合、ユーザーは個人用 [RMS](./rms-for-individuals.md)にサインアップできます。これにより、管理されていない azure テナントとそのユーザーのアカウントを持つ組織のディレクトリが作成され、そのユーザー (およびその後のユーザー) が azure Rights Management サービスに対して認証できるようになります。

このようなアカウントの認証方法は、他の組織の管理者が Azure Active Directory アカウントを構成している方法によって異なります。 たとえば、これらのアカウント用に作成したパスワード、フェデレーション、Active Directory Domain Services で作成した後 Azure Active Directory に同期したパスワードを使用できます。

その他の認証方法:

- Azure AD のアカウントを持っていないユーザー宛ての Office ドキュメントが添付されている電子メールを保護する場合、認証方法が異なります。 Azure Rights Management サービスは、Gmail など、いくつかの一般的なソーシャル ID プロバイダーと統合されます。 ユーザーの電子メール プロバイダーがサポートされている場合、ユーザーはそのサービスにサインインでき、電子メール プロバイダーによって認証が行われます。 ユーザーの電子メール プロバイダーがサポートされていない場合、または任意の設定として、ユーザーはワンタイム パスコードを申請できます。このパスコードでユーザーは認証を行い、保護されたドキュメントを含む電子メールを Web ブラウザーで表示することができます。

- Azure Information Protection では、サポートされているアプリケーションの Microsoft アカウントを使用できます。 現在、Microsoft アカウントが認証に使用されている場合、アプリケーションによっては、保護されたコンテンツを開けない場合があます。 [詳細情報](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>社外のユーザーをカスタム テンプレートに追加できますか。

はい。 Azure Portal で構成できる[保護設定](configure-policy-protection.md)では、組織の外部のユーザーとグループに (別組織の全ユーザーに対しても) アクセス許可を追加することができます。 これについては、必要に応じて「[Azure Information Protection を使用したセキュアなドキュメント コラボレーション](secure-collaboration-documents.md)」をご覧ください。 

Azure Information Protection ラベルがある場合は、最初にカスタム テンプレートをラベルに変換してから、Azure Potal でこれらの保護設定を構成する必要があります。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

または、PowerShell を使用して、カスタム テンプレート (およびラベル) に外部ユーザーを追加できます。 この構成には、テンプレートを更新するために使用する権限定義オブジェクトを使用する必要があります。

1. [AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)コマンドレットを使用して変数を作成することにより、権限定義オブジェクトで外部電子メールアドレスとその権限を指定します。

2. RightsDefinition パラメーターにこの変数を指定します。これには、 [Set AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) コマンドレットを使用します。

    ユーザーを既存のテンプレートに追加する場合、新しいユーザーだけでなく、テンプレート内の既存のユーザーにも、権限定義オブジェクトを定義する必要があります。 このシナリオでは、コマンドレットの「[例](/powershell/module/aipservice/set-aipservicetemplateproperty#examples)」セクションにある「**Example 3: Add new users and rights to a custom template (例 3: カスタム テンプレートへの新しいユーザーと権利の追加)**」が役に立ちます。

## <a name="what-type-of-groups-can-i-use-with-azure-rms"></a>Azure RMS では、どの種類のグループを使用できますか。
ほとんどのシナリオでは、電子メール アドレスを持つ、Azure AD の任意の種類のグループを使用できます。 この一般則は、使用権限を割り当てる際には常に適用できますが、Azure Rights Management サービスを管理する場合にはいくつかの例外があります。 詳細については、「[グループ アカウントに関する Azure Information Protection の要件](prepare.md#azure-information-protection-requirements-for-group-accounts)」を参照してください。

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>保護されたメールを Gmail または Hotmail のアカウントに送信するにはどうすればよいですか。

Exchange Online と Azure Rights Management サービスを使用する場合は、保護メッセージとしてユーザーに電子メールを送信するだけです。 たとえば、Outlook on the Web のコマンド バーにある新しい **[保護]** ボタンを選択するか、Outlook の **[転送不可]** ボタンまたはメニュー オプションを選択できます。 または、Azure Information Protection ラベルを選択して、自動的に転送不可を適用し、電子メールを分類することができます。

受信者には Gmail、Yahoo、または Microsoft アカウントにサインインするためのオプションが表示され、保護された電子メールを読むことができます。 また、ブラウザーで電子メールを読むためのワンタイム パスコードのオプションを選択することもできます。

このシナリオをサポートするには、Exchange Online を Azure Rights Management サービスおよび Office 365 Message Encryption の新しい機能で使用できるようにする必要があります。 この構成の詳細については、「[Exchange Online: IRM 構成](configure-office365.md#exchangeonline-irm-configuration)」を参照してください。

すべてのデバイスですべての電子メール アカウントをサポートする新機能の詳細については、ブログの投稿「[Announcing new capabilities available in Office 365 Message Encryption (Office 365 Message Encryption で使用できる新機能のお知らせ)](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)」を参照してください。

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Azure RMS では、どのデバイスとファイルの種類がサポートされていますか。

Azure Rights Management サービスをサポートしているデバイスの一覧については、「[Azure Rights Management データ保護をサポートするクライアント デバイス](./requirements.md#client-devices)」を参照してください。 サポートされているデバイスによっては、一部の Rights Management 機能が現在サポートされていないため、 [RMS 対応のアプリケーション](./requirements-applications.md)の表も確認してください。

Azure Rights Management サービスはあらゆる種類のファイルに対応しています。 テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、他のいくつかのアプリケーションのファイルの種類については、Azure Rights Management は暗号化と権限の適用 (アクセス許可) の両方を含むネイティブな保護を提供します。 他のすべてのアプリケーションとファイルの種類については、ファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証という一般的な保護機能が提供されます。

Azure Rights Management でネイティブでサポートされているファイル名拡張子の一覧については、「[Azure Information Protection クライアントでサポートされるファイルの種類](./rms-client/clientv2-admin-guide-file-types.md)」を参照してください。 一覧に含まれていないファイル名拡張子は、汎用的な保護をこれらのファイルに自動的に適用する Azure Information Protection クライアントを使用することによってサポートされます。

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>RMS で保護されている Office ドキュメントを開いた場合、関連付けられている一時ファイルも RMS で保護されますか。
いいえ。 このシナリオでは、関連付けられた一時ファイルには元のドキュメントのデータは含まれませんが、ファイルが開いている間はユーザーが入力したもののみが含まれます。 元のファイルとは異なり、一時ファイルは明らかに共有用に設計されておらず、BitLocker や EFS などのローカル セキュリティ コントロールによって保護され、デバイス上に残ります。

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>探している機能は、SharePoint で保護されたライブラリでは動作しないようです。機能のサポートは予定されていますか?
現在、Microsoft SharePoint では、IRM で保護されたライブラリを使用して、Rights Management テンプレート、ドキュメント追跡、およびその他の機能をサポートしていないドキュメントをサポートしています。 詳細については、「 [Office アプリケーションおよびサービス](./office-apps-services-support.md)」の「 [sharepoint の Microsoft 365 と sharepoint Server](./office-apps-services-support.md#sharepoint-in-microsoft-365-and-sharepoint-server) 」セクションを参照してください。

まだサポートされていない機能に関する情報については、[Enterprise Mobility and Security チーム ブログ](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-rights-management-services)のお知らせに注意していてください。

## <a name="how-do-i-configure-one-drive-in-sharepoint-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>SharePoint で1つのドライブを構成して、ユーザーが社内および社外のユーザーとファイルを安全に共有できるようにするには、操作方法ますか。
既定では、Microsoft 365 管理者として構成されていません。ユーザーが実行します。

SharePoint サイト管理者が所有する SharePoint ライブラリの IRM を有効にして構成するのと同じように、OneDrive は、ユーザーが自分の OneDrive ライブラリに対して IRM を有効にして構成するように設計されています。 ただし、PowerShell を使用して、ユーザーに代わってこの処理を行うことができます。 手順については、「 [Microsoft 365 の SharePoint と OneDrive: IRM の構成](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration)」を参照してください。

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>正常にデプロイするためのヒントやコツはありますか。

これまでに多数のデプロイをサポートし、顧客、パートナー、コンサルタント、サポート エンジニアから話を聞いてきた経験から言える一番のヒントは、**シンプルなポリシーを設計してデプロイすること** です。

Azure Information Protection では、他のユーザーと情報を安全に共有できるため、データ保護の範囲を詳細に指定することができます。 使用権限の制限の構成は慎重に行ってください。 多くの組織にとって、業務上最も重要な利点は、組織内のユーザーのアクセス許可を制限して、データ漏えいを防止できることです。 もちろん、印刷や編集などを防ぐ必要がある場合に比べて、はるかに詳細な情報を得ることができます。ただし、高レベルのセキュリティが本当に必要なドキュメントについては、例外としてより細かい制限を設け、1日に制限の厳しい使用権限を実装するのではなく、より段階的なアプローチを計画することをお勧めします。

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>退職した従業員が保護していたファイルにアクセスするには、どうすればよいですか。
[スーパー ユーザー機能](configure-super-users.md)を使用してください。この機能により、テナントで保護されているすべてのドキュメントと電子メールに対して承認されたユーザーにフル コントロール使用権限が与えられます。 スーパー ユーザーは常にこの保護されたコンテンツを読み取ることができ、必要に応じて、保護を解除したり、別のユーザーのために再度保護したりすることができます。 また必要であれば、スーパー ユーザー機能を使用して、権限を持つサービスによるファイルのインデックス化と検査を許可することができます。

コンテンツが SharePoint または OneDrive に保存されている場合、管理者は [SensitivityLabelEncryptedFile](/powershell/module/sharepoint-online/unlock-sposensitivitylabelencryptedfile) コマンドレットを実行して、秘密度ラベルと暗号化の両方を削除できます。 詳細については、[Microsoft 365 のドキュメント](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files#remove-encryption-for-a-labeled-document)を参照してください。

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management は画面キャプチャを防止できますか。
Windows プラットフォーム (Windows 7、Windows 8.1、Windows 10、Windows 10 Mobile) および Android で広く使われているさまざまな画面キャプチャ ツールについては、**コピーの** [使用権限](configure-usage-rights.md)を付与しなければ、Rights Management で画面キャプチャを防止できます。 ただし、iOS および Mac デバイスでは、いかなるアプリも画面キャプチャを防止することができません。 さらに、すべてのデバイス上のブラウザーは画面キャプチャを防止することができません。 ブラウザーでは、web 用に Outlook と Office を使用します。

画面のキャプチャを禁止しておくと、不注意や不測の出来事により機密性の高い情報が漏洩してしまう事態を避けることができます。 ただし、画面に表示されるデータをユーザーが共有する方法は多数あります。スクリーンショットを撮影する方法は、1つの方法にすぎません。 たとえば、表示される情報を共有しようとするユーザーは、カメラ付き携帯電話を使用して写真を撮影したり、データを再入力したり、単に口頭で他者に伝達することができます。

このように、あらゆるプラットフォームとソフトウェアが Rights Management API をサポートし、かつ画面キャプチャをブロックできたとしても、テクノロジだけでデータの漏洩を防ぐことができるわけではありません。 Rights Management は、承認および使用ポリシーを使用して重要なデータを保護するために役立つものの、このエンタープライズ権限管理ソリューションは、他の管理手段と共に使用する必要があります。 たとえば、物理的なセキュリティを実装したり、組織のデータへのアクセスが承認されているユーザーを慎重に検査および監視したり、どのようなデータを共有してはならないかを理解できるようにユーザーの教育に投資したりすることです。

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>ユーザーが [転送不可] を使用して電子メールを保護するのと、転送権限のないテンプレートを使用するのとでは、どのような違いがありますか。

名前や外観に反して、**[転送不可]** は転送権限の反対ではなく、テンプレートでもありません。 実際には、電子メールの転送を制限するだけでなく、メールボックス以外のメールのコピー、印刷、保存を制限する権限のセットです。 権限は、選択された受信者に基づき、ユーザーに動的に適用されます。管理者によって静的に割り当てられるものではありません。 詳細については、「 [Azure Information Protection の使用権限を構成する](configure-usage-rights.md)」の「[電子メールの [転送不可] オプション](configure-usage-rights.md#do-not-forward-option-for-emails)」セクションを参照してください。