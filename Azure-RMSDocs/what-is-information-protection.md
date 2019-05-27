---
title: Azure Information Protection とは - AIP
description: Azure Information Protection サービスの技術的な概要です。これは、組織でドキュメントや電子メールにラベル付けして、保存場所を問わずそのデータを分類および保護するのに役立ちます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/20/2019
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.openlocfilehash: 0bb1096a903be953eb9702bc89b6a8c98d340946
ms.sourcegitcommit: fe23bc3e24eb09b7450548dc32b4ef09c8970615
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "65935031"
---
# <a name="what-is-azure-information-protection"></a>Azure Information Protection とは

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection (AIP とも呼ばれます) は、ラベルを適用することで組織がドキュメントや電子メールを分類したり、必要に応じて保護したりするのに役立つクラウドベースのソリューションです。 ラベルの適用は、ルールや条件を定義する管理者が自動で実行するか、ユーザーが手動で実行するか、その組み合わせ (ユーザーにレコメンデーションが提示される) で実行します。 

ユーザーのコンピューターで動作する Azure Information Protection の例を、次の図に示します。 管理者は、機密データを検出するルールを使用してラベルを構成しました。この例ではクレジット カード情報が使用されます。 ユーザーがクレジット カード番号を含む Word ドキュメントを保存すると、管理者が構成したラベルを推奨するカスタム ツールヒントが表示されます。 このラベルによってドキュメントが分類され、保護されます。 

![Azure Information Protection による推奨分類の例](./media/info-protect-recommend-calloutsv2.png)

###### <a name="screenshot-from-the-azure-information-protection-clientfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>[Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)からのスクリーンショット

コンテンツを分類し (オプションで保護すると)、それを追跡したり、その用途を管理できるようになります。 データのフローを分析してビジネスに関する洞察を得たり、危険な動作を検出し修正措置を取ったり、文書へのアクセスを追跡したり、データの漏えいや誤用を防ぐことができます。

## <a name="how-labels-apply-classification"></a>ラベルによる分類のしくみ

Azure Information Protection のラベルは、文書と電子メールを分類するために使用します。 これを行うと、データの保存場所やデータの共有者に関係なく分類を識別できるようになります。 ラベルには、ヘッダー、フッター、透かしなどの視覚的なマーキングを含めることができます。 メタデータはクリア テキストでファイルと電子メール ヘッダーに追加されます。 クリア テキストなので、データ損失防止ソリューションなど、その他のサービスが分類を識別して適切なアクションを取ることができます。 

たとえば、次の電子メール メッセージは "一般" と分類されています。 ラベルでは、フッター "秘密度:一般" がメール メッセージに追加されました。 このフッターは、組織外に送信すべきではない一般的なビジネス データ用を示す、すべての受信者向けのビジュアル インジケーターです。 このラベルは、電子メール サービスがこの値を調べて監査エントリを作成したり、組織外への送信を回避したりできるように、電子メールのヘッダーに埋め込まれます。

![Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例](./media/example-email-footerv2.png)

###### <a name="screenshot-from-the-azure-information-protection-clientfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>[Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)からのスクリーンショット

## <a name="how-data-is-protected"></a>データ保護のしくみ

保護テクノロジには *Azure Rights Management* (しばしば Azure RMS と略される) が使用されています。 このテクノロジは、Microsoft の他のクラウド サービスやアプリケーション (Office 365 や Azure Active Directory など) にも統合されています。 また、独自の基幹業務アプリケーションや情報ベンダーの情報保護ソリューションで使用できます。アプリケーションやソリューションは、オンプレミスまたはクラウドのどちらにあってもかまいません。

この保護テクノロジでは、暗号化、ID、および承認ポリシーが使用されます。 文書や電子メールが Rights Management で保護されている場合、適用されるラベルの場合と同様に、どこに保存されているか (組織、ネットワーク、ファイル サーバー、アプリケーションの内部または外部) にかかわらず、適用される保護は維持されます。 この情報保護ソリューションならば、データが他者と共有されているときでも、所有者がデータの制御を維持できます。

たとえば、組織内のユーザーのみがアクセスできるようにレポート文書や売上予測のスプレッドシートを構成したり、その文書の編集の許可を制御したり、読み取り専用に制限したり、印刷できないよう制御することもできます。 電子メールについても同様に構成することができます。さらに、電子メールを転送不可に設定したり、[全員に返信] オプションを使用不可に設定したりできます。 

これらの保護設定は、ラベルの構成に含めることができます。そのため、ユーザーはラベルを適用するだけで、ドキュメントとメールの両方を分類できます。 ただし、保護をサポートするアプリケーションとサービスから同じ保護設定を使用することもできますが、ラベルを付けることはできません。 これらのアプリケーションとサービスでは、保護設定は "*Rights Management テンプレート*" として使用できるようになります。

### <a name="rights-management-templates"></a>Rights Management テンプレート

Azure Rights Management サービスを有効にするとすぐに、組織内のユーザーがデータにアクセスすることを制限する 2 つの既定のテンプレートが使用可能になります。 これらのテンプレートでは、即座に組織からのデータの漏えいを防止できます。 これらの既定のテンプレートを補うこともできます。その場合、より厳しい制御を適用する独自の保護設定を構成します。

保護設定を含む Azure Information Protection のラベルを作成すると、その処理の裏では、このアクションによって対応する Rights Management テンプレートが作成されます。 さらに、そのテンプレートは、Azure Rights Management をサポートするアプリケーションとサービスで使用できます。

たとえば、Exchange 管理センターから、これらのテンプレートを使用するように、Exchange Online メール フロー ルールを構成できます。

![Exchange Online のテンプレートを選択する場合の例](./media/templates-exchangeonline-callouts.png)

Azure Rights Management での保護の詳細については、「[Azure Rights Management とは](what-is-azure-rms.md)」を参照してください。

## <a name="integration-with-end-user-workflows-for-documents-and-emails"></a>ドキュメントおよび電子メール用のエンドユーザー ワークフローとの統合

Azure Information Protection は、Azure Information Protection クライアントがインストールされている場合、エンド ユーザーの既存のワークフローと統合されます。 このクライアントは、Office アプリケーションに、Word にこのバーを表示した最初の図のように Information Protection バーをインストールします。 同じ Information Protection バーが Excel、PowerPoint、および Outlook に追加されます。 次に例を示します。

![Excel の Azure Information Protection バーの例](./media/excelproplus-infoprotect-bar.png)

###### <a name="screenshot-from-the-azure-information-protection-unified-labeling-clientfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>[Azure Information Protection 統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)からのスクリーンショット 

エンド ユーザーはこの Information Protection バーを使用して、正しい分類のラベルを簡単に選択できるようになります。 必要に応じて、ラベルを自動的に適用してユーザーの推測を排除したり、組織のポリシーに準拠したりすることもできます。

追加のファイルの種類を分類して保護し、複数のファイルを一度にサポートするには、次のようにして、エクスプローラーからファイルまたはフォルダーを右クリックします。

![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](./media/right-click-classify-protect-folder.png)

エクスプローラーから **[分類して保護する]** メニュー オプションを選択すると、Office デスクトップ アプリで Information Protection バーを使用する場合と同じように、ラベルを選択することができます。 必要に応じて、独自のカスタム アクセス許可を設定することもできます。

パワー ユーザー (および管理者) は、PowerShell コマンドを使用すれば、複数のファイルの分類と保護をより効率的に管理して設定できることに気付くかもしれません。 これらのアクションを行う PowerShell コマンドは、クライアントと共に自動的に含まれますが、PowerShell モジュールを個別にインストールすることもできます。

ドキュメントが保護されたら、ユーザーと管理者はドキュメント追跡サイトを使用して、これらのドキュメントに誰がいつアクセスしているかを監視することができます。 不正使用が疑われる場合は、これらのドキュメントに対するアクセスを取り消すこともできます。

![ドキュメント追跡サイトの [アクセスの取り消し] アイコン](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>電子メールにおける追加の統合

Exchange Online で Azure Information Protection を使用する場合は、追加の利点を得られます:保護されたメールを任意のユーザーに送信し、そのユーザーが任意のデバイス上でそのメールを読み取れるようにすることができます。

たとえば、ユーザーが機密情報を、**Gmail**、**Hotmail**、または**Microsoft** アカウントを使用している個人用メール アドレスに送信する必要があるとします。 または、Office 365 用のアカウントまたは Azure AD 内のアカウントを持っていないユーザーに機密情報を送信する必要があるとします。 これらの電子メールは、保存時または送信中に暗号化し、本来の受信者のみが読み取ることができるようにする必要があります。

このシナリオには、[Office 365 Message Encryption の新機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)が必要です。 保護された電子メールを自分のネイティブ電子メール クライアントで開くことはできない受信者の場合は、ワンタイム パスコードを使用することでブラウザー内で機密情報を閲覧することができます。

たとえば、Gmail ユーザーには、電子メール メッセージに次の内容が表示されます。

![OME と AIP の Gmail 受信者エクスペリエンス](./media/ome-message.png)

電子メールを送信するユーザーにとって、ワークフローは、所属する組織内のユーザーに保護された電子メールを送信する場合と変わりありません。 たとえば、ユーザーは Azure Information Protection クライアントによって Outlook のリボンに追加される **[転送不可]** ボタンを選択することができます。 または、ユーザーが選択したラベルに [転送不可] 機能を統合することができます。これにより、電子メールは分類され保護されます。 次に例を示します。

![[転送不可] として構成されたラベルを選択](./media/recipients-only-label2.png)

###### <a name="screenshot-from-the-azure-information-protection-unified-labeling-clientfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>[Azure Information Protection 統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)からのスクリーンショット

または、権利保護を適用するメール フロー ルールを使用して、ユーザーを自動的に保護することができます。 

そのようなルールを適用した電子メールに Office ドキュメントを添付した場合、そのドキュメントも自動的に保護されます。

## <a name="classifying-and-protecting-existing-documents"></a>既存のドキュメントの分類と保護

ドキュメントと電子メールは、最初に作成したときにラベル付けすることが理想的です。 しかし、データ ストアには既存のドキュメントが多数ある場合があり、これらのドキュメントも分類して保護する必要があります。 これらのデータ ストアは、オンプレミスか、またはクラウド内にある場合があります。

オンプレミスのデータ ストアの場合、Azure Information Protection スキャナーを使用して、ローカル フォルダー、ネットワーク共有、SharePoint Server のサイトとライブラリにあるドキュメントの検出、分類、保護を行います。 スキャナーは、Windows Server 上のサービスとして実行されます。 ポリシー内の同じ規則を使用して、機密データを検出し、ドキュメントに特定のラベルを適用することができます。 または、ファイルの内容を検査せずに、データ リポジトリ内のすべてのドキュメントに既定のラベルを適用できます。 また、スキャナーを報告モードのみで使用して、所持していたことを知らなかった機密情報を発見することもできます。 

スキャナーのデプロイと使用方法については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」をご覧ください。

クラウドのデータ ストアの場合、Microsoft Cloud App Security を使用して、Box、SharePoint Online、OneDrive for Business 内にあるドキュメントにラベルを適用します。 詳細については、「[Azure Information Protection 分類ラベルを自動的に適用する](/cloud-app-security/use-case-information-protection)」と「[Azure Information Protection の統合](/cloud-app-security/azip-integration)」をご覧ください。

## <a name="latest-labeling-updates-for-microsoft-365"></a>Microsoft 365 のラベル付けに関する最新の更新

あらゆる場所にある機密情報の検出、分類、保護、および監視に Azure Information Protection が役立つしくみについて、最新情報をご覧ください:

> [!VIDEO https://www.youtube.com/embed/UI0p9xqMNfI]

## <a name="resources-for-azure-information-protection"></a>Azure Information Protection の参考資料

- 無料試用版:[Enterprise Mobility + Security E5](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- サブスクリプションのオプションと価格:[Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)

- クライアントのダウンロード:[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- カスタマイズ可能なユーザー ガイドをダウンロードする: [Azure Information Protection エンド ユーザー導入ガイド](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

- よく寄せられる質問:[Azure Information Protection に関してよく寄せられる質問](faqs.md)

- Yammer:[Azure Information Protection](https://www.yammer.com/AskIPTeam)

- ドキュメントの新しい項目:[Azure Information Protection テクニカル ブログ](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/bg-p/AzureInformationProtectionBlog/label-name/Docs)

その他のリソース: [Azure Information Protection の情報とサポート](information-support.md)

### <a name="microsoft-ignite"></a>Microsoft Ignite

オーランドでの Microsoft Ignite 2018 では、[Azure Information Protection](https://myignite.techcommunity.microsoft.com/sessions?q=Azure%2520Information%2520Protection) に関する多くのセッションが行われました。 参加できなかった方も後でセッションを確認できるように、すべてのセッションが記録されています。 推奨されるトップ 5 のセッションは次のとおりです。

- [BRK2006 - Use Microsoft Information Protection (MIP) to help protect your sensitive data everywhere, throughout its lifecycle (Microsoft Information Protection (MIP) を使用して、ライフサイクル全体を通してあらゆる場所の機密データを保護する)](https://myignite.techcommunity.microsoft.com/sessions/64297) - [YouTube ビデオ](https://youtu.be/gmHVF-1cLXA)をご覧ください
 
- [BRK3002 - Understanding how Microsoft Information Protection capabilities work together to protect sensitive information across devices, apps, and services (Microsoft Information Protection の機能を連携させて、デバイス、アプリ、およびサービスの間で機密情報を保護する方法について)](https://myignite.techcommunity.microsoft.com/sessions/64299) - [YouTube ビデオ](https://youtu.be/kL9Y7NGTyQQ)をご覧ください

- [BRK3009 - Accelerate deployment and adoption of Microsoft Information Protection solutions (Microsoft Information Protection ソリューションのデプロイと導入を加速させる)](https://myignite.techcommunity.microsoft.com/sessions/64283) - [YouTube ビデオ](https://www.youtube.com/watch?v=JsCyIVyQJmE)をご覧ください

- [BRK3397 - Protect and control your sensitive emails with Office 365 Message Encryption (Office 365 Message Encryption で、機密性の高いメールを保護および管理する)](https://myignite.techcommunity.microsoft.com/sessions/64327) - [YouTube ビデオ](https://www.youtube.com/watch?v=Ld4b4pFua0g)をご覧ください

- [THR2003 - Data discovery, Usage reporting and analytics for all your data with Microsoft Information Protection (Microsoft Information Protection を使用して、すべてのデータに対してデータ検出、使用状況レポート、および分析を行う)](https://myignite.techcommunity.microsoft.com/sessions/64301) - [YouTube ビデオ](https://www.youtube.com/watch?v=nzDIXd0XaeA)をご覧ください

この Ignite で行われた発表のロールアップについては、ブログ投稿「[Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)」(機密データを保護するために使用できる情報保護機能の発表) を参照してください。


## <a name="next-steps"></a>次の手順

[クイック スタート](quickstart-viewpolicy.md)と[チュートリアル](infoprotect-quick-start-tutorial.md)を参照すれば、Azure Information Protection をご自分で構成および確認できます。 また、このサービスを組織向けにデプロイする準備ができている場合は、[攻略ガイド](how-to-guides.md)を参照してください。
