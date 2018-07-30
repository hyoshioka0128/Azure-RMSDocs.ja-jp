---
title: Azure Information Protection とは
description: Azure Information Protection サービスの概要です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/23/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
ms.openlocfilehash: a30607f0a4be292827a3d8ef20f45332e688ae28
ms.sourcegitcommit: c7e943700189eeaad3f4c919cc0fa3410fd4df5b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2018
ms.locfileid: "39204494"
---
# <a name="what-is-azure-information-protection"></a>Azure Information Protection とは

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection (AIP とも呼ばれます) は、ラベルを適用することで組織がドキュメントや電子メールを分類したり、必要に応じて保護したりするのに役立つクラウドベースのソリューションです。 ラベルの適用は、ルールや条件を定義する管理者が自動で実行するか、ユーザーが手動で実行するか、その組み合わせ (ユーザーにレコメンデーションが提示される) で実行します。 

ユーザーのコンピューターで動作する Azure Information Protection の例を、次の図に示します。 管理者は、機密データを検出するルールを使用してラベルを構成しました。この例ではクレジット カード情報が使用されます。 ユーザーがクレジット カード番号を含む Word ドキュメントを保存すると、管理者が構成したラベルを推奨するカスタム ツールヒントが表示されます。 このラベルによってドキュメントが分類され、保護されます。 

![Azure Information Protection による推奨分類の例](../media/info-protect-recommend-calloutsv2.png)

コンテンツを分類し (オプションで保護すると)、それを追跡したり、その用途を管理できるようになります。 データのフローを分析してビジネスに関する洞察を得たり、危険な動作を検出し修正措置を取ったり、文書へのアクセスを追跡したり、データの漏えいや誤用を防ぐことができます。

## <a name="how-labels-apply-classification"></a>ラベルによる分類のしくみ

Azure Information Protection のラベルは、文書と電子メールを分類するために使用します。 これを行うと、データの保存場所やデータの共有者に関係なく分類を識別できるようになります。 ラベルには、ヘッダー、フッター、透かしなどの視覚的なマーキングを含めることができます。 メタデータはクリア テキストでファイルと電子メール ヘッダーに追加されます。 クリア テキストなので、データ損失防止ソリューションなど、その他のサービスが分類を識別して適切なアクションを取ることができます。 

たとえば、次の電子メール メッセージは "一般" と分類されています。 ラベルでは、"秘密度: 一般" のフッターが電子メール メッセージに追加されました。 このフッターは、組織外に送信すべきではない一般的なビジネス データ用を示す、すべての受信者向けのビジュアル インジケーターです。 このラベルは、電子メール サービスがこの値を調べて監査エントリを作成したり、組織外への送信を回避したりできるように、電子メールのヘッダーに埋め込まれます。

![Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例](../media/example-email-footerv2.png)


## <a name="how-data-is-protected"></a>データ保護のしくみ

保護テクノロジには *Azure Rights Management* (しばしば Azure RMS と略される) が使用されています。 このテクノロジは、Microsoft の他のクラウド サービスやアプリケーション (Office 365 や Azure Active Directory など) にも統合されています。 また、独自の基幹業務アプリケーションや情報ベンダーの情報保護ソリューションで使用できます。アプリケーションやソリューションは、オンプレミスまたはクラウドのどちらにあってもかまいません。

この保護テクノロジでは、暗号化、ID、および承認ポリシーが使用されます。 文書や電子メールが Rights Management で保護されている場合、適用されるラベルの場合と同様に、どこに保存されているか (組織、ネットワーク、ファイル サーバー、アプリケーションの内部または外部) にかかわらず、適用される保護は維持されます。 この情報保護ソリューションならば、データが他者と共有されているときでも、所有者がデータの制御を維持できます。

たとえば、組織内のユーザーのみがアクセスできるようにレポート文書や売上予測のスプレッドシートを構成したり、その文書の編集の許可を制御したり、読み取り専用に制限したり、印刷できないよう制御することもできます。 電子メールについても同様に構成することができます。さらに、電子メールを転送不可に設定したり、[全員に返信] オプションを使用不可に設定したりできます。 

これらの保護設定は、ラベルの構成に含めることができます。そのため、ユーザーはラベルを適用するだけで、ドキュメントとメールの両方を分類できます。 ただし、保護をサポートするアプリケーションとサービスから同じ保護設定を使用することもできますが、ラベルを付けることはできません。 これらのアプリケーションとサービスでは、保護設定は "*Rights Management テンプレート*" として使用できるようになります。

### <a name="rights-management-templates"></a>Rights Management テンプレート

Azure Rights Management サービスを有効にするとすぐに、組織内のユーザーがデータにアクセスすることを制限する 2 つの既定のテンプレートが使用可能になります。 これらのテンプレートでは、即座に組織からのデータの漏えいを防止できます。 これらの既定のテンプレートを補うこともできます。その場合、より厳しい制御を適用する独自の保護設定を構成します。

保護設定を含む Azure Information Protection のラベルを作成すると、その処理の裏では、このアクションによって対応する Rights Management テンプレートが作成されます。 さらに、そのテンプレートは、Azure Rights Management をサポートするアプリケーションとサービスで使用できます。

たとえば、Exchange 管理センターから、これらのテンプレートを使用するように、Exchange Online メール フロー ルールを構成できます。

![Exchange Online のテンプレートを選択する場合の例](../media/templates-exchangeonline-callouts.png)

Azure Rights Management での保護のしくみの詳細については、「[Azure Rights Management とは](what-is-azure-rms.md)」を参照してください。

## <a name="integration-with-end-user-workflows-for-documents-and-emails"></a>ドキュメントおよび電子メール用のエンドユーザー ワークフローとの統合

Azure Information Protection は、Azure Information Protection クライアントがインストールされている場合、エンド ユーザーの既存のワークフローと統合されます。 このクライアントは、Office アプリケーションに、Word にこのバーを表示した最初の図のように Information Protection バーをインストールします。 同じ Information Protection バーが Excel、PowerPoint、および Outlook に追加されます。 次に例を示します。

![Excel の Azure Information Protection バーの例](../media/excel2016-infoprotect-barv2.png)

エンド ユーザーはこの Information Protection バーを使用して、正しい分類のラベルを簡単に選択できるようになります。 必要に応じて、ラベルを自動的に適用してユーザーの推測を排除したり、組織のポリシーに準拠したりすることもできます。

追加のファイルの種類を分類して保護し、複数のファイルを一度にサポートするには、次のようにして、エクスプローラーからファイルまたはフォルダーを右クリックします。

![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](../media/right-click-classify-protect-folder.png)

エクスプローラーから **[分類して保護する]** メニュー オプションを選択すると、Office デスクトップ アプリで Information Protection バーを使用する場合と同じように、ラベルを選択することができます。 必要に応じて、独自のカスタム アクセス許可を設定することもできます。

パワー ユーザー (および管理者) は、PowerShell コマンドを使用すれば、複数のファイルの分類と保護をより効率的に管理して設定できることに気付くかもしれません。 これらのアクションを行う PowerShell コマンドは、クライアントと共に自動的に含まれますが、PowerShell モジュールを個別にインストールすることもできます。

ドキュメントが保護されたら、ユーザーと管理者はドキュメント追跡サイトを使用して、これらのドキュメントに誰がいつアクセスしているかを監視することができます。 不正使用が疑われる場合は、これらのドキュメントに対するアクセスを取り消すこともできます。

![ドキュメント追跡サイトの [アクセスの取り消し] アイコン](../media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>電子メールにおける追加の統合

Exchange Online で Azure Information Protection を使用する場合は、新たな利点として、保護されたメールを任意のユーザーに送信し、送信先のユーザーが任意のデバイスでそのメールを読み取れるようにすることができます。

たとえば、ユーザーが機密情報を、**Gmail**、**Hotmail**、または**Microsoft** アカウントを使用している個人用メール アカウントに送信する必要があるとします。 または、Office 365 用のアカウントまたは Azure AD 内のアカウントを持っていないユーザーに機密情報を送信する必要があるとします。 これらの電子メールは、保存時または送信中に暗号化し、本来の受信者のみが読み取ることができるようにする必要があります。

このシナリオには、[Office 365 Message Encryption の新機能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)が必要です。 保護された電子メールを自分のネイティブ電子メール クライアントで開くことはできない受信者の場合は、ワンタイム パスコードを使用することでブラウザー内で機密情報を閲覧することができます。

たとえば、Gmail ユーザーには、電子メール メッセージに次の内容が表示されます。

![OME と AIP の Gmail 受信者エクスペリエンス](../media/ome-message.png)

電子メールを送信するユーザーにとって、ワークフローは、所属する組織内のユーザーに保護された電子メールを送信する場合と変わりありません。 たとえば、ユーザーは Azure Information Protection クライアントによって Outlook のリボンに追加される **[転送不可]** ボタンを選択することができます。 または、ユーザーが選択したラベルに [転送不可] 機能を統合することができます。これにより、電子メールは分類され保護されます。

![[転送不可] として構成されたラベルを選択](../media/recipients-only-label.png)

または、権利保護を適用するメール フロー ルールを使用して、ユーザーを自動的に保護することができます。 

そのようなルールを適用した電子メールに Office ドキュメントを添付した場合、そのドキュメントも自動的に保護されます。

## <a name="classifying-and-protecting-existing-documents"></a>既存のドキュメントの分類と保護

ドキュメントと電子メールは、最初に作成したときにラベル付けすることが理想的です。 しかし、おそらくデータ ストアには既存のドキュメントが多数あり、これらのドキュメントも分類して保護する必要があります。 これらのデータ ストアは、オンプレミスか、またはクラウド内にある場合があります。

オンプレミスのデータ ストアの場合、Azure Information Protection スキャナーを使用して、ローカル フォルダー、ネットワーク共有、SharePoint Server のサイトとライブラリにあるドキュメントの検出、分類、保護を行います。 スキャナーは、Windows Server 上のサービスとして実行されます。 ポリシー内の同じ規則を使用して、機密データを検出し、ドキュメントに特定のラベルを適用することができます。 または、ファイルの内容を検査せずに、データ リポジトリ内のすべてのドキュメントに既定のラベルを適用できます。 また、スキャナーを報告モードのみで使用して、所持していたことを知らなかった機密情報を発見することもできます。 

スキャナーのデプロイと使用方法については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](../deploy-use/deploy-rms-connector.md)」をご覧ください。

クラウドのデータ ストアの場合、Microsoft Cloud App Security を使用して、Box、SharePoint Online、OneDrive for Business 内にあるドキュメントにラベルを適用します。 詳細については、「[Azure Information Protection 分類ラベルを自動的に適用する](/cloud-app-security/use-case-information-protection)」と「[Azure Information Protection の統合](/cloud-app-security/azip-integration)」をご覧ください。


## <a name="resources-for-azure-information-protection"></a>Azure Information Protection の参考資料

- 無料評価版: [Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- サブスクリプションのオプションと価格: [Azure Information Protection の価格](https://azure.microsoft.com/pricing/details/information-protection)

- クライアントのダウンロード: [Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- カスタマイズ可能なユーザー ガイドのダウンロード: [Azure Information Protection エンド ユーザー導入ガイド](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

- よく寄せられる質問: [Azure Information Protection に関してよく寄せられる質問](../get-started/faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/AskIPTeam)


さらに、**Microsoft Ignite 2017** では、オンデマンドで使用可能な Azure Information Protection に関する多くのセッションが提供されます。 今回のカンファレンスで発表された内容の概要については、「[What’s new in Azure Information Protection @ Ignite 2017 (Azure Information Protection の新機能 (Ignite 2017))](https://cloudblogs.microsoft.com/ENTERPRISEMOBILITY/2017/09/27/whats-new-in-azure-information-protection-ignite-2017/)」を参照してください。 

Ignite の Web サイトで、Azure Information Protection にタグ付けされているセッションを[検索して見つけられます](https://myignite.microsoft.com/videos?q=%2522azure%2520information%2520protection%2522)。 ただし、次のセッションを初めにご覧いただくことをお勧めします。

- [Microsoft の情報保護機能を使用してデータのライフサイクル全体を保護する](https://myignite.microsoft.com/videos/55397)

- [Azure Information Protection のデプロイと導入を加速させる](https://myignite.microsoft.com/videos/53454)

- [Azure Information Protection の新機能を確認し、ロードマップと戦略について学ぶ](https://myignite.microsoft.com/videos/53453)

- [コンプライアンス対応の暗号化キー管理方法](https://myignite.microsoft.com/videos/53455)

- [新しい Office 365 Message Encryption 機能で、機密性の高いメールを保護および管理する](https://myignite.microsoft.com/videos/53230)


## <a name="next-steps"></a>次のステップ

ブログの投稿「[Azure Information Protection: Ready, set, protect!](https://cloudblogs.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)」 (Azure Information Protection: 準備、設定、保護) をお読みください。

「[Azure Information Protection のクイック スタート チュートリアル](../get-started/infoprotect-quick-start-tutorial.md)」で説明されているように、5 つの簡単な手順で Azure Information Protection をご自分で構成および確認できます。 このサービスを組織向けにデプロイする準備ができている場合は、「[Azure Information Protection デプロイ ロードマップ](../plan-design/deployment-roadmap.md)」を参照してください。

Azure Information Protection の別名については、 [サービスの代替用語の一覧](azure-rms-aka.md)に関するページを参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
