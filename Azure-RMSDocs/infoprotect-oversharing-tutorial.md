---
title: チュートリアル - Azure Information Protection を使って過剰な共有を制御する - AIP
description: Azure Information Protection クライアントでのクライアントの詳細設定を構成して動作を確認し、警告、理由の入力、または Outlook からのメッセージの送信のブロックを行うための導入チュートリアルです。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/24/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 38def86f9bbc32edc083f856cf43101890b5a22e
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64562784"
---
# <a name="tutorial-configure-azure-information-protection-to-control-oversharing-of-information-using-outlook"></a>チュートリアル: Azure Information Protection を構成して Outlook を使用した情報の過剰な共有を制御する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

このチュートリアルで学習する内容は次のとおりです。
> [!div class="checklist"]
> * Outlook で警告、理由の入力、またはポップアップ メッセージをブロックする設定を構成する
> * 設定の動作を確認する
> * イベント ログに記録されたユーザー メッセージとアクションを確認する 

電子メールは、電子メールのメッセージ自体または添付ファイルに含まれているかにかかわらず、ユーザーによる不適切な情報共有の最も一般的な方法の 1 つです。 既知の機密情報を特定して、それが組織から流出することを防ぐデータ損失防止 (DLP) ソリューションを使用することができます。 しかし、一部のクライアントの詳細設定と共に Azure Information Protection クライアントを使用して、過剰な共有を防いだり、リアルタイムでフィードバックを提供する対話型メッセージでユーザーに説明したりすることもできます。

このチュートリアルでは、ユーザーによる確認や対応が可能な、警告、理由の入力、ブロック メッセージを示すラベルを 1 つだけ使用した基本的な構成を学習します。

このチュートリアルを完了するための所要時間は約 15 分です。

## <a name="prerequisites"></a>必要条件 

このチュートリアルを完了するための必要条件を次に示します。

1. Azure Information Protection プラン 2 を含むサブスクリプション。
    
    このプランを含むサブスクリプションを持っていない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

2. Azure portal に [Azure Information Protection] ブレードを追加しており、少なくともラベルが 1 つある。
    
    このチュートリアルでは既定のラベル (**[全般]**) を使用しますが、希望する場合は、このラベルを別のラベルに置き換えることができます。 [Azure Information Protection] ブレードの追加に関するヘルプが必要な場合、またはラベルがまだない場合は、「[クイック スタート: Azure portal で Azure Information Protection の使用を開始する](quickstart-viewpolicy.md)」を参照してください。

3. Windows (Windows 7 Service Pack 1 以降) を搭載しているコンピューター。また、このコンピューターで Outlook にサインインできる。 このチュートリアル中に Outlook を複数回再起動する準備をしておいてください。

4. Azure Information Protection クライアントがコンピューターにインストールされている。
    
    クライアントをインストールするには、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)に移動し、Azure Information Protection ページから **AzInfoProtection.exe** をダウンロードします。

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

では、始めましょう。

## <a name="identify-a-label-id-for-testing"></a>テスト用のラベル ID を識別する

このチュートリアルでは、ラベルを 1 つのみ使用して、ユーザーが結果として得られる動作を確認できるようにします。 任意のラベルを使用できますが、テスト用に適切な例は **[全般]** という名前の既定のラベルです。これは、一般的に公開を目的としていないビジネス データに適しており、保護は適用されません。

自分が選択したラベルを指定するには、Azure portal で識別するために、その ID を把握している必要があります。

1. 新しいブラウザー ウィンドウを開き、全体管理者として [Azure portal](https://portal.azure.com) にサインインします。次に、**[Azure Information Protection]** に移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

2. **[分類]** > **[ラベル]** を選択し、**[全般]** ラベルを選択して **[ラベル: 全般]** ブレードを開きます。 

3. ブレードの下部でラベル ID を確認します。
    
    ![Azure Information Protection チュートリアル - ラベル ID を確認する](./media/label-id.png)

4. 後の手順でこの値を簡単にコピーできるように、ラベル ID の値をコピーして一時ファイルに貼り付けます。 この例では、ラベル ID の値は **0e421e6d-ea17-4fdb-8f01-93a3e71333b8** です。

5. **[ラベル: 全般]** ブレードを閉じますが、Azure portal は閉じないでください。

## <a name="create-a-scoped-policy-to-test-the-new-advanced-client-settings"></a>スコープ ポリシーを作成して新しいクライアントの詳細設定をテストする

テストのために、新しいクライアントの詳細設定がお客様だけに適用されるように、新しいスコープ ポリシーを作成します。

1. **[Azure Information Protection - ポリシー]** ブレードで、**[新しいポリシーの追加]** を選択します。 既存のグローバル ポリシーからラベルと設定を示す **[ポリシー]** ブレードが表示されます。

2. **[Oversharing tutorial]\(過剰な共有のチュートリアル\)** のポリシー名を指定し、必要に応じて、**Outlook を使用した過剰な共有を制御するクライアントの詳細設定**という説明を指定します。

3. **[Specify which users/groups get this policy]\(このポリシーを取得するユーザー/グループを指定する\)** を選択し、後のブレードを使用して、自分のユーザー アカウントを指定します。

4. お客様のアカウント名が **[ポリシー]** ブレードに表示され、このブレードのラベルや設定をさらに変更することなく、**[保存]** を選択します。 選択を確認するメッセージが表示される場合があります。 

このスコープ ポリシーに、クライアントの詳細設定を追加する準備ができました。 **[Policy: Oversharing tutorial]\(ポリシー: 過剰な共有のチュートリアル\)** ブレードを閉じますが、Azure portal は閉じないでください。

## <a name="configure-and-test-advanced-client-settings-to-warn-prompt-for-justification-or-block-emails-that-have-the-general-label"></a>クライアントの詳細設定を構成してテストし、[全般] ラベルがある電子メールに対する警告、理由の確認、またはブロックを行う

チュートリアルのこの手順では、次のクライアントの詳細設定を指定して、それぞれを順番にテストします。

- **OutlookWarnUntrustedCollaborationLabel**
- **OutlookJustifyUntrustedCollaborationLabel**
- **OutlookBlockUntrustedCollaborationLabel**

### <a name="create-the-advanced-client-setting-to-warn-users-if-an-email-or-attachment-has-the-general-label"></a>電子メールまたは添付ファイルに [全般] ラベルがある場合、クライアントの詳細設定を作成してユーザーに警告する

新しく作成したスコープ ポリシーを使用して、**[全般]** ラベルの ID と共に **OutlookWarnUntrustedCollaborationLabel** という名前を付けた新しいクライアントの詳細設定を追加します。 

1. **[Azure Information Protection - ポリシー]** ブレードに戻って、**[Oversharing tutorial]\(過剰な共有のチュートリアル\)** の横にあるコンテキスト メニュー (**...**) を選択します。 次に **[詳細設定]** を選択します。

2. **[詳細設定]** ブレードで、詳細設定の名前 (**OutlookWarnUntrustedCollaborationLabel**) を入力し、値として自分のラベル ID を貼り付けます。 Microsoft のラベル ID の例を使用します。
    
    
    ![Azure Information Protection チュートリアル - OutlookWarnUntrustedCollaborationLabel クライアントの詳細設定を作成する ](./media/configure-warnmessage.png)

3. **[保存して閉じる]** を選択します。

**[ポリシー]** ブレードまたは Azure portal は閉じないでください。

### <a name="test-the-advanced-client-setting-to-warn-users-if-an-email-or-attachment-has-the-general-label"></a>電子メールまたは添付ファイルに [全般] ラベルがある場合、クライアントの詳細設定をテストしてユーザーに警告する

クライアント コンピューター上に、このクライアントの詳細設定を構成した結果が表示されます。

1. クライアント コンピューターで Outlook を開きます。 
    
    Outlook が既に開いている場合は、再起動します。 作成したばかりの変更をダウンロードするには、再起動が必要です。

2. 新しいメール メッセージを作成して、**[全般]** ラベルを適用します。 たとえば、**[ファイル]** タブから **[保護]** ボタン、**[全般]** の順に選択します。

3. **[宛先]** フィールドに自分の電子メール アドレスを指定し、件名に「**Testing the General label for the Warn message**」 (警告メッセージの [全般] ラベルをテストする) と入力します。 その後、電子メールを送信します。

4. クライアントの詳細設定の結果として、電子メールを送信する前に確認を求める次の警告が表示されます。 次に例を示します。
    
    ![Azure Information Protection チュートリアル - OutlookWarnUntrustedCollaborationLabel クライアントの詳細設定を表示する ](./media/see-warnmessage.png)
    
5. **[全般]** のラベルが付けられた電子メールを誤って送信しようとしたユーザーのように、**[キャンセル]** を選択します。 電子メールが送信されていないことがわかりますが、電子メール メッセージは残るため、コンテンツまたはラベルなどを変更することができます。

6. 変更を加えずに、もう一度 **[送信]** を選択します。 今回は、送信してもよいコンテンツであることを認めているユーザーのように、**[確認して送信]** を選択します。 電子メールが送信されます。

### <a name="change-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-has-the-general-label"></a>電子メールに [全般] ラベルがある場合、クライアントの詳細設定を変更してユーザーに理由を確認する

既存のクライアントの詳細設定を編集して、**[全般]** ラベル ID を保持しますが、名前を「**OutlookJustifyUntrustedCollaborationLabel**」に変更します。 

1. **[Azure Information Protection - ポリシー]** ブレードで、**[Oversharing tutorial]\(過剰な共有のチュートリアル\)** の横にあるコンテキスト メニュー (**...**) を選択します。 次に **[詳細設定]** を選択します。

2. **[詳細設定]** ブレードで、作成した前の詳細設定の名前 **OutlookWarnUntrustedCollaborationLabel** を **OutlookJustifyUntrustedCollaborationLabel** という新しい名前に置き換えます。
    
    ![Azure Information Protection チュートリアル - OutlookJustifyUntrustedCollaborationLabel クライアントの詳細設定を作成する ](./media/configure-justifymessage.png)

3. **[保存して閉じる]** を選択します。

**[ポリシー]** ブレードまたは Azure portal は閉じないでください。

### <a name="test-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-has-the-general-label"></a>電子メールに [全般] ラベルがある場合、クライアントの詳細設定をテストしてユーザーに理由を確認する

クライアント コンピューターに、この新しいクライアントの詳細設定の結果が表示されます。

1. クライアント コンピューター上で、Outlook を再起動して作成したばかりの変更をダウンロードします。

2. 新しい電子メール メッセージを作成して、前述のように、**[全般]** ラベルを適用します。 たとえば、**[ファイル]** タブから **[保護]** ボタン、**[全般]** の順に選択します。

3. **[宛先]** フィールドに自分の電子メール アドレスを指定し、件名に「**Testing the General label for the Justify message**」 (理由メッセージの [全般] ラベルをテストする) と入力します。 その後、電子メールを送信します。

4. 今回は、電子メールを送信する前に理由を提供することを求める、次のメッセージが表示されます。 次に例を示します。
    
    ![Azure Information Protection チュートリアル - OutlookJustifyUntrustedCollaborationLabel クライアントの詳細設定を表示する ](./media/see-justifymessage.png)
    
5. **[全般]** のラベルが付けられた電子メールを誤って送信しようとしたユーザーのように、**[キャンセル]** を選択します。 電子メールが送信されていないのがわかりますが、電子メール メッセージ自体が残るため、コンテンツまたはラベルなどを変更することができます。

6. 変更を加えずに、もう一度 **[送信]** を選択します。 今回は、**[I confirm the recipients are approved for sharing this content]\(受信者によるこのコンテンツの共有が承認済みであることを確認しました\)** などの理由オプションのいずれかを選択して、**[確認して送信]** を選択します。 電子メールが送信されます。

### <a name="change-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label"></a>クライアントの詳細設定を変更して、ユーザーが [全般] ラベルがある電子メールを送信できないようにする

既存のクライアントの詳細設定をもう 1 回編集して、**[全般]** ラベル ID を保持しますが、名前を「**OutlookBlockUntrustedCollaborationLabel**」に変更します。 

1. Azure portal の **[Azure Information Protection - ポリシー]** ブレードで、**[Oversharing tutorial]\(過剰な共有のチュートリアル\)** の横にあるコンテキスト メニュー (**...**) を選択します。 次に **[詳細設定]** を選択します。

2. **[詳細設定]** ブレードで、作成した前の詳細設定の名前 **OutlookJustifyUntrustedCollaborationLabel** を **OutlookBlockUntrustedCollaborationLabel** という新しい名前に置き換えます。
    
    ![Azure Information Protection チュートリアル - OutlookBlockUntrustedCollaborationLabel クライアントの詳細設定を作成する ](./media/configure-blockmessage.png)

3. **[保存して閉じる]** を選択します。

**[ポリシー]** ブレードまたは Azure portal は閉じないでください。

### <a name="test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label"></a>クライアントの詳細設定をテストして、ユーザーが [全般] ラベルがある電子メールを送信できないようにする

クライアント コンピューターに、この新しいクライアントの詳細設定の結果が表示されます。

1. クライアント コンピューター上で、Outlook を再起動して作成したばかりの変更をダウンロードします。

2. 新しい電子メール メッセージを作成して、前述のように、**[全般]** ラベルを適用します。 たとえば、**[ファイル]** タブから **[保護]** ボタン、**[全般]** の順に選択します。

3. **[宛先]** フィールドに自分の電子メール アドレスを指定し、件名に「**Testing the General label for the Block message**」 (ブロック メッセージの [全般] ラベルをテストする) と入力します。 その後、電子メールを送信します。

4. 今回は、電子メールを送信しないように次のメッセージが表示されます。 次に例を示します。
    
    ![Azure Information Protection チュートリアル - 電子メールのポップアップ メッセージをブロックする](./media/see-blockmessage.png)

5. ユーザーとしては、選択肢が **[OK]** のみであるため、変更を加えることができる電子メール メッセージに戻ることになります。 **[OK]** を選択して、この電子メール メッセージをキャンセルします。

### <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label"></a>イベント ログを使用して [全般] ラベルに対するメッセージとユーザー アクションを識別する

電子メールまたは添付ファイルにラベルが含まれないときに次のシナリオに移動する前に、イベント ビューアーを起動して、**[アプリケーションとサービス ログ]** > **[Azure Information Protection]** に移動します。

行ったテストごとに情報イベントが作成され、メッセージとユーザーの応答の両方が記録されます。

- 警告メッセージ: 情報 ID 301

- 理由メッセージ: 情報 ID 302

- ブロック メッセージ: 情報 ID 303

たとえば、最初のテストはユーザーに警告するためのもので、**[キャンセル]** を選択したので、**[ユーザーの応答]** で最初のイベント 301 に **[破棄済み]** と表示されます。 次に例を示します。

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Warn message.msg
Item Name: Testing the General label for the Warn message
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Dismissed
```

しかし、次のイベント 301 に反映される **[確認して送信]** を選択すると、**[ユーザーの応答]** には **[確認済み]** と表示されます。

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Warn message.msg
Item Name: Testing the General label for the Warn message
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Confirmed
```

理由メッセージでは、同じパターンが繰り返されます。これにはイベント 302 が含まれます。 最初のイベントには **[破棄済み]** の **[ユーザーの応答]** があり、2 つ目には選択された理由が表示されます。 次に例を示します。

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Justify message.msg
Item Name: Testing the General label for the Justify message
Process Name: OUTLOOK
Action: Justify
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
User Justification: I confirm the recipients are approved for sharing this content
Action Source: 
User Response: Confirmed

```

イベント ログの上部に、イベント 303 を含む、記録されたブロック メッセージが表示されます。 次に例を示します。

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Block message.msg
Item Name: Testing the General label for the Block message
Process Name: OUTLOOK
Action: Block
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
```

## <a name="configure-and-test-an-advanced-client-setting-to-warn-prompt-for-justification-or-block-emails-that-dont-have-a-label"></a>クライアントの詳細設定を構成してテストし、ラベルのない電子メールに対する警告、理由の確認、またはブロックを行う

チュートリアルのこの手順では、異なる値で新しいクライアントの詳細設定を指定して、それぞれを順番にテストします。

- **OutlookUnlabeledCollaborationAction**

### <a name="create-the-advanced-client-setting-to-warn-users-if-an-email-doesnt-have-a-label"></a>電子メールにラベルがない場合、クライアントの詳細設定を作成してユーザーに警告する

**OutlookUnlabeledCollaborationAction** という名前が付けられたこの新しいクライアントの詳細設定にラベル ID は必要ありませんが、ラベル付けされていないコンテンツに対して行うアクションを指定します。 

1. Azure portal で **[Azure Information Protection - ポリシー]** ブレードに戻り、**[Oversharing tutorial]\(過剰な共有のチュートリアル\)** の横にあるコンテキスト メニュー (**...**) を選択します。 次に **[詳細設定]** を選択します。

2. **[詳細設定]** ブレードで、詳細設定の名前 (**OutlookUnlabeledCollaborationAction**) を入力して、値に **[警告]** を指定します。
    
    ![Azure Information Protection tutorial - [警告] 値を使って OutlookUnlabeledCollaborationAction クライアントの詳細設定を作成する ](./media/configure-nolablewarn.png)

3. **[保存して閉じる]** を選択します。

**[ポリシー]** ブレードまたは Azure portal は閉じないでください。

### <a name="test-the-advanced-client-setting-to-warn-users-if-an-email-doesnt-have-a-label"></a>電子メールにラベルがない場合、クライアントの詳細設定をテストしてユーザーに警告する

クライアント コンピューターで、コンテンツにラベルがないときのために、この新しいクライアントの詳細設定を構成した結果が表示されます。

1. クライアント コンピューター上で、Outlook を再起動して作成したばかりの変更をダウンロードします。

2. 新しいメール メッセージを作成します。今回は、ラベルを適用しないでください。

3. **[宛先]** フィールドに自分の電子メール アドレスを指定し、件名に「**Testing send an email without a label for the Warn message**」 (警告メッセージにラベルを使用しないで電子メールの送信をテストする) と入力します。 その後、電子メールを送信します。

4. 今回は、**[確認して送信]** または **[キャンセル]** を行うことができる **[確認が必要]** のメッセージが表示されます。
    
    ![Azure Information Protection チュートリアル - [警告] 値を使って OutlookUnlabeledCollaborationAction クライアントの詳細設定を表示する](./media/see-nolablewarn.png)

5. **[確認して送信]** を選択します。

### <a name="change-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-is-unlabeled"></a>電子メールにラベル付けされていない場合、クライアントの詳細設定を変更してユーザーに理由を確認する

既存のクライアントの詳細設定を編集して、**OutlookUnlabeledCollaborationAction** の名前を保持しますが、値を **[理由]** に変更します。 

1. **[Azure Information Protection - ポリシー]** ブレードで、**[Oversharing tutorial]\(過剰な共有のチュートリアル\)** の横にあるコンテキスト メニュー (**...**) を選択します。 次に **[詳細設定]** を選択します。

2. **[詳細設定]** ブレードで、**OutlookUnlabeledCollaborationAction** 設定を見つけて、**[警告]** の前の値を **[理由]** という新しい値に置き換えます。
    
    ![Azure Information Protection tutorial - OutlookUnlabeledCollaborationAction クライアントの詳細設定を [理由] 値に変更する](./media/configure-justifymessage2.png)

3. **[保存して閉じる]** を選択します。

**[ポリシー]** ブレードまたは Azure portal は閉じないでください。

### <a name="test-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-isnt-labeled"></a>電子メールにラベルが付けられていない場合、クライアントの詳細設定をテストしてユーザーに理由を確認する

クライアント コンピューターに、このクライアントの詳細設定の値を変更した結果が表示されます。

1. クライアント コンピューター上で、Outlook を再起動して作成したばかりの変更をダウンロードします。

2. 新しいメール メッセージを作成します。前述のように、ラベルは適用しないでください。

3. **[宛先]** フィールドに自分の電子メール アドレスを指定し、件名に「**Testing send an email without a label for the Justify message**」 (理由メッセージにラベルを使用しないで電子メールの送信をテストする) と入力します。 その後、電子メールを送信します。

4. 今回は、さまざまなオプションと共に **[理由が必要です]** のメッセージが表示されます。
    
    ![Azure Information Protection チュートリアル - [理由] 値を使って OutlookUnlabeledCollaborationAction クライアントの詳細設定を表示する](./media/see-nolabljustify.png)

5. **[My manager approved sharing of this content]\(上司がこのコンテンツの共有を承認しました\)** などのオプションを選択します。 次に、**[確認して送信]** を選択します。

### <a name="change-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled"></a>クライアントの詳細設定を変更して、ユーザーが [全般] ラベルのない電子メールを送信できないようにする

前述のように、既存のクライアントの詳細設定を編集して、**OutlookUnlabeledCollaborationAction** の名前を保持しますが、値を **[ブロック]** に変更します。 

1. **[Azure Information Protection - ポリシー]** ブレードで、**[Oversharing tutorial]\(過剰な共有のチュートリアル\)** の横にあるコンテキスト メニュー (**...**) を選択します。 次に **[詳細設定]** を選択します。

2. **[詳細設定]** ブレードで、**OutlookUnlabeledCollaborationAction** 設定を確認し、**[理由]** の前の値を **[ブロック]** という新しい値に置き換えます。
    
    ![Azure Information Protection tutorial - OutlookUnlabeledCollaborationAction クライアントの詳細設定を [ブロック] 値に変更する](./media/configure-blockmessage2.png)

3. **[保存して閉じる]** を選択します。

**[ポリシー]** ブレードまたは Azure portal は閉じないでください。

### <a name="test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled"></a>クライアントの詳細設定をテストして、ユーザーが [全般] ラベルのない電子メールを送信できないようにする

クライアント コンピューターに、このクライアントの詳細設定の値を変更した結果が表示されます。

1. クライアント コンピューター上で、Outlook を再起動して作成したばかりの変更をダウンロードします。

2. 新しいメール メッセージを作成します。前述のように、ラベルは適用しないでください。

3. **[宛先]** フィールドに自分の電子メール アドレスを指定し、件名に「**Testing send an email without a label for the Block message**」 (ブロック メッセージにラベルを使用しないで電子メールの送信をテストする) と入力します。 その後、電子メールを送信します。

4. 今回は、電子メールを送信しないように次のメッセージが、ユーザーへの説明と共に表示されます。 次に例を示します。
    
    ![Azure Information Protection チュートリアル - [ブロック] 値で OutlookWarnUntrustedCollaborationLabel クライアントの詳細設定を表示する](./media/see-blockmessage2.png)

5. ユーザーの役割では、利用できるオプションは **[OK]** のみであることがわかります。これにより、ラベルを選択できる電子メール メッセージに戻ります。
    
    **[OK]** を選択して、この電子メール メッセージをキャンセルします。

### <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-unlabeled-email"></a>イベント ログを使用してラベル付けされていない電子メールにメッセージとユーザー アクションを識別する

前述のように、メッセージとユーザーの応答は、同じイベント ID と共にイベント ビューアー (**[アプリケーションとサービス ログ]** > **[Azure Information Protection]**) に記録されます。

- 警告メッセージ: 情報 ID 301

- 理由メッセージ: 情報 ID 302

- ブロック メッセージ: 情報 ID 303

たとえば、電子メールにラベルがない場合の理由の確認結果です。

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing send an email without a label for the Justify message.msg
Item Name: Testing send an email without a label for the Justify message
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```

## <a name="create-an-advanced-client-setting-to-exempt-these-messages-for-internal-recipients"></a>クライアントの詳細設定を作成して、内部受信者に対してこれらのメッセージの適用を除外する

受信者として自分の電子メール アドレスを使用し、これらのメッセージをテストしてきました。 しかし、運用環境では、受信者が組織外にいる場合にのみ、これらのメッセージの表示を選択してもよいでしょう。 この例外は、組織が常に共同作業をしているパートナーにまで広げることができます。

このしくみを示すために、**OutlookBlockTrustedDomains** という名前が付けられた新しいクライアントの詳細設定を作成し、自分の電子メール アドレスから独自のドメイン名を指定します。 これにより、電子メール アドレスでドメイン名を共有する受信者に表示されるブロック メッセージが回避されます。 同様に、**OutlookWarnTrustedDomains** と **OutlookJustifyTrustedDomains** に対してクライアントの詳細設定を作成できます。

1. Azure portal の **[Azure Information Protection - ポリシー]** ブレードで、**[Oversharing tutorial]\(過剰な共有のチュートリアル\)** の横にあるコンテキスト メニュー (**...**) を選択します。 次に **[詳細設定]** を選択します。

2. **[詳細設定]** ブレードで、詳細設定の名前 (**OutlookBlockTrustedDomains**) を入力して、値として自分の電子メール アドレスからドメイン名を貼り付けます。 次に例を示します。
    
    ![Azure Information Protection チュートリアル - OutlookBlockTrustedDomains クライアントの詳細設定を作成する](./media/configure-exemptblockdomain.png)

4. **[保存して閉じる]** を選択します。 **[ポリシー]** ブレードまたは Azure portal は閉じないでください。

5. [自分のアドレスにラベル付けされていない電子メールを送信するという前述のテスト](#test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled)を繰り返すと、ブロック メッセージは表示されなくなります。 しかし、組織外から新しい受信者を追加する場合、もう一度ブロック メッセージが表示されます。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルで行った変更を保持したくない場合は、次の操作を行います。

1. Azure portal の **[Azure Information Protection - ポリシー]** ブレードで、**[Oversharing tutorial]\(過剰な共有のチュートリアル\)** の横にあるコンテキスト メニュー (**...**) を選択します。 その後、**[ポリシーの削除]** を選択します。

2. 確認するメッセージが表示されたら、**[OK]** を選択します。

Outlook を再起動すると、このチュートリアルで構成した設定は構成されなくなります。

## <a name="next-steps"></a>次の手順

テストを速く済ませるために、このチュートリアルでは、添付ファイルのない、1 人の受信者への電子メール メッセージを使用しました。 しかし、複数の受信者、複数のラベルを含む同じメソッドを適用し、ユーザーにとってラベル付けの状態がわかりにくい添付ファイルにも同じロジックを適用することもできます。 たとえば、電子メール メッセージ自体には [公開] のラベルが付けられていますが、添付の PowerPoint プレゼンテーションには [全般] のラベルが付けられています。 詳細については、管理者ガイドの次のセクションを参照してください。[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](./rms-client/client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)

管理者ガイドには、クライアントの動作のカスタマイズに使用できるその他のクライアントの詳細設定に関する情報も含まれます。 完全なリストについては、「[使用可能なクライアントの詳細設定](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings)」を参照してください。
