---
title: Azure Information Protection 向けのユーザーとグループの準備
description: 組織の文書やメールを分類、ラベル付け、保護する前に、必要なユーザー アカウントとグループ アカウントが揃っていることを確認します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5f63b23bd6f4e6fdf1198d12e235991f4a692495
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809369"
---
# <a name="preparing-users-and-groups-for-azure-information-protection"></a>Azure Information Protection 向けのユーザーとグループの準備

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連する内容**:[AIP の統合ラベル付けクライアントとクラシック クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

組織に Azure Information Protection を展開する前に、組織のテナントに対し、Azure AD にユーザーとグループのアカウントが用意されていることを確認してください。

ユーザーとグループのアカウントは次のようなさまざまな方法で作成できます。

- Microsoft 365 管理センターでユーザーを作成し、Exchange Online 管理センターでグループを作成します。

- Azure Portal でユーザーとグループを作成します。

- Azure AD PowerShell と Exchange Online のコマンドレットを利用し、ユーザーとグループを作成します。

- オンプレミスの Active Directory でユーザーとグループを作成し、それを Azure AD に同期します。

- 別のディレクトリでユーザーとグループを作成し、それを Azure AD に同期します。

この一覧にある最初の 3 つのメソッドを使用してユーザーとグループを作成する場合 (1 つの例外を除く)、それらは自動的に Azure AD に作成され、Azure Information Protection でこれらのアカウントを直接使用できます。 ただし、多くの企業ネットワークではオンプレミスのディレクトリを利用し、ユーザーとグループを作成し、管理しています。 Azure Information Protection はそのようなアカウントを直接利用できません。Azure AD に同期させる必要があります。

前の段落で言及されている例外は、Exchange Online 用に作成できる動的配布リストです。 静的な配布リストとは異なり、これらのグループは Azure AD にレプリケートされないため、Azure Information Protection では使用できません。 

## <a name="how-users-and-groups-are-used-by-azure-information-protection"></a>Azure Information Protection でのユーザーとグループの利用方法

Azure Information Protection でユーザーとグループを使用するための 3 つのシナリオ:

ラベルを文書やメールに適用できるように Azure Information Protection ポリシーを構成するとき、**ラベルをユーザーに割り当てる**。 管理者だけがこれらのユーザーとグループを選択できます。

- 既定の Azure Information Protection ポリシーがテナントの Azure AD のすべてのユーザーに自動的に割り当てられます。 ただし、スコープ付きポリシーを利用し、指定のユーザーまたはグループに追加ラベルを割り当てることもできます。     

**使用権限とアクセス制御を割り当て**、Azure Rights Management サービスを構成する場合。 管理者とユーザーはこれらのユーザーとグループを選択できます。

- 使用権限では、ユーザーが文書やメールを開くことができるかが決められ、その利用方法が決められます。 たとえば、読み取り専用か、読み取りと印刷か、読み取りと編集などです。 

- アクセス制御には有効期限が含まれ、アクセスにはインターネットへの接続が必要かどうかが表示されます。 

特定のシナリオをサポートするように **Azure Rights Management サービスを構成する**。そのため、管理者のみがこれらのグループを選択できます。 たとえば、次を構成します。

- スーパー ユーザー。電子情報開示やデータ復旧に必要であれば、指名されたサービスまたはユーザーが暗号化されているコンテンツを開くことができます。

- Azure Rights Management サービスの委任管理。

- 段階的デプロイをサポートするオンボード コントロール。

## <a name="azure-information-protection-requirements-for-user-accounts"></a>Azure Information Protection の要件

ラベルを割り当てる:

- Azure AD のすべてのユーザー アカウントを利用して、追加ラベルをユーザーに割り当てるスコープ付きポリシーを構成できます。

使用権限とアクセス制御を割り当て、Azure Rights Management サービスを構成する:

- ユーザーに権限を与えるために、Azure AD では、**proxyAddresses** と **userPrincipalName** という 2 つの属性が利用されます。

- **Azure AD proxyAddresses** 属性は、あるアカウントのすべてのメール アドレスを保存します。さまざまな方法で反映できます。 たとえば、Exchange Online メールボックスを持つ Microsoft 365 のユーザーには、この属性に格納されている電子メールアドレスが自動的に設定されます。 Microsoft 365 ユーザーの代替電子メールアドレスを割り当てると、その電子メールアドレスもこの属性に保存されます。 オンプレミス アカウントから同期しているメール アドレスでも反映できます。 

    Azure Information Protection は、ドメインがテナントに追加されていれば ("検証済みドメイン")、この Azure AD proxyAddresses 属性のあらゆる値を利用できます。 ドメイン検証の詳細については、次をご覧ください。

    - Azure AD の場合: [カスタム ドメイン名を Azure Active Directory に追加する](/azure/active-directory/fundamentals/add-custom-domain)

    - Office 365 の場合: [office 365 にドメインを追加する](/office365/admin/setup/add-domain)

- **Azure AD userPrincipalName** 属性は、テナントのアカウントの Azure AD proxyAddresses 属性に値がないときにのみ利用されます。 たとえば、Azure portal でユーザーを作成したり、メールボックスを持たない Microsoft 365 のユーザーを作成したりすることができます。

### <a name="assigning-usage-rights-and-access-controls-to-external-users"></a>使用権限とアクセス制御を外部ユーザーに割り当てる

自分のテナントのユーザーに Azure AD proxyAddresses と Azure AD userPrincipalName を使用するだけでなく、Azure Information Protection ではまた、同じようにこれらの属性を利用し、別のテナントからのユーザーに権限を与えます。

その他の承認方法:

- Azure AD に含まれていない電子メール アドレスの場合、Microsoft アカウントで認証されていれば、Azure Information Protection でそれらを承認できます。 ただし、Microsoft アカウントが認証に使用されている場合、アプリケーションによっては、保護されたコンテンツを開けない場合があます。 [詳細情報](./secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

- Azure AD にアカウントを持たないユーザーに新しい機能を備えた Office 365 Message Encryption を利用してメールを送信するとき、まずそのユーザーが認証されます。その際、フェデレーションとソーシャル ID プロバイダーを利用するか、ワンタイム パスコードを利用します。 その後、保護されたメールに指定されているメール アドレスを利用し、ユーザーに権限を与えます。

## <a name="azure-information-protection-requirements-for-group-accounts"></a>グループ アカウントの Azure Information Protection 要件

ラベルを割り当てる:

- 追加ラベルをグループ メンバーに割り当てるスコープ付きポリシーを構成するには、ユーザーのテナントに対してドメインが検証されているメール アドレスが与えられたあらゆる種類の Azure AD グループを利用できます。 メール アドレスが与えられているグループはしばしば、メールが有効なグループと呼ばれています。

    たとえば、メールが有効なセキュリティグループ、静的な配布グループ、および Microsoft 365 グループを使用できます。 セキュリティ グループ (動的または静的) は利用できません。この種類のグループにはメール アドレスが与えられていないためです。 Exchange Online からの動的配布リストも使用できません。このグループは Azure AD にレプリケートされないためです。

使用権限とアクセス制御を割り当てる:

- ユーザーのテナントに対してドメインが検証されているメール アドレスが与えられたあらゆる種類の Azure AD グループを利用できます。 メール アドレスが与えられているグループはしばしば、メールが有効なグループと呼ばれています。 

Azure Rights Management サービスを構成する:

- テナントでドメインが検証されているメール アドレスが与えられたあらゆる種類の Azure AD グループを利用できるが、例外が 1 つあります。 その例外は、グループを利用するためにオンボード コントロールを構成するが、そのグループは自分のテナントの Azure AD セキュリティ グループにする必要があるときです。

- Azure Rights Management サービスの委任管理については、テナントでドメインが検証されているあらゆる Azure AD グループを利用できます (メール アドレスの有無は関係ありません)。

### <a name="assigning-usage-rights-and-access-controls-to-external-groups"></a>使用権限とアクセス制御を外部グループに割り当てる

自分のテナントのグループに Azure AD proxyAddresses を使用するだけでなく、Azure Information Protection ではまた、同じようにこれらの属性を利用し、別のテナントからのグループに権限を与えます。

## <a name="using-accounts-from-active-directory-on-premises-for-azure-information-protection"></a>Azure Information Protection にオンプレミス Active Directory アカウントを利用する

オンプレミスで管理しているアカウントに Azure Information Protection で使用したいアカウントがあれば、それを Azure AD と同期する必要があります。 デプロイを簡単にするために、[Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect) の利用をお勧めします。 ただし、同じ結果が得られるあらゆるディレクトリ同期方法を利用できます。

アカウントを同期するとき、すべての属性を同期する必要はありません。 同期が必要な属性の一覧については、Azure Active Directory 文書の [Azure RMS セクション](/azure/active-directory/connect/active-directory-aadconnectsync-attributes-synchronized#azure-rms)をご覧ください。

Azure Rights Management の属性一覧から、ユーザーの場合、**mail**、**proxyAddresses**、**userPrincipalName** のオンプレミス AD 属性が同期に必要になることがわかります。 **mail** と **proxyAddresses** の値が Azure AD proxyAddresses 属性と同期します。 詳細については、「[Azure AD に proxyAddresses 属性を反映する方法](https://support.microsoft.com/help/3190357/how-the-proxyaddresses-attribute-is-populated-in-azure-ad)」を参照してください。

## <a name="confirming-your-users-and-groups-are-prepared-for-azure-information-protection"></a>Azure Information Protection のためにユーザーとグループが用意されていることを確認する

Azure AD PowerShell を利用し、ユーザーとグループを Azure Information Protection で利用できることを確認できます。 また、PowerShell を利用し、承認に利用できる値を確認できます。 

たとえば、PowerShell セッションで Azure Active Directory 向け V1 PowerShell モジュール、[MSOnline](/powershell/module/msonline/) を利用し、最初にサービスに接続し、グローバル管理者の資格情報を入力します。

```ps
Connect-MsolService
```

注: このコマンドでうまくいかない場合、`Install-Module MSOnline` を実行して MSOnline モジュールをインストールできます。

次に、値が切り詰められないように PowerShell セッションを設定します。

```ps
$Formatenumerationlimit =-1
```

### <a name="confirm-user-accounts-are-ready-for-azure-information-protection"></a>ユーザー アカウントが Azure Information Protection で使えることを確認する

ユーザー アカウントを確認するには、次のコマンドを実行します。

```ps
Get-Msoluser | select DisplayName, UserPrincipalName, ProxyAddresses
```

最初に、Azure Information Protection で使用するユーザーが表示されていることを確認します。

次に、**ProxyAddresses** 列にデータが入力されているかどうかを確認します。 入力されている場合、Azure Information Protection でこの列のメール値を利用し、ユーザーに権限を付与できます。

**ProxyAddresses** 列にデータが入力されていない場合、**UserPrincipalName** is の値を利用してユーザーに Azure Rights Management サービスの権限が与えられます。

以下に例を示します。


|  表示名   |     UserPrincipalName      |                            ProxyAddresses                             |
|-----------------|----------------------------|-----------------------------------------------------------------------|
| Jagannath Reddy | jagannathreddy@contoso.com |                                  {}                                   |
|    Ankur Roy    |    ankurroy@contoso.com    | {SMTP:ankur.roy@contoso.com, smtp: ankur.roy@onmicrosoft.contoso.com} |

次の点に注意してください。

- Jagannath reddy Reddy のユーザーアカウントは、によって承認され <strong>jagannathreddy@contoso.com</strong> ます。

- Ankur Roy のユーザーアカウントは、およびを使用して承認できますが、は許可され <strong>ankur.roy@contoso.com</strong> <strong>ankur.roy@onmicrosoft.contoso.com</strong> ません <strong>ankurroy@contoso.com</strong> 。

ほとんどの場合、UserPrincipalName の値が ProxyAddresses フィールドの値の 1 つと一致します。 これは推奨構成ですが、メール アドレスに合わせて UPN を変更できない場合、次の手順を行う必要があります。

1. UPN 値のドメイン名が自分の Azure AD テナントに対して検証済みのドメインであれば、Azure AD のもう 1 つのメール アドレスとして UPN 値を追加します。それにより、UPN 値を利用し、Azure Information Protection の権限をユーザー アカウントに付与できます。

    UPN 値のドメイン名が自分のテナントで検証されているドメインではない場合、Azure Information Protection で使用できません。 ただし、グループのメール アドレスで検証済みのドメイン名が使用されていれば、ユーザーにグループのメンバーとして承認できます。

2. UPN がルーティング可能でない場合 (など <strong>ankurroy@contoso.local</strong> ) は、ユーザーの代替ログイン ID を構成し、この代替ログインを使用して Office にサインインする方法を指示します。 Office のレジストリ キーを設定する必要もあります。

    詳細については、「 [代替ログイン ID](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) と Office アプリケーションの構成」を参照して、 [SharePoint、OneDrive、および Lync Online への資格情報を定期的に確認](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)してください。

> [!TIP]
> Export-Csv コマンドレットを利用し、結果をスプレッドシートにエクスポートできます。検索やインポートのための一括編集などで管理が簡単になります。
>
> 例: `Get-MsolGroup | select DisplayName, ProxyAddresses | Export-Csv -Path UserAccounts.csv`

### <a name="confirm-group-accounts-are-ready-for-azure-information-protection"></a>グループ アカウントが Azure Information Protection で使えることを確認する

グループ アカウントを確認するには、次のコマンドを使用します。

```ps
Get-MsolGroup | select DisplayName, ProxyAddresses
```

Azure Information Protection で使用するグループが表示されていることを確認します。 表示されているグループについては、**ProxyAddresses** 列のメール アドレスを利用し、Azure Rights Management サービスのためにグループ メンバーに承認できます。

次に、Azure Information Protection で使用するユーザー (または、その他のグループ) がグループに含まれていることを確認します。 PowerShell を利用してこれを実行できます ([Get-MsolGroupMember](/powershell/module/msonline/Get-MsolGroupMember) など)。あるいは、管理ポータルを利用できます。

セキュリティ グループを利用する 2 つの Azure Rights Management サービス構成シナリオについては、次の PowerShell コマンドを利用し、それらのグループの識別に利用できるオブジェクト ID と表示名を見つけることができます。 Azure Portal を利用してこれらのグループを見つけ、オブジェクト ID と表示名の値をコピーすることもできます。

```ps
Get-MsolGroup | where {$_.GroupType -eq "Security"}
```

## <a name="considerations-for-azure-information-protection-if-email-addresses-change"></a>メール アドレスが変更された場合の Azure Information Protection の考慮事項

ユーザーまたはグループのメール アドレスを変更する場合、使用していないメール アドレスを第 2 メール アドレス (プロキシ アドレス、エイリアス、代替メール アドレスと呼ばれることもあります) としてユーザーまたはグループに追加することをお勧めします。 この作業を行う場合、使用していないメール アドレスは Azure AD proxyAddresses 属性に追加されます。 このようにアカウントを管理することで、使用していないメール アドレスが使われていたときに保存された使用権限やその他の構成もビジネスで引き続き利用できます。 

使用していないメール アドレスを第 2 メール アドレスにしない場合、新しいメール アドレスが与えられたユーザーまたはグループは、使用していないメール アドレスで以前に保護した文書やメールに対するアクセスを拒否されることがあります。 その場合、保護設定を改めて行い、新しいメール アドレスを保存する必要があります。 たとえば、ユーザーまたはグループにテンプレートまたはラベルの使用権限が与えられた場合、そのテンプレートまたはラベルを編集し、使用していないメール アドレスに与えたものと同じ使用権限を付けて新しいメール アドレスを指定します。

グループの場合、そのメール アドレスを変更することはまれです。個々のユーザーではなく、グループに使用権限を割り当てた場合、ユーザーのメール アドレスを変更しても特別な対処は必要ありません。 このシナリオでは、使用権限が個々のユーザーのメール アドレスではなく、グループのメール アドレスに割り当てられます。 これは、文書やメールを保護する使用権限を管理者が設定するとき、最も頻繁に採用される (そして推奨される) 手法です。 ただし、ユーザーが個々のユーザーに独自のアクセス許可を割り当てることの方がより一般的です。 あるユーザー アカウントまたはグループがアクセス付与に使われているかどうかは常に確認できるわけではないため、使用していないメール アドレスを第 2 メール アドレスとして常に追加しておくと安心です。

## <a name="group-membership-caching-by-azure-information-protection"></a>Azure Information Protection のグループ メンバーシップ キャッシュ

パフォーマンス上の理由から、Azure Information Protection はグループ メンバーシップをキャッシュします。 つまり、Azure AD でグループ メンバーシップを変更すると、そのグループが Azure Information Protection で使用されているとき、反映に最大 3 時間かかることがあります。この時間は変更される場合があります。 

使用権限を与えたり、Azure Rights Management サービスを構成したりするためにグループを使用するときに、あるいはスコープ付きポリシーを構成するときに変更やテストを行う場合、この遅延を必ず考慮してください。


## <a name="next-steps"></a>次のステップ

ユーザーとグループを Azure Information Protection に使用できることと、ドキュメントと電子メールの保護を開始する準備ができたことを確認したら、Azure Rights Management サービスをアクティブにする必要があるかどうかを確認します。 組織のドキュメントと電子メールを保護するには、このサービスをアクティブにする必要があります。 

- 2018 年 2 月以降: Azure Rights Management または Azure Information Protection を含むサブスクリプションを今月以降に取得した場合は、サービスが自動的にアクティブ化されます。 

- 2018 年 2 月より前にサブスクリプションを取得した場合: 自分でサービスをアクティブにする必要があります。 

アクティベーションの状態の確認など、詳細については、「 [Azure Information Protection からの保護サービスのアクティブ化](./activate-service.md)」を参照してください。

