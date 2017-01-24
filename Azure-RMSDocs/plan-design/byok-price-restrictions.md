---
title: "BYOK の料金と制限事項 | Azure Information Protection"
description: "Azure RMS でお客様が管理するキーを使用する場合 (Bring Your Own Key または BYOK と呼ばれます) は、制限事項を確認してください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 2e8a00d4c8d38387645d015d3f69a4d568fc9683


---

# <a name="byok-pricing-and-restrictions"></a>BYOK の料金と制限事項

>*適用対象: Azure Information Protection、Office 365*


Azure Information Protection が含まれているサブスクリプションを所有する組織は、追加料金なしで、顧客管理のキー (BYOK) を使用し、[キーの使用状況ログを記録](../deploy-use/log-analyze-usage.md)するように Azure Information Protection テナントを構成することができます。 

キーは Azure Key Vault に格納する必要があります。Azure Key Vault には有料 (または試用版) の Azure サブスクリプションが必要です。また、HSM で保護されたキーをサポートするには、Azure Key Vault Premium サービス層を使用する必要があります。 HSM で保護されたキーを Azure Key Vault で使用する場合は、月単位の料金が発生します。 詳細については、[Azure Key Vault の価格のページ](https://azure.microsoft.com/en-us/pricing/details/key-vault/)を参照してください。

Azure Information Protection テナント キーに対して Azure Key Vault を使用する場合は、このキーの専用のキー コンテナーを専用のサブスクリプションで使用することで、それが Azure Rights Management サービスのみで使用されるようにすることをお勧めします。 

## <a name="benefits-of-using-azure-key-vault"></a>Azure Key Vault を使用する利点

追加的な保証として Azure Information Protection 使用状況ログを使用することに加えて、これと [Azure Key Vault のログ記録](https://azure.microsoft.com/documentation/articles/key-vault-logging/) との相互参照を行って、Azure Rights Management サービスのみでこのキーが使用されていることを個別に監視することができます。 必要な場合、キー コンテナーに対するアクセス許可を削除することにより、キーへのアクセスをすぐに取り消すことができます。

Azure Information Protection テナント キーに Azure Key Vault を使用するその他の利点:

- Azure Key Vault は一元的なキー管理ソリューションであり、暗号化を使用するさまざまなクラウドベースのサービスおよびオンプレミス サービスに対して一貫した管理ソリューションを実現します。

- Azure Key Vault では、キー管理のためのさまざまな組み込みのインターフェイス (PowerShell、CLI、REST API、Azure ポータルなど) をサポートしています。 監視などの特定のタスク用に最適化された機能を提供するために、Key Vault には他のサービスやツールも統合されています。 たとえば、Operations Management Suite から Log Analytics を介してキーの使用状況ログを分析したり、指定した条件が満たされたときにアラートを設定したりすることができます。

- Azure Key Vault では、セキュリティのベスト プラクティスとして認識されている役割の分離を実現しています。 Azure Information Protection の管理者は、データ分類とデータ保護の管理に専念し、Azure Key Vault の管理者は、暗号化キーの管理と、セキュリティまたはコンプライアンスで必要となる特別なポリシーの管理に専念することができます。

- 組織によっては、マスター キーが存在する必要がある場合、制限を設けているところがあります。 多くの Azure リージョンでサービスが提供されているため、Azure Key Vault ではマスター キーの保存先について高度な制御を行います。 現在、28 の Azure リージョンの中から選択することができ、この数は増える予定です。 詳細については、Azure サイトの [リージョン別の利用可能な製品] (https://azure.microsoft.com/regions/services/) ページを参照してください。

Azure Key Vault では、キーの管理ができるだけでなく、セキュリティ管理者は同じ管理エクスペリエンスによって、暗号化を使用する他のサービスやアプリケーションの証明書やシークレット (パスワードなど) を格納し、アクセスし、管理することができます。 

Azure Key Vault の詳細については、「[Azure Key Vault とは](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)」を参照してください。最新情報と、他のサービスでこのテクノロジを使用する方法については、「[Azure Key Vault team blog](https://blogs.technet.microsoft.com/kv/)」 (Azure Key Vault チームのブログ) を参照してください。


## <a name="restrictions-when-using-byok"></a>BYOK を使用する場合の制限

個人用の RMS を使用して無料のアカウントにサインアップしているユーザーがいる場合、この構成では BYOK または使用状況ログの記録を構成するテナント管理者がいないので、これらの機能を使用することはできません。


> [!NOTE]
> 個人用 RMS の詳細については、「[個人用 RMS と Azure Rights Management](../understand-explore/rms-for-individuals.md)」を参照してください。

![BYOK は Exchange Online をサポートしていません](../media/RMS_BYOK_noExchange.png)

BYOK と使用状況のログ記録は、Azure Information Protection が使用する Azure Rights Management サービス (Azure RMS) と統合されたすべてのアプリケーションでシームレスに利用できます。 これには SharePoint Online などのクラウド サービス、Exchange や SharePoint を実行し、RMS コネクタを使用して Azure RMS と連携するオンプレミス サーバー、Office 2016 および Office 2013 などのクライアント アプリケーションが含まれます。 どのアプリケーションが Azure RMS のリクエストを作成するかにかかわらず、キー利用状況ログを取得できます。

例外が&1; つあります。現時点では、 **Azure RMS BYOK には Exchange Online との互換性がありません**。 Exchange Online を使用する場合、Azure RMS のデプロイは既定のキー管理モードのままにして、キーの作成と管理をマイクロソフトで行うことをお勧めします。 こうすれば、たとえば Exchange Online が Azure RMS BYOK をサポートする場合など、後で BYOK に変更できます。 ただし、すぐに必要な場合は、Azure RMS を BYOK でデプロイして、Exchange Online 用の RMS 機能を制限付きで使用することもできます (保護されていない電子メールと保護されていない添付ファイルは引き続き完全に機能します)。

-   Outlook Web Access の保護された電子メールや保護された添付ファイルは表示できません。

-   Exchange ActiveSync IRM を使用するモバイル デバイス上の保護された電子メールは表示できません。

-   トランスポート復号化 (たとえば、マルウェアのスキャンなど)、およびジャーナルの復号化を行うことはできません。そのため、保護された電子メールと保護された添付ファイルはスキップされます。

-   IRM ポリシーを適用するトランスポート保護ルールとデータ損失防止 (DLP) を使用することはできません。そのため、これらの方法を使用して RMS 保護を適用することはできません。

-   サーバーベースで保護された電子メールが検索されます。そのため、保護された電子メールはスキップされます。

Exchange Online 用に制限された RMS 機能を使用して Azure RMS BYOK を使用する場合、RMS は Windows の Outlook および Mac の電子メール クライアント、および Exchange ActiveSync IRM を使用していないその他の電子メール クライアントで動作します。

AD RMS から Azure RMS への移行を行う場合、信頼された発行ドメイン (TPD) としてキーが Exchange Online にインポートされていることがあります (これを Exchange の用語では BYOK と呼びますが、Azure Key Vault の BYOK とは別のものです)。 この場合、Exchange Online から TPD を削除して、テンプレートとポリシーの競合を防ぐ必要があります。 詳細については、Exchange Online コマンドレット ライブラリの「[Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx)」を参照してください。

場合によっては、Exchange Online の Azure RMS BYOK の例外は、実際には問題にならないこともあります。 たとえば、BYOK とログ作成を必要とする組織は、データ アプリケーション (Exchange、SharePoint、Office) をオンプレミスで実行し、Azure RMS を使用するのは、オンプレミス AD RMS では簡単に使用できない機能 (他社とのコラボレーションやモバイル クライアントからのアクセスなど) を使用するためです。 BYOK とログ作成はこのシナリオで問題なく動作し、組織は Azure RMS サブスクリプションを完全に制御できます。

## <a name="next-steps"></a>次のステップ

独自のキーを管理する場合は、「[Azure Rights Management テナント キーの実装](plan-implement-tenant-key.md#implementing-your-azure-information-protection-tenant-key)」を参照してください。

テナント キーを Microsoft が管理する既定の構成を使用する場合は、「Azure Rights Management テナント キーを計画して実装する」の「[次のステップ](plan-implement-tenant-key.md#next-steps)」セクションを参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


