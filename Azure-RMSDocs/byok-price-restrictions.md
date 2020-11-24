---
title: Bring Your Own Key (BYOK) の詳細-Azure Information Protection
description: お客様が管理するキーを使用する場合の詳細と制限事項について説明します ("your your key" または BYOK と呼ばれます)。 Azure Information Protection を使用します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cfe396cea14effdd77b912b32c7c64296806b4be
ms.sourcegitcommit: 3780bd234c0af60d4376f1cae093b8b0ab035a9f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "95570894"
---
# <a name="bring-your-own-key-byok-details-for-azure-information-protection"></a>Azure Information Protection の独自のキー (BYOK) の詳細を表示する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection サブスクリプションを持つ組織は、Microsoft によって生成される既定のキーではなく、独自のキーを使用してテナントを構成することができます。 この構成は、一般に BYOK (Bring Your Own Key) と呼ばれます。

BYOK と [使用状況ログ](log-analyze-usage.md) は、Azure Information Protection によって使用される Azure Rights Management サービスと統合するアプリケーションとシームレスに連携します。

サポートされているアプリケーションは次のとおりです。

- Microsoft SharePoint や Microsoft 365 など **のクラウドサービス**

- RMS コネクタ経由で Azure Rights Management サービスを使用する Exchange および SharePoint アプリケーションを実行する **オンプレミスサービス**

- Office 2019、Office 2016、Office 2013 など **のクライアントアプリケーション**

> [!TIP]
> 必要に応じて、追加のオンプレミスキーを使用して、特定のドキュメントに追加のセキュリティを適用します。 詳細については、「 [独自のキー (HYOK) 保護](configure-adrms-restrictions.md) (クラシッククライアント)」または「 [二重キー暗号化 (dke) 保護](plan-implement-tenant-key.md#double-key-encryption-dke-aip-unified-labeling-client-only)の保持」を参照してください。
> 

## <a name="azure-key-vault-key-storage"></a>Azure Key Vault キーストレージ

ユーザーが生成したキーは、BYOK 保護の Azure Key Vault に保存する必要があります。

> [!NOTE]
> Azure Key Vault で HSM で保護されたキーを使用するには [Azure Key Vault Premium サービスレベル](https://azure.microsoft.com/pricing/details/key-vault/)が必要です。これにより、月額サブスクリプション料金が追加で発生します。

### <a name="sharing-key-vaults-and-subscriptions"></a>キーコンテナーとサブスクリプションの共有

テナントキーには **専用のキーコンテナー** を使用することをお勧めします。 専用のキーコンテナーを使用すると、他のサービスからの呼び出しによって [サービスの制限](/azure/key-vault/general/service-limits) を超えないようにすることができます。 テナントキーが格納されている key vault のサービス制限を超えると、Azure Rights Management サービスの応答時間が調整される可能性があります。

さまざまなサービスのキー管理要件が異なるため、Microsoft では、key vault に **専用の Azure サブスクリプション** を使用することをお勧めします。 専用の Azure サブスクリプション:

- 誤ったミスから保護する

- 複数のサービスに異なる管理者がいる場合の安全性の向上

Azure Key Vault を使用する他のサービスと Azure サブスクリプションを共有するには、サブスクリプションが管理者の共通セットを共有していることを確認します。 サブスクリプションを使用するすべての管理者が、アクセスできるすべてのキーについて十分に理解していることを確認すると、キーが誤って構成される可能性が低くなります。

**例:** Azure Information Protection テナントキーの管理者が、Office 365 カスタマーキーと CRM online のキーを管理するユーザーと同じである場合に、共有 Azure サブスクリプションを使用します。 これらのサービスのキー管理者が異なる場合は、専用のサブスクリプションを使用することをお勧めします。

### <a name="benefits-of-using-azure-key-vault"></a>Azure Key Vault を使用する利点

Azure Key Vault は、暗号化を使用する多くのクラウドベースおよびオンプレミスのサービスに対して、一元化された一貫性のあるキー管理ソリューションを提供します。

Azure Key Vault では、キーの管理ができるだけでなく、セキュリティ管理者は同じ管理エクスペリエンスによって、暗号化を使用する他のサービスやアプリケーションの証明書やシークレット (パスワードなど) を格納し、アクセスし、管理することができます。

Azure Key Vault にテナントキーを格納すると、次のような利点があります。

|長所  |説明  |
|---------|---------|
|**組み込みインターフェイス**| Azure Key Vault では、キー管理のためのさまざまな組み込みのインターフェイス (PowerShell、CLI、REST API、Azure Portal など) をサポートしています。 <br /><br />その他のサービスやツールは、監視などの特定のタスク用に最適化された機能のために Key Vault と統合されています。 <br /><br />たとえば、Operations Management Suite Log analytics を使用してキー使用状況ログを分析し、指定した条件が満たされたときにアラートを設定します。        |
|**役割の分離**| Azure Key Vault は、セキュリティのベストプラクティスとして、役割の分離を提供します。 <br /><br />役割の分離により、Azure Information Protection 管理者は、データの分類と保護の管理、特定のセキュリティまたはコンプライアンス要件に対する暗号化キーとポリシーの管理など、最高の優先順位に専念できます。 |
|**マスターキーの場所**| Azure Key Vault はさまざまな場所で使用でき、マスターキーが有効な場合に制限のある組織をサポートします。 <br /><br />詳細については、Azure サイトの「[リージョン別の利用可能な製品](https://azure.microsoft.com/regions/services/)」のページを参照してください。|
|**分離セキュリティドメイン**|Azure Key Vault は、北米、EMEA (ヨーロッパ、中東、アフリカ)、アジアなどの地域のデータセンターに個別のセキュリティドメインを使用します。 <br /><br />また、Azure Key Vault では、Microsoft Azure Germany や Azure Government など、Azure のさまざまなインスタンスを使用します。 |
|**統一されたエクスペリエンス**| また Azure Key Vault を使用すると、セキュリティ管理者は、暗号化を使用する他のサービスの証明書やシークレット (パスワードなど) の保存、アクセス、および管理を行うことができます。 <br><br />テナントキーに Azure Key Vault を使用すると、これらの要素のすべてを管理する管理者はシームレスなユーザーエクスペリエンスを実現できます。|

最新の更新プログラムと、他のサービスが  [Azure Key Vault](/azure/key-vault/general/basic-concepts)を使用する方法については、 [Azure Key Vault チームのブログ](/archive/blogs/kv/)を参照してください。

## <a name="usage-logging-for-byok"></a>BYOK の使用状況ログ

使用状況ログは、Azure Rights Management サービスに要求を行うすべてのアプリケーションによって生成されます。

使用状況ログは省略可能ですが、Azure Information Protection のほぼリアルタイムの使用状況ログを使用して、テナントキーがどのように使用されているかを正確に確認することをお勧めします。

BYOK のキー使用状況ログの詳細については、「 [Azure Information Protection からの保護の使用状況のログ記録と分析](log-analyze-usage.md)」を参照してください。

> [!TIP]
> さらなる保証のために、Azure Information Protection 使用状況ログは [Azure Key Vault ログ記録](/azure/key-vault/general/logging)で相互参照できます。 Key Vault ログは、キーが Azure Rights Management サービスによってのみ使用されることを個別に監視するための信頼性の高い方法を提供します。
>
> 必要に応じて、キーコンテナーに対するアクセス許可を削除することで、キーへのアクセスを直ちに取り消します。

## <a name="options-for-creating-and-storing-your-key"></a>キーを作成して格納するためのオプション

> [!NOTE]
> 非運用テナントのみで使用するために、管理された HSM のサポート Azure Key Vault Azure Information Protection は、現在プレビューの段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 
>
> 管理された HSM サービスの詳細と、コンテナーとキーを設定する方法の詳細については、 [Azure Key Vault のドキュメント](/azure/key-vault/)を参照してください。 
>
> キー承認を付与するためのその他の手順については、以下で説明します。
>

BYOK は、Azure Key Vault またはオンプレミスのいずれかで作成されたキーをサポートします。

オンプレミスでキーを作成する場合は、そのキーを Key Vault に転送またはインポートし、キーを使用するように Azure Information Protection を構成する必要があります。 Azure Key Vault 内から、追加のキー管理を実行します。

独自のキーを作成して格納するためのオプション:

- **Azure Key Vault で作成されました。** HSM で保護されたキーまたはソフトウェアで保護されたキーとして Azure Key Vault にキーを作成して保存します。

- **オンプレミスで作成されます。** オンプレミスのキーを作成し、次のオプションのいずれかを使用して Azure Key Vault に転送します。

    - **Hsm で保護されたキー。 HSM で保護されたキーとして転送されます。** 選択された最も一般的な方法。

        この方法では、管理オーバーヘッドが最も多くなりますが、組織が特定の規制に従うことが必要になる場合があります。 Azure Key Vault によって使用される Hsm は、FIPS 140-2 Level 2 で検証されます。

    - **変換され、HSM で保護されたキーとして Azure Key Vault に転送される、ソフトウェアで保護されたキー。** このメソッドは、 [Active Directory Rights Management サービス (AD RMS) から移行](migrate-from-ad-rms-to-azure-rms.md)する場合にのみサポートされます。

    - **ソフトウェアで保護されたキーとして社内で作成され、ソフトウェアで保護されたキーとして Azure Key Vault に転送されます。** このメソッドにはが必要です。PFX 証明書ファイル。

たとえば、オンプレミスで作成されたキーを使用するには、次の手順を実行します。

1. 組織の IT およびセキュリティポリシーを使用して、オンプレミスでテナントキーを生成します。 このキーはマスター コピーです。 オンプレミスに保持され、バックアップを行う必要があります。

1. マスターキーのコピーを作成し、HSM から Azure Key Vault に安全に転送します。 このプロセス全体を通して、キーのマスターコピーがハードウェア保護の境界内に出ることはありません。

転送後、キーのコピーは Azure Key Vault によって保護されます。

## <a name="exporting-your-trusted-publishing-domain"></a>信頼された発行ドメインのエクスポート

Azure Information Protection の使用を停止することにした場合は、Azure Information Protection によって保護されたコンテンツの暗号化を解除するために、信頼された発行ドメイン (TPD) が必要になります。

ただし、Azure Information Protection キーに BYOK を使用している場合は、TPD のエクスポートはサポートされていません。

このシナリオを準備するには、適切な TPD を事前に作成しておく必要があります。 詳細については、「 [Azure Information Protection "Cloud Exit" プランを準備する方法](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631)」を参照してください。

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>Azure Information Protection テナント キーの BYOK を実装する

BYOK を実装するには、次の手順に従います。

1. [BYOK の前提条件を確認する](#prerequisites-for-byok)
1. [Key Vault の場所を選択します](#choosing-your-key-vault-location)
1. [キーを作成して構成する](#create-and-configure-your-key)

### <a name="prerequisites-for-byok"></a>BYOK の前提条件

BYOK の前提条件は、システムの構成によって異なります。 必要に応じて、システムが次の前提条件を満たしていることを確認します。

|要件  |説明  |
|---------|---------|
|**Azure サブスクリプション**     |すべての構成に必要です。 <br />詳細については、「 [BYOK と互換性のある Azure サブスクリプションがあることを確認](#verifying-that-you-have-a-byok-compatible-azure-subscription)する」を参照してください。         |
|**Azure Information Protection 用の AIPService PowerShell モジュール**|すべての構成に必要です。 <br />詳細については、「 [AIPService PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。|
|**BYOK の前提条件 Azure Key Vault** | オンプレミスで作成された HSM で保護されたキーを使用している場合は、Azure Key Vault のドキュメントに記載されている [BYOK の前提条件](/azure/key-vault/keys/hsm-protected-keys-byok#prerequisites) も満たしていることを確認してください。         |
|**Thales ファームウェアバージョン11.62**    |ソフトウェアキーからハードウェアキーへの移行時に、HSM に Thales ファームウェアを使用して AD RMS から Azure Information Protection に移行する場合は、Thales ファームウェアバージョン11.62 が必要です。
|**信頼された Microsoft サービスに対するファイアウォールのバイパス** |テナントキーを含む key vault が Azure Key Vault に Virtual Network サービスエンドポイントを使用している場合は、信頼された Microsoft サービスにこのファイアウォールのバイパスを許可する必要があります。 <br />詳細については、「[Virtual Network Service Endpoints for Azure Key Vault](/azure/key-vault/general/overview-vnet-service-endpoints)」(Azure Key Vault の仮想ネットワーク サービス エンドポイント) をご覧ください。       |

#### <a name="verifying-that-you-have-a-byok-compatible-azure-subscription"></a>BYOK と互換性のある Azure サブスクリプションがあることを確認しています

Azure Information Protection テナントには Azure サブスクリプションが必要です。 まだお持ちでない場合は、 [無料アカウント](https://azure.microsoft.com/pricing/free-trial/)にサインアップできます。 ただし、HSM で保護されたキーを使用するには、Azure Key Vault Premium サービス階層が必要です。

Azure Active Directory 構成と Azure Rights Management カスタムテンプレート構成へのアクセスを提供する無料の Azure サブスクリプションでは、Azure Key Vault を使用するのに十分では *ありません* 。

BYOK と互換性のある Azure サブスクリプションがあるかどうかを確認するには、次の手順を実行して、 [Azure PowerShell](/powershell/azure/) コマンドレットを使用して確認します。

1. 管理者として Azure PowerShell セッションを開始します。

1. を使用して、Azure Information Protection テナントのグローバル管理者としてサインインし `Connect-AzAccount` ます。

1. 表示されたトークンをクリップボードにコピーします。 次に、ブラウザーでにアクセス https://microsoft.com/devicelogin し、コピーしたトークンを入力します。

    詳細については、「 [Azure PowerShell でのサインイン](/powershell/azure/authenticate-azureps)」を参照してください。

1. PowerShell セッションで `Get-AzSubscription` 、「」と入力し、次の値が表示されることを確認します。

    - サブスクリプションの名前と ID
    - Azure Information Protection テナント ID
    - 状態が有効であることを確認する

    値が表示されず、プロンプトに戻った場合は、BYOK に使用できる Azure サブスクリプションがありません。

### <a name="choosing-your-key-vault-location"></a>Key Vault の場所の選択

Azure Information のテナント キーとして使用するキーを含む Key Vault を作成する場合は、場所を指定する必要があります。 この場所は Azure リージョン、または Azure インスタンスです。

まず、コンプライアンスについて選択し、ネットワーク待機時間を最小限に抑えます。

- コンプライアンス上の理由により BYOK キーの方法を選択した場合は、これらのコンプライアンス要件によって、Azure Information Protection テナントキーを格納するために使用できる Azure リージョンまたはインスタンスも必要になることがあります。

- Azure Information Protection キーへの保護チェーンのすべての暗号化呼び出し。 そのため、Azure Information Protection テナントと同じ Azure リージョンまたはインスタンスにキーコンテナーを作成することによって、これらの呼び出しに必要なネットワーク待機時間を最小限に抑えることができます。

Azure Information Protection テナントの場所を特定するには、 [AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) PowerShell コマンドレットを使用して、url からリージョンを識別します。 例:

```ps
LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing
```
    
リージョンは **rms.na.aadrm.com** から特定できます。この例では、北米となります。

次の表は、ネットワーク待機時間を最小限に抑えるために推奨される Azure リージョンとインスタンスを示しています。

|Azure リージョンまたはインスタンス|Key Vault に推奨される場所|
|---------------|--------------------|
|rms.**na**.aadrm.com|**米国中北部** または **米国東部**|
|rms.**eu**.aadrm.com|**北ヨーロッパ** または **西ヨーロッパ**|
|rms.**ap**.aadrm.com|**東アジア** または **東南アジア**|
|rms.**sa**.aadrm.com|**米国西部** または **米国東部**|
|rms.**govus**.aadrm.com|**米国中部** または **米国東部 2**|
|**aadrm.us**|**US Gov バージニア** または **US Gov アリゾナ**|
|**aadrm.cn**|**中国東部 2** または **中国北部 2**|

### <a name="create-and-configure-your-key"></a>キーを作成して構成する

>[!IMPORTANT]
> 管理対象 Hsm に固有の情報については、「Azure CLI を使用した管理された [hsm キーのキー承認の有効化](#enabling-key-authorization-for-managed-hsm-keys-via-azure-cli)」を参照してください。

Azure Information Protection に使用する Azure Key Vault とキーを作成します。 詳細については、 [Azure Key Vault のドキュメント](/azure/key-vault/)を参照してください。

BYOK の Azure Key Vault とキーを構成するには、次の点に注意してください。

- [キーの長さの要件](#key-length-requirements)
- [オンプレミスの HSM で保護されたキーを作成して key vault に転送する](#creating-an-hsm-protected-key-on-premises-and-transferring-it-to-your-key-vault)
- [キー ID を使用した Azure Information Protection の構成](#configuring-azure-information-protection-with-your-key-id)
- [キーを使用するように Azure Rights Management サービスを承認する](#authorizing-the-azure-rights-management-service-to-use-your-key)

#### <a name="key-length-requirements"></a>キーの長さの要件

キーを作成するときは、キーの長さが2048ビット (推奨) または1024ビットのどちらかであることを確認してください。 Azure Information Protection ではその他のキーの長さはサポートされていません。

> [!NOTE]
> 1024ビットキーは、アクティブなテナントキーに対して適切なレベルの保護を提供するものとは見なされません。
>
>マイクロソフトでは、1024ビットの RSA キーなどの下位キーの長さの使用を保証しておらず、SHA-1 などの不適切な保護レベルを提供するプロトコルの使用については推奨していません。
>

#### <a name="creating-an-hsm-protected-key-on-premises-and-transferring-it-to-your-key-vault"></a>オンプレミスの HSM で保護されたキーを作成して key vault に転送する

Hsm で保護されたキーをオンプレミスに作成し、それを HSM で保護されたキーとして key vault に転送するには、Azure Key Vault のドキュメントの「 [hsm で保護されたキーを生成して転送する方法](/azure/key-vault/keys/hsm-protected-keys-byok)」の手順に従って Azure Key Vault します。

転送されたキーを使用する Azure Information Protection には、次のようなすべての Key Vault 操作をキーに対して許可する必要があります。

- encrypt
- 復号化
- wrapKey
- unwrapKey
- sign
- 確認

既定では、すべての Key Vault 操作が許可されます。

特定のキーに対して許可されている操作を確認するには、次の PowerShell コマンドを実行します。

```ps
(Get-AzKeyVaultKey -VaultName <key vault name> -Name <key name>).Attributes.KeyOps
```

必要に応じて、 [AzKeyVaultKey](/powershell/module/az.keyvault/update-azkeyvaultkey) と *keyops* パラメーターを使用して、許可される操作を追加します。

#### <a name="configuring-azure-information-protection-with-your-key-id"></a>キー ID を使用した Azure Information Protection の構成

Azure Key Vault に格納されているキーには、キー ID があります。

キー ID は、キーコンテナーの名前、キーコンテナー、キーの名前、およびキーのバージョンを含む URL です。 例:

**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**.

キーコンテナーの URL を指定して、キーを使用するように Azure Information Protection を構成します。

#### <a name="authorizing-the-azure-rights-management-service-to-use-your-key"></a>キーを使用するように Azure Rights Management サービスを承認する

Azure Rights Management サービスは、キーを使用する権限を持っている必要があります。 Azure Key Vault 管理者は、Azure portal または Azure PowerShell を使用して、この承認を有効にすることができます。

##### <a name="enabling-key-authorization-using-the-azure-portal"></a>Azure portal を使用したキー承認の有効化

1. Azure portal にサインインし、[Key vault の **Key vaults**  >  **\<*your key vault name*>**  >  **アクセスポリシー**] [  >  **新規追加**] にアクセスします。

1. [ **アクセスポリシーの追加** ] ウィンドウで、[ **テンプレートからの構成 (オプション)** ] ボックスの一覧から [ **Azure Information Protection byok**] を選択し、[ **OK**] をクリックします。

    選択したテンプレートには次の構成が含まれます。

    - **Select principal** 値は **Microsoft Rights Management Services** に設定されています。
    - 選択した **キーのアクセス許可** には、 **Get、** **復号化、** および署名が含まれ **ます。**

##### <a name="enabling-key-authorization-using-powershell"></a>PowerShell を使用したキー承認の有効化

Key Vault PowerShell コマンドレット [AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)を実行し、GUID **00000012-0000-0000-c000-000000000000** を使用して Azure Rights Management サービスプリンシパルにアクセス許可を付与します。

例:

```ps
Set-AzKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get
```

##### <a name="enabling-key-authorization-for-managed-hsm-keys-via-azure-cli"></a>Azure CLI を使用した管理対象 HSM キーのキー承認の有効化

管理された **HSM 暗号化** ユーザーとして Azure Rights Management サービスプリンシパルのユーザーアクセス許可を付与するには、次のコマンドを実行します。

```PowerShell
az keyvault role assignment create --hsm-name "ContosoMHSM" --role "Managed HSM Crypto User" --assignee 00000012-0000-0000-c000-000000000000 --scope /keys/contosomhsmkey
```

各値の説明:
- **00000012-0000-0000-c000-000000000000** は、このコマンドで使用する GUID です。
- **ContosoMHSM** は、HSM のサンプル名です。 このコマンドを実行するときは、この値を独自の HSM 名に置き換えます。

管理された **Hsm 暗号化ユーザー** ユーザーロールを使用すると、ユーザーはキーの暗号化の解除、署名、およびアクセス許可の取得を行うことができます。これは、管理対象 hsm 機能に必要なすべての機能です。 

> [!NOTE]
> 管理対象 HSM がパブリックプレビューの間は、管理されている **Hsm 暗号化ユーザー** ロールを付与することは Azure CLI を通じてのみサポートされます。
> 

### <a name="configure-azure-information-protection-to-use-your-key"></a>キーを使用するように Azure Information Protection を構成する

上記のすべての手順を完了したら、このキーを組織のテナントキーとして使用するように Azure Information Protection を構成することができます。

Azure RMS コマンドレットを使用して、次のコマンドを実行します。

1. Azure Rights Management サービスに接続し、サインインします。
    ```ps
    Connect-AipService
    ```

1. キーの URL を指定して、 [AipServiceKeyVaultKey コマンドレット](/powershell/module/aipservice/use-aipservicekeyvaultkey)を実行します。 例:

    ```ps
    Use-AipServiceKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/<key-version>"
    ```

    > [!IMPORTANT]
    > この例で `<key-version>` は、は使用するキーのバージョンです。 バージョンを指定しない場合は、既定で現在のバージョンのキーが使用され、コマンドが動作するように見えることがあります。 ただし、キーが後で更新または更新された場合、 **AipServiceKeyVaultKey** コマンドを再度実行しても、Azure Rights Management サービスはテナントに対して機能しなくなります。
    >
    > 必要に応じて [AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey) コマンドを使用して、現在のキーのバージョン番号を取得します。
    >
    > 例: `Get-AzKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

    キーの URL が Azure Information Protection に対して正しく設定されていることを確認するには、Azure Key Vault で [AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey) コマンドを実行して、キーの url を表示します。

1. Azure Rights Management サービスが既にアクティブ化されている場合は、 [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) を実行して、このキーを azure Rights Management サービスのアクティブなテナントキーとして使用するように Azure Information Protection に指示します。

テナント用に自動的に作成された既定の Microsoft が作成したキーの代わりに、キーを使用するように Azure Information Protection が構成されるようになりました。

## <a name="next-steps"></a>次のステップ
BYOK 保護を構成したら、「 [テナントルートキー](get-started-tenant-root-keys.md) の概要」に進み、キーの使用と管理の詳細について説明します。