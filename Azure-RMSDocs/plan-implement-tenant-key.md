---
title: Azure Information Protection テナント キー
description: Microsoft Azure Information Protection のルート キーの管理ではなく作成してこのキーを管理する場合があります ("bring your own key"と呼ばれるまたは BYOK) のテナントの特定の規制に準拠します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 26999c8fdd079c7a34d39415d8beba6763a06f68
ms.sourcegitcommit: e0ce23467744ec6a4da49081461a459bc37c7d78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65443277"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーを計画して実装する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

この記事の情報は、Azure Information Protection テナント キーに関する計画および管理に役立ちます。 たとえば、マイクロソフトがテナント キーを管理する (既定値) のではなく、組織に該当する特定の規制に準拠するために、ユーザーが自分でテナント キーを管理する必要がある場合があります。 ユーザーでのテナント キーの管理は、Bring Your Own Key (BYOK) とも呼ばれます。

Azure Information Protection テナント キーとは

- Azure Information Protection テナント キーは組織のルート キーです。 ユーザー キー、コンピューター キー、ドキュメント暗号化キーなどの他のキーは、このルート キーから派生させることができます。 Azure Information Protection は、組織でこれらのキーを使用する場合は常に、暗号化により Azure Information Protection テナント キーにチェーンします。

- Azure Information Protection テナント キーは、Active Directory Rights Management サービス (AD RMS) からのサーバー ライセンサー証明書 (SLC) キーのオンライン版です。 

**概要:** 推奨されるテナント キー トポロジのクイック ガイドとして、次の表を使用します。 詳細については、別のドキュメントを参照してください。

|ビジネスの要件|推奨テナント キー トポロジ|
|------------------------|-----------------------------------|
|特別なハードウェア、追加のソフトウェア、または Azure サブスクリプションなしで、Azure Information Protection をすばやくデプロイする。<br /><br />以下に例を示します。テスト環境および組織にキー管理に関する規制上の要件がない場合。|マイクロソフト管理|
|コンプライアンスに関する規制、追加のセキュリティ、およびすべてのライフ サイクル操作の制御。 <br /><br />以下に例を示します。ハードウェア セキュリティ モジュール (HSM) でキーを保護する必要があります。|BYOK|


必要に応じて、デプロイ後に [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) コマンドレットを使ってテナント キー トポロジを変更できます。


## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>選択、テナント キー トポロジ。(既定値) を Microsoft が管理または自主管理 (BYOK)

組織に最適なテナント キー トポロジを決定します。

- **Microsoft による管理**: Microsoft によって組織のテナント キーが自動的に生成され、このキーは Azure Information Protection 専用に使用されます。 既定では、Microsoft はテナントにこのキーを使用し、テナント キー ライフ サイクルのほとんどの側面を管理します。 
    
    これは、管理オーバーヘッドが最も少なくて済むシンプルな方法です。 多くの場合、テナント キーの存在を意識することすらありません。 Azure Information Protection にサインアップすれば、それ以外のキー管理プロセスは Microsoft によって処理されます。

- **自主管理 (BYOK)**: テナント キーを完全に制御するには、Azure Information Protection で [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) を使用します。 このテナント キー トポロジの場合、Key Vault に直接キーを作成するか、オンプレミスで作成します。 オンプレミスで作成する場合は、このキーを Key Vault に転送またはインポートします。 その後、このキーを使用するように Azure Information Protection を構成して、Azure Key Vault で管理します。
    

### <a name="more-information-about-byok"></a>BYOK の詳細
独自のキーを作成する場合、次のオプションが提供されます。

- **オンプレミスで作成し、Key Vault に転送またはインポートするキー**:
    
    - オンプレミスで作成し、HSM 保護キーとして Key Vault に転送する HSM 保護キー。
    
    - オンプレミスで作成し、変換してから HSM 保護キーとして Key Vault に転送するソフトウェア保護キー。 このオプションがサポートされるのは、[Active Directory Rights Management サービス (AD RMS) から移行する](migrate-from-ad-rms-to-azure-rms.md)場合のみです。
    
    - オンプレミスで作成し、ソフトウェア保護キーとして Key Vault にインポートするソフトウェア保護キー。 このオプションには .PFX 証明書ファイルが必要です。
    
- **Key Vault で作成するキー**:
    
    - Key Vault で作成する HSM 保護キー。
    
    - Key Vault で作成するソフトウェア保護キー。

これらの BYOK オプションの中で最も一般的なのは、オンプレミスで作成し、HSM 保護キーとして Key Vault に転送する HSM 保護キーです。 このオプションの場合、管理オーバーヘッドが最大になりますが、特定の規制に準拠するために組織で必要になる場合があります。 Azure Key Vault で使用されている HSM は FIPS 140-2 レベル 2 検証済みです。

この方法では、次の状況が発生します。

1. 社内で IT ポリシーとセキュリティ ポリシーに沿ってテナント キーを作成します。 このキーはマスター コピーです。 オンプレミスで保持され、ユーザーがバックアップを行います。

2. このキーのコピーを作成して、HSM から Azure Key Vault にこのコピーを安全に転送します。 このプロセス全体で、このキーのマスター コピーがハードウェア保護境界の外に置かれることはありません。

3. キーのコピーは Azure Key Vault で保護されます。

> [!NOTE]
> 
> 追加の保護措置として、Azure Key Vault では北米、EMEA (ヨーロッパ、中東、アフリカ)、アジアなどの地域のデータ センターで独立したセキュリティ ドメインを使用しています。 また、Azure Key Vault では、Microsoft Azure Germany や Azure Government など、Azure のさまざまなインスタンスを使用します。 

オプションとして、テナント キーの使用状況と使用時期を正確に把握するために Azure Information Protection のほぼリアルタイムの使用状況ログを使用することもできます。

### <a name="when-you-have-decided-your-tenant-key-topology"></a>テナント キー トポロジを決定した場合

Microsoft でテナント キーを管理するようにした場合: 

- AD RMS から移行する場合を除き、テナントのキーの生成に関する操作は不要です。[次のステップ](plan-implement-tenant-key.md#next-steps)に進んでください。

- 現在 AD RMS を所有していて、Azure Information Protection に移行する場合は、次の記事に記載されている移行手順を使用します: [AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md) 

テナント キーを自主管理する場合、詳細については以下のセクションを参照してください。

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーの BYOK を実装する

このセクションでは、テナント キーの生成と管理を行う場合、つまり BYOK (Bring Your Own Key) シナリオについて説明します。

> [!NOTE]
> Microsoft によって管理されるテナント キーを使用して Azure Information Protection を使用開始していて、テナント キーを (BYOK に移動して) 管理したい場合、以前保護されていたドキュメントや電子メールには、アーカイブされたキーを使用して引き続きアクセスできます。 

### <a name="prerequisites-for-byok"></a>BYOK の前提条件
次の表に BYOK (Bring Your Own Key) の前提条件を示します。

|要件|詳細情報|
|---------------|--------------------|
|Azure Information Protection テナントには Azure サブスクリプションが必要です。 ない場合は、[無料アカウント](https://azure.microsoft.com/pricing/free-trial/)にサインアップできます。 <br /><br /> HSM 保護キーを使用するには、Azure Key Vault Premium サービス レベルが必要です。|Azure Active Directory の構成と、Azure Rights Management カスタム テンプレートの構成にアクセスできる無料の Azure サブスクリプション (**Azure Active Directory へのアクセス権**) では、Azure Key Vault を使用できません。 BYOK を使用できる Azure サブスクリプションがあることを確認するには使用[Azure PowerShell](/powershell/azure/overview)コマンドレット。 <br /><br /> 1.Azure PowerShell セッションを開始、**管理者として実行**オプション、およびを使用して、Azure Information Protection テナントのグローバル管理者としてサインイン`Connect-AzAccount`をコピーしてに結果として得られるトークン文字列を貼り付けます`https://microsoft.com/devicelogin`ブラウザーを使用しています。 <br /><br /> 詳細については、次を参照してください。 [Azure PowerShell を使用してサインイン](/powershell/azure/authenticate-azureps)します。 <br /><br />2.次のように入力し、サブスクリプションの名前と ID、Azure Information Protection テナント ID、有効な状態の値が表示されることを確認します。`Get-AzSubscription`<br /><br />値が表示されず、プロンプトに戻るだけの場合は、BYOK に使用できる Azure サブスクリプションがありません。 <br /><br />**注意**:BYOK の前提条件に加え、ソフトウェア キーとハードウェア キーを使用して AD RMS から Azure Information Protection への移行を行う場合は、Thales ファームウェアのバージョンが 11.62 以降である必要があります。|
|オンプレミスで作成する HSM 保護キーを使用するには: <br /><br />- Key Vault の BYOK のすべての前提条件の一覧。 |Azure Key Vault のドキュメントの「[BYOK の前提条件](/azure/key-vault/key-vault-hsm-protected-keys#prerequisites-for-byok)」を参照してください。 <br /><br /> **注意**:BYOK の前提条件に加え、ソフトウェア キーとハードウェア キーを使用して AD RMS から Azure Information Protection への移行を行う場合は、Thales ファームウェアのバージョンが 11.62 以降である必要があります。|
|テナント キーを含むキー コンテナーが Azure Key Vault の仮想ネットワーク サービス エンドポイントを使用する場合: <br /><br />- 信頼された Microsoft サービスを許可して、このファイアウォールをバイパスします。|詳細については、「[Virtual Network Service Endpoints for Azure Key Vault](/azure/key-vault/key-vault-overview-vnet-service-endpoints)」(Azure Key Vault の仮想ネットワーク サービス エンドポイント) をご覧ください。|
|Windows PowerShell 用の Azure Rights Management 管理モジュール。|インストール手順については、「[AADRM PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。 <br /><br />この Windows PowerShell モジュールを既にインストールしている場合は、次のコマンドを実行してバージョン番号が **2.9.0.0** 以上であることを確認します。`(Get-Module aadrm -ListAvailable).Version`|

Thales HSM の詳細と Thales HSM を Azure Key Vault と組み合わせて使用する方法については、[Thales の Web サイト](https://www.thales-esecurity.com/msrms/cloud)を参照してください。

### <a name="choosing-your-key-vault-location"></a>Key Vault の場所の選択

Azure Information のテナント キーとして使用するキーを含む Key Vault を作成する場合は、場所を指定する必要があります。 この場所は Azure リージョン、または Azure インスタンスです。

まず、コンプライアンスについて選択し、ネットワーク待機時間を最小限に抑えます。

- コンプライアンス上の理由で BYOK キー トポロジを選択した場合、コンプライアンス要件により、Azure Information Protection テナント キーを格納する Azure リージョンまたは Azure インスタンスが要求される可能性があります。

- 保護のためのすべての暗号化呼び出しは Azure Information Protection テナント キーにチェーンされるため、これらの呼び出しで発生するネットワーク待機時間を最小限に抑える必要があります。 そのためには、Azure Information Protection テナントと同じ Azure リージョンまたはインスタンスに Key Vault を作成します。

Azure Information Protection テナントの場所を特定するには、[Get-AadrmConfiguration](/powershell/module/aadrm/get-aadrmconfiguration) PowerShell コマンドレットを使用し、URL からリージョンを特定します。 以下に例を示します。

    LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

リージョンは **rms.na.aadrm.com** から特定できます。この例では、北米となります。

次の表を使用して、ネットワーク待機時間を最小限に抑えるのに推奨される Azure リージョンまたはインスタンスを特定します。

|Azure リージョンまたはインスタンス|Key Vault に推奨される場所|
|---------------|--------------------|
|rms.**na**.aadrm.com|**米国中北部**または**米国東部**|
|rms.**eu**.aadrm.com|**北ヨーロッパ**または**西ヨーロッパ**|
|rms.**ap**.aadrm.com|**東アジア**または**東南アジア**|
|rms.**sa**.aadrm.com|**米国西部**または**米国東部**|
|rms.**govus**.aadrm.com|**米国中部**または**米国東部 2**|


### <a name="instructions-for-byok"></a>BYOK の手順

Azure Key Vault ドキュメントを使用して、Azure Information Protection で使用するキーと Key Vault を作成します。 例については、「[Azure Key Vault の概要](/azure/key-vault/key-vault-get-started)」を参照してください。

キーの長さが 2048 ビット (推奨) または 1024 ビットであることを確認してください。 Azure Information Protection ではその他のキーの長さはサポートされていません。

オンプレミスで HSM 保護キーを作成し、HSM 保護キーとして Key Vault に転送する場合は、「[Azure Key Vault の HSM 保護キーを生成し、転送する方法](/azure/key-vault/key-vault-hsm-protected-keys)」の手順に従ってください。

Azure Information Protection でキーを使用するには、キーに対して Key Vault のすべての操作が許可される必要があります。 これは、既定の構成と操作は、暗号化、復号化、wrapKey、unwrapKey、記号、および確認します。 次の PowerShell コマンドを使用して、キーの許可された操作を確認することができます:`(Get-AzKeyVaultKey -VaultName <key vault name> -Name <key name>).Attributes.KeyOps`します。 必要に応じて、許可された操作の追加を使用して[Update AzKeyVaultKey](/powershell/module/az.keyvault/update-azkeyvaultkey)と*KeyOps*パラメーター。

Key Vault に格納されているキーにはキー ID があります。 このキー ID は、Key Vault の名前、キー コンテナー、キーの名前、およびキーのバージョンが含まれる URL です。 たとえば、**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** です。 キー コンテナー URL を指定して、このキーを使用するように Azure Information Protection を構成する必要があります。

Azure Information Protection でキーを使用するには、Azure Rights Management サービスが組織の Key Vault にあるキーの使用を承認されている必要があります。 そのために、Azure Key Vault 管理者は Azure portal または Azure PowerShell を使用できます。

Azure portal を使用した構成:

1. **[キー コンテナー]** > **\<*ご使用のキー コンテナー名*>** > **[アクセス ポリシー]** > **[新規追加]** に移動します。

2. **[アクセス ポリシーの追加]** ブレードで、**[Configure from template]\(テンプレートからの構成\)** (省略可能) リスト ボックスから **[Azure Information Protection BYOK]** を選択し、**[OK]** をクリックします。
    
    選択したテンプレートには次の構成が含まれます。
    
    - **[プリンシパルの選択]** に対して、**[Microsoft Rights Management Services]** が自動的に割り当てられます。
    - **[取得]**、**[暗号化解除]**、および **[サイン]** に対して、キーのアクセス許可が自動的に選択されます。 

PowerShell を使用した構成:

- Key Vault の PowerShell コマンドレットを実行[セット AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)、GUID を使用して、Azure Rights Management サービス プリンシパルにアクセス許可を付与**00000012-0000-0000-c000-000000000000**. 以下に例を示します。
    
        Set-AzKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get

このキーを組織の Azure Information Protection テナント キーとして使用するように、Azure Information Protection を構成できるようになったとします。 Azure RMS コマンドレットを使用するには、まず Azure Rights Management サービスに接続してサインインします。

    Connect-AadrmService

次に、[Use-AadrmKeyVaultKey コマンドレット](/powershell/module/aadrm/use-aadrmkeyvaultkey)を実行して、キー URL を指定します。 以下に例を示します。

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> この例では、"aaaabbbbcccc111122223333" は使用するキーのバージョンです。 バージョンを指定しない場合は、現在のバージョンのキーが警告なしで使用され、機能するコマンドが表示されます。 ただし、Key Vault のキーを後で更新 (新たに) する場合、AadrmKeyVaultKey コマンドをもう一度実行する場合でも、Azure Rights Management サービスはテナントの機能を停止します。
> 
> このコマンドを実行する場合は、キー名だけでなく、キーのバージョンを指定することを確認してください。 Azure Key Vault cmd を使用する[Get AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey)を現在のキーのバージョン番号を取得します。 たとえば次のようになります。`Get-AzKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

キーの URL が Azure Information Protection に対して正しく設定されていることを確認する必要がある場合: Azure Key vault では、次のように実行します。 [Get AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey)キーを参照する URL。

最後に、Azure Rights Management サービスが既にアクティブ化されている場合は、[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) を実行して、Azure Rights Management サービスのアクティブなテナント キーとしてこのキーを使用するように Azure Information Protection に指示します。 この手順を行わないと、Azure Information Protection は、テナントに対して自動的に作成された、既定の Microsoft 管理キーを使用し続けます。


## <a name="next-steps"></a>次の手順

テナント キーを計画および必要に応じて作成して構成した後は、次の操作を行います。

1.  テナント キーの使用を開始します。
    
    - 保護サービスをまだアクティブにしていない場合は、この段階で Rights Management サービスをアクティブにして、組織が Azure Information Protection の使用を開始できるようにする必要があります。 ユーザーはすぐに (Azure Key Vault の自主管理、または Microsoft 管理による) テナント キーの使用を開始します。
    
        アクティブ化の詳細については、「[Rights Management をアクティブにする](./activate-service.md)」を参照してください。
        
    - 既に Rights Management サービスをアクティブにしていてテナント キーを自主管理する場合、ユーザーは古いテナント キーから新しいテナント キーへと段階的に移行します。 この段階的な移行は、完了するまでに数週間かかる場合があります。 古いテナント キーで保護されていたドキュメントやファイルは、権限のあるユーザーが引き続きアクセスできます。
        
2. 使用状況のログを使用することを検討します。このログには Azure Rights Management サービスで実行されるすべてのトランザクションが記録されます。
    
    テナント キーを自主管理する場合、ログにはテナント キーの使用に関する情報が記録されます。 Excel で表示されるログ ファイルで次のスニペットを参照してください。要求の種類である **KeyVaultDecryptRequest** および **KeyVaultSignRequest** では、テナント キーが使用されています。
    
    ![Excel のログ ファイル、テナント キーが使用されていることがわかる](./media/RMS_Logging.png)
    
    使用状況ログの詳細については、「[Azure Rights Management サービスの使用状況をログに記録して分析する](./log-analyze-usage.md)」を参照してください。
    
3.  テナント キーを管理します。
    
    テナント キーのライフ サイクル操作の詳細については、「[Azure Information Protection テナント キーに対する操作](./operations-tenant-key.md)」を参照してください。
