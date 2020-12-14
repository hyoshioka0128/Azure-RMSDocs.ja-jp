---
title: Azure Information Protection (AIP) ラベル付け、分類、保護
description: Azure Information Protection (AIP) がドキュメントと電子メールにラベルを付けて、データの分類と保護を行う方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 71f07f5ffb9167ab61653cef10c610968ff74786
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384198"
---
# <a name="azure-information-protection-aip-labeling-classification-and-protection"></a>Azure Information Protection (AIP) ラベル付け、分類、保護

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***関連**: [Azure Information Protection Windows 用のクライアントと従来のクライアントとの統合](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection (AIP) は、組織がドキュメントや電子メールにラベルを適用して、分類および保護できるようにするクラウドベースのソリューションです。 

たとえば、管理者は、クレジット カート情報などの機密データを検出するルールを使用するラベルを構成することができます。 この場合、Word ファイルにクレジット カード情報を保存するすべてのユーザーに対して、このシナリオに合った関連ラベルの適用を推奨するヒントをドキュメントの上部に表示することができます。

ラベルによってドキュメントを[分類](#how-labels-apply-classification-with-aip)し、必要に応じて[保護](#how-aip-protects-your-data)することができます。これにより、次の操作が可能になります。

- コンテンツの使用方法を **追跡および制御する**
- **データ フローを分析** してビジネスに関する分析情報を得る **- 危険な動作を検出** して修正措置を講じる
- **ドキュメントへのアクセスを追跡** し、データの漏えいや悪用を防ぐ
- その他...

## <a name="how-labels-apply-classification-with-aip"></a>AIP でのラベルによる分類のしくみ

AIP でコンテンツにラベルを付けるには、次のものが含まれます。

- データの保存場所やデータの共有者に関係なく識別できる **分類**。
- ヘッダー、フッター、透かしなどの **視覚的なマーキング**。
- **メタデータ**。クリアテキストでファイルと電子メールヘッダーに追加されます。 クリア テキストのメタデータでは、その他のサービスが分類を識別して適切なアクションを取ることができます

たとえば、次の図では、ラベル付けによって電子メールメッセージが *一般* に分類されています。

:::image type="content" source="media/example-email-footerv2.png" alt-text="Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例":::

この例では、ラベルは次も行っています。

- ***[秘密度: 全般* ] のフッターを電子メールメッセージに追加しまし** た。 このフッターは、組織外に送信すべきではない一般的なビジネス データ用を示す、すべての受信者向けのビジュアル インジケーターです。
- **電子メールヘッダーに埋め込まれたメタデータ**。 ヘッダー データを使用すると、電子メール サービスはラベルを検査し、理論上、監査エントリを作成できるようになり、組織外への送信ができなくなります。

ラベルは、管理者がルールと条件を使用して手動で適用することも、ユーザーが手動で適用することもできます。また、管理者がユーザーに表示する推奨事項を定義する組み合わせを使用することもできます

## <a name="how-aip-protects-your-data"></a>AIP によってデータを保護する方法

Azure Information Protection では、データを保護するために ["*Azure Rights Management サービス*" (Azure RMS)](what-is-azure-rms.md) が使用されます。 

Azure RMS は、Microsoft の他のクラウド サービスやアプリケーション (Office 365 や Azure Active Directory など) に統合されますが、独自に使用したり、サードパーティーのアプリケーションや情報保護ソリューションと共に使用したりもできます。 Azure RMS はオンプレミスとクラウド ソリューションの両方で動作します。

Azure RMS では暗号化、ID、および承認ポリシーが使用されます。 AIP ラベルと同様に、Azure RMS を使用して適用された保護は、ドキュメントや電子メールの場所に関係なく保持されます。そのため、他のユーザーと共有されている場合でも、コンテンツを確実に管理できます。

保護設定は:

- ラベル **の構成の一部**。ユーザーはラベルを適用するだけで、ドキュメントと電子メールを分類して保護することができます。 
- 保護をサポートするがラベル付けをサポートしていないアプリケーションやサービスによって、**独自に使用され** ます。 

    保護のみをサポートするアプリケーションとサービスでは、保護設定は [Rights Management テンプレート](#rights-management-templates)として表示されます。

たとえば、組織内のユーザーのみがアクセスできるように、レポートや売上予測スプレッドシートを構成することができます。 この場合、保護設定を適用して、ドキュメントを編集できるかどうかを制御したり、読み取り専用に制限したり、印刷されないようにしたりできます。

電子メールに同様の保護設定を適用して、転送されないようにしたり、[全員に返信] オプションを使用できないようにしたりできます。

### <a name="rights-management-templates"></a>Rights Management テンプレート

Azure Rights Management サービスを有効にするとすぐに、組織内のユーザーがデータにアクセスすることを制限する 2 つの既定の Rights Management テンプレートが使用可能になります。 これらのテンプレートをすぐに使用するか、独自の保護設定を構成して、新しいテンプレートにより制限の厳しいコントロールを適用します。

Rights Management テンプレートは、Azure Rights Management をサポートするすべてのアプリケーションやサービスで使用できます。

次の図は Exchange 管理センターの例を示しています。Exchange Online メール フロー ルールで RMS テンプレートを使用するように構成することができます。

:::image type="content" source="media/templates-exchangeonline-callouts.png" alt-text="Exchange Online のテンプレートを選択する場合の例":::

> [!NOTE]
> 保護設定を含む AIP ラベルを作成すると、ラベルとは別に使用できる、対応する Rights Management テンプレートも作成されます。 
>  

詳細については、「[Azure Rights Management とは](what-is-azure-rms.md)」を参照してください

## <a name="aip-and-end-user-integration-for-documents-and-emails"></a>ドキュメントおよび電子メール用の AIP とエンドユーザーの統合

AIP クライアントにより、Office アプリケーションに Information Protection バーがインストールされ、エンド ユーザーが AIP とドキュメントや電子メールを統合できるようになります。

たとえば、Excel の場合は次のようになります。

![Excel の Azure Information Protection バーの例](./media/excelproplus-infoprotect-bar.png)

ラベルをドキュメントや電子メールに自動的に適用して、ユーザーの推測を排除したり、組織のポリシーに準拠したりできますが、Information Protection バーを使用すると、エンド ユーザーがラベルを選択して、分類を自分で適用することができます。

さらに、AIP クライアントを使用すると、ユーザーは Windows エクスプローラーの右クリック メニューを使用して、追加のファイルの種類、または複数のファイルを一度に分類して保護できるようになります。 次に例を示します。

:::image type="content" source="media/right-click-classify-protect-folder.png" alt-text="Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]":::

**[分類して保護する]** メニュー オプションは、Office アプリケーションの Information Protection バーと同様に機能し、ユーザーがラベルを選択したり、カスタムのアクセス許可を設定したりできるようになります。

> [!TIP]
> パワー ユーザーまたは管理者は、PowerShell コマンドを使用すれば、複数のファイルの分類と保護をより効率的に管理して設定できることに気付くかもしれません。 クライアントには[関連する PowerShell コマンド](https://docs.microsoft.com/powershell/module/azureinformationprotection)が含まれており、個別にインストールすることもできます。

ユーザーと管理者は、ドキュメント追跡サイトを使用して、保護されたドキュメントを監視したり、誰がいつアクセスしたかを観察したりできます。 不正使用が疑われる場合、これらの文書に対するアクセスを取り消すことも可能です。 次に例を示します。

![ドキュメント追跡サイトの [アクセスの取り消し] アイコン](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>電子メールにおける追加の統合

Exchange Online で AIP を使用すると、保護された電子メールがどのデバイスでも読み取れることが保証されるため、任意のユーザーに送信できるというベネフィットもあります。

たとえば、機密情報を、**Gmail**、**Hotmail**、または **Microsoft** アカウントを使用している個人用メール アドレス、または Office 365 や Azure AD のアカウントがないユーザーに送信する必要があるとします。 これらの電子メールは、保存時または送信中に暗号化し、本来の受信者のみが読み取ることができるようにする必要があります。

このシナリオには、[Office 365 Message Encryption の機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)が必要です。 受信者が組み込みの電子メールクライアントで保護された電子メールを開くことができない場合は、ワンタイムパスコードを使用してブラウザーで機微な情報を読み取ることができます。

たとえば、Gmail ユーザーが受信した電子メール メッセージに次のプロンプトが表示される場合があります。

:::image type="content" source="media/ome-message.png" alt-text="OME と AIP の Gmail 受信者エクスペリエンス":::

電子メールを送信するユーザーに必要なアクションは、所属する組織内のユーザーに保護された電子メールを送信する場合と変わりありません。 たとえば、AIP クライアントによって Outlook のリボンに追加される **[転送不可]** ボタンを選択します。 

または、[ **転送不可** ] 機能をラベルに統合して、ユーザーが分類と保護の両方をこの電子メールに適用できるようにすることもできます。 次に例を示します。

![[転送不可] として構成されたラベルを選択](./media/recipients-only-label2.png)

管理者は、権利保護を適用するメール フロー ルールを構成して、ユーザーを自動的に保護することもできます。

そのようなメールに添付された Office ドキュメントも、自動的に保護されます。

## <a name="scanning-for-existing-content-to-classify-and-protect"></a>既存のコンテンツをスキャンして分類および保護する

ドキュメントや電子メールのラベル付けは作成時に行うのが理想的です。 しかし、既に多数のドキュメントがオンプレミスまたはクラウドに保存されている場合は、これらのドキュメントも分類して保護する必要があります。

既存のコンテンツを分類して保護するには、次のいずれかの方法を使用します。

- **オンプレミス ストレージ**: [Azure Information Protection スキャナー](deploy-aip-scanner.md)を使用して、ネットワーク共有と、Microsoft SharePoint Server のサイトとライブラリにあるドキュメントの検出、分類、保護を行います。

    スキャナーは、Windows Server 上でサービスとして実行され、同じポリシー ルールを使用して機密情報を検出し、特定のラベルをドキュメントに適用します。 

    または、スキャナーを使用してファイルの内容を検査せずに、データ リポジトリ内のすべてのドキュメントに既定のラベルを適用します。 スキャナーを報告モードのみで使用して、所持していたことを知らなかった機密情報を発見することもできます。

- **クラウド データ ストレージ**: [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/azip-integration) を使用して、Box、SharePoint、OneDrive 内にあるドキュメントにラベルを適用します。 チュートリアルについては、「[Azure Information Protection 分類ラベルの自動適用](https://docs.microsoft.com/cloud-app-security/use-case-information-protection)」を参照してください 


## <a name="next-steps"></a>次のステップ

クイックスタートとチュートリアルを使用して、Azure Information Protection を構成して表示します。

- [クイック スタート: 統合ラベル付けクライアントのデプロイ](quickstart-deploy-client.md)
- [チュートリアル:Azure Information Protection (AIP) 統合ラベル付けスキャナーのインストール](tutorial-install-scanner.md)
- [チュートリアル: Azure Information Protection (AIP) スキャナーを使用して機密コンテンツを検出する](tutorial-scan-networks-and-content.md)
- [チュートリアル: Azure Information Protection (AIP) を使用した Outlook での過剰共有の防止](tutorial-preventing-oversharing.md)

このサービスを組織向けにデプロイする準備ができている場合は、[攻略ガイド](how-to-guides.md)を参照してください。
