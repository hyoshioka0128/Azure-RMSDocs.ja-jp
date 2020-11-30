---
title: AD RMS から Azure Information Protection への移行 - フェーズ 1
description: AD RMS から Azure Information Protection への移行のフェーズ 1 には、手順 1 から 3 が含まれます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d954d3ee-3c48-4241-aecf-01f4c75fa62c
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 13c63f2e96b27a31b9afb91fbc8c03b9b198f9c1
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316825"
---
# <a name="migration-phase-1---preparation"></a>移行フェーズ 1 - 準備

>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

AD RMS から Azure Information Protection への移行フェーズ 1 では、次の情報を使用してください。 この手順では「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 1 から 3 について説明し、ユーザーに影響を与えずに移行の環境を準備します。

## <a name="step-1-install-the-aipservice-powershell-module-and-identify-your-tenant-url"></a>手順 1: AIPService PowerShell モジュールをインストールし、テナントの URL を指定する

**Aipservice** モジュールをインストールして、Azure Information Protection のデータ保護を提供するサービスを構成および管理できるようにします。

手順については、「 [AIPService PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。

移行手順の一部を完了するには、テナントの Azure Rights Management サービスの URL を把握しておく必要があります。これにより、への参照が表示されたときに、その URL をに置き換えることができ *\<Your Tenant URL\>* ます。 

Azure Rights Management サービス URL は、**<GUID>.rms.<リージョン>.aadrm.com** という形式です。 例: **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

### <a name="to-identify-your-azure-rights-management-service-url"></a>Azure Rights Management サービス URL を確認するには

1. Azure Rights Management サービスに接続し、求められたら、テナントのグローバル管理者の資格情報を入力します。

    ```PowerShell
    Connect-AipService
    ```

2. テナントの構成を取得します。

    ```PowerShell
    Get-AipServiceConfiguration
    ```

3. **LicensingIntranetDistributionPointUrl** の値をコピーし、この文字列から `/_wmcs\licensing` を除去します。

    残りの部分が Azure Information Protection テナントの Azure Rights Management サービス URL に相当します。 この値は後続の移行指示で、多くの場合、*YourTenantURL* という短縮形式で表現されています。

    次の PowerShell コマンドを実行することで、値が正しいことを確認できます。

    ```PowerShell
    (Get-AipServiceConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]
    ```

## <a name="step-2-prepare-for-client-migration"></a>手順 2. クライアントの移行を準備する

ほとんどの移行では、すべてのクライアントを一度に移行するのは実際的ではないため、少しずつクライアントを移行することがよくあります。 

つまり、Azure Information Protection を使用するクライアントとまだ AD RMS を使用するクライアントが共存する期間があります。 移行前と移行後の両方のユーザーをサポートするには、オンボーディング制御を使用し、移行前のスクリプトをデプロイします。 

> [!NOTE]
> まだ移行されていないユーザーが、Azure Rights Management を使用する移行の済んだユーザーによって保護されているコンテンツを使用できるように、移行プロセスの間はこの手順が必要です。
> 

**クライアントの移行を準備するには**

1. たとえば **AIPMigrated** といった名前のグループを作成します。 このグループは Active Directory で作成し、クラウドに同期することも、Microsoft 365 または Azure Active Directory で作成することもできます。 

    この時点では、このグループにユーザーを割り当てないでください。 後の手順でユーザーを移行するときに、このグループに追加します。

1. 次のいずれかの方法を使用して、このグループのオブジェクト ID を書き留めておきます。

    - **Azure AD PowerShell を使用します。** たとえば、モジュールのバージョン1.0 では、 [get-msolgroup](/powershell/msonline/v1/Get-MsolGroup) コマンドを使用します。 
    - Azure portal からグループの **オブジェクト ID をコピー** します。

1. このグループをオンボーディング制御用に構成し、このグループのメンバーのみが Azure Rights Management を使ってコンテンツを保護できるようにします。 

    これを行うには、PowerShell セッションで Azure Rights Management サービスに接続します。 プロンプトが表示されたら、グローバル管理者の資格情報を指定します。

    ```PowerShell
    Connect-AipService
    ```

    このグループをオンボードコントロール用に構成し、この例のグループオブジェクト ID を使用します。 プロンプトが表示されたら、「 **Y** 」と入力して確認します。

    ```PowerShell
    Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fba99fed-32a0-44e0-b032-37b419009501" -Scope WindowsApp
    ```

1. [**Migration-Scripts.zip**](https://go.microsoft.com/fwlink/?LinkId=524619)ファイルをダウンロードします。

1. ファイルを抽出し、 **Prepare-Client** の指示に従って、AD RMS クラスターのエクストラネットライセンス URL のサーバー名が含まれるようにします。 この名前を見つけるには、次の手順を実行します。

    1. Active Directory Rights Management サービス コンソールで、クラスターの名前をクリックします。 

    1. **[クラスターの詳細]** で、[エクストラネット クラスターの URL] セクションの **[ライセンス]** からサーバー名をコピーします。 例: **rmscluster.contoso.com**。

    > [!IMPORTANT]
    > この手順では、**adrms.contoso.com** のアドレスの例を実際の AD RMS サーバーのアドレスに置き換えます。 
    >
    > これを行うときは、アドレスの前または後に追加のスペースがないことに注意してください。 余分なスペースは移行スクリプトを分割し、問題の根本原因として特定するのは非常に困難です。 
    >
    > 編集ツールによっては、テキストを貼り付けた後でスペースが自動的に追加されることがあります。
    >

5. このスクリプトをすべての Windows コンピューターにデプロイして、クライアントの移行を始めるときに、まだ移行されていないクライアントが、Azure Rights Management サービスを使うようになっている移行の済んだクライアントによって保護されているコンテンツを使用する場合に、AD RMS と通信できるようにします。

    グループ ポリシーまたは他のソフトウェア展開メカニズムを使って、このスクリプトを展開できます。

## <a name="step-3-prepare-your-exchange-deployment-for-migration"></a>手順 3. Exchange の展開を移行用に準備する

オンプレミスの Exchange または Exchange Online を使っている場合、Exchange と AD RMS デプロイを統合している可能性があります。 この手順ではそれを、既存の AD RMS の構成を使用し、Azure RMS によって保護されるコンテンツをサポートするように構成します。

[実際のテナントの Azure Rights Management サービス URL](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url) を確認しておき、次のコマンドの *&lt;YourTenantURL&gt;* をその値に置き換えることができるようにします。

Exchange on-premises または Exchange Online を AD RMS と統合しているかどうかに応じて、次のいずれかの操作を行います。

- [オンプレミスの Exchange と AD RMS の統合](#if-you-have-integrated-exchange-on-premises-with-ad-rms)
- [AD RMS を使用した Exchange Online の統合](#if-you-have-integrated-exchange-online-with-ad-rms)
### <a name="if-you-have-integrated-exchange-online-with-ad-rms"></a>Exchange Online を AD RMS と統合している場合

1. Exchange Online PowerShell セッションを開きます。

1. 次の PowerShell コマンドを1つずつ、またはスクリプトで実行します。

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -internallicensingenabled $true 
    ```

### <a name="if-you-have-integrated-exchange-on-premises-with-ad-rms"></a>オンプレミスの Exchange を AD RMS と統合している場合

各 exchange 組織について、各 Exchange サーバーでレジストリ値を追加し、PowerShell コマンドを実行します。

1. Exchange 2013 または Exchange 2016 を使用している場合は、次のレジストリ値を追加します。

    - **レジストリパス:**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection`

    - **種類:** Reg_SZ

    - **値:** `https://\<Your Tenant URL\>/_wmcs/licensing`

    - **データ:**`https://\<AD RMS Extranet Licensing URL\>/_wmcs/licensing`

1. 次の PowerShell コマンドを1つずつ、またはスクリプトで実行します。

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -RefreshServerCertificates
    Set-IRMConfiguration -internallicensingenabled $true
    IISReset
    ```

Exchange Online またはオンプレミスの Exchange に対してこれらのコマンドを実行すると、移行前に AD RMS によって保護されたコンテンツをサポートするように構成されていた Exchange 展開は、移行後も Azure RMS によって保護されたコンテンツをサポートします。 

Exchange 展開では、後の移行手順まで、引き続き AD RMS を使って保護されたコンテンツをサポートします。

## <a name="next-steps"></a>次のステップ

「[フェーズ 2: サーバー側の構成](migrate-from-ad-rms-phase2.md)」に進みます。
