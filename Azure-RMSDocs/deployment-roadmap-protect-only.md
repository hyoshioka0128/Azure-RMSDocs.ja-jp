---
title: Azure Information Protection (AIP) の展開ロードマップ (保護のみ)
description: 保護のみを実装する場合は、次の手順を使用して、組織の Azure Information Protection (AIP) の準備、実装、および管理を行います。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/23/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f56373bfd3aa37b13b89a552e1767bd954c81bde
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570255"
---
# <a name="azure-information-protection-deployment-roadmap-for-protection-only"></a>Azure Information Protection の展開ロードマップ (保護のみ)

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と **ラベル管理** は、**2021 年 3 月 31 日** で **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

> [!TIP]
> または、次のいずれかの記事を検索することもできます。
> - [分類、ラベル付け、保護のための展開ロードマップを AIP](deployment-roadmap-classify-label-protect.md)
> - [Azure Information Protection を使用する一般的なシナリオに関する攻略ガイド](how-to-guides.md)
>- [Azure Information Protection リリースロードマップ](information-support.md#information-about-new-releases-and-updates)

データ保護のみを実装する場合は、次の手順を推奨設定として使用して、組織の Azure Information Protection の準備、実装、管理を行うことができます。

このロードマップは、分類とラベルの両方をサポートしていないサブスクリプションをお持ちのお客様にお勧めしますが、ラベルなしの保護をサポートしています。 AIP classic クライアントがインストールされている必要があります。 

## <a name="deployment-process"></a>デプロイ プロセス

次の手順に従います。

1. [AIP protection サービスを含むサブスクリプションがあることを確認します。](#confirm-that-you-have-a-subscription-that-includes-the-aip-protection-service) 
1. [Azure Information Protection を使用するためのテナントを用意する](#prepare-your-tenant-to-use-azure-information-protection)
1. [Azure Information Protection クラシックとクライアントをインストールする Rights Management 用のアプリケーションとサービスを構成する](#install-the-azure-information-protection-classic-and-client-configure-applications-and-services-for-rights-management)
1. [データ保護ソリューションを使用および監視する](#use-and-monitor-your-data-protection-solutions)
1. [必要に応じてテナント アカウントの保護サービスを管理する](#administer-the-protection-service-for-your-tenant-account-as-needed)

## <a name="confirm-that-you-have-a-subscription-that-includes-the-aip-protection-service"></a>AIP protection サービスを含むサブスクリプションがあることを確認します。

予想される機能を含むサブスクリプションが組織にあることを確認します。 サブスクリプション情報と機能一覧は、[ [Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection) ] ページで使用できます。

ドキュメントと電子メールを保護する組織内の各ユーザーに、このサブスクリプションのライセンスを割り当てます。

> [!IMPORTANT]
> ユーザー ライセンスを無料の個人用 RMS サブスクリプションから手動で割り当てることや、このライセンスを組織の Azure Rights Management サービスの管理目的で使用することはしないでください。 
>
> このようなライセンスは、Microsoft 365 管理センターに **Rights Management Adhoc** と表示されるとともに、Azure AD PowerShell コマンドレット [Get-MsolAccountSku](/previous-versions/azure/dn194118(v=azure.100)) を実行したときに **RIGHTSMANAGEMENT_ADHOC** と表示されます。 
>
> 個人用 RMS サブスクリプションが自動的に付与されてユーザーに割り当てられるしくみの詳細については、「[個人用 RMS と Azure Information Protection](./rms-for-individuals.md)」を参照してください。

## <a name="prepare-your-tenant-to-use-azure-information-protection"></a>Azure Information Protection を使用するためのテナントを用意する

Azure Information Protection の保護サービスの使用を開始する前に、次の準備を行います。

1. **AIP のユーザーアカウントとグループを設定します。**

    Microsoft 365 テナントに、Azure Information Protection が組織のユーザーを認証および承認するために使用するユーザーアカウントとグループが含まれていることを確認します。 必要に応じて、これらのアカウントとグループを作成するか、オンプレミスのディレクトリからそれらを同期します。 

    詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

1. **テナントキーをどのように管理するかを決定します。**

    Microsoft でテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 セキュリティを強化するには、"hold your key" (HYOK) 保護を実装します。 

    詳しくは、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」をご覧ください。

1. **AIP 用の PowerShell をインストール** します。

    インターネットにアクセスできる1台以上のコンピューターに AIPService 用の PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行しても構いません。 

    詳細については、「 [AIPService PowerShell モジュールのインストール](./install-powershell.md)」を参照してください。

1. **AD RMS のみ: データをクラウドに移行** します。

    現在、AD RMS を使用している場合: キー、テンプレート、URL をクラウドに移行する統合を実行します。 

    詳細については、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

1. **保護をアクティブ化** します。

    文書や電子メールの保護を開始できるように、保護サービスがアクティブになっていることを確認します。 を段階的に展開する場合は、ユーザーの保護を適用する機能を制限するようにユーザーのオンボードコントロールを構成します。 

    詳細については、「[Activating the protection service from Azure Information Protection (Azure Information Protection の保護サービスのアクティブ化)](./activate-service.md)」をご覧ください。

1. **必要に応じてオプションの機能を構成** します。

    次の機能のいずれか、または後で構成することを検討してください。
    
    |機能  |説明  |
    |---------|---------|
    |**保護設定のカスタムテンプレート**     |  既定のテンプレートが組織にとって十分でない場合は、カスタムテンプレートを構成します。 </br>詳細については、「[Azure Information Protection のテンプレートを構成して管理する](./configure-policy-templates.md)」を参照してください。       |
    |**使用状況ログの記録**     | 使用状況ログを構成して、組織が保護サービスをどのように使用しているかを監視します。 </br>詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。        |
    | | |

## <a name="install-the-azure-information-protection-classic-and-client-configure-applications-and-services-for-rights-management"></a>Azure Information Protection クラシックとクライアントをインストールする Rights Management 用のアプリケーションとサービスを構成する

次の手順に従います。

1. **Azure Information Protection クラシッククライアントを展開する**
    
    Office 2010 をサポートし、Office ドキュメントや電子メール以外のファイルを保護し、保護されたドキュメントを追跡し、このクライアントのユーザートレーニングを提供するために、ユーザー用のクラシッククライアントをインストールします。 

    詳細については、「[Azure Information Protection client for Windows](./rms-client/aip-client.md)」(Windows 用 Azure Information Protection クライアント) を参照してください。

2. **Office のアプリケーションとサービスを構成する**
    
    SharePoint または Exchange Online で information rights management (IRM) 機能を使用するように Office アプリケーションとサービスを構成します。 

    詳細については、「 [Azure Rights Management 用のアプリケーションの構成](./configure-applications.md)」を参照してください。

3. **データ回復のスーパー ユーザー機能を構成する**
    
    Azure Information Protection によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure Rights Management のスーパー ユーザーとして構成します。 

    詳細については、「 [Azure Information Protection および探索サービスまたはデータの回復用のスーパーユーザーの構成](./configure-super-users.md)」を参照してください。

4. **既存ファイルを一括で保護する** 
    
    PowerShell コマンドレットを使用して、複数のファイルの種類を一括保護または一括保護解除することができます。 

    詳細については、管理者ガイドの「 [Azure Information Protection クライアントでの PowerShell の使用](./rms-client/client-admin-guide-powershell.md) 」を参照してください。
    
    Windows ベースのファイル サーバー上のファイルに対しては、スクリプトと Windows Server ファイル分類インフラストラクチャでこれらのコマンドレットを使用することができます。 詳細については、「[Windows Server ファイル分類インフラストラクチャ (FCI) での RMS の保護](./rms-client/configure-fci.md)」を参照してください。

5. **オンプレミス サーバーのコネクタをデプロイする**
    
    保護サービスで使用するオンプレミスのサービスがある場合は、Rights Management コネクタをインストールして構成します。 

    詳細については、「[Azure Rights Management コネクタをデプロイする](./deploy-rms-connector.md)」を参照してください。

## <a name="use-and-monitor-your-data-protection-solutions"></a>データ保護ソリューションを使用および監視する

これで、データを保護し、会社が保護サービスを使用している方法をログに記録する準備が整いました。 

詳細については次を参照してください:

- [Azure Rights Management サービスを利用したファイルの保護でユーザーを支援するヘルプ](./help-users.md)
- [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)

## <a name="administer-the-protection-service-for-your-tenant-account-as-needed"></a>必要に応じてテナント アカウントの保護サービスを管理する

保護サービスの使用を開始するときに、PowerShell がスクリプトまたは管理変更の自動化に役立つことがあります。 一部の高度な構成には、PowerShell も必要になる場合があります。 

詳細については、「 [PowerShell を使用した Azure Information Protection からの保護の管理](./administer-powershell.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

Azure Information Protection を展開するときに、 [よく寄せられる質問](faqs.md)と、その他のリソースの [情報とサポート](information-support.md) に関するページを確認すると役立つ場合があります。