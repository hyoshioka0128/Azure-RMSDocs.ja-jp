---
title: "Azure Information Protection とは"
description: "Azure Information Protection サービスの概要です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/12/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
ms.openlocfilehash: fff96103544242510b7e53b1636f1f95fbd4bb2b
ms.sourcegitcommit: c5e117f5329c6e5a93d5858a3b4609aadd8a6e7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2017
---
# <a name="what-is-azure-information-protection"></a>Azure Information Protection とは

>*適用対象: Azure Information Protection*

Azure Information Protection とは、組織が文書や電子メールを、分類、ラベル付けおよび保護するためのクラウドベースのソリューションです。 これは、ルールや条件を定義する管理者が自動で実行するか、推奨が提示されたユーザーが手動で実行するか、両者で実行します。 

次の図に動作中の Azure Information Protection の例を示します。 管理者によって機密データを検出するルールが構成されています (この場合は、クレジット カード情報)。 ユーザーがクレジット カード情報を含む Word 文書を保存すると、管理者が構成した特定のラベルを適用することを推奨するカスタム ツールヒントが表示されます。 このラベルによって分類されます。また、構成によっては文書も保護されます。 

![Azure Information Protection による推奨分類の例](../media/info-protect-recommend-calloutsv2.png)

コンテンツを分類し (オプションで保護すると)、それを追跡したり、その用途を管理できるようになります。 データのフローを分析してビジネスに関する洞察を得たり、危険な動作を検出し修正措置を取ったり、文書へのアクセスを追跡したり、データの漏えいや誤用を防ぐことができます。

## <a name="how-labels-apply-classification"></a>ラベルによる分類のしくみ

Azure Information Protection のラベルは、文書と電子メールを分類するために使用します。 これを行うと、データの保存場所やデータの共有者に関係なく、いつでも分類を識別できるようになります。 ラベルには、ヘッダー、フッター、透かしなどの視覚的なマーキングが含まれます。 メタデータはクリア テキストでファイルと電子メール ヘッダーに追加されます。 クリア テキストなので、データ損失防止ソリューションなど、その他のサービスが分類を識別して適切なアクションを取ることができます。 

たとえば、次の電子メール メッセージは "一般" と分類されています。 このラベルはフッターとして電子メール メッセージに追加されます。 このフッターは、組織外に送信すべきではない一般的なビジネス データ用を示す、すべての受信者向けのビジュアル インジケーターです。 このラベルは、電子メール サービスがこの値を調べて、監査エントリを作成したり、組織外に送信されたりすることを阻止するよう、電子メールのヘッダーにも埋め込まれます。

![Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例](../media/example-email-footerv2.png)


## <a name="how-data-is-protected"></a>データ保護のしくみ

保護テクノロジには *Azure Rights Management* (しばしば Azure RMS と略される) が使用されています。 このテクノロジは、Microsoft の他のクラウド サービスやアプリケーション (Office 365 や Azure Active Directory など) にも統合されています。 また、独自の基幹業務アプリケーションや情報ベンダーの情報保護ソリューションで使用できます。アプリケーションやソリューションは、オンプレミスまたはクラウドのどちらにあってもかまいません。

この保護テクノロジでは、暗号化、ID、および承認ポリシーが使用されます。 文書や電子メールが Rights Management で保護されている場合、適用されるラベルの場合と同様に、どこに保存されているか (組織、ネットワーク、ファイル サーバー、アプリケーションの内部または外部) にかかわらず、適用される保護は維持されます。 この情報保護ソリューションならば、データが他者と共有されているときでも、所有者がデータの制御を維持できます。

たとえば、組織内のユーザーのみがアクセスできるようにレポート文書や売上予測のスプレッドシートを構成したり、その文書の編集の許可を制御したり、読み取り専用に制限したり、印刷できないよう制御することもできます。 電子メールについても同様に構成することができます。さらに、電子メールを転送不可に設定したり、[全員に返信] オプションを使用不可に設定したりできます。 これらの保護タスクは、*Rights Management テンプレート*を使用して単純化および合理化できます。

### <a name="rights-management-templates"></a>Rights Management テンプレート

Azure Rights Management サービスを有効にすると直ちに、組織内のユーザーがデータにアクセスすることを制限する 2 つのテンプレートが既定で作成されます。 これらのテンプレートでは、即座に組織からのデータの漏えいを防止できます。 より制限を厳しく制御する、これらの既定のテンプレートを補うカスタム テンプレートを独自で構成することも可能です。

これらのテンプレートをラベル構成の一部にすると、文書 (または電子メール メッセージ) に特定のラベルが適用されると、データの分類と自動での保護が同時にされるようにすることができます。 Azure Rights Management テクノロジをサポートする製品およびサービスのユーザーや管理者が、テンプレートを選択することもできます。

この例では、Azure ポータルから Azure Information Protection ポリシーを構成するときに、ラベルのテンプレートを選択する方法を示します。

![Azure ポータルでテンプレートを選択する場合の例](../media/info-protect-template-callout.png)

同じテンプレートを Exchange 管理センターから選択することもできます。 たとえば、Exchange は Azure Rights Management テクノロジをサポートしているので、このようなテンプレートを使用する Exchange Online メール フロー ルールを構成できます。

![Exchange Online のテンプレートを選択する場合の例](../media/templates-exchangeonline-callouts.png)

Azure Rights Management での保護のしくみの詳細については、「[Azure Rights Management とは](what-is-azure-rms.md)」を参照してください。

## <a name="integration-with-end-user-workflows"></a>エンドユーザーのワークフローとの統合

Azure Information Protection は、Azure Information Protection クライアントがインストールされている場合、エンド ユーザーの既存のワークフローと統合されます。 このクライアントは、Office アプリケーションに、Word にこのバーを表示した最初の図のように Information Protection バーをインストールします。 同じ Information Protection バーが Excel、PowerPoint、および Outlook に追加されます。 たとえば、

![Excel の Azure Information Protection バーの例](../media/excel2016-infoprotect-barv2.png)

エンド ユーザーはこの Information Protection バーを使用して、正しい分類のラベルを簡単に選択できるようになります。 必要に応じて、ラベルを自動的に適用してユーザーの推測を排除したり、組織のポリシーに準拠したりすることもできます。

追加のファイルの種類を分類して保護し、複数のファイルを一度にサポートするには、次のようにして、エクスプローラーからファイルまたはフォルダーを右クリックします。

![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](../media/right-click-classify-protect-folder.png)

エクスプローラーから **[分類して保護する]** メニュー オプションを選択すると、Office デスクトップ アプリで Information Protection バーを使用する場合と同じように、ラベルを選択することができます。 必要に応じて、独自のカスタム アクセス許可を設定することもできます。

パワー ユーザー (および管理者) は、PowerShell コマンドを使用すれば、複数のファイルの分類と保護をより効率的に管理して設定できることに気付くかもしれません。 これを行う PowerShell コマンドは、クライアントと共に自動的に含まれますが、PowerShell モジュールを個別にインストールすることもできます。

ドキュメントが保護されたら、ユーザーと管理者はドキュメント追跡サイトを使用して、これらのドキュメントに誰がいつアクセスしているかを監視することができます。 不正使用が疑われる場合は、これらのドキュメントに対するアクセスを取り消すこともできます。

![ドキュメント追跡サイトの [アクセスの取り消し] アイコン](../media/tracking-site-revoke-access-icon.png)


## <a name="resources-for-azure-information-protection"></a>Azure Information Protection の参考資料

- お知らせ: [Azure Information Protection が一般公開されました](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/04/azure-information-protection-is-now-generally-available/)

- 無料評価版: [Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- クライアントのダウンロード: [Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- よく寄せられる質問: [Azure Information Protection に関してよく寄せられる質問](../get-started/faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)

- ビデオ: "Information Protection のヒント トップ 5"

    <iframe width="560" height="315" src="https://www.youtube.com/embed/GWcnZFMPcnE" frameborder="0" allowfullscreen></iframe>

    さらに、Microsoft Ignite 2016 では Azure Information Protection に関する多くのオンデマンド セッションが提供されます。

    - [BRK2127: データを安全に保護し共有するために包括的な ID ベースのソリューションを採用する](https://myignite.microsoft.com/videos?q=BRK2127)
    
    - [THR2107: Azure Information Protection を使用して安全に共同作業を行う](https://myignite.microsoft.com/videos?q=THR2107)
    
    - [THR2108: Azure Information Protection を使用してデータを包括的に保護する](https://myignite.microsoft.com/videos?q=THR2108)
    
    - [BRK3095: 分類、ラベル付け、保護によって永続的なデータ保護が実現されるしくみを説明する](https://myignite.microsoft.com/videos?q=BRK3095)
    
    - [BRK2128: Microsoft Office 365 と Azure Information Protection を利用してセキュリティで保護された電子メールを送信する](https://myignite.microsoft.com/videos?q=BRK2128)


## <a name="next-steps"></a>次のステップ

ブログの投稿「[Azure Information Protection: Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)」 (Azure Information Protection: 準備、設定、保護) をお読みください。

「[Quick start tutorial for Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md)」 (Azure Information Protection のクイック スタート チュートリアル) で説明されているように、5 つの簡単な手順で Azure Information Protection をご自分で構成および確認できます。

Azure Rights Management または Azure Information Protection の別名については、 [サービスの代替用語の一覧](azure-rms-aka.md)に関するページを参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]