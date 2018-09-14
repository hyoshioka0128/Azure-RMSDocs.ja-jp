---
title: Azure RMS および AD RMS 用の環境を準備する
description: AD RMS がデプロイされた Azure Rights Management の場合のガイダンス。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/29/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d93e761db545ac9934ca04f7cad148203cdb8c12
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2018
ms.locfileid: "44151777"
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Active Directory Rights Management サービス (AD RMS) もある場合の Azure Rights Management 用の環境の準備

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Active Directory Rights Management サービス (AD RMS) を使用する場合のガイダンス

Azure Rights Management サービスがアクティブ化されていて、かつ AD RMS も使用している場合、この組み合わせには互換性がありません。 追加の手順を行うことなく、一部のコンピューターでは、Azure Rights Management サービスの使用が自動的に開始され、AD RMS クラスターへの接続も行われる場合があります。 このシナリオはサポートされておらず、信頼できる結果が得られないため、追加の手順を実行することが重要です。 

**AD RMS をデプロイしているかどうかを確認するには:**

1. オプションとはいえ、ほとんどの AD RMS デプロイでは、ドメイン コンピューターが AD RMS クラスターを検出できるように Active Directory にサービス接続ポイント (SCP) を発行しています。 
    
    Active Directory に SCP を発行しているかどうかを確認するには、ADSI Edit を使用します: `CN=Configuration [server name], CN=Services, CN=RightsManagementServices, CN=SCP`

2. SCP を使用していない場合、AD RMS クラスターに接続する Windows コンピューターでは、Windows レジストリを使用してクライアント側のサービスの検出またはライセンスのリダイレクトを構成する必要があります: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation` または `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\ServiceLocation`
    
    これらのレジストリ構成について詳しくは、「[Windows レジストリを使用してクライアント側のサービスの検出を有効にする](./rms-client/client-deployment-notes.md#enabling-client-side-service-discovery-by-using-the-windows-registry)」と「[ライセンス サーバーのトラフィックのリダイレクト](./rms-client/client-deployment-notes.md#redirecting-licensing-server-traffic)」をご覧ください。   

組織に AD RMS がデプロイされる場合は、Azure Information Protection に移行可能かどうかを検討してください。 Azure Information Protection には、AD RMS よりも優れた点が多数あります。 たとえば、モバイル デバイスのサポート強化や、Exchange Server や SharePoint Server に加えて Office 365 サービスとの統合を備えています。 詳細については、「[Azure Information Protection と AD RMS の比較](compare-on-premise.md)」をご覧ください。

Azure Information Protection に移行しても、以前に保護されていたコンテンツへのアクセスを失うことはありません。また、コンテンツの保護の解除したり、コンテンツを再保護する必要はありません。 AD RMS をプロビジョニング解除した後でも、AD RMS によって保護されていたドキュメントと電子メールを引き続き開くことができます。

Azure Information Protection に移行する場合でも、制限事項を受け入れて現在の AD RMS デプロイを使用する場合でも、Azure Rights Management サービスが非アクティブ化されていることをまず確認する必要があります。 手順については、該当するシナリオ向けの手順に従います。

- [2018 年 2 月以降に購入した Azure Rights Management を含むサブスクリプションの場合](#your-subscription-was-purchased-during-or-after-february-2018)

- [サブスクリプションの購入が 2018 年 2 月以前であり、Exchange Online がある場合](#your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online)

- [Azure Portal で Azure Information Protection ポリシーを構成するときに保護をアクティブにするためのオプションが表示される場合](#you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection)


## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>2018 年 2 月以降に購入したサブスクリプション

2018 年 2 月末日まで、Azure Information Protection を含む新しいサブスクリプションでは、既定により Azure Rights Management サービスがアクティブになります。 このサービスが自動的にアクティブ化されていて、Active Directory Rights Management サービス (AD RMS) も使用している場合は、この組み合わせには互換性がありません。したがって、でくるだけ早く Azure Rights Management サービスを非アクティブ化することが重要です。 

### <a name="step-1-deactivate-azure-rights-management"></a>手順 1: Azure Rights Management を非アクティブ化する
Azure Rights Management を非アクティブ化するには、次のいずれかの手順を使用します。

> [!TIP]
> Windows PowerShell の [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) コマンドレットを使用して Azure Rights Management サービスを非アクティブ化することもできます。

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Office 365 管理センターから Rights Management を非アクティブ化するには

1. Office 365 管理者向けの [Rights Management ページ](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) に移動します。
    
    サインインを求められたら、Office 365 のグローバル管理者であるアカウントを使用します。

2. **[Rights Management]** ページで、**[非アクティブ化]** をクリックします。

3.  **[Rights Management を非アクティブ化しますか?]** というメッセージが表示されたら、**[非アクティブ化]** をクリックします。

**[Rights Management がアクティブ化されていません]** というテキストとアクティブ化するオプションが表示されます。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Azure ポータルから Rights Management を非アクティブ化するには

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
    以前に [Azure Information Protection] ブレードにアクセスしたことがない場合、このブレードをポータルに追加するには、1 回限りの[追加の手順](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time)を参照してください。

2. メニュー オプションで、**[保護のアクティブ化]** を選択します。 

3.  **[Azure Information Protection - Protection activation]\(Azure Information Protection - 保護のアクティブ化\)** ブレードで、**[非アクティブ化]** を選びます。 **[はい]** を選択して選択肢を確定します。

情報バーに **[非アクティブ化が正常に完了しました]\(Deactivation finished successfully\)** と表示され、**[非アクティブ化]** が **[アクティブ化]** に変わります。 

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行ガイダンス「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」をご覧ください


## <a name="your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online"></a>サブスクリプションの購入が 2018 年 2 月以前であり、Exchange Online がある場合

サブスクリプションに Azure Rights Management または Azure Information Protection が含まれ、かつテナントで Exchange Online を使用している場合、Microsoft ではこれらのサブスクリプションの Azure Rights Management サービスのアクティブ化を開始しています。 これらのテナントに対して、自動アクティブ化は 2018 年 8 月 1 日にロール アウトを開始します。

サービスが自動的にアクティブ化され、かつ AD RMS を使用している場合、この組み合わせには互換性がないため、サービスの自動更新からテナントを除外することが重要です。 

### <a name="step-1-opt-out-from-the-automatic-service-update"></a>手順 1: サービスの自動更新から除外する

次の [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration) Exchange Online PowerShell コマンドを使用します: `Set-IRMConfiguration -AutomaticServiceUpdateEnabled $false`

[詳細情報](https://support.office.com/article/protection-features-in-azure-information-protection-rolling-out-to-existing-office-365-tenants-7ad6f58e-65d7-4c82-8e65-0b773666634d) 

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行ガイダンス「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」をご覧ください


## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Azure Information Protection を構成する際に保護をアクティブにするためのオプションが表示される

**[Azure Information Protection - 保護のアクティブ化]** のブレードには、Azure Rights Management サービスをアクティブ化するためのオプションがあります。  

AD RMS も使用している場合は、**[アクティブ化]** オプションを選択しないでください。 Azure Rights Management サービスがアクティブになっていない場合でも、分類のみを適用するラベルで Azure Information Protection を使用できます。 データ保護を含まない特別な既定ポリシーが自動的に作成されます。これらの構成オプションは、Azure Rights Management サービスがアクティブになるまで使用不可のままです。

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>手順 1: 分類とラベル付けのために Azure Information Protection ポリシーを構成する (保護なし)

**[Azure Information Protection - ラベル]** ブレードから、データ保護のためのオプションが含まれていないラベルを表示して構成します。 ラベルとポリシーの設定を構成する方法について詳しくは、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。

### <a name="step-2-start-planning-for-migration"></a>手順 2: 移行の計画を開始する

移行ガイダンス「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」をご覧ください

### <a name="step-3-configure-labels-for-protection"></a>手順 3: 保護のためのラベルを構成する

移行プロセス時に Azure Rights Management サービスをアクティブにした場合は、データ保護のためにラベルを構成できます。 ただし、ユーザーをバッチで移行する場合は、保護を適用するラベルの範囲が移行対象のユーザーのみに指定されていることを確認してください。


