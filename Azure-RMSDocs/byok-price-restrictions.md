---
title: BYOK の詳細-Azure Information Protection
description: お客様が管理するキーを使用する場合の詳細と制限事項について説明します ("your your key" または BYOK と呼ばれます)。 Azure Information Protection を使用します。
author: cabailey
ms.author: cabailey
manager: rkarlin
ms.date: 11/22/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4a82afdeee9459b460b98a385102147c6c78ff28
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935182"
---
# <a name="bring-your-own-key-byok-details-for-azure-information-protection"></a>Azure Information Protection の独自のキー (BYOK) の詳細を表示する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Information Protection が含まれているサブスクリプションを持っている組織は、ユーザーが管理するキーを使用して[その使用状況をログに記録](log-analyze-usage.md)するように Azure Information Protection テナントを構成できます。 お客様が管理するキー構成は、"自分のキーを持ち込む"、BYOK と呼ばれることがよくあります。

このユーザーが管理するキーは、Azure サブスクリプションを必要とする Azure Key Vault に格納する必要があります。 HSM 保護キーを使用するには、Azure Key Vault Premium サービス レベルが必要です。 Azure Key Vault のキーを使用する場合は、月単位の料金が発生します。 詳細については、[Azure Key Vault の価格のページ](https://azure.microsoft.com/pricing/details/key-vault/)を参照してください。

Azure Information Protection テナント キーに対して Azure Key Vault を使用する場合は、このキーの専用のキー コンテナーを使用することで、それが Azure Rights Management サービスのみで使用されるようにすることをお勧めします。 この構成によって、その他のサービスの呼び出しがキー コンテナーの[サービスの制限](/azure/key-vault/key-vault-service-limits)を超えないようにすることができます。このために、Azure Rights Management サービスの応答時間が調整されることもあります。  

さらに、通常、Azure Key Vault を使用するサービスごとに異なるキー管理要件があるため、無効な構成に対する安全策として、このキー コンテナーに別の Azure サブスクリプションを使用することをお勧めします。 

ただし、Azure Key Vault を使用する他のサービスと Azure サブスクリプションを共有する場合は、サブスクリプションで管理者の共通セットを共有しているようにします。 この予防措置は、サブスクリプションを使用する管理者が、アクセス権のあるすべてのキーをよく理解していることを意味します。そのため、誤って構成する可能性は低くなります。 

たとえば、Azure Information Protection テナント キーの管理者が、Office 365 カスタマー キーと CRM Online のキーを管理するユーザーと同じ場合に共有された Azure サブスクリプションです。 

または、顧客キーまたは CRM Online のキーを管理する管理者が Azure Information Protection テナントキーを管理するユーザーと同じでない場合は、Azure Information Protection に対して Azure サブスクリプションを共有しないことをお勧めします。

## <a name="benefits-of-using-azure-key-vault"></a>Azure Key Vault を使用する利点

さらなる保証を行うために、 [Azure Key Vault ログ](/azure/key-vault/key-vault-logging)を使用して Azure Information Protection の使用状況ログを相互参照できます。 Key Vault ログには、Azure Rights Management サービスのみがキーを使用していることを個別に監視する方法が用意されています。 必要な場合、キー コンテナーに対するアクセス許可を削除することにより、キーへのアクセスをすぐに取り消すことができます。

Azure Information Protection テナントキーに Azure Key Vault を使用するその他の利点を次に示します。

- Azure Key Vault は一元的なキー管理ソリューションであり、暗号化を使用するさまざまなクラウドベースのサービスおよびオンプレミス サービスに対して一貫した管理ソリューションを実現します。

- Azure Key Vault では、キー管理のためのさまざまな組み込みのインターフェイス (PowerShell、CLI、REST API、Azure Portal など) をサポートしています。 監視などの特定のタスク用に最適化された機能を提供するために、Key Vault には他のサービスやツールも統合されています。 たとえば、Operations Management Suite から Log Analytics を介してキーの使用状況ログを分析したり、指定した条件が満たされたときにアラートを設定したりすることができます。

- Azure Key Vault では、セキュリティのベスト プラクティスとして認識されている役割の分離を実現しています。 Azure Information Protection の管理者は、データ分類とデータ保護の管理に専念し、Azure Key Vault の管理者は、暗号化キーの管理と、セキュリティまたはコンプライアンスで必要となる特別なポリシーの管理に専念することができます。

- 組織によっては、マスター キーが存在する必要がある場合、制限を設けているところがあります。 多くの Azure リージョンでサービスが提供されているため、Azure Key Vault ではマスター キーの保存先について高度な制御を行います。 複数の Azure リージョンから選択することができ、この数を増やすことが予想されます。 詳細については、Azure サイトの「[リージョン別の利用可能な製品](https://azure.microsoft.com/regions/services/)」のページを参照してください。

Azure Key Vault では、キーの管理ができるだけでなく、セキュリティ管理者は同じ管理エクスペリエンスによって、暗号化を使用する他のサービスやアプリケーションの証明書やシークレット (パスワードなど) を格納し、アクセスし、管理することができます。 

Azure Key Vault の詳細については、「[Azure Key Vault とは](/azure/key-vault/key-vault-whatis)」を参照してください。最新情報と、他のサービスでこのテクノロジを使用する方法については、「[Azure Key Vault team blog](https://blogs.technet.microsoft.com/kv/)」 (Azure Key Vault チームのブログ) を参照してください。

## <a name="byok-support-for-services-and-clients"></a>サービスとクライアントの BYOK のサポート

BYOK と[使用状況ログ](log-analyze-usage.md)は、データを保護するために Azure Information Protection によって使用される Azure Rights Management サービスと統合されているすべてのアプリケーションでシームレスに動作します。 これには SharePoint Online などのクラウド サービス、Exchange や SharePoint を実行し、RMS コネクタを使用して Azure Rights Management サービスと連携するオンプレミス サーバー、Office 2019、Office 2016、および Office 2013 などのクライアント アプリケーションが含まれます。 

Azure Rights Management サービスに要求を送信するアプリケーションによって、キー使用状況ログを取得します。

## <a name="next-steps"></a>次のステップ

独自のキーを管理する場合は、「[Azure Information Protection テナント キーを実装する](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key)」を参照してください。

テナント キーを Microsoft が管理する既定の構成を使用する場合は、「Azure Information Protection テナント キーを計画して実装する」の「[次の手順](plan-implement-tenant-key.md#next-steps)」セクションを参照してください。

