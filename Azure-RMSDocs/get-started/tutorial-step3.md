---
# required metadata

title: Azure RMS のクイック スタート チュートリアル - 手順 3. | Azure RMS
description: 5 つの手順を実行するだけで 15 分もかからずに組織の Microsoft Azure Rights Management を簡単に試すことができるチュートリアルの 3 番目の手順。
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c604e749-8918-40e8-8148-6bd000cb2be2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Azure RMS のクイック スタート: 手順 3. 電子メールによる保護対象のドキュメントの送信

*適用対象: Azure Rights Management、Office 365*


移動: 
> [!div class="op_single_selector"]
- [概要](quick-start-tutorial.md)
- [手順 1. Azure RMS をアクティブ化する](tutorial-step1.md)
- [手順 2. RMS 共有アプリをインストールする](tutorial-step2.md)
- [手順 3. 機密ドキュメントを電子メールで送信する](tutorial-step3.md)
- [手順 4. 受信者がドキュメントを閲覧する](tutorial-step4.md)
- [手順 5. ドキュメントを追跡する](tutorial-step5.md)


この手順では、まず Word を使用してドキュメントを作成し、保護対象であることがわかるように **Confidential.docx** という名前で保存します。 このチュートリアルでは、ドキュメントの内容にどのようなテキストが含まれていても実際には問題はありませんが、承認された受信者がドキュメントを読んだことを簡単に確認できるようなテキストを含めることができます。 たとえば、次のようなテキストが考えられます。 **電子メールの添付ファイルからこのテキストを読み取ることができた場合には、送信者が Azure RMS で保護したファイルを正常に共有できたことになります。**

これで、電子メールでこのドキュメントを安全に共有する準備ができました。

![Azure RMS のクイック スタート チュートリアルの手順 3](../media/AzRMS_Tutorial_3_Screenshots.png)

### 電子メールで、ドキュメントを安全に共有するには

1.  Outlook を使用して、新しいメッセージを作成し、作成したファイルを添付します。

2.  [ **宛先** ] ボックスで、1 つ以上の仕事用の電子メール アドレスを入力します。 必ず **janetm@contoso.com** または **p.dover@fabrikam.com** のような仕事用の電子メール アドレスを指定してください。現時点では、Azure Rights Management は、自宅で使用するインターネット プロバイダーの個人用の電子メール アドレスをサポートしていないためです。 Azure Rights Management を送信先のユーザーも使用しているかどうかを気にする必要はありません。

3.  「  **機密ドキュメント** 」のような件名を入力し、本文に「 **この機密ドキュメントを読んでください。ただし、他の人とは共有しないでください。**」のような短いメッセージを入力します。

4.  次に、[ **RMS** ] グループの [ **メッセージ** ] タブで、[ **保護ファイルの共有** ] をクリックし、もう一度 [ **保護ファイルの共有** ] をクリックします。

5.  [ **保護ファイルの共有** ] ダイアログ ボックスで次の操作を実行します。

    1.  [ **閲覧者 – 表示のみ**] を選択します。

        これにより、受信者はドキュメントを表示できるものの、編集したり、印刷したりすることはできなくなります。

    2.  [ **他の人がこれらのドキュメントを開こうとしたときに電子メールを受け取る**] を選択します。

        受信者が添付ファイルを開こうとするたびに、電子メールの通知を受け取ります。また、受信者以外が開こうとした場合にも通知を受け取ります。これは、受信者が共同作業者に電子メールを転送した場合などが考えられます。 そのような場合には、アクセスが拒否された旨の通知を受け取ります。ユーザーの詳細を確認したうえで、そのユーザーが開くことができるドキュメントのコピーを送信するかどうかを決定できます。

    3.  [ **これらのドキュメントへのアクセスをすぐに取り消せるようにする**] を選択します。

        このオプションを選択すると、受信者は添付ファイルを開くにあたり、必ずインターネットに接続していなければならなくなります。ただし、送信者が後からドキュメントを取り消した場合に、受信者がそのドキュメントを開こうとしても、開けなくすることができるという利点があります。 このオプションを選択しなかった場合には、受信者はインターネットに接続しなくてもドキュメントを開くことができます。ただし、送信者が後からドキュメントを取り消した場合に、取り消しが有効になるまで遅延が発生する可能性があるという欠点があります。

    4.  [ **今すぐ送信**] をクリックします。

        ファイルが添付された電子メールは、指定した電子メール アドレスに送信されます。 電子メール メッセージ以外にも、受信者には Azure Rights Management によって保護された添付ドキュメントを読むための手順が表示されます。

保護されたドキュメントを送信したので、受信者に電子メールを受信するまで待って、受信したら開くよう依頼できます。 Outlook はまだ終了しないでください。最後の手順で添付ファイルを追跡する際に、もう一度 Outlook を使用します。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|電子メールで共有するファイルを保護するためのすべての手順、および別の方法|[Rights Management 共有アプリケーションを使用して、電子メールで共有するファイルを保護する](../rms-client/sharing-app-protect-by-email.md)|
|**[保護ファイルの共有]** ダイアログ ボックスのオプションについて|[Rights Management 共有アプリケーションのダイアログ ボックス オプション](../rms-client/sharing-app-dialog-box.md)|


>[!div class="step-by-step"] [« 手順 2](tutorial-step2.md)
[手順 4 »](tutorial-step4.md)

<!--HONumber=May16_HO2-->

