---
# required metadata

title: "Azure RMS のクイック スタート チュートリアル - 手順 5 | AZURE RMS"
description: "5 つの手順を実行するだけで 15 分もかからずに組織の Microsoft Azure Rights Management を簡単に試すことができるチュートリアルの最後の手順。"
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: aa06826d-c227-449b-93ea-6ce394608997

# optional metadata

ROBOTS:
audience:
ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
ms.tgt_pltfrm:
ms.technology:
ms.custom:

---


# Azure RMS のクイック スタート: 手順 5. 保護されているドキュメントの追跡

*適用対象: Azure Rights Management、Office 365*


移動: 
> [!div class="op_single_selector"]
- [概要](quick-start-tutorial.md)
- [手順 1. Azure RMS をアクティブ化する](tutorial-step1.md)
- [手順 2. RMS 共有アプリをインストールする](tutorial-step2.md)
- [手順 3. 機密ドキュメントを電子メールで送信する](tutorial-step3.md)
- [手順 4. 受信者がドキュメントを閲覧する](tutorial-step4.md)
- [手順 5. ドキュメントを追跡する](tutorial-step5.md)

![Azure RMS のクイック スタート チュートリアルの手順 5](../media/AzRMS_QuickStartSteps5.PNG)

> [!NOTE]
> この手順では、ドキュメント追跡をサポートするサブスクリプションが必要です。 サブスクリプションにドキュメント追跡が含まれているかどうかを確認するには、 [Rights Management Services (RMS) 製品の比較](https://technet.microsoft.com/dn858608.aspx)に関するページを参照してください。

この手順は省略可能ですが、ほとんどのユーザーが宛先に送信した添付ファイルが開かれたかどうか、また、開かれた時間と場所を知りたいと考えています。 例:

-   指定した時間までに、相手から返答を受けたいと考えている場合、ドキュメント追跡サイトを使用すると、締め切りが近づいているのに相手がドキュメント開いていないことがわかります。 タイミングよく催促するために、フォローアップの電子メールを送信するか、電話します。

-   相手がドキュメントを開いたことを確認したら、フォローアップして相手に不明点があるかどうか、または補足情報が必要かどうかをたずねます。

![チュートリアルの手順 5 のスクリーンショット](../media/AzRMS_Tutorial_5_Screenshots.png)

### 保護されているドキュメントを追跡するには

1.  Outlook を使用して、[ **ホーム** ] タブの [ **RMS** ] グループで [ **使用の追跡**] をクリックします。

2.  [ **条件に従って保護し、共有する** ] ページが表示された場合は、[ **サインイン** ] をクリックし、ユーザー名とパスワードをもう一度入力します。

3.  **[共有ドキュメント]** ページに、電子メールに添付されたドキュメント **Confidential.docx** が表示されます。 この時点では、このドキュメントは表示される唯一のファイルですが、共有するドキュメントの数を増やすと、一覧が拡張されます。

    このページから、ドキュメントを共有した時刻 (保護されたファイルが添付された電子メールを送信した時刻)、最後のアクティビティの日付、電子メールの宛先の受信者名を確認できます。 追加の詳細を確認するには、ドキュメント名をクリックします。

4.  表示された新しいページには、クリックしたファイルの名前が付きます。ここでは、このドキュメントのみについての詳細の概要と、このドキュメントに対して使用可能なその他のオプション ([**一覧**]、[ **タイムライン**]、[ **マップ**]、[ **設定**]) が表示されます。

    各オプションをクリックすると、保護されたドキュメントを追跡するさまざまな方法を確認できます。 このほか、[ **概要** ] ページで、[ **Excel で開く** ] をクリックして情報をスプレッドシートにエクスポートしたり、[ **アクセスの取り消し** ] をクリックしてドキュメントの共有を停止したりできます。

保護されたドキュメントに対するアクティビティを詳細に追跡したり、(必要に応じて) アクセスを取り消したりするときは、このサイトを使用します。 ブラウザーで次のリンクを使用すると、モバイル デバイスやタブレットからでもこのサイトにアクセスできます: [ドキュメント追跡](http://go.microsoft.com/fwlink/?LinkId=529562)

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|ドキュメントを追跡する手順の完全版|[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](../rms-client/sharing-app-track-revoke.md)|
|ドキュメント追跡に関する 2 分間のビデオ|[Azure RMS のドキュメントの追跡と取り消し](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)|
|トラブルシューティングとお客様からの質問|[ドキュメント追跡の FAQ](https://technet.microsoft.com/dn947488)|

### 次のステップ
このチュートリアルでは、Azure RMS でデータを保護する方法について、1 つのシナリオだけについて、手順に沿って説明しました。 その他の一般的な使用方法の詳細については、「[Azure Active Directory Rights Management の概要](../understand-explore/what-is-azure-rms.md)」の「[Azure RMS の動作](../understand-explore/what-admins-users-see.md)」を参照してください。 これ以外にも、記事には Azure RMS の動作のしくみや解決できるビジネス上の問題に関する役立つセクションが記載されています。

Azure RMS を組織にデプロイする準備ができたら、[Azure Rights Management のデプロイ ロードマップ](../plan-design/deployment-roadmap.md)を使用して、デプロイの手順と具体的な操作手順のリンクを確認してください。

あるいは、特定のシナリオ、関連構成手順、エンド ユーザー文書の一覧が必要な場合、「[Azure Rights Management の迅速なデプロイ ガイド](../get-started/rapid-deployment-guide.md)」を参照してください。

>[!div class="step-by-step"] [概要](quick-start-tutorial.md)
[手順 1](tutorial-step1.md)
[手順 2](tutorial-step2.md)
[手順 3](tutorial-step3.md)
[手順 4](tutorial-step4.md)
*手順 5*


<!--HONumber=May16_HO2-->


