---
title: Azure RMS および AD RMS 用の環境を準備する
description: Azure Rights Management が AD RMS デプロイされている場合の管理者向けガイダンス。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f4bbef451f161f40d29a7a890161592db76373a5
ms.sourcegitcommit: 24c97b58849af4322d3211b8d3165734d5ad6c88
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "95569966"
---
# <a name="prepare-the-environment-for-azure-rights-management-when-you-have-ad-rms"></a>AD RMS がある場合に Azure Rights Management 用に環境を準備する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Active Directory Rights Management サービス (AD RMS) を使用する場合のガイダンス

Azure Rights Management サービスがアクティブ化されていて、かつ AD RMS も使用している場合、この組み合わせには互換性がありません。 追加の手順を行うことなく、一部のコンピューターでは、Azure Rights Management サービスの使用が自動的に開始され、AD RMS クラスターへの接続も行われる場合があります。 このシナリオはサポートされておらず、信頼できる結果が得られないため、追加の手順を実行することが重要です。 

**AD RMS をデプロイしているかどうかを確認するには:**

1. オプションとはいえ、ほとんどの AD RMS デプロイでは、ドメイン コンピューターが AD RMS クラスターを検出できるように Active Directory にサービス接続ポイント (SCP) を発行しています。 
    
    Active Directory に SCP を発行しているかどうかを確認するには、ADSI Edit を使用します: `CN=Configuration [server name], CN=Services, CN=RightsManagementServices, CN=SCP`

2. SCP を使用していない場合、AD RMS クラスターに接続する Windows コンピューターでは、Windows レジストリを使用してクライアント側のサービスの検出またはライセンスのリダイレクトを構成する必要があります: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation` または `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\ServiceLocation`
    
    これらのレジストリ構成について詳しくは、「[Windows レジストリを使用してクライアント側のサービスの検出を有効にする](./rms-client/client-deployment-notes.md#enabling-client-side-service-discovery-by-using-the-windows-registry)」と「[ライセンス サーバーのトラフィックのリダイレクト](./rms-client/client-deployment-notes.md#redirecting-licensing-server-traffic)」をご覧ください。   

組織に AD RMS がデプロイされる場合は、Azure Information Protection に移行可能かどうかを検討してください。 Azure Information Protection には、AD RMS よりも優れた点が多数あります。 たとえば、モバイルデバイスのサポートが強化され、Exchange Server や SharePoint Server と共に Microsoft 365 サービスとの統合が実現しています。 詳細については、「[Azure Information Protection と AD RMS の比較](compare-on-premise.md)」をご覧ください。

Azure Information Protection に移行すると、以前に保護されていたコンテンツにアクセスできなくなり、コンテンツを保護または保護解除する必要がなくなります。 AD RMS によって保護されたドキュメントと電子メールは、AD RMS をプロビジョニング解除した後でも開くことができます。

Azure Information Protection に移行する場合でも、制限事項を受け入れて現在の AD RMS デプロイを使用する場合でも、Azure Rights Management サービスが非アクティブ化されていることをまず確認する必要があります。 手順については、該当するシナリオ向けの手順に従います。

- [Azure Rights Management を含むサブスクリプションが2018年2月以降に購入されました](#your-subscription-was-purchased-during-or-after-february-2018)

- [サブスクリプションの購入が 2018 年 2 月以前であり、Exchange Online がある場合](#your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online)

- [Azure Portal で Azure Information Protection ポリシーを構成するときに保護をアクティブにするためのオプションが表示される場合](#you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection)


## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>2018 年 2 月以降に購入したサブスクリプション

2018 年 2 月末日まで、Azure Information Protection を含む新しいサブスクリプションでは、既定により Azure Rights Management サービスがアクティブになります。 このサービスが自動的にアクティブ化されていて、Active Directory Rights Management サービス (AD RMS) も使用している場合は、この組み合わせには互換性がありません。したがって、でくるだけ早く Azure Rights Management サービスを非アクティブ化することが重要です。 

### <a name="step-1-deactivate-azure-rights-management"></a>手順 1: Azure Rights Management を非アクティブ化する
Azure Rights Management を非アクティブ化するには、次のいずれかの手順を使用します。

> [!TIP]
> また、Windows PowerShell コマンドレットである [-AipService](/powershell/module/aipservice/disable-aipservice)を使用して、Azure Rights Management サービスを非アクティブ化することもできます。

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>Microsoft 365 管理センターから Rights Management を非アクティブ化するには

1. Microsoft 365 管理者の [Rights Management のページ](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) にアクセスします。
    
    サインインを求めるメッセージが表示された場合は、Microsoft 365 のグローバル管理者であるアカウントを使用します。

2. [**Rights Management**] ページで、[**非アクティブ化**] をクリックします。

3.  **[Rights Management を非アクティブ化しますか?]** というメッセージが表示されたら、**[非アクティブ化]** をクリックします。

"**Rights Management はアクティブ化されていません**" というテキストと、アクティブ化するオプションが表示されます。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Azure ポータルから Rights Management を非アクティブ化するには

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。
    
    以前に Azure Information Protection ウィンドウにアクセスしていない場合は、このウィンドウをポータルに追加するための1回限りの [追加の手順](configure-policy.md#to-access-the-azure-information-protection-pane-for-the-first-time) を参照してください。

2. メニュー オプションで、**[保護のアクティブ化]** を選択します。 

3.  [ **Azure Information Protection 保護のアクティブ化** ] ウィンドウで、[ **非アクティブ化**] を選択します。 **[はい]** を選択して選択肢を確定します。

情報バーに **[非アクティブ化が正常に完了しました]\(Deactivation finished successfully\)** と表示され、**[非アクティブ化]** が **[アクティブ化]** に変わります。 

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行のガイダンスについては、「 [AD RMS から Azure Information Protection への](migrate-from-ad-rms-to-azure-rms.md)移行」を参照してください。


## <a name="your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online"></a>サブスクリプションの購入が 2018 年 2 月以前であり、Exchange Online がある場合

サブスクリプションに Azure Rights Management または Azure Information Protection が含まれ、かつテナントで Exchange Online を使用している場合、Microsoft ではこれらのサブスクリプションの Azure Rights Management サービスのアクティブ化を開始しています。 これらのテナントに対して、自動アクティブ化は 2018 年 8 月 1 日にロール アウトを開始します。

サービスが自動的にアクティブ化され、かつ AD RMS を使用している場合、この組み合わせには互換性がないため、サービスの自動更新からテナントを除外することが重要です。 

### <a name="step-1-opt-out-from-the-automatic-service-update"></a>手順 1: サービスの自動更新から除外する

次の [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration) Exchange Online PowerShell コマンドを使用します: `Set-IRMConfiguration -AutomaticServiceUpdateEnabled $false`

[詳細情報](https://support.office.com/article/protection-features-in-azure-information-protection-rolling-out-to-existing-office-365-tenants-7ad6f58e-65d7-4c82-8e65-0b773666634d) 

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行のガイダンスについては、「 [AD RMS から Azure Information Protection への](migrate-from-ad-rms-to-azure-rms.md)移行」を参照してください。


## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Azure Information Protection を構成する際に保護をアクティブにするためのオプションが表示される

**Azure Information Protection 保護のアクティブ化** ウィンドウには、Azure Rights Management サービスをアクティブ化するオプションがあります。  

AD RMS も使用している場合は、**[アクティブ化]** オプションを選択しないでください。 Azure Rights Management サービスがアクティブになっていない場合でも、分類のみを適用するラベルには Azure Information Protection を使用できます。 データ保護を含まない特別な既定ポリシーが自動的に作成されます。これらの構成オプションは、Azure Rights Management サービスがアクティブになるまで使用不可のままです。

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>手順 1: 分類とラベル付けのために Azure Information Protection ポリシーを構成する (保護なし)

[ **Azure Information Protection ラベル** ] ウィンドウで、データ保護のオプションを含まないラベルを表示および構成します。 ラベルとポリシーの設定を構成する方法について詳しくは、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行のガイダンスについては、「 [AD RMS から Azure Information Protection への](migrate-from-ad-rms-to-azure-rms.md)移行」を参照してください。

### <a name="step-3-configure-labels-for-protection"></a>手順 3: 保護のためのラベルを構成する

移行プロセスの一環として Azure Rights Management サービスをアクティブにした後で、データ保護のためにラベルを構成できます。 ただし、ユーザーをバッチで移行する場合は、保護を適用するラベルの範囲が移行対象のユーザーのみに指定されていることを確認してください。


