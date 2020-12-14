---
title: 分類、ラベル付け、保護のために Azure Information Protection (AIP) を展開する
description: データを分類、ラベル付け、保護する必要がある場合は、次の手順に従って、組織の Azure Information Protection (AIP) の準備、実装、および管理を行います。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 594d6fed74e2a8330c2a523ddbab5da2dd3d880c
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382498"
---
# <a name="aip-deployment-roadmap-for-classification-labeling-and-protection"></a>分類、ラベル付け、保護のための展開ロードマップを AIP

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

データを分類、ラベル付け、保護する必要がある場合は、次の手順を推奨設定として使用して、組織の Azure Information Protection を準備、実装、および管理することができます。

このロードマップは、サポートサブスクリプションをご利用のお客様にお勧めします。 その他の機能として、機密情報の検出、分類用のドキュメントや電子メールのラベル付けなどがあります。 

ラベルは保護を適用して、ユーザーにとってこの手順を簡略化することもできます。 

> [!TIP]
> または、次のいずれかの記事を検索することもできます。
> - [データ保護のみの AIP ロードマップ](deployment-roadmap-protect-only.md)
> - [Azure Information Protection を使用する一般的なシナリオに関する攻略ガイド](how-to-guides.md)
> - [Azure Information Protection リリースロードマップ](information-support.md#information-about-new-releases-and-updates)

## <a name="deployment-process"></a>デプロイ プロセス

次の手順を実行します。

1. [サブスクリプションを確認し、ユーザー ライセンスを割り当てる](#confirm-your-subscription-and-assign-user-licenses)
1. [Azure Information Protection を使用するためのテナントを用意する](#prepare-your-tenant-to-use-azure-information-protection)
1. [分類とラベル付けを構成し、デプロイする](#configure-and-deploy-classification-and-labeling)
1. [データ保護を準備する](#prepare-for-data-protection)
1. [データ保護のためのラベル、設定、アプリケーション、およびサービスを構成する](#configure-labels-and-settings-applications-and-services-for-data-protection)
1. [データ保護ソリューションを使用および監視する](#use-and-monitor-your-data-protection-solutions)
1. [必要に応じてテナント アカウントの保護サービスを管理する](#administer-the-protection-service-for-your-tenant-account-as-needed)

> [!TIP]
> 既に Azure Information Protection の保護機能を使用している場合は、 これらの手順の多くを省略し、手順 [3](#configure-and-deploy-classification-and-labeling) と [5.1](#configure-labels-and-settings-applications-and-services-for-data-protection)に焦点を当てることができます。

## <a name="confirm-your-subscription-and-assign-user-licenses"></a>サブスクリプションを確認し、ユーザー ライセンスを割り当てる

予想される機能を含むサブスクリプションが組織にあることを確認します。 これらの詳細については、 [Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection) に関するページを参照してください。

次に、文書や電子メールを分類し、ラベルを付け、保護する各ユーザーにこのサブスクリプションのライセンスを割り当てます。

> [!IMPORTANT]
> 無料の個人用 RMS サブスクリプションからユーザーライセンスを手動で割り当てることは避けてください。このライセンスを使用して、組織の Azure Rights Management サービスを管理することは避けてください。 
>
> このようなライセンスは、Microsoft 365 管理センターに **Rights Management Adhoc** と表示されるとともに、Azure AD PowerShell コマンドレット [Get-MsolAccountSku](/previous-versions/azure/dn194118(v=azure.100)) を実行したときに **RIGHTSMANAGEMENT_ADHOC** と表示されます。 
>
> 詳細については、「個人用 [RMS と Azure Information Protection](./rms-for-individuals.md)」を参照してください。
> 
## <a name="prepare-your-tenant-to-use-azure-information-protection"></a>Azure Information Protection を使用するためのテナントを用意する

Azure Information Protection の使用を開始する前に、ユーザーの認証と承認に AIP が使用できるユーザーアカウントとグループ Microsoft 365 または Azure Active Directory があることを確認してください。

必要に応じて、これらのアカウントとグループを作成するか、オンプレミスのディレクトリからそれらを同期します。 

詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

## <a name="configure-and-deploy-classification-and-labeling"></a>分類とラベル付けを構成し、デプロイする

次の手順を実行します。

1. **ファイルをスキャンする (省略可能ですが推奨される)**

    [Azure Information Protection クライアントを展開](quickstart-deploy-client.md)し、スキャナーを [インストール](tutorial-install-scanner.md) して [実行](tutorial-scan-networks-and-content.md) し、ローカルデータストアに保存されている機密情報を見つけます。 

    スキャナーで検出される情報は、ご使用の分類法で役立ち、必要なラベルおよび保護が必要なファイルに関する貴重な情報を提供します。

    スキャナー **検出** モードはラベルの構成や分類を必要としないため、展開のこの初期段階に適しています。 このスキャナー構成は、推奨ラベルまたは自動ラベル付けを構成するまで、次の展開手順と並行して使用することもできます。

1. **既定の AIP ポリシーをカスタマイズ** します。

    分類戦略がまだない場合は、データに必要なラベルを決定するための基準として既定のポリシーを使用します。 ニーズに合わせて、必要に応じてこれらのラベルをカスタマイズします。

    たとえば、次の詳細を使用してラベルを再構成することができます。

    - ラベルで分類の決定がサポートされていることを確認します。
    - ユーザーが手動でラベル付けするためのポリシーを構成する
    - 各シナリオでどのラベルを適用する必要があるかを説明するために、ユーザーガイダンスを記述します。
    - 保護を自動的に適用するラベルを使用して既定のポリシーが作成されている場合は、設定のテスト中に保護設定を一時的に削除するか、ラベルを無効にすることができます。 

    統一されたラベル付けクライアントの秘密度ラベルとラベル付けポリシーは、Microsoft 365 security center、Microsoft 365 コンプライアンスセンター、または Microsoft 365 セキュリティ & コンプライアンスセンターで構成されます。 詳細については、「 [秘密度ラベルについ](/microsoft-365/compliance/sensitivity-labels)て」を参照してください。

1. **クライアントをユーザーに展開する**

    ポリシーを構成したら、Azure Information Protection クライアントをユーザーに展開します。 ラベルを選択するときに、ユーザートレーニングと具体的な指示を提供します。 

    詳細については、「 [クライアント管理者ガイド](./rms-client/clientv2-admin-guide.md)」を参照してください。

1. **より高度な構成を導入する**

    ユーザーがドキュメントや電子メールのラベルを使いやすくなるまで待ちます。 準備ができたら、次のような高度な構成を導入します。

    - 既定のラベルの適用
    - 分類レベルが低いラベルを選択した場合、またはラベルを削除した場合に、理由をユーザーに求める
    - すべてのドキュメントと電子メールにラベルがあることを義務付ける
    - ヘッダー、フッター、または透かしのカスタマイズ
    - 推奨ラベルと自動ラベル付け

    詳細については、「 [管理者ガイド: カスタム構成](rms-client/client-admin-guide-customizations.md)」を参照してください。
     
    > [!TIP]
    > ラベルが自動的にラベル付けされるように構成した場合は、探索モードでローカルデータストアに対して [Azure Information Protection スキャナー](deploy-aip-scanner-manage.md) を再実行し、ポリシーに一致させます。 
    > 
    > 検出モードでスキャナーを実行すると、どのラベルがファイルに適用されるかがわかります。これにより、ラベルの構成を微調整し、ファイルを一括して分類および保護するための準備を行うことができます。 
    > 

## <a name="prepare-for-data-protection"></a>データ保護を準備する

ユーザーがドキュメントや電子メールのラベル付けに慣れると、最も機密性の高いデータのデータ保護が導入されます。

データ保護を準備するには、次の手順を実行します。

1. **テナントキーをどのように管理するかを決定** します。

    Microsoft でテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 
 
    オンプレミスの追加の保護の詳細とオプションについては、「 [Azure Information Protection テナントキーの計画と実装](plan-implement-tenant-key.md)」を参照してください。

1. **AIP 用の PowerShell をインストール** します。

    インターネットにアクセスできる1台以上のコンピューターに **Aipservice** 用の PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行しても構いません。 

    詳細については、「 [AIPService PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。

1. **AD RMS のみ**: キー、テンプレート、url をクラウドに移行します。

    現在 AD RMS を使用している場合は、移行を実行して、キー、テンプレート、Url をクラウドに移動します。 
    
    詳細については、「[AD RMS から Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

1. **保護をアクティブ化** します。

    文書や電子メールの保護を開始できるように、保護サービスがアクティブになっていることを確認します。 複数のフェーズで展開する場合は、ユーザーによる保護の適用を制限するようにユーザーのオンボードコントロールを構成します。 

    詳細については、「[Activating the protection service from Azure Information Protection (Azure Information Protection の保護サービスのアクティブ化)](./activate-service.md)」をご覧ください。

1. **使用状況ログを検討します (省略可能)**。

    組織での保護サービスの使用状況を監視するために、使用状況をログに記録することを検討してください。 この手順は、今実行しても後で実行しても構いません。 

    詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。

## <a name="configure-labels-and-settings-applications-and-services-for-data-protection"></a>データ保護のためのラベル、設定、アプリケーション、およびサービスを構成する

次の手順を実行します。

1. **保護を適用するラベルを更新する**
    
    詳細については、[機密ラベルの暗号化を使用したコンテンツへのアクセスの制限](/microsoft-365/compliance/encryption-sensitivity-labels)に関する記事をご覧ください。

    > [!IMPORTANT]
    > Exchange が information Rights Management (IRM) 用に構成されていない場合でも、ユーザーは Outlook でラベルを適用して Rights Management 保護を適用できます。 
    > 
    > ただし、Exchange が IRM 用に構成されるまで、または [新しい機能を使用する Microsoft 365 メッセージの暗号化](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)が行われるまで、組織は Exchange で Azure Rights Management 保護を使用するすべての機能を利用することはできません。 この追加の構成は、次のリストに含まれています (Exchange Online 用は 2、Exchange オンプレミス用は 5)。 
    > 
    
1. **Office のアプリケーションとサービスを構成する**
    
    Microsoft SharePoint または Exchange Online で information rights management (IRM) 機能を使用するように Office アプリケーションとサービスを構成します。 

    詳細については、「 [Azure Rights Management 用のアプリケーションの構成](configure-applications.md)」を参照してください。

1. **データ回復のスーパー ユーザー機能を構成する**
    
    Azure Information Protection によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure Rights Management のスーパー ユーザーとして構成します。 

    詳細については、「 [Azure Information Protection および探索サービスまたはデータの回復用のスーパーユーザーの構成](./configure-super-users.md)」を参照してください。

1. **既存ファイルを一括で分類および保護する**
    
    オンプレミス データ ストアに対し、ファイルが自動的にラベル付けされるように、[Azure Information Protection スキャナー](deploy-aip-scanner.md)を強制モードで実行します。
    
    Pc 上のファイルについては、PowerShell コマンドレットを使用してファイルを分類および保護します。 詳細については、「Azure Information Protection 統合された [ラベル付けクライアントでの PowerShell の使用](./rms-client/clientv2-admin-guide-powershell.md)」を参照してください。

    クラウド ベースのデータ ストアに対しては、[Azure Cloud App Security](/cloud-app-security) を使用します。 

    > [!TIP]
    > 既存のファイルを一括で分類して保護することは、cloud app security の主なユースケースの1つではありませんが、ドキュメントに記載されている [回避策](/cloud-app-security/azip-integration#enable-azure-information-protection) は、ファイルを分類および保護するのに役立ちます。

6. **SharePoint サーバー上で IRM で保護されたライブラリ用のコネクタと、Exchange On-Premises 用の IRM で保護された電子メールをデプロイする**
    
    SharePoint と Exchange On-Premises をお持ちで、これらの Information Rights Management (IRM) 機能を使用する場合は、Rights Management コネクタをインストールして構成します。 

    詳細については、「[Azure Rights Management コネクタをデプロイする](./deploy-rms-connector.md)」を参照してください。

## <a name="use-and-monitor-your-data-protection-solutions"></a>データ保護ソリューションを使用および監視する

これで、組織が構成したラベルをどのように使用しているかを監視し、機密情報を保護していることを確認する準備ができました。 

詳細については、次のページを参照してください。

- [Azure Information Protection の中央レポート](reports-aip.md) -現在プレビュー中
- [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)

## <a name="administer-the-protection-service-for-your-tenant-account-as-needed"></a>必要に応じてテナント アカウントの保護サービスを管理する

保護サービスの使用を開始するときに、PowerShell がスクリプトまたは管理変更の自動化に役立つことがあります。 一部の高度な構成には、PowerShell も必要になる場合があります。 

詳細については、「 [PowerShell を使用した Azure Information Protection からの保護の管理](./administer-powershell.md)」を参照してください。

## <a name="references-for-classic-client-environments"></a>クラシッククライアント環境のリファレンス

**関連**: AIP classic client のみ

従来のクライアントを使用している場合は、上記のリンクの代わりに次の参照を使用します。

- クラシッククライアントで提供されている **スキャナーをデプロイして実行** します。 詳細については、「 [Azure Information Protection クラシックスキャナーとは](deploy-aip-scanner-classic.md)」を参照してください。

- **Azure portal でポリシーを構成します。** 詳細については、「 [Azure Information Protection ポリシーの構成](./configure-policy.md) 」および「 [Rights Management 保護のラベルを構成する方法](./configure-policy-protection.md)」を参照してください。

- 従来の [クライアント管理者ガイド](./rms-client/client-admin-guide.md)と [従来のクライアントのカスタム構成手順](rms-client/client-admin-guide-customizations.md)を使用して、**ユーザー用にクライアントを展開** します。

- **Powershell の手順**: [Azure Information Protection クライアントでの powershell の使用](./rms-client/client-admin-guide-powershell.md)

- **ローカル監視**: [Windows イベントモニターを使用したローカルの使用状況ログ](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-classic-client)

> [!TIP]
> また、保護のみを目的として [Azure Information Protection 展開のロードマップ](deployment-roadmap-protect-only.md)を使用することもできます。これは、従来のクライアントでのみサポートされています。

## <a name="next-steps"></a>次のステップ

Azure Information Protection を展開するときに、 [よく寄せられる質問](faqs.md)、 [既知の問題](known-issues.md)、およびその他のリソースに関する [情報とサポート](information-support.md) ページを確認すると役立つ場合があります。