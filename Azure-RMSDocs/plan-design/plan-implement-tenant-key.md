---
title: "Azure Rights Management テナント キーを計画して実装する | Azure Information Protection"
description: "Azure Information Protection テナント キーに関する計画および管理に役立つ情報です。 Microsoft がテナント キーを管理する (既定値) のではなく、組織に該当する特定の規制に準拠するために、ユーザーが自分でテナント キーを管理する必要がある場合があります。 ユーザーでのテナント キーの管理は、Bring Your Own Key (BYOK) とも呼ばれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f0403d85406cc8642654569958e3482a5d991352
ms.openlocfilehash: 10e51ed108bedc59a66be86b8b27a140f899dd45


---

# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーを計画して実装する

>*適用対象: Azure Information Protection、Office 365*

この記事の情報は、Azure Information Protection テナント キーに関する計画および管理に役立ちます。 たとえば、マイクロソフトがテナント キーを管理する (既定値) のではなく、組織に該当する特定の規制に準拠するために、ユーザーが自分でテナント キーを管理する必要がある場合があります。 ユーザーでのテナント キーの管理は、Bring Your Own Key (BYOK) とも呼ばれます。

> [!NOTE]
> Azure Information Protection テナント キーのオンプレミスに相当するものは、サーバー ライセンサー証明書 (SLC) キーと呼ばれます。 Azure Information Protection では、Azure Information Protection のサブスクリプションがある組織ごとに 1 つ以上のキーを保持します。 組織で Azure Information Protection に対して使用されるキー (ユーザー キー、コンピューター キー、ドキュメント暗号化キーなど) は、すべて暗号化されて Azure Information Protection テナント キーにチェーンされます。

**概要:** 次の表は、推奨されるテナント キー トポロジのクイック ガイドとして使用してください。 詳細については、別のドキュメントを参照してください。

Microsoft 管理のテナント キーを使用して Azure Information Protection をデプロイする場合、後で BYOK に変更することができます。 ただし現時点では、Azure Information Protection テナント キーを BYOK から Microsoft 管理に変更することはできません。

|ビジネスの要件|推奨テナント キー トポロジ|
|------------------------|-----------------------------------|
|特殊なハードウェアを必要としない Azure Information Protection を短時間でデプロイする場合|Microsoft 管理|
|Azure Rights Management サービスを使用して、Exchange Online で完全な IRM 機能が必要な場合|Microsoft 管理|
|キーはユーザーによって作成され、ハードウェア セキュリティ モジュール (HSM) で保護されます|BYOK<br /><br />現時点では、この構成を使用すると Exchange Online での IRM 機能には制限があります。 詳細については、「[BYOK の料金と制限事項](byok-price-restrictions.md)」を参照してください。|

## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>テナント キー トポロジを選択する:Microsoft による管理 (既定) または自主管理 (BYOK)
組織に最適なテナント キー トポロジを決定します。 既定では、Azure Information Protection でテナント キーが生成され、テナント キー ライフサイクルのほとんどの側面が管理されます。 これは、管理オーバーヘッドが最も少なくて済むシンプルな方法です。 多くの場合、テナント キーの存在を意識することすらありません。 Azure Information Protection にサインアップすれば、それ以外のキー管理プロセスは Microsoft によって処理されます。

または、[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) を使用して、テナント キーを完全に管理することもできます。 このシナリオでは、テナント キーを作成して、社内でマスター コピーを保持する必要があります。 多くの場合、このシナリオは BYOK (Bring Your Own Key) と呼ばれます。 この方法では、次の状況が発生します。

1.  社内で IT ポリシーとセキュリティ ポリシーに沿ってテナント キーを作成します。

2.  Azure Key Vault を使用して、そのテナント キーを社内のハードウェア セキュリティ モジュール (HSM) から Microsoft が所有し管理する HSM にセキュリティで保護した状態で転送します。 このプロセス全体で、テナント キーがハードウェア保護境界の外に置かれることはありません。

3.  テナント キーを Microsoft に転送するときは、Azure Key Vault により常時保護されます。

オプションとして、テナント キーの使用状況と使用時期を正確に把握するために Azure Information Protection のほぼリアルタイムの使用状況ログを使用することもできます。

> [!NOTE]
> 追加の保護措置として、Azure Key Vault では北米、EMEA (欧州、中東、アフリカ)、アジアなどの地域のデータ センターで独立したセキュリティ ドメインを使用しています。 また、Microsoft Azure Germany や Azure Government など、さまざまな Azure のインスタンスが対象になります。 テナント キーを自主管理する場合、キーは、Azure Information Protection テナントが登録されている地域またはインスタンスのセキュリティ ドメインに関連付けられています。 たとえば、欧州のお客様のテナント キーを北米やアジアのデータセンターで使用することはできません。

## <a name="the-tenant-key-lifecycle"></a>テナント キーのライフサイクル
Microsoft でテナント キーを管理することになった場合、キー ライフサイクル操作の大半を Microsoft で行います。 ただし、テナント キーを自主管理することになった場合、Azure Key Vault でキー ライフサイクル操作の多くといくつかの追加の手順を自社で行う必要があります。

この 2 つの方法の概要と比較を次の図に示します。 最初の図から、Microsoft がテナント キーを管理するという既定構成では管理者のオーバーヘッドが非常に少ないことがわかります。

![Azure Information Protection テナント キー ライフサイクル - Microsoft が既定で管理](../media/RMS_BYOK_cloud.png)

2 番目の図では、テナント キーを自主管理する場合に必要な追加の手順を示しています。

![Azure Information Protection テナント キー ライフサイクル - 自分で管理 (BYOK)](../media/RMS_BYOK_onprem4.png)

テナント キーを Microsoft で管理する場合、キーの生成に関する操作は不要です。「[次のステップ](plan-implement-tenant-key.md#next-steps)」に進んでください。  

テナント キーを自主管理する場合、詳細については以下のセクションを参照してください。

## <a name="implementing-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーを実装する

このセクションでは、テナント キーの生成と管理を行う場合、つまり BYOK (Bring Your Own Key) シナリオについて説明します。


> [!IMPORTANT]
> Microsoft によって管理されるテナント キーを使用して Azure Information Protection を使用開始していて、テナント キーを (BYOK に移動して) 管理したい場合、以前保護されていたドキュメントや電子メールには、アーカイブされたキーを使用して引き続きアクセスできます。 ただし、Office 2010 を実行しているユーザーがいる場合、これらの手順を実行する前に [Microsoft サポートにお問い合わせください](../get-started/information-support.md#to-contact-microsoft-support)。 これらのコンピューターには、追加の構成手順が必要です。
> 
> キーの処理に関して組織固有のポリシーがある場合も [Microsoft サポートにお問い合わせください](../get-started/information-support.md#to-contact-microsoft-support)。

### <a name="prerequisites-for-byok"></a>BYOK の前提条件
次の表に BYOK (Bring Your Own Key) の前提条件を示します。

|要件|詳細情報|
|---------------|--------------------|
|Azure Information Protection をサポートするサブスクリプション。|使用可能なサブスクリプションの詳細については、Azure Information Protection の[価格設定ページ](https://go.microsoft.com/fwlink/?LinkId=827589)をご覧ください。|
|個人向け RMS または Exchange Online は使用しないでください。 または、Exchange Online を使用する場合は、この構成で BYOK を使用することには制限があることをご理解ください。|BYOK の現在の制限事項の詳細については、「[BYOK の料金と制限事項](byok-price-restrictions.md)」を参照してください。<br /><br />**重要**: 現在、BYOK には Exchange Online との互換性がありません。|
|有料または試用版の Azure サブスクリプションなど、Key Vault BYOK のすべての前提条件。 |Azure Key Vault のドキュメントの「[BYOK の前提条件](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok)」を参照してください。 <br /><br /> Azure Active Directory の構成と、Azure Rights Management カスタム テンプレートの構成にアクセスできる無料の Azure サブスクリプション (**Azure Active Directory へのアクセス権**) では、Azure Key Vault を使用できません。 BYOK を使用できる Azure サブスクリプションがあることを確認するには、次のように [Azure Resource Manager](https://msdn.microsoft.com/library/azure/mt786812\(v=azure.300\).aspx) の PowerShell コマンドレットを使用します。 <br /><br /> 1.次のコマンドを使用し、Azure PowerShell セッションを開始して Azure アカウントにサインインします。`Login-AzureRmAccount`<br /><br />2.次のように入力し、サブスクリプションの名前と ID、テナント ID、有効な状態の値が表示されることを確認します。`Get-AzureRmSubscription`<br /><br />値が表示されず、プロンプトに戻るだけの場合は、BYOK に使用できる Azure サブスクリプションがありません。 <br /><br />**注**: BYOK の前提条件に加え、ソフトウェア キーとハードウェア キーを使用して AD RMS から Azure Information Protection への移行を行う場合は、Thales ファームウェアのバージョンが 11.62 以降である必要があります。|
|Windows PowerShell 用の Azure Rights Management 管理モジュール。|インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。 <br /><br />この Windows PowerShell モジュールを既にインストールしている場合は、次のコマンドを実行してバージョン番号が **2.5.0.0** 以上であることを確認します。`(Get-Module aadrm -ListAvailable).Version`|

Thales HSM の詳細と Thales HSM を Azure Key Vault と組み合わせて使用する方法については、[Thales の Web サイト](https://www.thales-esecurity.com/msrms/cloud)を参照してください。

### <a name="instructions-for-byok"></a>BYOK の手順

独自のテナント キーを生成し Azure Key Vault に転送するには、Azure Key Vault のドキュメントの「[Azure Key Vault の HSM 保護キーを生成し、転送する方法](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/)」に記載された手順に従ってください。

キーが Key Vault に転送されると、キーには Key Vault でキー ID が付与されます。キー ID は、キーの資格情報コンテナーの名前、キー コンテナー、キーの名前、キーのバージョンが含まれる URL です。 例: **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** この URL を指定して、Azure Information Protection から Azure Rights Management サービスにこのキーを使用するように指示する必要があります。

ただし、Azure Information Protection では、Azure Rights Management サービスが組織のキー コンテナーにあるキーを使用することを承認されてからのみ、このキーを使用することができます。 このようにするには、Azure Key Vault 管理者が Key Vault PowerShell コマンドレット [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/en-us/library/mt603625(v=azure.300\).aspx) を使用して Azure Rights Management サービス プリンシパルにアクセス許可を付与します。このときに GUID 00000012-0000-0000-c000-000000000000 を使用します。 次に例を示します。

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

このキーを組織の Azure Information Protection テナント キーとして使用するように、Azure Information Protection を構成できるようになったとします。 Azure RMS コマンドレットを使用するには、まず Azure Rights Management サービスに接続してサインインします。

    Connect-AadrmService

次に、[Use-AadrmKeyVaultKey コマンドレット](https://msdn.microsoft.com/library/azure/mt759829.aspx)を実行して、キー URL を指定します。 次に例を示します。

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> この例では、"aaaabbbbcccc111122223333" は使用するキーのバージョンです。 バージョンを指定しない場合は、現在のバージョンのキーが警告なしで使用され、機能するコマンドが表示されます。 ただし、Key Vault のキーを後で更新 (新たに) する場合、AadrmKeyVaultKey コマンドをもう一度実行する場合でも、Azure Rights Management サービスはテナントの機能を停止します。
>
>このコマンドを実行する場合は、キー名だけでなく、キーのバージョンを指定することを確認してください。 Azure Key Vault コマンドの [Get AzureKeyVaultKey](https://docs.microsoft.com/powershell/resourcemanager/azurerm.keyvault\/v2.3.0\/get-azurekeyvaultkey) を使用して、現在のキーのバージョン番号を取得できます。 例: `Get-AzureKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

キーの URL が Azure RMS サービスで正しく設定されていることを、Azure Key Vault で確認する必要がある場合は、[Get-AzureKeyVaultKey](https://msdn.microsoft.com/en-us/library/dn868053(v=azure.300\).aspx) を実行して、キーの URL を表示します。


## <a name="next-steps"></a>次のステップ

テナント キーを計画 (および必要に応じて生成) した後は、次の操作を行います。

1.  テナント キーの使用を開始します。

    -   まだの場合は、この段階で Rights Management サービスをアクティブにして、組織が Azure Information Protection の使用を開始できるようにする必要があります。 ユーザーはすぐにテナント キーの使用を開始します (Azure Key Vault の Microsoft による管理または顧客管理)。

        アクティブ化の詳細については、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

    -   既に Rights Management サービスをアクティブにしていてテナント キーを自主管理する場合、ユーザーは古いテナント キーから新しいテナント キーへと段階的に移行します。この段階的な移行が完了するまで数週間かかることがあります。 古いテナント キーで保護されていたドキュメントやファイルは、権限のあるユーザーが引き続きアクセスできます。

2.  使用状況のログを使用することを検討します。このログには Azure Rights Management サービスで実行されるすべてのトランザクションが記録されます。

    テナント キーを自主管理する場合、ログにはテナント キーの使用に関する情報が記録されます。 Excel で表示されるログ ファイルで次のスニペットを参照してください。要求の種類である **KeyVaultDecryptRequest** および **KeyVaultSignRequest** では、テナント キーが使用されています。

    ![Excel のログ ファイル、テナント キーが使用されていることがわかる](../media/RMS_Logging.png)

    使用状況ログの詳細については、「[Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。

3.  テナント キーを維持管理します。

    詳細については、「[Azure Rights Management テナント キーに対する操作](../deploy-use/operations-tenant-key.md)」を参照してください。




<!--HONumber=Dec16_HO2-->


