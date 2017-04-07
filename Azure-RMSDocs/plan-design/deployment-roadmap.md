---
title: "Azure Information Protection デプロイ ロードマップ"
description: "組織の Azure Information Protection を準備、実装、管理するには、これらの手順に従ってください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9300c6d06042a489dd256069da4faa88426df9aa
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="azure-information-protection-deployment-roadmap"></a>Azure Information Protection デプロイ ロードマップ

>*適用対象: Azure Information Protection、Office 365*

組織の Azure Information Protection を準備、実装、管理するには、次の手順に従ってください。

ただし、運用環境にロールアウトせずに、簡単に Azure Information Protection を試す場合は、「[Azure Information Protection のクイック スタート チュートリアル](../get-started/infoprotect-quick-start-tutorial.md)」を参照してください。

> [!IMPORTANT]
> 次の手順を実行する前に、「[Azure Information Protection の要件](../get-started/requirements-azure-rms.md)」を確認してください。

組織に適用できて、必要な[サブスクリプション](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)機能に対応するデプロイ ロードマップを選択します。

- [分類、ラベル付け、保護を使用する](#deployment-roadmap-for-classification-labeling-and-protection)

- [データ保護のみを使用する](#deployment-roadmap-for-data-protection-only)


## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>分類、ラベル付け、保護のデプロイ ロードマップ

> [!NOTE]
> データ保護のために Azure Rights Management サービスを既に使用していますか? これらの手順の多くを省略し、手順 3 と 5.1 だけ実行することもできます。

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>手順 1: サブスクリプションを確認し、ユーザー ライセンスを割り当てる
Azure Information Protection サイトの[サブスクリプション情報](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)と[機能一覧](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)を見て、必要な機能を含むサブスクリプションを組織が所有していることを確認します。 次に、文書や電子メールを分類し、ラベルを付け、保護する各ユーザーにこのサブスクリプションのライセンスを割り当てます。

注: ユーザー ライセンスを無料の個人用 RMS サブスクリプションから手動で割り当てることや、このライセンスを組織の Azure Rights Management サービスの管理目的で使用することはしないでください。 このようなライセンスは、Office 365 管理センターに **Rights Management Adhoc** と表示されるとともに、Azure AD PowerShell コマンドレット [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) を実行したときに **RIGHTSMANAGEMENT_ADHOC** と表示されます。 個人用 RMS サブスクリプションが自動的に付与されてユーザーに割り当てられるしくみの詳細については、「[個人用 RMS と Azure Information Protection](../understand-explore/rms-for-individuals.md)」を参照してください。


### <a name="step-2-prepare-your-tenant-account-to-use-azure-information-protection"></a>手順 2: Azure Information Protection を使用するためのテナント アカウントを用意する
Azure Information Protection の使用を開始する前に、次の準備を行います。

- 組織のユーザーを認証するために Azure Information Protection で利用される Office 365 または Azure Active Directory にユーザー アカウントとグループがあることを確認します。 必要に応じて、これらのアカウントとグループを作成するか、またはオンプレミスのディレクトリからそれらを同期します。 詳細については、「[Azure Information Protection の準備](prepare.md)」を参照してください。

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>手順 3: 分類とラベル付けを構成し、デプロイする

分類方法がまだ用意されていない場合、[既定の Azure Information Protection ポリシー](../deploy-use/configure-policy-default.md)を確認し、組織データに割り当てる分類ラベルを決める際の基準として利用します。 ビジネス要件に合わせてこれらをカスタマイズできます。 

分類決定をサポートするために必要な変更を行うには、既定の Azure Information Protection ラベルを再構成します。 ユーザーによる手動ラベル付けのポリシーを構成し、適用するラベルとタイミングを説明するユーザー ガイダンスを記述します。 Azure Information Protection ポリシーの構成方法については、「[Azure Information Protection ポリシーの構成](../deploy-use/configure-policy.md)」を参照してください。

次に、ユーザーの Azure Information Protection クライアントをデプロイし、ユーザー トレーニングとラベルの選択に関する指示を与えます。 クライアントのインストールとサポートの詳細については、「[Azure Information Protection クライアント管理者ガイド](../rms-client/client-admin-guide.md)」を参照してください。

しばらくしてユーザーが文書や電子メールのラベル付けに慣れたら、さらに高度な構成を導入します。 次のようなものが含まれます。

- 既定のラベルを適用する

- 下位の分類レベルのラベルを選択したとき、理由をユーザーに求める

- すべての文書や電子メールにラベルを付けるように要求する

- カスタマイズされたヘッダー、フッター、透かし

- 推奨事項や自動ラベル付けをサポートする条件

この段階では、文書や電子メールを保護するためのオプションを選択しないでください。

### <a name="step-4-prepare-for-rights-management-data-protection"></a>手順 4: Rights Management データ保護を準備する

ユーザーが文書や電子メールのラベル付けに慣れたら、最も機密性の高いデータのデータ保護を導入できます。 この段階では、Azure Rights Management サービスの次の準備が必要です。

1. マイクロソフトでテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 現時点では、Exchange Online を使用する場合、BYOK は使用できない点に注意してください。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

2. インターネットにアクセスできる&1; つ以上のコンピューターで [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 向けの Windows PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management サービス用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

3. 現在、オンプレミスの Rights Management サービスを使用している場合: キー、テンプレート、URL をクラウドに移行する統合を実行します。 詳細については、「[AD RMS から Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

4. 文書や電子メールの保護を開始できるように、Azure Rights Management サービスを有効にします。 段階的に展開する必要がある場合、特定のユーザーの使用量を制限するオンボーディング コントロールを構成します。 詳細については、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

必要に応じて、次の構成を考慮してください。

-   既定の権限ポリシー テンプレートが組織にとって十分でない場合はカスタム テンプレート。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

-   組織での Rights Management の使用方法を監視できるようにするための使用ログ。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。

### <a name="step-5-configure-your-azure-information-protection-policy-applications-and-services-for-rights-management-data-protection"></a>手順 5: Rights Management データ保護のために Azure Information Protection ポリシー、アプリケーション、サービスを構成する

1. Azure Information Protection ポリシーを更新し、データ保護を適用する
    
    1 つまたは複数のラベルで Rights Management 保護を適用できるように、Azure Information Protection ポリシーを変更します。 詳しくは、「[Rights Management による保護を適用するようにラベルを構成する方法](../deploy-use/configure-policy-protection.md)」を参照してください。
    
    Exchange が Information Rights Management (IRM) 用に構成されていない場合でも、ユーザーは Outlook で Rights Management による保護を適用するラベルを適用できます。 ただし、Exchange が IRM 用に構成されるまで、組織は Exchange で Azure Rights Management による保護を使用するすべての機能を利用できません。 この追加の構成は、Exchange Online の手順 3、および Exchange オンプレミスの手順 6 に含まれています。 

2. IRM のために Office のアプリケーションとサービスを構成する
    
    SharePoint Online または Exchange Online の Information Rights Management (IRM) 機能のために Office のアプリケーションとサービスを構成します。 詳細については、「[Azure Rights Management 用にアプリケーションを構成する](../deploy-use/configure-applications.md)」を参照してください。

3. データ回復のスーパー ユーザー機能を構成する
    
    Azure Rights Management によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure Rights Management のスーパー ユーザーとして構成します。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」を参照してください。

4. ファイルを一括して分類および保護する (必要な場合)
    
    ファイルの分類と保護と、分類と保護の削除に使用する PowerShell コマンドレットは、Azure Information Protection クライアントと共に自動的にインストールされます。 詳細については、管理者ガイドの「[Using PowerShell with the Azure Information Protection client](..\rms-client\client-admin-guide-powershell.md)」(Azure Information Protection クライアントでの PowerShell の使用) を参照してください。

6. オンプレミス サーバーのコネクタをデプロイする
    
    Azure Rights Management サービスで使用するオンプレミスのサービスがある場合は、Rights Management コネクタをインストールして構成します。 詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。

### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>手順 4: データ保護ソリューションを使用し、監視する
データを保護し、構成したラベルと Rights Management データ保護を会社がどのように使用しているかをログに記録する準備が整いました。 このデプロイ フェーズのサポートの詳細については、以下を参照してください。

- [Azure Rights Management サービスを利用したファイルの保護でユーザーを支援するヘルプ](../deploy-use/help-users.md)

-  [Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)

- [クライアント ファイルおよび使用状況ログの記録](../rms-client/client-admin-guide-files-and-logging.md)

Windows ベースのファイル サーバーで、ファイル分類インフラストラクチャを使用してファイルを自動的に保護することに関する情報は、「[Windows Server ファイル分類インフラストラクチャ (FCI) での RMS 保護](../rms-client/configure-fci.md)」を参照してください。

### <a name="step-5-administer-the-rights-management-service-for-your-tenant-account-as-needed"></a>手順 5: 必要に応じてテナント アカウントの Rights Management サービスを管理する
Azure Rights Management サービスの使用を開始するとき、Windows PowerShell のモジュールが管理変更のスクリプト化または自動化に役立つことがあります。 詳細については、「[Windows PowerShell を使用した Azure Rights Management サービスの管理](../deploy-use/administer-powershell.md)」を参照してください。


## <a name="deployment-roadmap-for-data-protection-only"></a>データ保護のみのデプロイ ロードマップ

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-azure-rights-management"></a>手順 1:Azure Rights Management を含むサブスクリプションがあることを確認します。
Azure Information Protection サイトの[サブスクリプション情報](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)と[機能一覧](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)を見て、必要な機能を含むサブスクリプションを組織が所有していることを確認します。 次に、Azure Rights Management サービスを利用して文書や電子メールを保護する、組織内の各ユーザーにこのサブスクリプションのライセンスを割り当てます。

注: ユーザー ライセンスを無料の個人用 RMS サブスクリプションから手動で割り当てることや、このライセンスを組織の Azure Rights Management サービスの管理目的で使用することはしないでください。 このようなライセンスは、Office 365 管理センターに **Rights Management Adhoc** と表示されるとともに、Azure AD PowerShell コマンドレット [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) を実行したときに **RIGHTSMANAGEMENT_ADHOC** と表示されます。 個人用 RMS サブスクリプションが自動的に付与されてユーザーに割り当てられるしくみの詳細については、「[個人用 RMS と Azure Information Protection](../understand-explore/rms-for-individuals.md)」を参照してください。


### <a name="step-2-prepare-your-tenant-account-to-use-the-azure-rights-management-service"></a>手順 2: Azure Rights Management サービスを使用するためにテナント アカウントを準備する
[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] を使用する前に、次の準備を行います。

1.  Office 365 テナントに、組織のユーザーを認証するのに Azure Information Protection で使用されるユーザー アカウントとグループが含まれていることを確認します。 必要に応じて、これらのアカウントとグループを作成するか、またはオンプレミスのディレクトリからそれらを同期します。 詳細については、「[Azure Rights Management の準備を行う](prepare.md)」を参照してください。

2. マイクロソフトでテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 現時点では、Exchange Online を使用する場合、BYOK は使用できない点に注意してください。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

3. インターネットにアクセスできる&1; つ以上のコンピューターで [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 向けの Windows PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

4. 現在、オンプレミスの Rights Management サービスを使用している場合: キー、テンプレート、URL をクラウドに移行する統合を実行します。 詳細については、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

5. サービスの使用を開始できるように Rights Management をアクティブ化します。 段階的に展開する必要がある場合、特定のユーザーの使用量を制限するオンボーディング コントロールを構成します。 詳細については、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

必要に応じて、次の構成を考慮してください。

-   既定の権限ポリシー テンプレートが組織にとって十分でない場合はカスタム テンプレート。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

-   組織での Rights Management の使用方法を監視できるようにするための使用ログ。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。

### <a name="step-3-install-the-client-and-configure-applications-and-services-for-rights-management"></a>手順 3: クライアントをインストールし、Rights Management のアプリケーションとサービスを構成する

1. Azure Information Protection クライアントのデプロイ
    
    Office 2010 のサポート、Office ドキュメントと電子メール以外のファイルの保護、保護されたドキュメントの追跡には、ユーザーに Azure Information Protection をインストールします。 このクライアントのユーザー トレーニングを行います。 詳細については、「[Azure Information Protection client for Windows](../rms-client/aip-client.md)」(Windows 用 Azure Information Protection クライアント) を参照してください。

2. IRM のために Office のアプリケーションとサービスを構成する
    
    SharePoint Online または Exchange Online の Information Rights Management (IRM) 機能のために Office のアプリケーションとサービスを構成します。 詳細については、「[Azure Rights Management 用にアプリケーションを構成する](../deploy-use/configure-applications.md)」を参照してください。

3. データ回復のスーパー ユーザー機能を構成する
    
    Azure Rights Management によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure Rights Management のスーパー ユーザーとして構成します。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」を参照してください。

4. ファイルを一括して保護する (必要な場合) 
    
    複数のファイルの種類を一括して保護する、または一括して保護を解除する PowerShell コマンドレットは、Azure Information Protection クライアントと共に自動的にインストールされます。 詳細については、管理者ガイドの「[Using PowerShell with the Azure Information Protection client](..\rms-client\client-admin-guide-powershell.md)」(Azure Information Protection クライアントでの PowerShell の使用) を参照してください。

5. オンプレミス サーバーのコネクタをデプロイする
    
    Azure Rights Management サービスで使用するオンプレミスのサービスがある場合は、Rights Management コネクタをインストールして構成します。 詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。


### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>手順 4: データ保護ソリューションを使用し、監視する
これでデータを保護し、組織で Rights Management を使用する方法を記録する準備が整いました。 このデプロイ段階の詳細については、「[Azure Rights Management サービスを利用したファイルの保護でユーザーを支援するヘルプ](../deploy-use/help-users.md)」と「[Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。

Windows ベースのファイル サーバーで、ファイル分類インフラストラクチャを使用してファイルを自動的に保護することに関する情報は、「[Windows Server ファイル分類インフラストラクチャ (FCI) での RMS 保護](../rms-client/configure-fci.md)」を参照してください。

### <a name="step-5-administer-the-rights-management-service-for-your-tenant-account-as-needed"></a>手順 5: 必要に応じてテナント アカウントの Rights Management サービスを管理する
Azure Rights Management サービスの使用を開始するとき、Windows PowerShell のモジュールが管理変更のスクリプト化または自動化に役立つことがあります。 詳細については、「[Windows PowerShell を使用した Azure Rights Management サービスの管理](../deploy-use/administer-powershell.md)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
