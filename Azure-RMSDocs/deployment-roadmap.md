---
title: Azure Information Protection デプロイ ロードマップ
description: 組織の Azure Information Protection を準備、実装、管理するには、これらの手順に従ってください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 58567d3a8d76da4f872558a7aeea102562c7c3cf
ms.sourcegitcommit: 98d539901b2e5829a2aad685d10fb13fd8d7dec4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/17/2020
ms.locfileid: "77423162"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Azure Information Protection デプロイ ロードマップ

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

組織の Azure Information Protection を準備、実装、管理するための推奨事項として、次の手順に従ってください。

方法 

- Azure Information Protection のシナリオベースの命令を探していますか? [Azure Information Protection を使用する一般的なシナリオについては、「ハウツーガイド](how-to-guides.md)」を参照してください。

- Azure Information Protection リリースロードマップをお探しですか? [新しいリリースと更新プログラムに関する情報を](information-support.md#information-about-new-releases-and-updates)参照してください。

### <a name="identify-your-deployment-roadmap"></a>デプロイ ロードマップを特定する

次のいずれかの手順を実行して Azure Information Protection をデプロイする前に、「[Azure Information Protection の要件](./requirements.md)」を確認してください。

次に、ご自分の組織に適用可能で、必要な[サブスクリプション機能](https://azure.microsoft.com/pricing/details/information-protection/)に一致するデプロイ ロードマップを選択します。

- [分類、ラベル付け、保護を使用する](#deployment-roadmap-for-classification-labeling-and-protection)
    
    サポートされているサブスクリプションがある場合に推奨されるパス。これは、追加機能が機密情報の検出、分類のためのドキュメントや電子メールのラベル付けをサポートするためです。 ラベルは、この複雑さをユーザーから抽象化して、保護を適用することもできます。
    
    デプロイの手順は、ラベルの Azure Information Protection に適しています。また、統一されたラベル[付けプラットフォーム](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)を使用する秘密度ラベルにも適しています。

- [データ保護のみを使用する](#deployment-roadmap-for-data-protection-only)
    
    分類とラベルをサポートするサブスクリプションがなくても、ラベルのない保護をサポートする場合に使用するパス。

## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>分類、ラベル付け、保護のデプロイ ロードマップ

> [!NOTE]
> 既に Azure Information Protection の保護機能を使用している場合は、 これらの手順の多くを省略し、手順 3 と 5.1 だけ実行することもできます。

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>手順 1: サブスクリプションを確認し、ユーザー ライセンスを割り当てる
「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)」ページのサブスクリプション情報と機能一覧を見て、必要な機能を含むサブスクリプションを組織が所有していることを確認します。 次に、文書や電子メールを分類し、ラベルを付け、保護する各ユーザーにこのサブスクリプションのライセンスを割り当てます。

注: ユーザー ライセンスを無料の個人用 RMS サブスクリプションから手動で割り当てることや、このライセンスを組織の Azure Rights Management サービスの管理目的で使用することはしないでください。 このようなライセンスは、Microsoft 365 管理センターに **Rights Management Adhoc** と表示されるとともに、Azure AD PowerShell コマンドレット **Get-MsolAccountSku** を実行したときに [RIGHTSMANAGEMENT_ADHOC](https://msdn.microsoft.com/library/azure/dn194118.aspx) と表示されます。 個人用 RMS サブスクリプションが自動的に付与されてユーザーに割り当てられるしくみの詳細については、「[個人用 RMS と Azure Information Protection](./rms-for-individuals.md)」を参照してください。

### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>手順 2: Azure Information Protection を使用するためのテナントを用意する

Azure Information Protection を使用するには、事前に Office 365 または Azure Active Directory にユーザー アカウントとグループがあることを確認します。 これらのユーザー アカウントとグループは、組織のユーザーを認証および承認するのに Azure Information Protection で使用されます。 必要に応じて、これらのアカウントとグループを作成するか、またはオンプレミスのディレクトリからそれらを同期します。 

詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>手順 3: 分類とラベル付けを構成し、デプロイする

ラベルとポリシー設定を構成する前に、使用する Azure Information Protection クライアント (従来のクライアントまたは統一されたラベル付けクライアント) を決定します。 または、両方のクライアントが必要になる場合もあります。 ここでは、このクライアントの決定が必要であるため、ラベルとポリシー設定を構成するために使用する管理ポータルを把握しておく必要があります。 この決定に役立つ詳細については、「[使用する Azure Information Protection クライアントを選択](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers)する」を参照してください。

> [!TIP]
> **省略可能ですが推奨される**方法: ローカルデータストアに格納されている機密情報を検出するには、[スキャナーのクイックスタート](quickstart-findsensitiveinfo.md)を使用することを検討してください。 スキャナーで検出される情報は、ご使用の分類法で役立ち、必要なラベルおよび保護が必要なファイルに関する貴重な情報を提供します。
> 
> スキャナー検出モードではラベルを構成する必要がなく、分類分類を定義することもできないため、この方法でスキャナーを実行すると、展開の初期段階に適しています。 このスキャナーの構成は、推奨ラベルまたは自動ラベル付けを構成するまで、次の展開手順と並行して使用することもできます。

分類方法がまだない場合は、[既定の Azure Information Protection ポリシー](./configure-policy-default.md)を確認し、これを組織のデータに割り当てる分類ラベルを決定するための基準として使用します。 ビジネス要件に合わせてこれらをカスタマイズできます。

ラベルを再構成して、分類の決定をサポートするために必要な変更を行います。 ユーザーによる手動ラベル付けのポリシーを構成し、適用するラベルとタイミングを説明するユーザー ガイダンスを記述します。 自動的に保護を適用するラベルで既定のポリシーが作成されている場合、保護設定を一時的に削除するか、ラベルを無効化します。 ラベルとポリシー設定を構成する方法の詳細については、次のドキュメントを参照してください。

- クラシッククライアントの Azure Information Protection ラベル: [Azure Information Protection ポリシーの構成](./configure-policy.md)

- 統一されたラベル付けクライアントの秘密度ラベル:[機密ラベルについての詳細](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)情報

次に、Azure Information Protection クライアント (クラシック) または Azure Information Protection 統合されたラベル付けクライアントをユーザーに展開します。 ラベルを選択するときに、ユーザートレーニングと具体的な指示を提供します。 クライアントのインストールとサポートの詳細については、管理者ガイドを参照してください。

- [Azure Information Protection クライアント管理者ガイド](./rms-client/client-admin-guide.md)

- [Azure Information Protection 統合されたラベル付けクライアント管理者ガイド](./rms-client/clientv2-admin-guide.md)

しばらくしてユーザーが文書や電子メールのラベル付けに慣れたら、さらに高度な構成を導入します。 次のようなものが含まれます。

- 既定のラベルを適用する

- 下位の分類レベルのラベルを選択したり、ラベルの削除を選択した場合に、理由をユーザーに求める

- すべての文書や電子メールにラベルを付けるように要求する

- カスタマイズされたヘッダー、フッター、透かし

- 推奨ラベルと自動ラベル付け

この段階では、文書や電子メールを保護するためのオプションを選択しないでください。 ただし、自動ラベル付け用のラベルを構成した後は、ローカル データ ストアで [Azure Information Protection スキャナー](deploy-aip-scanner.md)を検索モードで実行して、ポリシーに適合させます。 この構成でスキャナーを実行すると、ファイルにどのラベルが適用されるかがわかります。 この情報は、ラベル構成の微調整に役立ち、ファイルを一括で分類して保護するための準備ができます。 

### <a name="step-4-prepare-for-data-protection"></a>手順 4: データ保護を準備する

ユーザーが文書や電子メールのラベル付けに慣れたら、最も機密性の高いデータのデータ保護を導入できます。 この段階には次の準備が必要です。

1. マイクロソフトでテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

2. インターネットにアクセスできる1台以上のコンピューターに AIPService 用の PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行してもかまいません。 詳細については、「 [AIPService PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。

3. 現在、AD RMS を使用している場合: キー、テンプレート、URL をクラウドに移行する統合を実行します。 詳細については、「[AD RMS から Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

4. 文書や電子メールの保護を開始できるように、保護サービスがアクティブになっていることを確認します。 段階的に展開する必要がある場合、ユーザーによる保護の適用を制限するオンボーディング コントロールを構成します。 詳細については、「[Activating the protection service from Azure Information Protection (Azure Information Protection の保護サービスのアクティブ化)](./activate-service.md)」をご覧ください。

必要に応じて、次の構成を考慮してください。

- 組織での保護サービスの使用方法を監視できるようにするための使用ログ。 この手順は、今実行しても後で実行してもかまいません。 詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。

### <a name="step-5-configure-labels-and-settings-applications-and-services-for-data-protection"></a>手順 5: データ保護のためのラベル、設定、アプリケーション、およびサービスを構成する

1. 保護を適用するラベルを更新する
    
    Azure Information Protection クライアント (クラシック) については、「 [Rights Management 保護のラベルを構成する方法](./configure-policy-protection.md)」を参照してください。
    
    Azure Information Protection の統合ラベル付けクライアントについては、「[秘密度ラベルの暗号化を使用したコンテンツへのアクセスの制限](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)」を参照してください。
    
    Exchange が Information Rights Management (IRM) 用に構成されていない場合でも、ユーザーは Outlook で Rights Management による保護を適用するラベルを適用できます。 ただし、IRM または [Office 365 Message Encryption と新機能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)に適するように Exchange が構成されるまで、組織は Exchange で Azure Rights Management による保護を使用するすべての機能を利用できません。 この追加の構成は、次のリストに含まれています (Exchange Online 用は 2、Exchange オンプレミス用は 5)。 

2. Office のアプリケーションとサービスを構成する
    
    SharePoint Online または Exchange Online の Information Rights Management (IRM) 機能のために Office のアプリケーションとサービスを構成します。 詳細については、「[Azure Rights Management 用にアプリケーションを構成する](configure-applications.md)」を参照してください。

3. データ回復のスーパー ユーザー機能を構成する
    
    Azure Information Protection によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure Rights Management のスーパー ユーザーとして構成します。 詳細については、「 [Azure Information Protection および探索サービスまたはデータの回復用のスーパーユーザーの構成](./configure-super-users.md)」を参照してください。

4. 既存ファイルを一括で分類および保護する
    
    オンプレミス データ ストアに対し、ファイルが自動的にラベル付けされるように、[Azure Information Protection スキャナー](deploy-aip-scanner.md)を強制モードで実行します。 クラウド ベースのデータ ストアに対しては、[Azure Cloud App Security](https://docs.microsoft.com/cloud-app-security) を使用します。
    
    PC 上のファイルに対しては、PowerShell コマンドレットを使用してファイルを分類して保護することができます。 詳細については、次の管理者ガイドを参照してください。
    
    - Azure Information Protection クライアント (クラシック): [Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md)
    
    - Azure Information Protection 統合されたラベル付けクライアント: [Azure Information Protection のラベル付けクライアントでの PowerShell の使用](./rms-client/clientv2-admin-guide-powershell.md)

6. SharePoint サーバー上で IRM で保護されたライブラリ用のコネクタと、Exchange On-Premises 用の IRM で保護された電子メールをデプロイする
    
    SharePoint と Exchange On-Premises をお持ちで、これらの Information Rights Management (IRM) 機能を使用する場合は、Rights Management コネクタをインストールして構成します。 詳細については、「[Azure Rights Management コネクタをデプロイする](./deploy-rms-connector.md)」を参照してください。

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>手順 6: データ保護ソリューションを使用および監視する
これで、構成したラベルを組織がどのように使用しているかを監視して、機密情報を保護していることを確認する準備ができました。 このデプロイ フェーズのサポートの詳細については、以下を参照してください。

- [Azure Information Protection の中央レポート](reports-aip.md)-現在プレビュー中

- Azure Information Protection クライアントの[Windows イベントモニターを使用したローカルの使用状況ログ](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)(クラシック)

- [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)

### <a name="step-7-administer-the-protection-service-for-your-tenant-account-as-needed"></a>手順 7: 必要に応じてテナント アカウントの保護サービスを管理する

保護サービスの使用を開始するときに、PowerShell がスクリプトまたは管理変更の自動化に役立つことがあります。 一部の高度な構成には、PowerShell も必要になる場合があります。 

詳細については、「 [PowerShell を使用した Azure Information Protection からの保護の管理](./administer-powershell.md)」を参照してください。


## <a name="deployment-roadmap-for-data-protection-only"></a>データ保護のみのデプロイ ロードマップ

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-the-protection-service-from-azure-information-protection"></a>手順 1: Azure Information Protection の保護サービスを含むサブスクリプションがあることを確認する

「[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)」ページのサブスクリプション情報と機能一覧を見て、必要な機能を含むサブスクリプションを組織が所有していることを確認します。 次に、文書や電子メールを保護する組織内の各ユーザーに、このサブスクリプションのライセンスを割り当てます。

注: ユーザー ライセンスを無料の個人用 RMS サブスクリプションから手動で割り当てることや、このライセンスを組織の Azure Rights Management サービスの管理目的で使用することはしないでください。 このようなライセンスは、Microsoft 365 管理センターに **Rights Management Adhoc** と表示されるとともに、Azure AD PowerShell コマンドレット **Get-MsolAccountSku** を実行したときに [RIGHTSMANAGEMENT_ADHOC](https://msdn.microsoft.com/library/azure/dn194118.aspx) と表示されます。 個人用 RMS サブスクリプションが自動的に付与されてユーザーに割り当てられるしくみの詳細については、「[個人用 RMS と Azure Information Protection](./rms-for-individuals.md)」を参照してください。


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>手順 2: Azure Information Protection を使用するためのテナントを用意する

Azure Information Protection の保護サービスの使用を開始する前に、次の準備を行います。

1. Office 365 テナントに、組織のユーザーを認証および承認するのに Azure Information Protection で使用されるユーザー アカウントとグループが含まれていることを確認します。 必要に応じて、これらのアカウントとグループを作成するか、またはオンプレミスのディレクトリからそれらを同期します。 詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

2. マイクロソフトでテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

3. インターネットにアクセスできる1台以上のコンピューターに AIPService 用の PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行してもかまいません。 詳細については、「 [AIPService PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。

4. 現在、AD RMS を使用している場合: キー、テンプレート、URL をクラウドに移行する統合を実行します。 詳細については、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

5. 文書や電子メールの保護を開始できるように、保護サービスがアクティブになっていることを確認します。 段階的に展開する必要がある場合、ユーザーによる保護の適用を制限するオンボーディング コントロールを構成します。 詳細については、「[Activating the protection service from Azure Information Protection (Azure Information Protection の保護サービスのアクティブ化)](./activate-service.md)」をご覧ください。

必要に応じて、次の構成を考慮してください。

- 既定のテンプレートが組織にとって十分でない場合は、保護設定のためのカスタム テンプレート。 この手順は、今実行しても後で実行してもかまいません。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](./configure-policy-templates.md)」を参照してください。

- 組織での保護サービスの使用方法を監視できるようにするための使用ログ。 この手順は、今実行しても後で実行してもかまいません。 詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。

### <a name="step-3-install-the-azure-information-protection-client-classic-and-configure-applications-and-services-for-rights-management"></a>手順 3: Azure Information Protection クライアント (クラシック) をインストールし、Rights Management 用のアプリケーションとサービスを構成する

1. Azure Information Protection クライアントを展開する (クラシック)
    
    Office 2010 をサポートし、Office ドキュメントや電子メール以外のファイルを保護し、保護されたドキュメントを追跡するために、ユーザー用のクラシッククライアントをインストールします。 このクライアントのユーザー トレーニングを行います。 詳細については、「[Azure Information Protection client for Windows](./rms-client/aip-client.md)」(Windows 用 Azure Information Protection クライアント) を参照してください。

2. Office のアプリケーションとサービスを構成する
    
    SharePoint Online または Exchange Online の Information Rights Management (IRM) 機能のために Office のアプリケーションとサービスを構成します。 詳細については、「[Azure Rights Management 用にアプリケーションを構成する](./configure-applications.md)」を参照してください。

3. データ回復のスーパー ユーザー機能を構成する
    
    Azure Information Protection によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure Rights Management のスーパー ユーザーとして構成します。 詳細については、「 [Azure Information Protection および探索サービスまたはデータの回復用のスーパーユーザーの構成](./configure-super-users.md)」を参照してください。

4. 既存ファイルを一括で保護する 
    
    PowerShell コマンドレットを使用して、複数のファイルの種類を一括保護または一括保護解除することができます。 詳細については、管理者ガイドの「[Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)」(Azure Information Protection クライアントでの PowerShell の使用) を参照してください。
    
    Windows ベースのファイル サーバー上のファイルに対しては、スクリプトと Windows Server ファイル分類インフラストラクチャでこれらのコマンドレットを使用することができます。 詳細については、「[Windows Server ファイル分類インフラストラクチャ (FCI) での RMS の保護](./rms-client/configure-fci.md)」を参照してください。

5. オンプレミス サーバーのコネクタをデプロイする
    
    保護サービスで使用するオンプレミスのサービスがある場合は、Rights Management コネクタをインストールして構成します。 詳細については、「[Azure Rights Management コネクタをデプロイする](./deploy-rms-connector.md)」を参照してください。

### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>手順 4: データ保護ソリューションを使用し、監視する

これでデータを保護し、会社で保護サービスを使用する方法を記録する準備が整いました。 このデプロイフェーズをサポートするための追加情報については、「 [Azure Rights Management サービスを使用](./help-users.md)したファイルの保護」および「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。

### <a name="step-5-administer-the-protection-service-for-your-tenant-account-as-needed"></a>手順 5: 必要に応じてテナント アカウントの保護サービスを管理する

保護サービスの使用を開始するときに、PowerShell がスクリプトまたは管理変更の自動化に役立つことがあります。 一部の高度な構成には、PowerShell も必要になる場合があります。 

詳細については、「 [PowerShell を使用した Azure Information Protection からの保護の管理](./administer-powershell.md)」を参照してください。

## <a name="next-steps"></a>次のステップ:

Azure Information Protection を展開するときに、[よく寄せられる質問](faqs.md)と、その他のリソースの[情報とサポート](information-support.md)に関するページを確認すると役立つ場合があります。