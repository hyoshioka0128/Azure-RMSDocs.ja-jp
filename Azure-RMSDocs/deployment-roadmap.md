---
title: Azure Information Protection デプロイ ロードマップ
description: 組織の Azure Information Protection を準備、実装、管理するには、これらの手順に従ってください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2220572757081ad35a90a2dcebb23531e1ebee14
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68788811"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Azure Information Protection デプロイ ロードマップ

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

組織の Azure Information Protection を準備、実装、管理するための推奨事項として、次の手順に従ってください。

ただし、シナリオに基づく手順をお探しの場合は、「[How to guides for common scenarios that use Azure Information Protection (Azure Information Protection を使用する一般的なシナリオ向けの攻略ガイド)](how-to-guides.md)」を参照してください。

> [!NOTE]
> 製品リリースのロードマップをお探しの場合は、「[新しいリリースと更新プログラムに関する情報](information-support.md#information-about-new-releases-and-updates)」セクションを参照してください。

### <a name="identify-your-deployment-roadmap"></a>デプロイ ロードマップを特定する

次のいずれかの手順を実行して Azure Information Protection をデプロイする前に、「[Azure Information Protection の要件](./requirements.md)」を確認してください。

次に、ご自分の組織に適用可能で、必要な[サブスクリプション機能](https://azure.microsoft.com/pricing/details/information-protection/)に一致するデプロイ ロードマップを選択します。

- [分類、ラベル付け、保護を使用する](#deployment-roadmap-for-classification-labeling-and-protection)

- [データ保護のみを使用する](#deployment-roadmap-for-data-protection-only)


## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>分類、ラベル付け、保護のデプロイ ロードマップ

> [!NOTE]
> 既に Azure Information Protection の保護機能を使用している場合は、 これらの手順の多くを省略し、手順 3 と 5.1 だけ実行することもできます。

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>手順 1:サブスクリプションを確認し、ユーザー ライセンスを割り当てる
「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)」ページのサブスクリプション情報と機能一覧を見て、必要な機能を含むサブスクリプションを組織が所有していることを確認します。 次に、文書や電子メールを分類し、ラベルを付け、保護する各ユーザーにこのサブスクリプションのライセンスを割り当てます。

メモ:ユーザー ライセンスを無料の個人用 RMS サブスクリプションから手動で割り当てることや、このライセンスを組織の Azure Rights Management サービスの管理目的で使用することはしないでください。 このようなライセンスは、Microsoft 365 管理センターに **Rights Management Adhoc** と表示されるとともに、Azure AD PowerShell コマンドレット [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) を実行したときに **RIGHTSMANAGEMENT_ADHOC** と表示されます。 個人用 RMS サブスクリプションが自動的に付与されてユーザーに割り当てられるしくみの詳細については、「[個人用 RMS と Azure Information Protection](./rms-for-individuals.md)」を参照してください。

### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>手順 2:Azure Information Protection を使用するためのテナントを用意する

Azure Information Protection を使用するには、事前に Office 365 または Azure Active Directory にユーザー アカウントとグループがあることを確認します。 これらのユーザー アカウントとグループは、組織のユーザーを認証および承認するのに Azure Information Protection で使用されます。 必要に応じて、これらのアカウントとグループを作成するか、またはオンプレミスのディレクトリからそれらを同期します。 

詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>手順 3:分類とラベル付けを構成し、デプロイする

> [!TIP]
> **省略可能だが推奨される手順**: ローカル データ ストアにどのような機密情報があるかを検出するため、Azure Information Protection スキャナーのデプロイを検討してください。 このシナリオに対応した[クイック スタート](quickstart-findsensitiveinfo.md)を用意しています。 スキャナーで検出される情報は、ご使用の分類法で役立ち、必要なラベルおよび保護が必要なファイルに関する貴重な情報を提供します。
> 
> スキャナーは、Windows Server 上のローカル ファイル、ネットワーク共有内のファイル、および SharePoint のオンプレミス バージョンのファイル内のよく知られている機密情報の種類を検索するように構成できます。 この構成にラベルを構成する必要はなく、また分類法を定義する必要もないため、デプロイの非常に早い段階には、この方法でスキャナーを実行するのが適しています。 ラベルの条件を構成するまで、次の手順に従ってスキャナーのこの構成を並列で使用することもできます。

分類方法がまだ用意されていない場合、[既定の Azure Information Protection ポリシー](./configure-policy-default.md)を確認し、組織データに割り当てる分類ラベルを決める際の基準として利用します。 ビジネス要件に合わせてこれらをカスタマイズできます。

分類決定をサポートするために必要な変更を行うには、既定の Azure Information Protection ラベルを再構成します。 ユーザーによる手動ラベル付けのポリシーを構成し、適用するラベルとタイミングを説明するユーザー ガイダンスを記述します。 自動的に保護を適用するラベルで既定のポリシーが作成されている場合、保護設定を一時的に削除するか、ラベルを無効化します。 Azure Information Protection ポリシーの構成方法については、「[Azure Information Protection ポリシーの構成](./configure-policy.md)」を参照してください。

次に、ユーザーに対して[Azure Information Protection クライアントまたは Azure Information Protection の統一されたラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)を展開し、ラベルを選択する際のユーザートレーニングと具体的な指示を提供します。 クライアントのインストールとサポートの詳細については、管理者ガイドを参照してください。

- [Azure Information Protection クライアント管理者ガイド](./rms-client/client-admin-guide.md)

- [Azure Information Protection 統合されたラベル付けクライアント管理者ガイド](./rms-client/clientv2-admin-guide.md)

しばらくしてユーザーが文書や電子メールのラベル付けに慣れたら、さらに高度な構成を導入します。 次のようなものが含まれます。

- 既定のラベルを適用する

- 下位の分類レベルのラベルを選択したり、ラベルの削除を選択した場合に、理由をユーザーに求める

- すべての文書や電子メールにラベルを付けるように要求する

- カスタマイズされたヘッダー、フッター、透かし

- 推奨事項や自動ラベル付けをサポートする条件

この段階では、文書や電子メールを保護するためのオプションを選択しないでください。 ただし、自動ラベル付け用のラベルを構成した後は、ローカル データ ストアで [Azure Information Protection スキャナー](deploy-aip-scanner.md)を検索モードで実行して、ポリシーに適合させます。 この構成でスキャナーを実行すると、ファイルにどのラベルが適用されるかがわかります。 この情報は、ラベル構成の微調整に役立ち、ファイルを一括で分類して保護するための準備ができます。 

### <a name="step-4-prepare-for-data-protection"></a>手順 4:データ保護を準備する

ユーザーが文書や電子メールのラベル付けに慣れたら、最も機密性の高いデータのデータ保護を導入できます。 この段階には次の準備が必要です。

1. マイクロソフトでテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

2. インターネットにアクセスできる1台以上のコンピューターに AIPService 用の PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行しても構いません。 詳細については、「 [AIPService PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。

3. 現在、AD RMS を使用している場合: キー、テンプレート、Url をクラウドに移動するには、移行を実行します。 詳細については、「[AD RMS から Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

4. 文書や電子メールの保護を開始できるように、保護サービスがアクティブになっていることを確認します。 段階的に展開する必要がある場合、ユーザーによる保護の適用を制限するオンボーディング コントロールを構成します。 詳細については、「[Activating the protection service from Azure Information Protection (Azure Information Protection の保護サービスのアクティブ化)](./activate-service.md)」をご覧ください。

必要に応じて、次の構成を考慮してください。

- 組織での保護サービスの使用方法を監視できるようにするための使用ログ。 この手順は、今実行しても後で実行しても構いません。 詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。

### <a name="step-5-configure-your-azure-information-protection-policy-applications-and-services-for-data-protection"></a>手順 5:データ保護のために Azure Information Protection ポリシー、アプリケーション、サービスを構成する

1. 保護を適用するラベルを更新する
    
    Azure Information Protection クライアントについては、「 [Rights Management 保護のラベルを構成する方法](./configure-policy-protection.md)」を参照してください。
    
    Azure Information Protection の統合ラベル付けクライアントについては、「[秘密度ラベルの暗号化を使用したコンテンツへのアクセスの制限](https://docs.microsoft.com/Office365/SecurityCompliance/encryption-sensitivity-labels)」を参照してください。
    
    Exchange が Information Rights Management (IRM) 用に構成されていない場合でも、ユーザーは Outlook で Rights Management による保護を適用するラベルを適用できます。 ただし、IRM または [Office 365 Message Encryption と新機能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)に適するように Exchange が構成されるまで、組織は Exchange で Azure Rights Management による保護を使用するすべての機能を利用できません。 この追加の構成は、次のリストに含まれています (Exchange Online 用は 2、Exchange オンプレミス用は 5)。 

2. Office のアプリケーションとサービスを構成する
    
    SharePoint Online または Exchange Online の Information Rights Management (IRM) 機能のために Office のアプリケーションとサービスを構成します。 詳細については、「[Azure Rights Management 用にアプリケーションを構成する](configure-applications.md)」を参照してください。

3. データ回復のスーパー ユーザー機能を構成する
    
    Azure Information Protection によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure Rights Management のスーパー ユーザーとして構成します。 詳細については、「 [Azure Information Protection および探索サービスまたはデータの回復用のスーパーユーザーの構成](./configure-super-users.md)」を参照してください。

4. 既存ファイルを一括で分類および保護する
    
    オンプレミス データ ストアに対し、ファイルが自動的にラベル付けされるように、[Azure Information Protection スキャナー](deploy-aip-scanner.md)を強制モードで実行します。 クラウド ベースのデータ ストアに対しては、[Azure Cloud App Security](https://docs.microsoft.com/cloud-app-security) を使用します。
    
    PC 上のファイルに対しては、PowerShell コマンドレットを使用してファイルを分類して保護することができます。 詳細については、管理者ガイドの「[Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)」(Azure Information Protection クライアントでの PowerShell の使用) を参照してください。

6. SharePoint サーバー上で IRM で保護されたライブラリ用のコネクタと、Exchange On-Premises 用の IRM で保護された電子メールをデプロイする
    
    SharePoint と Exchange On-Premises をお持ちで、これらの Information Rights Management (IRM) 機能を使用する場合は、Rights Management コネクタをインストールして構成します。 詳細については、「[Azure Rights Management コネクタをデプロイする](./deploy-rms-connector.md)」を参照してください。

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>手順 6: データ保護ソリューションを使用および監視する
これで、構成したラベルを組織がどのように使用しているかを監視して、機密情報を保護していることを確認する準備ができました。 このデプロイ フェーズのサポートの詳細については、以下を参照してください。

- [Azure Information Protection のレポート](reports-aip.md) - 現在プレビュー段階

- [Azure Information Protection クライアント](./rms-client/client-admin-guide-files-and-logging.md)のクライアントファイルと使用状況ログ

- [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)

### <a name="step-7-administer-the-protection-service-for-your-tenant-account-as-needed"></a>手順 7: 必要に応じてテナント アカウントの保護サービスを管理する

保護サービスの使用を開始するときに、PowerShell がスクリプトまたは管理変更の自動化に役立つことがあります。 一部の高度な構成には、PowerShell も必要になる場合があります。 

詳細については、「 [PowerShell を使用した Azure Information Protection からの保護の管理](./administer-powershell.md)」を参照してください。


## <a name="deployment-roadmap-for-data-protection-only"></a>データ保護のみのデプロイ ロードマップ

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-the-protection-service-from-azure-information-protection"></a>手順 1:Azure Information Protection の保護サービスを含むサブスクリプションがあることを確認する

「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)」ページのサブスクリプション情報と機能一覧を見て、必要な機能を含むサブスクリプションを組織が所有していることを確認します。 次に、文書や電子メールを保護する組織内の各ユーザーに、このサブスクリプションのライセンスを割り当てます。

メモ:ユーザー ライセンスを無料の個人用 RMS サブスクリプションから手動で割り当てることや、このライセンスを組織の Azure Rights Management サービスの管理目的で使用することはしないでください。 このようなライセンスは、Microsoft 365 管理センターに **Rights Management Adhoc** と表示されるとともに、Azure AD PowerShell コマンドレット [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) を実行したときに **RIGHTSMANAGEMENT_ADHOC** と表示されます。 個人用 RMS サブスクリプションが自動的に付与されてユーザーに割り当てられるしくみの詳細については、「[個人用 RMS と Azure Information Protection](./rms-for-individuals.md)」を参照してください。


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>手順 2:Azure Information Protection を使用するためのテナントを用意する

Azure Information Protection の保護サービスの使用を開始する前に、次の準備を行います。

1. Office 365 テナントに、組織のユーザーを認証および承認するのに Azure Information Protection で使用されるユーザー アカウントとグループが含まれていることを確認します。 必要に応じて、これらのアカウントとグループを作成するか、またはオンプレミスのディレクトリからそれらを同期します。 詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

2. マイクロソフトでテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

3. インターネットにアクセスできる1台以上のコンピューターに AIPService 用の PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行しても構いません。 詳細については、「 [AIPService PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。

4. 現在、AD RMS を使用している場合: キー、テンプレート、Url をクラウドに移動するには、移行を実行します。 詳細については、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

5. 文書や電子メールの保護を開始できるように、保護サービスがアクティブになっていることを確認します。 段階的に展開する必要がある場合、ユーザーによる保護の適用を制限するオンボーディング コントロールを構成します。 詳細については、「[Activating the protection service from Azure Information Protection (Azure Information Protection の保護サービスのアクティブ化)](./activate-service.md)」をご覧ください。

必要に応じて、次の構成を考慮してください。

- 既定のテンプレートが組織にとって十分でない場合は、保護設定のためのカスタム テンプレート。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](./configure-policy-templates.md)」を参照してください。

- 組織での保護サービスの使用方法を監視できるようにするための使用ログ。 この手順は、今実行しても後で実行しても構いません。 詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。

### <a name="step-3-install-the-azure-information-protection-client-and-configure-applications-and-services-for-rights-management"></a>手順 3:Azure Information Protection クライアントをインストールし、Rights Management 用のアプリケーションとサービスを構成する

1. Azure Information Protection クライアントのデプロイ
    
    Office 2010 のサポート、Office ドキュメントと電子メール以外のファイルの保護、保護されたドキュメントの追跡には、ユーザーに Azure Information Protection をインストールします。 このクライアントのユーザー トレーニングを行います。 詳細については、「[Azure Information Protection client for Windows](./rms-client/aip-client.md)」(Windows 用 Azure Information Protection クライアント) を参照してください。

2. Office のアプリケーションとサービスを構成する
    
    SharePoint Online または Exchange Online の Information Rights Management (IRM) 機能のために Office のアプリケーションとサービスを構成します。 詳細については、「[Azure Rights Management 用にアプリケーションを構成する](./configure-applications.md)」を参照してください。

3. データ回復のスーパー ユーザー機能を構成する
    
    Azure Information Protection によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure Rights Management のスーパー ユーザーとして構成します。 詳細については、「 [Azure Information Protection および探索サービスまたはデータの回復用のスーパーユーザーの構成](./configure-super-users.md)」を参照してください。

4. 既存ファイルを一括で保護する 
    
    PowerShell コマンドレットを使用して、複数のファイルの種類を一括保護または一括保護解除することができます。 詳細については、管理者ガイドの「[Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)」(Azure Information Protection クライアントでの PowerShell の使用) を参照してください。
    
    Windows ベースのファイル サーバー上のファイルに対しては、スクリプトと Windows Server ファイル分類インフラストラクチャでこれらのコマンドレットを使用することができます。 詳細については、「[Windows Server ファイル分類インフラストラクチャ (FCI) での RMS の保護](./rms-client/configure-fci.md)」を参照してください。

5. オンプレミス サーバーのコネクタをデプロイする
    
    保護サービスで使用するオンプレミスのサービスがある場合は、Rights Management コネクタをインストールして構成します。 詳細については、「[Azure Rights Management コネクタをデプロイする](./deploy-rms-connector.md)」を参照してください。

### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>手順 4:データ保護ソリューションを使用および監視する

これでデータを保護し、会社で保護サービスを使用する方法を記録する準備が整いました。 このデプロイフェーズをサポートするための追加情報については、「 [Azure Rights Management サービスを使用](./help-users.md)したファイルの保護」および「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。

### <a name="step-5-administer-the-protection-service-for-your-tenant-account-as-needed"></a>手順 5:必要に応じてテナント アカウントの保護サービスを管理する

保護サービスの使用を開始するときに、PowerShell がスクリプトまたは管理変更の自動化に役立つことがあります。 一部の高度な構成には、PowerShell も必要になる場合があります。 

詳細については、「 [PowerShell を使用した Azure Information Protection からの保護の管理](./administer-powershell.md)」を参照してください。
