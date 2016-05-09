---
# required metadata

title: Azure Rights Management の迅速なデプロイ ガイド | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c994d616-cff6-4930-9228-a7f7d198a160

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Rights Management の迅速なデプロイ ガイド
このガイドは、「**デプロイと使用**」セクションの構成情報を補足するもので、実装する具体的なシナリオを一覧から選択することにより、Azure Rights Management (Azure RMS) を迅速にデプロイして使用する際に役立ちます。

シナリオには、管理者向けの指示とそれに伴うエンド ユーザー向けのドキュメントの両方が用意されています。 エンド ユーザーにこのドキュメント (指示やお知らせ) を配布する前に、まずドキュメントをビジネス要件および既存のワーク フローに合わせてカスタマイズする必要があります。 一連の指示やお知らせの例では、最終的なエンド ユーザー マニュアルの体裁を示します。

各シナリオには要件の一覧と、必要であれば、詳細情報のリンクが含まれます。それにより、ソリューションを個別に、また、任意の順番でデプロイできます。

ここで説明するシナリオでは、最も一般的な例を示します。 Azure RMS を使用すると、組織内および組織間の膨大なシナリオの情報を保護できるため、この同じモデルを使用して、独自のシナリオを定義し、自分の環境やユーザー環境にデプロイすることができます。 特定のシナリオに注目することにより、Azure RMS のデプロイが、よりビジネスの目標に沿ったものになります。 さらに、経験上、「機密文書を保護する」などの一般的なガイダンスより、シナリオ固有の指示に密接かつ体系的に従う傾向があることがわかっています。

これらのソリューションをロールアウトする前に、会社のデータを保護するための変更を行うこと、そのためにエンド ユーザーからの変更が必要な場合があることをエンド ユーザーに広く告知することができます。 次の表の後に、通信の例を示します。

> [!NOTE]
> このガイドについてのご質問やご意見がある場合は、このページのフィードバック メカニズムを使用するか、または [AskIPTeam@Microsoft.com](mailto:%20askipteam@microsoft.com?subject=Rapid%20Deployment%20Guide%20feedback) まで電子メール メッセージを送信してください。

## Azure RMS のシナリオ
Azure RMS を短時間でデプロイし、ビジネス上の特定の問題に対処するには、ビジネス上の目標に最も一致するシナリオを選択し、必要に応じてカスタマイズします。



**その結果として発生したアクセスを追跡する機能を使用して、安全に Office ファイルを他の組織内のユーザーに電子メールで送信します (企業間コラボレーション)。**

例:

- 価格表、ロードマップ、リリース予定を顧客に送信します。

- 作業指図またはマーケティング仕様をベンダーに送信します。

- 支払/入金または見積依頼 (RFQ) をパートナーに送信します。

参照: [シナリオ - Office ファイルを別の組織のユーザーと共有する方法](scenario-share-office-file-externally.md)

**SharePoint ライブラリに格納されているドキュメントが自分の管理下にあることを確認します**

例:

- 部門別のスプレッドシートとレポート。

- デザイン ドキュメントやその他の成果物のチーム間共同作業

参照: [シナリオ - SharePoint に保存されているドキュメントを管理する](scenario-sharepoint.md)

**経営陣は電子メールを使って特権情報を安全に交換できます**

例:

- 買収計画の共有

- 法律問題の話し合いまたは情報拡散

- 一時解雇の可能性やその他の機密案件に関する情報

参照: [シナリオ - 役員が安全に特権情報を交換できるようにする](scenario-executives-email.md)

**ファイル サーバー上のすべてのファイルを自動的に保護します**

例:

- 知的財産の損失を防ぐために社内で保持する必要がある CAD ドキュメント

- 情報の漏えいを防いで競争力を維持するために非公開にしておく必要があるマーケティング プロモーションの計画と日付

参照: [シナリオ - ファイル サーバー共有上のファイルを保護する](scenario-fci.md)

**機密性が高く、ビジネスに大きな影響を及ぼすドキュメントを厳格に保護します**

例:

- 会社固有のものであるレシピや数式の情報

- 機密性の高い企業買収や合併の計画

- 天然資源の調査データ

参照: [シナリオ - 重要度の高い (いくつかの) ファイルを保護する](scenario-secure-most-valuable-files.md)

**社外秘の電子メールと添付ファイルを安全に送信します**

例:

- 会社のビジョン ステートメント

- 組織図、再編成のニュース、またはプロモーションのお知らせ

- 会社のポリシー情報

参照: [シナリオ - 社外秘の電子メールを送信する](scenario-company-confidential-email.md)

**ワーク フォルダーでの Office ファイルの永続的な保護を適用します**

例:

- 社外秘のプロジェクトの Word 文書をローカルで編集する

- 機密データやビジネスに大きな影響を及ぼすデータを含むスプレッドシートをローカルで作成する

- プレゼンテーションが最終版になるまで組織の外部に漏えいしたり、誤って公開したりしてはならない作成中の PowerPoint プレゼンテーションをローカルに保存する

参照: [シナリオ - 永続的な保護を提供するために作業フォルダーを構成する](scenario-work-folders.md)




## ロールアウトする前のユーザーへのアナウンス
次の通信メッセージの例を使用して、Azure RMS をデプロイするには一定の変更が伴うということをユーザーに通知できます。 次のテキストをコピーして貼り付け、組織のリーダーシップ チームの誰か、可能であれば、最高経営責任者から、すべてのユーザーに電子メールで送信します。 このテキストに変更を加え、ユーザーおよび組織により関連性の高い内容にすることを検討してください。

![](../media/AzRMS_ExampleBanner.png)

### データを保護するために加える変更
誤ってパートナーに送信されたドキュメントへのアクセスをブロックしたいと思ったことはありますか。 送信した最新の製品ニュースを顧客が読んだかどうかを知りたいと思ったことはありますか。 見せてはいけない相手に送信される心配なく、機密の製品情報を共有する必要がありますか。

IT部門は Microsoft Azure Rights Management (Azure RMS) をエンタープライズ データ保護ソリューションとして実装する際の一定の変更をロールアウトしているため、以上のことが間もなく可能になります。 これらのソリューションの多くでは、ユーザーが特に何もしなくても必要な保護が自動的に適用されますが、 変更が必要な場合には、IT 部門が情報および指示を送信し、質問や問題があるユーザーはヘルプ デスクのサポートを受けることができます。

たとえば、共有するドキュメントを追跡する (および必要に応じて、取り消す) には、ドキュメント追跡サイトを使用します。

![](../media/AzRMS_Tutorial_5_Screenshots.png)

このしくみを紹介する 2 分間のビデオ「[Azure RMS のドキュメントの追跡と取り消し](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)」をご覧ください。

この組織の最も重要な資産の 1 つは、私たちが日常的に生成、保存、および使用しているデータです。 こうしたデータは、競争力を獲得し、業績を上げるために役立ちます。 そのため、データの管理を維持し、必要のない人がデータにアクセスできないようにすることが重要です。

このソリューションを実装することにより、重要なデータを保護し、データを管理するためのツールを利用することができます。 これらの変更の実装にご協力いただきありがとうございます。



<!--HONumber=Apr16_HO3-->

