---
title: Azure Information Protection 向けのユーザーとグループの準備
description: 分類、ラベル付け、組織のドキュメントと電子メールの保護などを開始する必要があるユーザーとグループ アカウントがあることを確認してください。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7d9c58649eb06b614a25e28c909d34318ea80133
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="preparing-users-and-groups-for-azure-information-protection"></a>Azure Information Protection 向けのユーザーとグループの準備

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

組織の Azure Information Protection を展開する前に、組織のテナントの Azure AD にユーザーとグループのアカウントがあることを確認します。

ユーザーとグループ用にこれらのアカウントを作成する方法は、次を含めさまざまにあります。

- Office 365 管理センターでユーザーを作成し、Exchange Online 管理センターでグループを作成します。

- Azure Portal で、ユーザーとグループを作成します。

- Azure AD PowerShell と Exchange Online コマンドレットを使用して、ユーザーとグループを作成します。

- オンプレミスの Active Directory にユーザーとグループを作成し、それらを Azure AD と同期させます。

- 別のディレクトリにユーザーとグループを作成し、それらを Azure AD と同期させます。

この一覧にある最初の 3 つのメソッドを使用してユーザーとグループを作成するとき、ユーザーとグループは自動的に Azure AD に作成されて、Azure Information Protection でこれらのアカウントを直接使用できます。 ただし、多くの企業ネットワークでは、オンプレミスのディレクトリを使用してユーザーとグループを作成および管理します。 Azure Information Protection では、これらのアカウントを直接使用できません。Azure AD に同期する必要があります。

## <a name="how-users-and-groups-are-used-by-azure-information-protection"></a>Azure Information Protection によるユーザーとグループの使用方法

Azure Information Protection でユーザーとグループを使用するシナリオは 3 通りあります。

- **ラベルをユーザーに割り当てる場合**: ラベル付けと分類を使用するケースが該当します。 管理者だけが次のグループを選択します。
    
    - 既定の Azure Information Protection ポリシーは、テナントの Azure AD にあるすべてのユーザーに対して自動的に割り当てられます。 ただし、スコープを持つポリシーを使用して、指定したユーザーまたはグループに追加のラベルを割り当てることもできます。

- **使用権限とアクセス制御を割り当てる場合**: Azure Rights Management サービスを使用してドキュメントと電子メールを保護します。 管理者とユーザーが、これらのユーザーとグループを選択できます。

    - 使用権限は、ドキュメントや電子メールをユーザーが開くことができるかと、その使用方法を決定します。 たとえば、読み取り専用、読み取りと印刷、または読み取りと編集などができます。

    - アクセス制御には、有効期限日とアクセスのためにインターネット接続が必要かどうかが含まれます。

- **Azure Rights Management サービスを構成する場合**: 特定のシナリオをサポートするためであり、したがって、管理者のみがこれらのグループを選択します。 たとえば、次のような構成の例があります。

    - スーパー ユーザー。eDiscovery またはデータ回復で必要な場合に、指定されたサービスまたはユーザーが暗号化されたコンテンツを開くことができるようにします。

    - Azure Rights Management サービスの代理管理。

    - 段階的デプロイをサポートするオンボーディング コントロール。

**ラベルをユーザーに割り当てる場合**: Azure Information Protection ポリシーを構成するときに、ラベルをドキュメントや電子メールに適用できるようにします。 管理者のみがこれらのユーザーとグループを選択できます。

- 既定の Azure Information Protection ポリシーは、テナントの Azure AD にあるすべてのユーザーに対して自動的に割り当てられます。 ただし、スコープを持つポリシーを使用して、指定したユーザーまたはグループに追加のラベルを割り当てることもできます。     

**使用権限とアクセス制御を割り当てる場合**: Azure Rights Management サービスを使用してドキュメントと電子メールを保護します。 管理者とユーザーが、これらのユーザーとグループを選択できます。

- 使用権限は、ドキュメントや電子メールをユーザーが開くことができるかと、その使用方法を決定します。 たとえば、読み取り専用、読み取りと印刷、または読み取りと編集などができます。 

- アクセス制御には、有効期限日とアクセスのためにインターネット接続が必要かどうかが含まれます。 

**Azure Rights Management サービスを構成する場合**: 特定のシナリオをサポートするためであり、したがって、管理者のみがこれらのグループを選択します。 たとえば、次のような構成の例があります。

- スーパー ユーザー。eDiscovery またはデータ回復で必要な場合に、指定されたサービスまたはユーザーが暗号化されたコンテンツを開くことができるようにします。

- Azure Rights Management サービスの代理管理。

- 段階的デプロイをサポートするオンボーディング コントロール。

## <a name="azure-information-protection-requirements-for-user-accounts"></a>ユーザー アカウントに関する Azure Information Protection の要件

ラベルを割り当てる場合:

- Azure AD にあるすべてのユーザー アカウントは、追加のラベルをユーザーに割り当てるスコープ ポリシーを構成するために使用できます。

使用権限とアクセス制御を割り当て、Azure Rights Management サービスを構成する場合:

- ユーザーを承認するために Azure AD 内の 2 つの属性、**proxyAddresses** と **userPrincipalName** が使用されます。

- **Azure AD proxyAddresses** 属性は、単一アカウントのすべての電子メール アドレスを格納するために使用され、さまざまな方法でデータを設定できます。 たとえば、Exchange Online メールボックスを持つ Office 365 内のユーザーであれば、この属性に格納されている電子メール アドレスを自動的に持つことになります。 代替電子メール アドレスを Office 365 ユーザーに割り当てると、それもこの属性に保存されます。 オンプレミスのアカウントから同期する電子メール アドレスでも設定できます。 
    
    ドメインがテナントに追加されている場合 ("確認済みドメイン")、Azure Information Protection では Azure AD proxyAddresses 属性にある任意の値を使用できます。 ドメインの確認の詳細については、以下の項目をご覧ください。
    
    - Azure AD: 「[Azure Active Directory へのカスタム ドメイン名の追加](/active-directory/active-directory-add-domain)」

    - Office 365: 「[ドメインとユーザーを Office 365 に追加する](https://go.microsoft.com/fwlinkid/?linkid=847121)」

- **Azure AD userPrincipalName** 属性は、テナントにあるアカウントに対する値が Azure AD proxyAddresses 属性にない場合にのみ使用されます。 たとえば、Azure Portal でユーザーを作成するか、メールボックスのない Office 365 のユーザーを作成する場合です。

### <a name="assigning-usage-rights-and-access-controls-to-external-users"></a>使用権限とアクセス制御を外部ユーザーに割り当てる

Azure Information Protection では、テナント内のユーザー用に Azure AD proxyAddresses と Azure AD userPrincipalName を使用することに加え、別のテナントのユーザーを承認するためにもこれらの属性を同様に使用します。

Office 365 Message Encryption と新機能を利用し、Azure AD にアカウントを持っていないユーザーにメールを送信すると、ソーシャル ID プロバイダーとのフェデレーションかワンタイム パスコードにより最初にユーザーが認証されます。 保護されているメールに指定されているメール アドレスがユーザーの認証に使用されます。

## <a name="azure-information-protection-requirements-for-group-accounts"></a>グループ アカウントに関する Azure Information Protection の要件

ラベルを割り当てる場合:

- 追加のラベルをグループ メンバーに割り当てるスコープ ポリシーを構成するために、ユーザーのテナントの確認済みドメインを含む電子メール アドレスを持つ任意の種類のグループを Azure AD で使用することができます。 電子メール アドレスを持つグループを、メールが有効なグループと呼ぶことがあります。
    
    たとえば、メールが有効なセキュリティ グループ、配布グループ (静的または動的)、Office 365 グループを使用できます。 セキュリティ グループ (動的または静的) は、電子メール アドレスを持っていない種類のグループであるため使用できません。

使用権限とアクセス制御を割り当てる場合:

- Azure AD にある任意の種類のグループを使用できます。Azure AD には、ユーザーのテナントに対する確認済みのドメインを含む電子メール アドレスがあります。 電子メール アドレスを持つグループを、メールが有効なグループと呼ぶことがあります。 

Azure Rights Management サービスを構成する場合:

- テナント内の確認済みドメインの電子メール アドレスを持つ、Azure AD にある任意の種類のグループを使用できますが、例外が 1 つあります。 その例外とは、グループを使用するためのオンボーディング コントロールを構成する場合です。この場合は、テナントの Azure AD 内のセキュリティ グループである必要があります。

- テナント内の確認済みドメインに属している、Azure AD にある任意のグループ (電子メール アドレスの有無を問わない) を、Azure Rights Management サービスの代理管理に使用できます。

### <a name="assigning-usage-rights-and-access-controls-to-external-groups"></a>使用権限とアクセス制御を外部グループに割り当てる

Azure Information Protection では、テナント内のグループ用に Azure AD proxyAddresses を使用することに加え、別のテナントのグループを承認するためにもこの属性を同様に使用します。

## <a name="using-accounts-from-active-directory-on-premises-for-azure-information-protection"></a>オンプレミスの Active Directory からのアカウントを Azure Information Protection 用に使用する

オンプレミスで管理されているアカウントがあり、Azure Information Protection でこのアカウントを使用したい場合は、このアカウントを Azure AD と同期する必要があります。 展開を容易にするために、[Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) を使用することお勧めします。 ただし、任意のディレクトリ同期方式を使用して同じ結果を達成できます。

アカウントを同期するとき、すべての属性を同期する必要はありません。 同期する必要がある属性の一覧については、Azure Active Directory のドキュメントの [Azure RMS に関するセクション](/azure/active-directory/connect/active-directory-aadconnectsync-attributes-synchronized#azure-rms)をご覧ください。

Azure Rights Management 用の属性の一覧を見ると、ユーザーの場合は、オンプレミス AD 属性のうち、**mail**、**proxyAddresses**、**userPrincipalName** が同期用に必要であることがわかります。 **mail** と **proxyAddresses** の値が、Azure AD proxyAddresses 属性に同期されます。 詳細については、「[Azure AD に proxyAddresses 属性を反映する方法](https://support.microsoft.com/help/3190357/how-the-proxyaddresses-attribute-is-populated-in-azure-ad)」をご覧ください。

## <a name="confirming-your-users-and-groups-are-prepared-for-azure-information-protection"></a>ユーザーとグループが Azure Information Protection 用に準備されたことを確認する

Azure AD PowerShell を使用して、ユーザーとグループを Azure Information Protection に使用できることを確認できます。 PowerShell を使用して、それらを承認するために使用できる値を確認できます。 

たとえば、Azure Active Directory の V1 PowerShell モジュール、[MSOnline](/powershell/module/msonline/?view=azureadps-1.0) を使用して、PowerShell セッションで、まず、サービスに接続し、グローバル管理者の資格情報を指定します。

    Connect-MsolService


注: このコマンドが機能しない場合は、`Install-Module MSOnline` を実行して MSOnline モジュールをインストールできます。

次に、PowerShell セッションを構成して、値を切り捨てないようにします。

    $Formatenumerationlimit =-1

### <a name="confirm-user-accounts-are-ready-for-azure-information-protection"></a>ユーザー アカウントが Azure Information Protection の準備ができていることを確認する

ユーザー アカウントを確認するには、次のコマンドを実行します。

    Get-Msoluser | select DisplayName, UserPrincipalName, ProxyAddresses

まず、Azure Information Protection で使用したいユーザーが表示されることを確認します。

次に、**ProxyAddresses** 列が設定されているかどうかをチェックします。 設定されている場合は、Azure Information Protection のユーザーを承認するためにこの列の電子メールの値を使用できます。

**ProxyAddresses** 列が設定されていない場合は、**UserPrincipalName** の値が Azure Rights Management サービスのユーザーを承認するために使用されます。

次に例を示します。

|表示名|UserPrincipalName|ProxyAddresses
|-------------------|-----------------|--------------------|
|Jagannath Reddy |jagannathreddy@contoso.com|{}|
|Ankur Roy|ankurroy@contoso.com|{SMTP:ankur.roy@contoso.com, smtp: ankur.roy@onmicrosoft.contoso.com}|

この例では、次の点に注意してください。

- Jagannath Reddy のユーザー アカウントは  **jagannathreddy@contoso.com** によって承認されることになります。

-  Ankur Roy のユーザー アカウントは、**ankur.roy@contoso.com** と **ankur.roy@onmicrosoft.contoso.com** を使用して承認できますが、 **ankurroy@contoso.com** では承認できません。

通常、UserPrincipalName の値は、ProxyAddresses フィールドにあるいずれかの値と一致します。 これは、お勧めの構成ですが、電子メール アドレスと一致するように UPN を変更できない場合は、次の手順を実行する必要があります。

1. UPN 値内のドメイン名が Azure AD テナントの確認済みドメインの場合は、Azure AD 内の別の電子メール アドレスとして UPN 値を追加することで、UPN 値を Azure Information Protection のユーザー アカウントの承認に使用できるようにします。

    UPN 値内のドメイン名がテナントの確認済みドメインでない場合は、Azure Information Protection で使用できません。 ただし、グループ電子メール アドレスが検証済みドメイン名を使用している場合、このユーザーはグループのメンバーとしてまだ承認できます。

2. UPN がルーティングできない場合は (たとえば、**ankurroy@contoso.local**)、ユーザーの代替ログイン ID を構成し、この代替ログインを使用して Office にサインインする方法をユーザーに指示してください。 Office のレジストリ キーを設定する必要もあります。

    詳細については、「[代替ログイン ID を構成する](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)」と「[Office applications periodically prompt for credentials to SharePoint Online, OneDrive, and Lync Online (Office アプリケーションは SharePoint のオンライン、OneDrive、 Lync オンラインの資格情報を定期的に要求する)](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)」をご覧ください。

> [!TIP]
> Export-Csv コマンドレットを使用すると、結果をスプレッド シートにエクスポートでき、インポートの検索や一括編集などの管理が容易になります。
>
> 例: `Get-MsolGroup | select DisplayName, ProxyAddresses | Export-Csv -Path UserAccounts.csv`

### <a name="confirm-group-accounts-are-ready-for-azure-information-protection"></a>グループ アカウントが Azure Information Protection の準備ができていることを確認する

グループ アカウントを確認するには、次のコマンドを使用します。

    Get-MsolGroup | select DisplayName, ProxyAddresses

Azure Information Protection で使用したいグループが表示されることを確認します。 表示されるグループでは、**ProxyAddresses** 列内の電子メール アドレスを使用して、グループ メンバーを Azure Rights Management サービスに対して承認できます。

次に、Azure Information Protection 用に使用したいユーザー (またはその他のグループ) がこのグループに含まれていることを確認します。 これを行うには、PowerShell を使用するか (たとえば、 [Get-MsolGroupMember](/powershell/module/msonline/Get-MsolGroupMember?view=azureadps-1.0))、または管理ポータルを使用できます。

セキュリティ グループを使用する 2 つの Azure Rights Management サービスの構成シナリオでは、次の PowerShell コマンドを使用してオブジェクト ID を検索し、これらのグループを識別するために使用できる名前を表示できます。 Azure Portal を使用してこれらのグループを検索し、オブジェクト ID と表示名の値をコピーすることもできます。

    Get-MsolGroup | where {$_.GroupType -eq "Security"}

## <a name="considerations-for-azure-information-protection-if-email-addresses-change"></a>電子メール アドレスが変更される場合の Azure Information Protection に関する考慮事項

ユーザーまたはグループの電子メール アドレスを変更する場合は、ユーザーまたはグループに 2 つ目の電子メール アドレス (プロキシ アドレス、エイリアス、または代替電子メール アドレスとも呼ぶ) として、古い電子メール アドレスを追加することをお勧めします。 これを行うと、古い電子メール アドレスは、Azure AD proxyAddresses 属性に追加されます。 このアカウントの管理によって、任意の使用権限や、古い電子メール アドレスが使用されていたときに保存されその他の構成のビジネス継続性が確保されます。 

これを実施できない場合、新しい電子メール アドレスを使用するユーザーまたはグループは、古いメール アドレスを使用して、以前保護されていたドキュメントと電子メールへのアクセスが拒否されるリスクを負います。 この場合は、保護構成を繰り返して、新しいメール アドレスを保存する必要があります。 たとえば、ユーザーまたはグループがテンプレートまたはラベルの使用権限を付与されている場合、これらのテンプレートまたはラベルを編集するか、古いメール アドレスに付与したのと同じ使用権限を使って新しいメール アドレスを指定します。

グループの電子メール アドレスを変更することはまれであり、個々のユーザーではなくグループに使用権限を割り当てれば、ユーザーの電子メール アドレスが変更されても問題になりません。 このシナリオでは、使用権限は、グループの電子メール アドレスに割り当てられており、個々のユーザー電子メール アドレスにではありません。 これは、管理者がドキュメントと電子メールを保護する使用権限を構成するための最も可能性のある (およびお勧めの) 方式です。 ただし、ユーザーは個々のユーザーのカスタム アクセス許可を割り当てることのほうが一般的です。 アクセスを許可するためにユーザー アカウントとグループのいずれが使用されているのかを常時把握することはできないため、古い電子メール アドレスを 2 つ目の電子メール アドレスとして常に追加することが最も安全な方法です。

## <a name="group-membership-caching-by-azure-information-protection"></a>Azure Information Protection によるグループ メンバーシップのキャッシュ

パフォーマンス上の理由により、Azure Information Protection ではグループ メンバーシップをキャッシュします。 つまり、これらのグループが Azure Information Protection によって使用される場合に Azure AD 内でグループ メンバーシップの変更内容が有効になるまで最長で 3 時間かかることがあり、この期間は変わる可能性があるということです。 

使用権限の割り当てまたは Azure Rights Management サービスの構成を行うためにグループを使用する場合、またはスコープ付きポリシーを構成する場合は、すべての変更や、実行するテストで、この遅延を考慮してください。


## <a name="next-steps"></a>次の手順

ユーザーとグループを Azure Information Protection に使用できることと、ドキュメントと電子メールの保護を開始する準備ができたことを確認したら、Azure Rights Management サービスをアクティブにする必要があるかどうかを確認します。 組織のドキュメントと電子メールを保護するには、このサービスをアクティブにする必要があります。 

- 2018 年 2 月以降: Azure Rights Management または Azure Information Protection を含むサブスクリプションを今月以降に取得した場合は、サービスが自動的にアクティブ化されます。 

- 2018 年 2 月より前にサブスクリプションを取得した場合: 自分でサービスをアクティブにする必要があります。 

アクティブ化の状態の確認を含む詳細については、「[Azure Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
