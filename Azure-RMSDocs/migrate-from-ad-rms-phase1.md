---
title: AD RMS から Azure Information Protection への移行 - フェーズ 1
description: AD RMS から Azure Information Protection への移行のフェーズ 1 には、手順 1 から 3 が含まれます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d954d3ee-3c48-4241-aecf-01f4c75fa62c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b5a27e874af808136274a50d25310d722f399032
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181635"
---
# <a name="migration-phase-1---preparation"></a>移行フェーズ 1 - 準備

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

AD RMS から Azure Information Protection への移行フェーズ 1 では、次の情報を使用してください。 この手順では「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 1 から 3 について説明し、ユーザーに影響を与えずに移行の環境を準備します。


## <a name="step-1-install-the-aadrm-powershell-module-and-identify-your-tenant-url"></a>手順 1:AADRM PowerShell モジュールをインストールし、自分のテナント URL を特定する

Azure Information Protection のデータ保護を指定するサービスを構成および管理できるように、AADRM モジュールをインストールします。

手順については、「[AADRM PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。

> [!NOTE]
> この Windows PowerShell モジュールを既にダウンロードしている場合は、`(Get-Module aadrm -ListAvailable).Version` コマンドを実行して、バージョン番号が **2.9.0.0** 以上であることを確認します。

移行手順の一部では、\<*実際のテナント URL*\> が参照されたときに置き換えることができるように、テナントの Azure Rights Management サービス URL を確認しておく必要があります。 Azure Rights Management サービス URL は、**<GUID>.rms.<リージョン>.aadrm.com** という形式です。

以下に例を示します。**5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

### <a name="to-identify-your-azure-rights-management-service-url"></a>Azure Rights Management サービス URL を確認するには

1. Azure Rights Management サービスに接続し、求められたら、テナントのグローバル管理者の資格情報を入力します。
    
        Connect-AadrmService
    
2. テナントの構成を取得します。
    
        Get-AadrmConfiguration
    
3. **LicensingIntranetDistributionPointUrl** の値をコピーし、この文字列から `/_wmcs\licensing` を除去します。 
    
    残りの部分が Azure Information Protection テナントの Azure Rights Management サービス URL に相当します。 この値は後続の移行指示で、多くの場合、*YourTenantURL* という短縮形式で表現されています。
    
    次の PowerShell コマンドを実行することで、値が正しいことを確認できます。
    
            (Get-AadrmConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

## <a name="step-2-prepare-for-client-migration"></a>手順 2. クライアントの移行を準備する

ほとんどの移行では、すべてのクライアントを一度に移行するのは実際的ではないため、少しずつクライアントを移行することがよくあります。 つまり、Azure Information Protection を使用するクライアントとまだ AD RMS を使用するクライアントが共存する期間があります。 移行前と移行後の両方のユーザーをサポートするには、オンボーディング制御を使用し、移行前のスクリプトをデプロイします。 まだ移行されていないユーザーが、Azure Rights Management を使用する移行の済んだユーザーによって保護されているコンテンツを使用できるように、移行プロセスの間はこの手順が必要です。

1. たとえば **AIPMigrated** といった名前のグループを作成します。 このグループは、Active Directory で作成してクラウドに同期しても、Office 365 または Azure Active Directory で作成してもかまいません。 この時点では、このグループにユーザーを割り当てないでください。 後の手順でユーザーを移行するときに、このグループに追加します。

    このグループのオブジェクト ID を記録しておきます。 そのためには、Azure AD PowerShell を使います。たとえば、バージョン 1.0 のモジュールについては、[Get-MsolGroup](/powershell/msonline/v1/Get-MsolGroup) コマンドを使います。 または、Azure Portal から、グループのオブジェクト ID をコピーしてもかまいません。

2. このグループをオンボーディング制御用に構成し、このグループのメンバーのみが Azure Rights Management を使ってコンテンツを保護できるようにします。 そのためには、PowerShell セッションで Azure Rights Management サービスに接続し、メッセージが表示されたら、グローバル管理者の資格情報を指定します。

        Connect-Aadrmservice

    その後、このグループをオンボーディング制御用に構成し、この例のオブジェクト ID を実際のグループ オブジェクト ID に置き換えて、確認を求められたら「**Y**」と入力します。

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fba99fed-32a0-44e0-b032-37b419009501" -Scope WindowsApp

3. クライアント移行スクリプトが含まれる[次のファイルをダウンロード](https://go.microsoft.com/fwlink/?LinkId=524619)します。
    
    **Migration-Scripts.zip**
    
4. ファイルを抽出し、**Prepare-Client.cmd** の指示に従って、実際の AD RMS クラスター エクストラネット ライセンス URL のサーバー名が含まれるようにします。 
    
    この名前を見つけるには: Active Directory Rights Management サービス コンソールで、クラスターの名前をクリックします。 **[クラスターの詳細]** で、[エクストラネット クラスターの URL] セクションの **[ライセンス]** からサーバー名をコピーします。 例: **rmscluster.contoso.com**。

    > [!IMPORTANT]
    > この手順では、**adrms.contoso.com** のアドレスの例を実際の AD RMS サーバーのアドレスに置き換えます。 これを行うときは、アドレスの前または後に余計なスペースが入らないように注意してください。余計なスペースがあると、移行スクリプトが中断し、問題の根本原因の特定が非常に困難になります。 編集ツールによっては、テキストを貼り付けた後でスペースが自動的に追加されることがあります。
    >

5. このスクリプトをすべての Windows コンピューターにデプロイして、クライアントの移行を始めるときに、まだ移行されていないクライアントが、Azure Rights Management サービスを使うようになっている移行の済んだクライアントによって保護されているコンテンツを使用する場合に、AD RMS と通信できるようにします。

    グループ ポリシーまたは他のソフトウェア展開メカニズムを使って、このスクリプトを展開できます。

## <a name="step-3-prepare-your-exchange-deployment-for-migration"></a>手順 3. Exchange の展開を移行用に準備する

オンプレミスの Exchange または Exchange Online を使っている場合、Exchange と AD RMS デプロイを統合している可能性があります。 この手順ではそれを、既存の AD RMS の構成を使用し、Azure RMS によって保護されるコンテンツをサポートするように構成します。 

[実際のテナントの Azure Rights Management サービス URL](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url) を確認しておき、次のコマンドの *&lt;YourTenantURL&gt;* をその値に置き換えることができるようにします。 

**Exchange Online を AD RMS と統合している場合**: Exchange Online PowerShell セッションを開き、以下の PowerShell コマンドを 1 つずつ、またはスクリプト内で実行します。

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -internallicensingenabled $true 

**オンプレミスの Exchange を AD RMS と統合している場合**: Exchange 組織ごとに、まず各 Exchange サーバー上でレジストリ値を追加してから PowerShell コマンドを実行します。 

Exchange 2013 と Exchange 2016 のレジストリ値:

**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**次のように入力します。** Reg_SZ

**値:** https://\<実際のテナント URL\>/_wmcs/licensing

**データ:** https://\<AD RMS エクストラネット ライセンス URL\>/_wmcs/licensing

---

Exchange 2010 のレジストリ値:

**レジストリ パス:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**次のように入力します。** Reg_SZ

**値:** https://\<実際のテナント URL\>/_wmcs/licensing

**データ:** https://\<AD RMS エクストラネット ライセンス URL>/_wmcs/licensing

---

1 つずつ、またはスクリプト内で実行する PowerShell コマンド

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -RefreshServerCertificates
    Set-IRMConfiguration -internallicensingenabled $true
    IISReset


Exchange Online またはオンプレミスの Exchange に対してこれらのコマンドを実行すると、移行前に AD RMS によって保護されたコンテンツをサポートするように構成されていた Exchange 展開は、移行後も Azure RMS によって保護されたコンテンツをサポートします。 Exchange 展開では、後の移行手順まで、引き続き AD RMS を使って保護されたコンテンツをサポートします。


## <a name="next-steps"></a>次の手順
「[フェーズ 2: サーバー側の構成](migrate-from-ad-rms-phase2.md)」に進みます。

