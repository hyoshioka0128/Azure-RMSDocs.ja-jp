---
title: "Azure Information Protection とは | Azure Information Protection"
description: "Azure Information Protection サービスの概要です。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
translationtype: Human Translation
ms.sourcegitcommit: 590f12e0c6c6122a6bc0a559940870c18f0e2d39
ms.openlocfilehash: 350a3cb877674208b4c560bb841135904aee1136


---

# Azure Information Protection とは

>*適用対象: Azure Information Protection*

Azure Information Protection とは、組織が文書や電子メールを、分類、ラベル付けおよび保護するためのクラウドベースのソリューションです。 これは、ルールや条件を定義する管理者が自動で実行するか、推奨が提示されたユーザーが手動で実行するか、両者で実行します。 

次の図に動作中の Azure Information Protection の例を示します。 管理者によって機密データを検出するルールが構成されています (この場合は、クレジット カード情報)。 ユーザーがクレジット カード情報を含む Word 文書を保存すると、管理者が構成した特定のラベルを適用することを推奨するカスタム ツールヒントが表示されます。文書はこれによって分類され、オプションで保護されます。 

![Azure Information Protection による推奨分類の例](../media/info-protect-recommend-callouts.png)

コンテンツを分類し (オプションで保護すると)、それを追跡したり、その用途を管理できるようになります。 データのフローを分析してビジネスに関する洞察を得たり、危険な動作を検出し修正措置を取ったり、文書へのアクセスを追跡したり、データの漏えいや誤用を防ぐことができます。

## ラベルによる分類のしくみ

Azure Information Protection のラベルは、文書と電子メールを分類するために使用します。 これを行うと、データの保存場所やデータの共有者に関係なく、いつでも分類を識別できるようになります。 永続的なラベルには、ヘッダー、フッター、透かしなどの視覚的なマーキングが含まれます。 (データ損失防止ソリューションなどの) その他のサービスが分類を識別して適切なアクションを取れるように、ファイルと電子メールのヘッダーにはクリア テキストでメタデータが追加されます。 

たとえば、次の電子メール メッセージは "内部" と分類されています。 これが内部用であり、組織外には送信されるべきではないことをすべての受信者が視覚的に確認できるように、このラベルは電子メールのフッターに追加されます。 このラベルは、電子メール サービスがこの値を調べて、監査エントリを作成したり、組織外に送信されることを阻止するよう、電子メールのヘッダーにも埋め込まれます。

![Azure Information Protection の分類を示す電子メール フッターおよびヘッダーの例](../media/example-email-footer-header.png)


## データ保護のしくみ

保護テクノロジには *Azure Rights Management* (しばしば Azure RMS と略される) が使用されています。 このテクノロジは、Microsoft の他のクラウド サービスやアプリケーション (Office 365 や Azure Active Directory など) にも統合されています。 また、独自の基幹業務アプリケーションや情報ベンダーの情報保護ソリューションで使用できます。アプリケーションやソリューションは、オンプレミスまたはクラウドのどちらにあってもかまいません。

この保護テクノロジでは、暗号化、ID、および承認ポリシーが使用されます。 文書や電子メールが Rights Management で保護されている場合、永続的ラベルの場合と同様に、どこに保存されているか (組織、ネットワーク、ファイル サーバー、アプリケーションの内部または外部) にかかわらず保護は維持されます。 この情報保護ソリューションならば、データが他者と共有されているときでも、所有者がデータの制御を維持できます。

たとえば、組織内のユーザーのみがアクセスできるようにレポート文書や売上予測のスプレッドシートを構成したり、その文書の編集の許可を制御したり、読み取り専用に制限したり、印刷できないよう制御することもできます。 電子メールについても同様に構成することができます。さらに、電子メールを転送不可に設定したり、[全員に返信] オプションを使用不可に設定したりできます。 これらの保護タスクは、*Rights Management テンプレート*を使用して単純化および合理化できます。

### Rights Management テンプレート

Azure Rights Management サービスを有効にすると直ちに、組織内のユーザーがデータにアクセスすることを制限する 2 つのテンプレートが既定で作成されます。 これらのテンプレートでは、即座に組織からのデータの漏えいを防止できます。 より制限を厳しく制御する、これらの既定のテンプレートを補うカスタム テンプレートを独自で構成することも可能です。

これらのテンプレートをラベル構成の一部にすると、文書 (または電子メール メッセージ) に特定のラベルが適用されると、データの分類と自動での保護が同時にされるようにすることができます。 Azure Rights Management テクノロジをサポートする製品およびサービスのユーザーや管理者が、テンプレートを選択することもできます。

この例では、Azure ポータルから Azure Information Protection ポリシーを構成するときに、ラベルのテンプレートを選択する方法を示します。

![Azure ポータルでテンプレートを選択する場合の例](../media/templates-infoprotection-callouts.png)

この同じテンプレートは、Azure Rights Management テクノロジをサポートする Exchange Online のメール フローのルールを構成する Exchange 管理センターからも選択できます。

![Exchange Online のテンプレートを選択する場合の例](../media/templates-exchangeonline-callouts.png)

Azure Rights Management での保護のしくみの詳細については、「[Azure Rights Management とは](what-is-azure-rms.md)」を参照してください。

## エンド ユーザーのワークフローとの統合

Azure Information Protection は、Azure Information Protection クライアントがインストールされている場合、エンド ユーザーの既存のワークフローと統合されます。 このクライアントは、Office アプリケーションに、最初の図のように Information Protection バーをインストールします。 Excel、PowerPoint、および Outlook にも同じバーが追加されます。 たとえば、

![Excel の Azure Information Protection バーの例](../media/excel2013-infoprotect-bar2.png)

この Information Protection バーにより、エンド ユーザーは、適切な分類ラベルを選択でき、必要に応じてこれらのラベルにより、文書や電子メールを自動で保護することもできるようになります。

ユーザーが保護されている文書を電子メールで共有する場合、これらの文書にアクセスしているユーザーやいつアクセスされているかを文書の追跡サイトから監視することができます。 不正使用が疑われる場合、これらの文書に対するアクセスを取り消すことも可能です。


## Azure Information Protection の参考資料

- お知らせ: [Azure Information Protection が一般公開されました](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/04/azure-information-protection-is-now-generally-available/)

- 無料評価版: [Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- クライアントのダウンロード: [Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- よく寄せられる質問: [Azure Information Protection に関してよく寄せられる質問](../get-started/faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)

- ビデオ プレゼンテーション:

    <iframe width="560" height="315" src="https://www.youtube.com/embed/N9Ip0m6d3G0" frameborder="0" allowfullscreen></iframe>


## 次のステップ

「[Quick start tutorial for Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md)」 (Azure Information Protection のクイック スタート チュートリアル) で説明されているように、5 つの簡単な手順で Azure Information Protection をご自分で構成および確認できます。

Azure Rights Management または Azure Information Protection の別名 [サービスの代替用語の一覧](azure-rms-aka.md)に関するページを参照してください。


<!--HONumber=Oct16_HO1-->


