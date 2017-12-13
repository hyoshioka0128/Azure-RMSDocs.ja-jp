---
title: "BYOK の料金と制限事項 - Azure Information Protection"
description: "Azure Information Protection でお客様が管理するキーを使用する場合 (Bring Your Own Key または BYOK と呼ばれます) は、制限事項を確認してください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 981f7349c9ae279d48f5cb4795ffc2087f5ae4d8
ms.sourcegitcommit: 850869505942f9d1b74720085d253de4b54b19c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2017
---
# <a name="byok-pricing-and-restrictions"></a>BYOK の料金と制限事項

>*適用対象: Azure Information Protection、Office 365*


Azure Information Protection が含まれているサブスクリプションを所有する組織は、追加料金なしで、顧客管理のキー (BYOK) を使用し、[キーの使用状況ログを記録](../deploy-use/log-analyze-usage.md)するように Azure Information Protection テナントを構成することができます。 

キーは Azure Key Vault に保存する必要があります。これには Azure サブスクリプションが必要です。 HSM 保護キーを使用するには、Azure Key Vault Premium サービス レベルが必要です。 Azure Key Vault のキーを使用する場合は、月単位の料金が発生します。 詳細については、[Azure Key Vault の価格のページ](https://azure.microsoft.com/en-us/pricing/details/key-vault/)を参照してください。

Azure Information Protection テナント キーに対して Azure Key Vault を使用する場合は、このキーの専用のキー コンテナーを使用することで、それが Azure Rights Management サービスのみで使用されるようにすることをお勧めします。 この構成によって、その他のサービスの呼び出しがキー コンテナーの[サービスの制限](/azure/key-vault/key-vault-service-limits)を超えないようにすることができます。このために、Azure Rights Management サービスの応答時間が調整されることもあります。  

さらに、通常、Azure Key Vault を使用するサービスごとに異なるキー管理要件があるため、無効な構成に対する安全策として、このキー コンテナーに別の Azure サブスクリプションを使用することをお勧めします。 

ただし、Azure Key Vault を使用する他のサービスと Azure サブスクリプションを共有する場合は、サブスクリプションで管理者の共通セットを共有しているようにします。 この予防措置は、サブスクリプションを使用する管理者が、アクセス権のあるすべてのキーをよく理解していることを意味します。そのため、誤って構成する可能性は低くなります。 たとえば、Azure Information Protection テナント キーの管理者が、Office 365 カスタマー キーと CRM Online のキーを管理するユーザーと同じ場合に共有された Azure サブスクリプションです。 ただし、カスタマー キーと CRM Online のキーを管理する管理者が、Azure Information Protection テナント キーの管理者とは異なる場合は、Azure Information Protection の Azure サブスクリプションを共有しないことをお勧めします。

## <a name="benefits-of-using-azure-key-vault"></a>Azure Key Vault を使用する利点

追加的な保証として Azure Information Protection 使用状況ログを使用することに加えて、これと [Azure Key Vault のログ記録](https://azure.microsoft.com/documentation/articles/key-vault-logging/) との相互参照を行って、Azure Rights Management サービスのみでこのキーが使用されていることを個別に監視することができます。 必要な場合、キー コンテナーに対するアクセス許可を削除することにより、キーへのアクセスをすぐに取り消すことができます。

Azure Information Protection テナント キーに Azure Key Vault を使用するその他の利点:

- Azure Key Vault は一元的なキー管理ソリューションであり、暗号化を使用するさまざまなクラウドベースのサービスおよびオンプレミス サービスに対して一貫した管理ソリューションを実現します。

- Azure Key Vault では、キー管理のためのさまざまな組み込みのインターフェイス (PowerShell、CLI、REST API、Azure Portal など) をサポートしています。 監視などの特定のタスク用に最適化された機能を提供するために、Key Vault には他のサービスやツールも統合されています。 たとえば、Operations Management Suite から Log Analytics を介してキーの使用状況ログを分析したり、指定した条件が満たされたときにアラートを設定したりすることができます。

- Azure Key Vault では、セキュリティのベスト プラクティスとして認識されている役割の分離を実現しています。 Azure Information Protection の管理者は、データ分類とデータ保護の管理に専念し、Azure Key Vault の管理者は、暗号化キーの管理と、セキュリティまたはコンプライアンスで必要となる特別なポリシーの管理に専念することができます。

- 組織によっては、マスター キーが存在する必要がある場合、制限を設けているところがあります。 多くの Azure リージョンでサービスが提供されているため、Azure Key Vault ではマスター キーの保存先について高度な制御を行います。 現在、28 の Azure リージョンの中から選択することができ、この数は増える予定です。 詳細については、Azure サイトの [リージョン別の利用可能な製品] (https://azure.microsoft.com/regions/services/) ページを参照してください。

Azure Key Vault では、キーの管理ができるだけでなく、セキュリティ管理者は同じ管理エクスペリエンスによって、暗号化を使用する他のサービスやアプリケーションの証明書やシークレット (パスワードなど) を格納し、アクセスし、管理することができます。 

Azure Key Vault の詳細については、「[Azure Key Vault とは](/azure/key-vault/key-vault-whatis)」を参照してください。最新情報と、他のサービスでこのテクノロジを使用する方法については、「[Azure Key Vault team blog](https://blogs.technet.microsoft.com/kv/)」 (Azure Key Vault チームのブログ) を参照してください。

## <a name="restrictions-when-using-byok"></a>BYOK を使用する場合の制限

BYOK と使用状況のログ記録は、Azure Information Protection が使用する Azure Rights Management サービスと統合されたすべてのアプリケーションでシームレスに利用できます。 これには SharePoint Online などのクラウド サービス、Exchange や SharePoint を実行し、RMS コネクタを使用して Azure Rights Management サービスと連携するオンプレミス サーバー、Office 2016 および Office 2013 などのクライアント アプリケーションが含まれます。 どのアプリケーションが Azure Rights Management サービスのリクエストを作成するかにかかわらず、キー利用状況ログを取得できます。

Azure RMS から信頼された発行ドメイン (TPD) をインポートし、Exchange Online IRM を前に有効にしている場合、「[Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)」 (Azure Information Protection 上に構築される新しい Office 365 メッセージの暗号化機能の設定) の手順に従い、Azure Information Protection の BYOK に対応している Exchange Online の新機能を有効にします。

## <a name="next-steps"></a>次のステップ

独自のキーを管理する場合は、「[Azure Rights Management テナント キーの実装](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key)」を参照してください。

テナント キーを Microsoft が管理する既定の構成を使用する場合は、「Azure Rights Management テナント キーを計画して実装する」の「[次のステップ](plan-implement-tenant-key.md#next-steps)」セクションを参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
