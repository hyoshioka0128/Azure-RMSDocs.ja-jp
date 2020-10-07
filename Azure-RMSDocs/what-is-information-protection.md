---
title: Azure Information Protection (AIP) とは
description: Azure Information Protection (AIP) は、組織によるドキュメントやメールのラベル付けに役立つサービスです。 AIP によって、保存されている場所に関係なくデータの分類と保護を行うことができます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/23/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 25b520e08d8379580226d589fec511d502065156
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91588407"
---
# <a name="what-is-azure-information-protection"></a>Azure Information Protection とは

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection (AIP) は、組織がドキュメントや電子メールにラベルを適用して、分類および保護できるようにするクラウドベースのソリューションです。 次のようにラベルを適用できます。

- 管理者がルールと条件を使用して**自動的に**
- ユーザーが**手動で**
- **組み合わせによって** (管理者の定義した推奨事項がユーザーに表示される)

たとえば、管理者は、クレジット カート情報などの機密データを検出するルールを使用するラベルを構成することができます。 この場合、Word ファイルにクレジット カード情報を保存するすべてのユーザーに対して、このシナリオに合った関連ラベルの適用を推奨するヒントをドキュメントの上部に表示することができます。

ラベルによってドキュメントを[分類](#how-labels-apply-classification-with-aip)し、必要に応じて[保護](#how-aip-protects-your-data)することができます。これにより、次の操作が可能になります。

- コンテンツの使用方法を**追跡および制御する**
- **データ フローを分析**してビジネスに関する分析情報を得る **- 危険な動作を検出**して修正措置を講じる
- **ドキュメントへのアクセスを追跡**し、データの漏えいや悪用を防ぐ
- その他...

## <a name="how-labels-apply-classification-with-aip"></a>AIP でのラベルによる分類のしくみ

Azure Information Protection を使用して、ドキュメントとメールの両方に分類ラベルを適用できます。

次のようなコンテンツのラベル付けがあります。

- データの保存場所やデータの共有者に関係なく識別できる**分類**。
- ヘッダー、フッター、透かしなどの**視覚的なマーキング**。
- クリア テキストでファイルと電子メール ヘッダーに追加される**メタデータ**。 クリア テキストのメタデータでは、その他のサービスが分類を識別して適切なアクションを取ることができます

たとえば、次の図では、[統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)を使用したラベル付けによって、電子メール メッセージが "*一般*" と分類されています。

:::image type="content" source="media/example-email-footerv2.png" alt-text="Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例&quot;:::

この例では、ラベルは次も行っています。

- **フッター &quot;*秘密度: 一般*" がメール メッセージに追加されました。** このフッターは、組織外に送信すべきではない一般的なビジネス データ用を示す、すべての受信者向けのビジュアル インジケーターです。
- **電子メール ヘッダーにメタデータが埋め込まれました。** ヘッダー データを使用すると、電子メール サービスはラベルを検査し、理論上、監査エントリを作成できるようになり、組織外への送信ができなくなります。

## <a name="how-aip-protects-your-data"></a>AIP によってデータを保護する方法

Azure Information Protection では、データを保護するために ["*Azure Rights Management サービス*" (Azure RMS)](what-is-azure-rms.md) が使用されます。 

Azure RMS は、Microsoft の他のクラウド サービスやアプリケーション (Microsoft 365 や Azure Active Directory など) に統合されますが、独自に使用したり、サードパーティーのアプリケーションや情報保護ソリューションと共に使用したりもできます。 Azure RMS はオンプレミスとクラウド ソリューションの両方で動作します。

Azure RMS では暗号化、ID、および承認ポリシーが使用されます。 AIP ラベルと同様に、Azure RMS を使用して適用された保護は、ドキュメントや電子メールの場所に関係なく保持されます。そのため、他のユーザーと共有されている場合でも、コンテンツを確実に管理できます。

保護設定は:

- **ラベルの構成に含めることができます**。そのため、ユーザーはラベルを適用するだけで、ドキュメントとメールを分類して保護できます。 
- 保護をサポートするアプリケーションとサービスによって**独自に使用することもできます**。ただし、ラベルを付けることはできません。 

    保護のみをサポートするアプリケーションとサービスでは、保護設定は [Rights Management テンプレート](#rights-management-templates)として表示されます。

たとえば、組織内のユーザーのみがアクセスできるように、レポートや売上予測スプレッドシートを構成することができます。 この場合、保護設定を適用して、ドキュメントを編集できるかどうかを制御したり、読み取り専用に制限したり、印刷されないようにしたりできます。

電子メールに同様の保護設定を適用して、転送されないようにしたり、[全員に返信] オプションを使用できないようにしたりできます。

### <a name="rights-management-templates"></a>Rights Management テンプレート

Azure Rights Management サービスを有効にするとすぐに、組織内のユーザーがデータにアクセスすることを制限する 2 つの既定の Rights Management テンプレートが使用可能になります。 これらのテンプレートをすぐに使用するか、独自の保護設定を構成して、新しいテンプレートにより制限の厳しいコントロールを適用します。

Rights Management テンプレートは、Azure Rights Management をサポートするすべてのアプリケーションやサービスで使用できます。

次の図は Exchange 管理センターの例を示しています。Exchange Online メール フロー ルールで RMS テンプレートを使用するように構成することができます。

:::image type="content" source="media/templates-exchangeonline-callouts.png" alt-text="Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例&quot;:::

この例では、ラベルは次も行っています。

- **フッター &quot;*秘密度: 一般*":::

> [!NOTE]
> 保護設定を含む AIP ラベルを作成すると、ラベルとは別に使用できる、対応する Rights Management テンプレートも作成されます。 
>  

詳細については、「[Azure Rights Management とは](what-is-azure-rms.md)」を参照してください

## <a name="aip-and-end-user-integration-for-documents-and-emails"></a>ドキュメントおよび電子メール用の AIP とエンドユーザーの統合

AIP クライアントにより、Office アプリケーションに Information Protection バーがインストールされ、エンド ユーザーが AIP とドキュメントや電子メールを統合できるようになります。

たとえば、Excel で[統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)を使用している場合:

![Excel の Azure Information Protection バーの例](./media/excelproplus-infoprotect-bar.png)

ラベルをドキュメントや電子メールに自動的に適用して、ユーザーの推測を排除したり、組織のポリシーに準拠したりできますが、Information Protection バーを使用すると、エンド ユーザーがラベルを選択して、分類を自分で適用することができます。

さらに、AIP クライアントを使用すると、ユーザーは Windows エクスプローラーの右クリック メニューを使用して、追加のファイルの種類、または複数のファイルを一度に分類して保護できるようになります。 次に例を示します。

:::image type="content" source="media/right-click-classify-protect-folder.png" alt-text="Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例&quot;:::

この例では、ラベルは次も行っています。

- **フッター &quot;*秘密度: 一般*":::

**[分類して保護する]** メニュー オプションは、Office アプリケーションの Information Protection バーと同様に機能し、ユーザーがラベルを選択したり、カスタムのアクセス許可を設定したりできるようになります。

> [!TIP]
> パワー ユーザーまたは管理者は、PowerShell コマンドを使用すれば、複数のファイルの分類と保護をより効率的に管理して設定できることに気付くかもしれません。 クライアントには[関連する PowerShell コマンド](/powershell/module/azureinformationprotection)が含まれており、個別にインストールすることもできます。

ユーザーと管理者は、ドキュメント追跡サイトを使用して、保護されたドキュメントを監視したり、誰がいつアクセスしたかを観察したりできます。 不正使用が疑われる場合、これらの文書に対するアクセスを取り消すことも可能です。 次に例を示します。

![ドキュメント追跡サイトの [アクセスの取り消し] アイコン](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>電子メールにおける追加の統合

Exchange Online で AIP を使用すると、保護された電子メールがどのデバイスでも読み取れることが保証されるため、任意のユーザーに送信できるというベネフィットもあります。

たとえば、機密情報を、**Gmail**、**Hotmail**、または **Microsoft** アカウントを使用している個人用メール アドレス、または Microsoft 365 や Azure AD のアカウントがないユーザーに送信する必要があるとします。 これらの電子メールは、保存時または送信中に暗号化し、本来の受信者のみが読み取ることができるようにする必要があります。

このシナリオには、[Office 365 Message Encryption の機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)が必要です。 保護された電子メールを自分のネイティブ電子メール クライアントで開くことはできない受信者の場合は、ワンタイム パスコードを使用することでブラウザー内で機密情報を閲覧することができます。

たとえば、Gmail ユーザーが受信した電子メール メッセージに次のプロンプトが表示される場合があります。

:::image type="content" source="media/ome-message.png" alt-text="Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例&quot;:::

この例では、ラベルは次も行っています。

- **フッター &quot;*秘密度: 一般*":::

電子メールを送信するユーザーに必要なアクションは、所属する組織内のユーザーに保護された電子メールを送信する場合と変わりありません。 たとえば、AIP クライアントによって Outlook のリボンに追加される **[転送不可]** ボタンを選択します。 

または、[転送不可] 機能をラベルに統合して、ユーザーが分類と保護の両方をその電子メールに適用できるようにすることもできます。 たとえば、[統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)で:

![[転送不可] として構成されたラベルを選択](./media/recipients-only-label2.png)

管理者は、権利保護を適用するメール フロー ルールを構成して、ユーザーを自動的に保護することもできます。

そのようなメールに添付された Office ドキュメントも、自動的に保護されます。

## <a name="scanning-for-existing-content-to-classify-and-protect"></a>既存のコンテンツをスキャンして分類および保護する

ドキュメントや電子メールのラベル付けは作成時に行うのが理想的です。 しかし、既に多数のドキュメントがオンプレミスまたはクラウドに保存されている場合は、これらのドキュメントも分類して保護する必要があります。

既存のコンテンツを分類して保護するには、次のいずれかの方法を使用します。

- **オンプレミス ストレージ**: [Azure Information Protection スキャナー](deploy-aip-scanner.md)を使用して、ネットワーク共有と、Microsoft SharePoint Server のサイトとライブラリにあるドキュメントの検出、分類、保護を行います。

    スキャナーは、Windows Server 上でサービスとして実行され、同じポリシー ルールを使用して機密情報を検出し、特定のラベルをドキュメントに適用します。 

    または、スキャナーを使用してファイルの内容を検査せずに、データ リポジトリ内のすべてのドキュメントに既定のラベルを適用します。 スキャナーを報告モードのみで使用して、所持していたことを知らなかった機密情報を発見することもできます。

- **クラウド データ ストレージ**: [Microsoft Cloud App Security](/cloud-app-security/azip-integration) を使用して、Box、SharePoint、OneDrive 内にあるドキュメントにラベルを適用します。 チュートリアルについては、「[Azure Information Protection 分類ラベルの自動適用](/cloud-app-security/use-case-information-protection)」を参照してください 

## <a name="latest-labeling-updates-for-microsoft-365"></a>Microsoft 365 のラベル付けに関する最新の更新

Microsoft 365 を使用した、あらゆる場所にある機密情報の検出、分類、保護、および監視に Azure Information Protection が役立つしくみについて、最新情報をご覧ください:

> [!VIDEO https://www.youtube.com/embed/UI0p9xqMNfI]

詳細については、次をご覧ください。

- [Microsoft 365 管理センターの新機能](/microsoft-365/admin/whats-new-in-preview)
- [SharePoint 管理センターの新機能](/sharepoint/what-s-new-in-admin-center)

## <a name="additional-azure-information-protection-resources"></a>Azure Information Protection の追加資料

- **無料試用版:** [Enterprise Mobility + Security E5](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- **サブスクリプションのオプションと価格:** [Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)

- **クライアントのダウンロード:** [Azure Information Protection クライアント](https://www.microsoft.com/download/details.aspx?id=53018)

- **カスタマイズ可能なエンド ユーザー ガイドのダウンロード:** [Azure Information Protection エンド ユーザー導入ガイド](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

- **よくあるご質問:** [Azure Information Protection に関してよく寄せられる質問](faqs.md)

- **Yammer:** [Azure Information Protection](https://www.yammer.com/AskIPTeam)

- **Docs Twitter フィード:** [https://twitter.com/docsmsft](https://twitter.com/docsmsft)

**その他のリソース:** [Azure Information Protection の情報とサポート](information-support.md)

### <a name="microsoft-ignite"></a>Microsoft Ignite

Microsoft Ignite 2019 オーランドは大成功でした。 そこでは、最新の更新プログラムと機能強化を含む Azure Information Protection に関する有益な情報が多数提供されました。 ご参加いただけなかった場合でも、後から視聴できるようにセッションが録画されています。

お勧めする上位 5 つのセッションについて、次の一覧をご覧ください。

- [BRK2119 - 機密データをセキュリティで保護しましょう。Microsoft Information Protection の最新機能について理解します](https://myignite.techcommunity.microsoft.com/sessions/81172?source=sessions)
 
- [THR3067 - データを理解する:ご自分の機密データ環境をよりよく理解するための上位 5 つのヒントとテクニック](https://myignite.techcommunity.microsoft.com/sessions/81183)

- [BRK3103 - 機密性の高いファイルとデータを保護することは、困難な場合があります。セキュリティと従業員の生産性を両立させる、適切なデータ保護オプションを選択します](https://myignite.techcommunity.microsoft.com/sessions/81177?source=sessions)

- [BRK2120 - Azure Information Protection をご理解いただけましたか。統一ラベル付け、ポリシーの構成、クライアント、分析について説明します](https://myignite.techcommunity.microsoft.com/sessions/81178?source=sessions)

- [BRK2121 - Microsoft Information Protection SDK を使用して、機密ラベル付けと保護の機能を独自のアプリと ISV ソリューションにまで拡張します](https://myignite.techcommunity.microsoft.com/sessions/81179?source=sessions)

最新のブログ投稿: [機密データがある場所を把握し、Microsoft 365 でインテリジェントに保護する](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Understand-where-your-sensitive-data-is-located-and/ba-p/960465)


## <a name="next-steps"></a>次のステップ

[クイック スタート](quickstart-viewpolicy.md)と[チュートリアル](infoprotect-quick-start-tutorial.md)を参照すれば、Azure Information Protection をご自分で構成および確認できます。 

このサービスを組織向けにデプロイする準備ができている場合は、[攻略ガイド](how-to-guides.md)を参照してください。