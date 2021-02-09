---
title: チュートリアル - Azure Information Protection (AIP) を使用した過剰共有の防止
description: Azure Information Protection (AIP) クライアントを使用して、ユーザーがコンテンツを過剰に共有できないようにするための詳細なチュートリアルです。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 6936402c9b58bf46b94e71ab597ce04c0391f59d
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240820"
---
# <a name="tutorial-preventing-oversharing-in-outlook-using-azure-information-protection-aip"></a>チュートリアル:Azure Information Protection (AIP) を使用した Outlook での過剰共有の防止

>**適用対象*:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***関連する内容**:[Windows 用の Azure Information Protection 統合ラベル付けクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

システム管理者は、組織のコンテンツがセキュリティで保護され、信頼されたユーザーとのみ共有されるように保証する必要があります。 ユーザーがコンテンツを不適切に共有する最も一般的な方法の 1 つが、電子メールです。 特定のユーザーのみにアクセスを制限する、信頼された外部ユーザーとのみコンテンツを共有するなど、Outlook を使用した過剰共有を防ぐようにポリシーを構成します。

**必要な時間:** このチュートリアルは 30 分で完了できます。

このチュートリアルでは、以下の内容を学習します。
> [!div class="checklist"]
> * 特定のラベル付け条件に対して、警告、正当な理由、ブロック動作を構成する
> * 設定の動作を確認する
> * イベント ログに記録されたユーザー メッセージとアクションを確認する 

## <a name="tutorial-prerequisites"></a>チュートリアルの前提条件

このチュートリアルを開始する前に、次のシステム要件を満たしていることを確認してください。

|前提条件  |説明  |
|---------|---------|
|**コンピューターの要件**     | 次のことを確認してください。 <br /><br />- Windows コンピューターに Azure Information Protection 統合ラベル付けクライアントがインストールされている。 詳細については、「[クイック スタート: Azure Information Protection (AIP) 統合ラベル付けクライアントのデプロイ](quickstart-deploy-client.md)」を参照してください。 <br /><br />- PowerShell がインストールされており、PowerShell を管理者として実行できる。 <br /><br />- Outlook にサインインできる。 このチュートリアル中に Outlook を複数回再起動する準備をしておいてください。     |
|**Azure Information Protection のサブスクリプション**     |   [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/) を含む Azure サブスクリプションが必要です。 <br /><br />これらのサブスクリプションのいずれかがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成してください。       |
|**秘密度ラベルとテスト ポリシー**     |  ポリシーで構成されている **全般** 秘密度ラベル。 <br /><br />ラベル付け管理センター (Microsoft 365 コンプライアンス センター、Microsoft 365 セキュリティ センター、または Microsoft 365 セキュリティ/コンプライアンス センター) で秘密度ラベルを構成します。 詳細については、[Microsoft 365 のドキュメント](/microsoft-365/compliance/create-sensitivity-labels)を参照してください。 <br /><br />このチュートリアルでは、ライブ ポリシーに影響を与えないように、テスト ポリシーを使用することをお勧めします。 <br />お使いのポリシーの名前と **全般** ラベルの GUID が手元にあることを確認します。   |
| | |

始めましょう。 

## <a name="implement-a-warning-message-for-emails-labeled-as-general"></a>"全般" ラベルの付いた電子メールに対する警告メッセージを実装する

この手順では、Outlook ユーザーが、**全般** ラベルが付いた電子メールを送信する前に警告メッセージが表示されるようにポリシーを構成する方法について説明します。 

ユーザーは警告に従い、ラベルかコンテンツのどちらかを変更するか、またはそのまま電子メールを送信するかを選択することができます。

1. クライアント コンピューターで、PowerShell を管理者として実行します。

1. 次のコマンドを実行して、**全般** ラベルに対する警告メッセージを定義します。 このコマンドをコピーしたら、**Global** をポリシーの名前、長い文字列を独自のラベル ID に置き換えます。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}
    ```

    この例では、ポリシーの名前は **Global** で、**全般** ラベルの GUID は **8faca7b8-8d20-48a3-8ea2-0f96310a848e** です。

    > [!TIP]
    > この設定を複数のラベルに適用する場合は、値の中に GUID をコンマで区切って列挙します。

1. Outlook で設定をテストします。

    1. クライアント コンピューターで、Outlook を開くか再起動して、更新された設定を取得します。

    1. 新しいメール メッセージを作成して、**[全般]** ラベルを適用します。 メッセージ ツールバーで、:::image type="icon" source="media/i-sensitivity.PNG" border="false"::: **[秘密度]** ボタンを選択してから、 **[全般]** を選択します。

    1. **[送信先]** フィールドをご自分のメール アドレスを使用して定義し、 **[件名]** フィールドに `Testing a warning message for the General label` を指定して、電子メールを送信します。

        次の警告が表示され、電子メールを送信する前に確認するように求められます。 次に例を示します。

        :::image type="content" source="media/qs-tutor/ul-see-warnmessage.png" alt-text="&quot;全般&quot; ラベルに対する警告メッセージのテスト":::

    1. **全般** ラベルが付けられた電子メールを誤って送信しようとしたユーザーのつもりで操作します。 ここでは、警告に従うので、 **[キャンセル]** を選択します。

        電子メールは送信されませんが、開いたままになっているので、コンテンツまたはラベルを変更できます。

    1. 変更を加える必要はなく、コンテンツを送信するのが適切であると判断することができます。 **[送信]** を再度選択します。 今回は、警告が表示されたら、 **[確認して送信]** を選択します。

        電子メールが送信されます。

次に、["全般" 電子メールが外部に送信される場合にのみ、警告メッセージを表示します](#show-a-warning-message-for-general-emails-only-when-theyre-sent-externally)。

## <a name="show-a-warning-message-for-general-emails-only-when-theyre-sent-externally"></a>"全般" 電子メールが外部に送信される場合にのみ、警告メッセージを表示する

この手順では、ここまで構成した警告メッセージに例外を追加して、外部受信者にのみ警告メッセージが表示されるようにする方法について説明します。

**全般** 電子メールを内部に送信する場合、警告メッセージは表示されません。

1. クライアント コンピューターで、PowerShell を管理者として実行します。

1. 次のコマンドを実行して、ドメインを警告メッセージ用の信頼される側のドメインとして定義します。 このコマンドをコピーしたら、**Global** をポリシーの名前、**contoso.com** を独自のドメインに置き換えます。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnTrustedDomains="contoso.com"}    
    ```

    > [!TIP]
    > 信頼されるパートナーを追加する場合など、この設定を複数のドメインに適用する場合は、値の中にドメインをコンマで区切って列挙します。

1. Outlook で設定をテストします。

    1. クライアント コンピューターで、Outlook を開くか再起動して、更新された設定を取得します。

    1. 新しいメール メッセージを作成して、**[全般]** ラベルを適用します。 メッセージ ツールバーで、:::image type="icon" source="media/i-sensitivity.PNG" border="false"::: **[秘密度]** ボタンを選択してから、 **[全般]** を選択します。

    1. **[送信先]** フィールドをご自分のメール アドレスを使用して定義し、 **[件名]** フィールドに `Testing a warning message for the General label` を指定して、電子メールを送信します。

        電子メールが送信され、警告は表示されません。

## <a name="request-users-to-justify-sending-unlabeled-content"></a>ラベル付けされていないコンテンツの送信の正当な理由を示すようにユーザーに要求する

この手順では、ラベル付けされていないコンテンツを送信する正当な理由をユーザーが示さなければならないように詳細設定を構成する方法について説明します。 

1. クライアント コンピューターで、PowerShell を管理者として実行します。

1. ユーザーが、ラベル付けされていない電子メールを送信しようとした場合に Outlook に理由メッセージが表示されるようにするには、**Global** をポリシーの名前に置き換え、以下を実行します。
 
    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Justify"}
    ```

1. Outlook で設定をテストします。

    1. クライアント コンピューターで、Outlook を開くか再起動して、更新された設定を取得します。

    1. 新しい電子メール メッセージを作成し、適用されているラベルがないことを確認します。
    
        たとえば、ポリシーにより既定のラベルが適用されている場合は、:::image type="icon" source="media/i-sensitivity.PNG" border="false"::: ボタンを使用して削除します。 

    1. **[送信先]** フィールドをご自分のメール アドレスを使用して定義し、 **[件名]** フィールドに `Testing the justification message for unlabeled content` を指定して、電子メールを送信します。
    
        次の例のようなポップアップが表示されます。

        :::image type="content" source="media/qs-tutor/ul-see-nolabljustify.png" alt-text="ラベル付けされていないコンテンツに対する理由メッセージのサンプル":::

    1. いずれかのオプションを選択します。 3 番目のオプション **[Other, as explained] (その他、理由は以下のとおり)** を選択した場合は、テキスト ボックスにサンプル テキストを入力します。 
    
    1. **[確認して送信]** を選択します。
    
        電子メールが送信されます。

次に、[自由記載の理由プロンプトをカスタマイズします](#customize-the-free-text-justification-prompt)。

## <a name="customize-the-free-text-justification-prompt"></a>自由記載の理由プロンプトをカスタマイズする

この手順では、既定の理由メッセージの 3 番目のオプションをカスタマイズする方法について説明します。 

たとえば、具体的詳細を追加するようにユーザーに求めるテキストを追加したり、ユーザーに機密データを入力しないように注意を促したりすることができます。

1. クライアント コンピューターで、PowerShell を管理者として実行します。

1. 表示される理由メッセージの自由記載プロンプトをカスタマイズするには、**Global** をポリシー名に置き換え、以下を実行します。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{JustificationTextForUserText="Other (please explain) - Do not enter sensitive info"}
    ```

    > [!TIP]
    > 引用符で囲んだ値は、代わりに追加したい他のテキストに自由に置き換えることができます。 

1. Outlook で設定をテストします。

    1. クライアント コンピューターで、Outlook を開くか再起動して、更新された設定を取得します。

    1. 新しい電子メール メッセージを作成し、適用されているラベルがないようにします。 

        たとえば、ポリシーにより既定のラベルが適用されている場合は、:::image type="icon" source="media/i-sensitivity.PNG" border="false"::: ボタンを使用して削除します。 

    1. **[送信先]** フィールドをご自分のメール アドレスを使用して定義し、 **[件名]** フィールドに `Testing a customized free text justification prompt` を指定して、電子メールを送信します。
    
        理由のポップアップが表示され、今度はカスタマイズしたテキストが表示されます。 次に例を示します。 

        :::image type="content" source="media/qs-tutor/ul-see-nolabljustify-custom.png" alt-text="理由プロンプトに、カスタマイズされた自由記載プロンプトが使用されているサンプル":::
        
## <a name="block-users-from-sending-unlabeled-powerpoint-messages"></a>ユーザーがラベル付けされていない PowerPoint メッセージを送信できないようにする

この手順では、ユーザーが Outlook からラベル付けされていない PowerPoint ファイルを送信できないようにする方法について説明します。

1. クライアント コンピューターで、PowerShell を管理者として実行します。

1. ラベル付けされていないコンテンツが Outlook から送信されないようにするには、**Global** をポリシーの名前に置き換え、以下を実行します。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Block"}
    ```

1. このブロック動作を PowerPoint ファイルの特定の種類のみに制限するには、**Global** をポリシーの名前に置き換え、以下を実行します。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.POTX,.POTM,.POT,.PPTX"}
    ```

1. Outlook で設定をテストします。

    1. クライアント コンピューターで、PowerPoint を開き、新しい **.pptx** ファイルを作成します。ファイルはラベル付けされていないままにします。

    1. Outlook を開くか再起動して、更新された設定を取得します。
    
    1. ラベル付けされていない PowerPoint ファイルを新しい Outlook メッセージに添付します。

    1. **[送信先]** フィールドをご自分のメール アドレスを使用して定義し、 **[件名]** フィールドに `Testing sending unlabeled PowerPoint files` を指定して、電子メールを送信します。
    
        Outlook によって電子メールの送信がブロックされ、次のメッセージが表示されます。

        :::image type="content" source="media/qs-tutor/ul-see-blockmessage.png" alt-text="ラベル付けされていない PowerPoint 添付ファイルに対するメッセージをブロックするサンプル":::

次に、[ラベル付けされていない PowerPoint メッセージのブロック メッセージをカスタマイズします](#customize-the-block-message-for-unlabeled-powerpoint-messages)。

## <a name="customize-the-block-message-for-unlabeled-powerpoint-messages"></a>ラベル付けされていない PowerPoint メッセージのブロック メッセージをカスタマイズする

この手順では、ユーザーがラベル付けされていない PowerPoint ファイルを外部ユーザーに送信しようとしたときに表示されるメッセージをカスタマイズする方法について説明します。

> [!IMPORTANT]
> この手順では、定義済みのすべての設定を **OutlookUnlabeledCollaborationAction** 詳細プロパティを使用してオーバーライドします。これを表示するのはチュートリアルの目的のためだけです。
>
> 実稼働環境では、**OutlookUnlabeledCollaborationAction** 詳細プロパティを使用してルールを定義する、"*または*" 下記のように定義した json ファイルを使用して複雑なルールを定義する、の "*いずれか*" により、複雑化させないようにすることをお勧めします。
>

**json ファイルを使用してルールを定義するには、次のようにします。**

1. 次のコードを使用して、**OutlookCollaborationRule_1.json** という名前の **.json** ファイルを作成します。

    ```JSON
    {   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",
                     "LabelId" : null,
                    "Extensions": [
                                    ".PPTX",
                                    ".PPTM",
                                    ".POTX",
                                    ".POTM",
                                    ".POT",
                                    ".PPTX"
                                 ]
                    
                },
                {                   
                    "type" : "EmailLabel",
                     "LabelId" : null
                }
            ]
        },      
        {           
            "type" : "Email Block",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Email Blocked",                 
                    "Body": "Sending PowerPoint files to external recipients requires that you label your files so that we can classify and protect Contoso content.<br><br>List of attachments that are not labeled:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br>Label your document and send it again."              
                },          
            },          
            "DefaultLanguage": "en-us"      
        }   
      ] 
    }
    ```
1. クライアント コンピューターからアクセスできる場所に、**OutlookCollaborationRule_1.json** ファイルを保存します。

1. クライアント コンピューターで、PowerShell を管理者として実行します。

1. ブロック メッセージをカスタマイズするには、次のコードをコピーし、**C:\OutlookCollaborationRule_1.json** を .json ファイルへのパス、**General** をポリシーの名前に置き換えます。 

    ```PowerShell
    $filedata = Get-Content "C:\OutlookCollaborationRule_1.json”
    Set-LabelPolicy -Identity General -AdvancedSettings @{OutlookCollaborationRule_1 ="$filedata"}    
    ```

    コードを実行して、.json ファイルで定義した設定を実装します。

1. Outlook で設定をテストします。

    1. クライアント コンピューターで、PowerPoint を開き、新しい **.pptx** ファイルを作成します。ファイルはラベル付けされていないままにします。

    1. Outlook を開くか再起動して、更新された設定を取得します。
    
    1. ラベル付けされていない PowerPoint ファイルを新しい Outlook メッセージに添付します。

    1. **[送信先]** フィールドをご自分のメール アドレスを使用して定義し、 **[件名]** フィールドに `Testing customized blocking message for unlabeled PowerPoint files` を指定して、電子メールを送信します。
    
        Outlook によって電子メールの送信がブロックされ、次のメッセージが表示されます。

        :::image type="content" source="media/qs-tutor/ul-see-custom-blockmessage.png" alt-text="ラベルのない PowerPoint ファイルのカスタム ブロック メッセージ":::

次に、[イベント ログを使用して "全般" ラベルに対するメッセージとユーザー アクションを識別します](#use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label)。

## <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label"></a>イベント ログを使用して [全般] ラベルに対するメッセージとユーザー アクションを識別する

このチュートリアルでは、警告、理由、ブロック メッセージを含む、いくつかの種類の過剰共有を防ぐために、Outlook で AIP の動作をカスタマイズする方法について学習しました。 また、ローカル クライアント コンピューターで Outlook の動作を確認しました。

ここで、Windows イベント ビューアーを開始して、発生したアクションのログを確認できます。

**AIP ログ イベントのイベント ビューアーを確認するには、次のようにします。**

クライアント コンピューターで、Windows イベント ビューアー アプリケーションを開き、 **[アプリケーションとサービス ログ]**  >  **[Azure Information Protection]** に移動します。

実行したテストごとにログに記録された情報イベントが表示されます。メッセージとユーザー応答の両方の詳細が含まれます。

- **警告メッセージ**:情報 ID 301
- **理由メッセージ**:情報 ID 302
- **ブロック メッセージ**:情報 ID 303

次に例を示します。

- [警告メッセージ テストのイベント ログを確認する](#check-the-event-log-for-your-warning-message-tests)
- [理由メッセージ テストのイベント ログを確認する](#check-the-event-log-for-your-justify-message-tests)
- [ブロック メッセージ テストのイベント ログを確認する](#check-the-event-log-for-your-block-message-tests)

### <a name="check-the-event-log-for-your-warning-message-tests"></a>警告メッセージ テストのイベント ログを確認する

最初のテストでは、ユーザーに警告が表示され、 **[キャンセル]** を選択しました。 この場合、最初のイベント 301 の **User Response (ユーザーの応答)** に **Dismissed (却下済み)** が表示されます。

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing a warning message for the General label.msg
Item Name: Testing a warning message for the General label
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Dismissed
```

しかし、次のイベント 301 に反映される **[確認して送信]** を選択すると、**[ユーザーの応答]** には **[確認済み]** と表示されます。

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing a warning message for the General label.msg
Item Name: Testing a warning message for the General label
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Confirmed
```

### <a name="check-the-event-log-for-your-justify-message-tests"></a>理由メッセージ テストのイベント ログを確認する

理由メッセージでは、同じパターンが繰り返されます。これにはイベント 302 が含まれます。 最初のイベントには **[破棄済み]** の **[ユーザーの応答]** があり、2 つ目には選択された理由が表示されます。 次に例を示します。

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the justification message for unlabeled content.msg
Item Name: Testing the justification message for unlabeled content
Process Name: OUTLOOK
Action: Justify
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
User Justification: I confirm the recipients are approved for sharing this content
Action Source: 
User Response: Confirmed

```

### <a name="check-the-event-log-for-your-block-message-tests"></a>ブロック メッセージ テストのイベント ログを確認する

イベント ログの上部に、イベント 303 を含む、記録されたブロック メッセージが表示されます。 次に例を示します。

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing sending unlabeled PowerPoint files.msg
Item Name: Testing sending unlabeled PowerPoint files
Process Name: OUTLOOK
Action: Block
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
```

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを終了したら、テスト ポリシーを後で参照できるように保持することも、削除してリソースをクリーン アップすることもできます。

ポリシーを削除する場合は、それを作成した管理センター (Microsoft 365 コンプライアンスセンター、Microsoft 365 セキュリティセンター、または Microsoft 365 セキュリティ/コンプライアンス センター) で行います。

詳細については、[Microsoft 365 のドキュメント](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)を参照してください

削除したら、このチュートリアルで定義した設定で構成されることがなくなるように、クライアント コンピューターの Outlook を再起動します。

## <a name="next-steps"></a>次のステップ

テストを速く済ませるために、このチュートリアルでは、添付ファイルのない、1 人の受信者への電子メール メッセージを使用しました。 

同じ方法を複数の受信者とラベル、または添付ファイルに適用すると、ラベル付けの状態がユーザーにわかりにくくなることがあります。

たとえば、**公開** ラベルの付いた電子メール メッセージにポップアップ メッセージを表示するが、**全般** ラベルの付いた PowerPoint プレゼンテーションは添付したい場合があります。

詳細プロパティと Outlook カスタマイズの詳細については、「[管理者ガイド:Azure Information Protection 統合ラベル付けクライアントのカスタム構成](rms-client/clientv2-admin-guide-customizations.md)」を参照してください。