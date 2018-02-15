---
title: "Azure Information Protection 向けのユーザーとグループの準備"
description: "組織の文書やメールを分類、ラベル付け、保護する前に、必要なユーザー アカウントとグループ アカウントが揃っていることを確認します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/18/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: de06bc202ff60e6850ba217fe7ded79c0753d925
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2018
---
# <a name="preparing-users-and-groups-for-azure-information-protection"></a>Azure Information Protection 向けのユーザーとグループの準備

>*適用対象: Azure Information Protection、Office 365*

組織に Azure Information Protection を展開する前に、組織のテナントに対し、Azure AD にユーザーとグループのアカウントが用意されていることを確認してください。

ユーザーとグループのアカウントは次のようなさまざまな方法で作成できます。

- Office 365 管理センターでユーザーを作成し、Exchange Online 管理センターでグループを作成します。

- Azure Portal でユーザーとグループを作成します。

- Azure AD PowerShell と Exchange Online のコマンドレットを利用し、ユーザーとグループを作成します。

- オンプレミスの Active Directory でユーザーとグループを作成し、それを Azure AD に同期します。

- 別のディレクトリでユーザーとグループを作成し、それを Azure AD に同期します。

この一覧の最初の 3 つの方法でユーザーとグループを作成すると、ユーザーとグループが Azure AD で自動的に作成されます。そのアカウントを Azure Information Protection は直接利用できます。 ただし、多くの企業ネットワークではオンプレミスのディレクトリを利用し、ユーザーとグループを作成し、管理しています。 Azure Information Protection はそのようなアカウントを直接利用できません。Azure AD に同期させる必要があります。

## <a name="how-users-and-groups-are-used-by-azure-information-protection"></a>Azure Information Protection でのユーザーとグループの利用方法

Azure Information Protection でユーザーとグループを使用するための 3 つのシナリオ:

- ラベル付けや分類のとき、**ラベルをユーザーに割り当てる場合**。 管理者だけがこれらのグループを選択できます。

    - 既定の Azure Information Protection ポリシーがテナントの Azure AD のすべてのユーザーに自動的に割り当てられます。 ただし、スコープ付きポリシーを利用し、指定のユーザーまたはグループに追加ラベルを割り当てることもできます。     

- **使用権限とアクセス制御を割り当て**、Azure Rights Management サービスを構成する場合。 管理者とユーザーはこれらのユーザーとグループを選択できます。

    - 使用権限では、ユーザーが文書やメールを開くことができるかが決められ、その利用方法が決められます。 たとえば、読み取り専用か、読み取りと印刷か、読み取りと編集などです。

    - アクセス制御では、有効期限が決められ、インターネットへの接続がアクセスに必要かどうかが決められます。

- 特定のシナリオをサポートするように **Azure Rights Management サービスを構成する**。そのため、管理者のみがこれらのグループを選択できます。 たとえば、次を構成します。

    - スーパー ユーザー。電子情報開示やデータ復旧に必要であれば、指名されたサービスまたはユーザーが暗号化されているコンテンツを開くことができます。

    - Azure Rights Management サービスの委任管理。

    - 段階的デプロイをサポートするオンボード コントロール。

ラベルを文書やメールに適用できるように Azure Information Protection ポリシーを構成するとき、**ラベルをユーザーに割り当てる**。 管理者だけがこれらのユーザーとグループを選択できます。

- 既定の Azure Information Protection ポリシーがテナントの Azure AD のすべてのユーザーに自動的に割り当てられます。 ただし、スコープ付きポリシーを利用し、指定のユーザーまたはグループに追加ラベルを割り当てることもできます。     

**使用権限とアクセス制御を割り当て**、Azure Rights Management サービスを構成する場合。 管理者とユーザーはこれらのユーザーとグループを選択できます。

- 使用権限では、ユーザーが文書やメールを開くことができるかが決められ、その利用方法が決められます。 たとえば、読み取り専用か、読み取りと印刷か、読み取りと編集などです。 

- アクセス制御では、有効期限が決められ、インターネットへの接続がアクセスに必要かどうかが決められます。 

特定のシナリオをサポートするように **Azure Rights Management サービスを構成する**。そのため、管理者のみがこれらのグループを選択できます。 たとえば、次を構成します。

- スーパー ユーザー。電子情報開示やデータ復旧に必要であれば、指名されたサービスまたはユーザーが暗号化されているコンテンツを開くことができます。

- Azure Rights Management サービスの委任管理。

- 段階的デプロイをサポートするオンボード コントロール。

## <a name="azure-information-protection-requirements-for-user-accounts"></a>Azure Information Protection の要件

ラベルを割り当てる:

- Azure AD のすべてのユーザー アカウントを利用して、追加ラベルをユーザーに割り当てるスコープ付きポリシーを構成できます。

使用権限とアクセス制御を割り当て、Azure Rights Management サービスを構成する:

- ユーザーに権限を与えるために、Azure AD では、**proxyAddresses** と **userPrincipalName** という 2 つの属性が利用されます。

- **Azure AD proxyAddresses** 属性は、あるアカウントのすべてのメール アドレスを保存します。さまざまな方法で反映できます。 たとえば、Office 365 のユーザーに Exchange Online メールボックスが与えられている場合、この属性に保存されているメール アドレスが自動的に与えられます。 Office 365 ユーザーの代替メール アドレスを割り当てると、それもこの属性に保存されます。 オンプレミス アカウントから同期しているメール アドレスでも反映できます。 
    
    Azure Information Protection は、ドメインがテナントに追加されていれば ("検証済みドメイン")、この Azure AD proxyAddresses 属性のあらゆる値を利用できます。 ドメイン検証の詳細については、次をご覧ください。
    
    - Azure AD の場合: [カスタム ドメイン名を Azure Active Directory に追加する](/active-directory/active-directory-add-domain)

    - Office 365 の場合: [Office 365 にドメインとユーザーを追加する](https://go.microsoft.com/fwlinkid/?linkid=847121)

- **Azure AD userPrincipalName** 属性は、テナントのアカウントの Azure AD proxyAddresses 属性に値がないときにのみ利用されます。 たとえば、Azure Portal でユーザーを作成するか、メールボックスを持たない Office 365 ユーザーを作成します。

### <a name="assigning-usage-rights-and-access-controls-to-external-users"></a>使用権限とアクセス制御を外部ユーザーに割り当てる

自分のテナントのユーザーに Azure AD proxyAddresses と Azure AD userPrincipalName を使用するだけでなく、Azure Information Protection ではまた、同じようにこれらの属性を利用し、別のテナントからのユーザーに権限を与えます。

Azure AD にアカウントを持たないユーザーに新しい機能を備えた Office 365 Message Encryption を利用してメールを送信するとき、まずそのユーザーが認証されます。その際、フェデレーションとソーシャル ID プロバイダーを利用するか、ワンタイム パスコードを利用します。 その後、保護されたメールに指定されているメール アドレスを利用し、ユーザーに権限を与えます。

## <a name="azure-information-protection-requirements-for-group-accounts"></a>グループ アカウントの Azure Information Protection 要件

ラベルを割り当てる:

- 追加ラベルをグループ メンバーに割り当てるスコープ付きポリシーを構成するには、ユーザーのテナントに対してドメインが検証されているメール アドレスが与えられたあらゆる種類の Azure AD グループを利用できます。 メール アドレスが与えられているグループはしばしば、メールが有効なグループと呼ばれています。
    
    たとえば、メールが有効なセキュリティ グループ、配布グループ (静的または動的)、Office 365 グループを利用できます。 セキュリティ グループ (動的または静的) は利用できません。この種類のグループにはメール アドレスが与えられていないためです。

使用権限とアクセス制御を割り当てる:

- ユーザーのテナントに対してドメインが検証されているメール アドレスが与えられたあらゆる種類の Azure AD グループを利用できます。 メール アドレスが与えられているグループはしばしば、メールが有効なグループと呼ばれています。 

Azure Rights Management サービスを構成する:

- テナントでドメインが検証されているメール アドレスが与えられたあらゆる種類の Azure AD グループを利用できるが、例外が 1 つあります。 その例外は、グループを利用するためにオンボード コントロールを構成するが、そのグループは自分のテナントの Azure AD セキュリティ グループにする必要があるときです。

- Azure Rights Management サービスの委任管理については、テナントでドメインが検証されているあらゆる Azure AD グループを利用できます (メール アドレスの有無は関係ありません)。

### <a name="assigning-usage-rights-and-access-controls-to-external-groups"></a>使用権限とアクセス制御を外部グループに割り当てる

自分のテナントのグループに Azure AD proxyAddresses を使用するだけでなく、Azure Information Protection ではまた、同じようにこれらの属性を利用し、別のテナントからのグループに権限を与えます。

## <a name="using-accounts-from-active-directory-on-premises-for-azure-information-protection"></a>Azure Information Protection にオンプレミス Active Directory アカウントを利用する

オンプレミスで管理しているアカウントに Azure Information Protection で使用したいアカウントがあれば、それを Azure AD と同期する必要があります。 デプロイを簡単にするために、[Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) の利用をお勧めします。 ただし、同じ結果が得られるあらゆるディレクトリ同期方法を利用できます。

アカウントを同期するとき、すべての属性を同期する必要はありません。 同期が必要な属性の一覧については、Azure Active Directory 文書の [Azure RMS セクション](/azure/active-directory/connect/active-directory-aadconnectsync-attributes-synchronized#azure-rms)をご覧ください。

Azure Rights Management の属性一覧から、ユーザーの場合、**mail**、**proxyAddresses**、**userPrincipalName** のオンプレミス AD 属性が同期に必要になることがわかります。 **mail** と **proxyAddresses** の値が Azure AD proxyAddresses 属性と同期します。 詳細については、「[Azure AD に proxyAddresses 属性を反映する方法](https://support.microsoft.com/help/3190357/how-the-proxyaddresses-attribute-is-populated-in-azure-ad)」を参照してください。

## <a name="confirming-your-users-and-groups-are-prepared-for-azure-information-protection"></a>Azure Information Protection のためにユーザーとグループが用意されていることを確認する

Azure AD PowerShell を利用し、ユーザーとグループを Azure Information Protection で利用できることを確認できます。 また、PowerShell を利用し、承認に利用できる値を確認できます。 

たとえば、PowerShell セッションで Azure Active Directory 向け V1 PowerShell モジュール、[MSOnline](/powershell/module/msonline/?view=azureadps-1.0) を利用し、最初にサービスに接続し、グローバル管理者の資格情報を入力します。

    Connect-MsolService


注: このコマンドでうまくいかない場合、`Install-Module MSOnline` を実行して MSOnline モジュールをインストールできます。

次に、値が切り詰められないように PowerShell セッションを設定します。

    $Formatenumerationlimit =-1

### <a name="confirm-user-accounts-are-ready-for-azure-information-protection"></a>ユーザー アカウントが Azure Information Protection で使えることを確認する

ユーザー アカウントを確認するには、次のコマンドを実行します。

    Get-Msoluser | select DisplayName, UserPrincipalName, ProxyAddresses

最初に、Azure Information Protection で使用するユーザーが表示されていることを確認します。

次に、**ProxyAddresses** 列にデータが入力されているかどうかを確認します。 入力されている場合、Azure Information Protection でこの列のメール値を利用し、ユーザーに権限を付与できます。

**ProxyAddresses** 列にデータが入力されていない場合、**UserPrincipalName** is の値を利用してユーザーに Azure Rights Management サービスの権限が与えられます。

例 :

|表示名|UserPrincipalName|ProxyAddresses
|-------------------|-----------------|--------------------|
|Jagannath Reddy |jagannathreddy@contoso.com|{}|
|Ankur Roy|ankurroy@contoso.com|{SMTP:ankur.roy@contoso.com, smtp: ankur.roy@onmicrosoft.contoso.com}|

この例では、次の点に注意してください。

- Jagannath Reddy のユーザー アカウントが **jagannathreddy@contoso.com** によって承認されます。

-  Ankur Roy のユーザー アカウントは **ankur.roy@contoso.com** と **ankur.roy@onmicrosoft.contoso.com** で承認されます。**ankurroy@contoso.com** は利用されません。

ほとんどの場合、UserPrincipalName の値が ProxyAddresses フィールドの値の 1 つと一致します。 これは推奨構成ですが、メール アドレスに合わせて UPN を変更できない場合、次の手順を行う必要があります。

1. UPN 値のドメイン名が自分の Azure AD テナントに対して検証済みのドメインであれば、Azure AD のもう 1 つのメール アドレスとして UPN 値を追加します。それにより、UPN 値を利用し、Azure Information Protection の権限をユーザー アカウントに付与できます。

    UPN 値のドメイン名が自分のテナントで検証されているドメインではない場合、Azure Information Protection で使用できません。 ただし、グループのメール アドレスで検証済みのドメイン名が使用されていれば、ユーザーにグループのメンバーとして承認できます。

2. UPN がルーティング可能ではない場合 (**ankurroy@contoso.local** など)、ユーザーの代替ログイン ID を設定し、その代替ログインで Office にサインインする方法を指示してください。 Office のレジストリ キーを設定する必要もあります。

    詳細については、「[Configuring Alternate Login ID](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)」 (代替ログイン ID を設定する) と「[Office applications periodically prompt for credentials to SharePoint Online, OneDrive, and Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)」 (Office アプリケーションでは、SharePoint Online、OneDrive、Lync Online の資格情報が定期的に要求されます) を参照してください。

> [!TIP]
> Export-Csv コマンドレットを利用し、結果をスプレッドシートにエクスポートできます。検索やインポートのための一括編集などで管理が簡単になります。
>
> 例: `Get-MsolGroup | select DisplayName, ProxyAddresses | Export-Csv -Path UserAccounts.csv`

### <a name="confirm-group-accounts-are-ready-for-azure-information-protection"></a>グループ アカウントが Azure Information Protection で使えることを確認する

グループ アカウントを確認するには、次のコマンドを使用します。

    Get-MsolGroup | select DisplayName, ProxyAddresses

Azure Information Protection で使用するグループが表示されていることを確認します。 表示されているグループについては、**ProxyAddresses** 列のメール アドレスを利用し、Azure Rights Management サービスのためにグループ メンバーに承認できます。

次に、Azure Information Protection で使用するユーザー (または、その他のグループ) がグループに含まれていることを確認します。 PowerShell を利用してこれを実行できます ([Get-MsolGroupMember](/powershell/module/msonline/Get-MsolGroupMember?view=azureadps-1.0) など)。あるいは、管理ポータルを利用できます。

セキュリティ グループを利用する 2 つの Azure Rights Management サービス構成シナリオについては、次の PowerShell コマンドを利用し、それらのグループの識別に利用できるオブジェクト ID と表示名を見つけることができます。 Azure Portal を利用してこれらのグループを見つけ、オブジェクト ID と表示名の値をコピーすることもできます。

    Get-MsolGroup | where {$_.GroupType -eq "Security"}

## <a name="considerations-for-azure-information-protection-if-email-addresses-change"></a>メール アドレスが変更された場合の Azure Information Protection の考慮事項

ユーザーまたはグループのメール アドレスを変更する場合、使用していないメール アドレスを第 2 メール アドレス (プロキシ アドレス、エイリアス、代替メール アドレスと呼ばれることもあります) としてユーザーまたはグループに追加することをお勧めします。 この作業を行う場合、使用していないメール アドレスは Azure AD proxyAddresses 属性に追加されます。 このようにアカウントを管理することで、使用していないメール アドレスが使われていたときに保存された使用権限やその他の構成もビジネスで引き続き利用できます。 

使用していないメール アドレスを第 2 メール アドレスにしない場合、新しいメール アドレスが与えられたユーザーまたはグループは、使用していないメール アドレスで以前に保護した文書やメールに対するアクセスを拒否されることがあります。 その場合、保護設定を改めて行い、新しいメール アドレスを保存する必要があります。 たとえば、ユーザーまたはグループにテンプレートまたはラベルの使用権限が与えられた場合、そのテンプレートまたはラベルを編集し、使用していないメール アドレスに与えたものと同じ使用権限を付けて新しいメール アドレスを指定します。

グループの場合、そのメール アドレスを変更することはまれです。個々のユーザーではなく、グループに使用権限を割り当てた場合、ユーザーのメール アドレスを変更しても特別な対処は必要ありません。 このシナリオでは、使用権限が個々のユーザーのメール アドレスではなく、グループのメール アドレスに割り当てられます。 これは、文書やメールを保護する使用権限を管理者が設定するとき、最も頻繁に採用される (そして推奨される) 手法です。 ただし、ユーザーが個々のユーザーに独自のアクセス許可を割り当てることの方がより一般的です。 あるユーザー アカウントまたはグループがアクセス付与に使われているかどうかは常に確認できるわけではないため、使用していないメール アドレスを第 2 メール アドレスとして常に追加しておくと安心です。

## <a name="group-membership-caching-by-azure-information-protection"></a>Azure Information Protection のグループ メンバーシップ キャッシュ

パフォーマンス上の理由から、Azure Information Protection はグループ メンバーシップをキャッシュします。 つまり、Azure AD でグループ メンバーシップを変更すると、そのグループが Azure Information Protection で使用されているとき、反映に最大 3 時間かかることがあります。この時間は変更される場合があります。 

使用権限を与えたり、Azure Rights Management サービスを構成したりするためにグループを使用するときに、あるいはスコープ付きポリシーを構成するときに変更やテストを行う場合、この遅延を必ず考慮してください。


## <a name="next-steps"></a>次の手順

ユーザーやグループを Azure Information Protection で使用できることを確認し、文書やメールの保護を始める用意ができたら、Rights Management サービスを起動し、そのデータ保護サービスを有効にします。 詳細については、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
