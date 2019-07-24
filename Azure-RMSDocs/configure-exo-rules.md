---
title: Azure Information Protection ラベルの Exchange Online メールフロールール
description: Azure Information Protection ラベルの Exchange Online メール フロー ルールを構成するための手順と例を示します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ms.reviewer: shakella
ms.suite: ems
ms.openlocfilehash: f738f990e6a4c2f79e4eede12431c1afe15803cd
ms.sourcegitcommit: 7992e1dc791d6d919036f7aa98bcdd21a6c32ad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68428554"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>Azure Information Protection ラベルの Exchange Online メール フロー ルールの構成

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Exchange Online でメール フロー ルールを構成して Azure Information Protection ラベルを使用し、特定のシナリオに向けた追加の保護を適用するときに、次の情報を参考にしてください。 例えば:

- 既定のラベルは **[全般]** で、保護は適用されません。 このラベルを含む外部からの電子メールには、追加の [転送不可] 保護アクションが適用されます。

- **Confidential \ Partners** ラベルを含む添付ファイル付きの電子メールが組織外のユーザーに送信され、その電子メールが保護されていない場合、暗号化のみの保護アクションが追加で適用されます。

アクションとして保護を適用するメール フロー ルール は、電子メールが既に保護されている場合は無視されます。 たとえば、電子メール メッセージが [転送不可] によって保護されている場合、暗号化のみのオプションを使用する Exchange メール フロー ルールでは変更できません。  

これらの例は、変更するだけでなく拡張することもできます。 たとえば、さらに条件を追加します。 詳しくは、Exchange Online のドキュメントの「[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx)」をご覧ください。

電子メール メッセージを暗号化するメール フロー ルールを構成する方法について詳しくは、Office ドキュメントの「[Office 365 でメール メッセージを暗号化するメール フロー ルールを定義する](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)」をご覧ください。 

## <a name="prerequisite-know-your-label-guid"></a>前提条件:ご自分のラベルの GUID を把握している

Azure Information Protection ラベルはメタデータに格納されるため、Exchange Online のメール フロー ルールでは、メッセージと Office ドキュメント添付ファイルに対するこの情報を読み取ることができます。 メール フロー ルールでは、PDF ドキュメントのメタデータを検査することはできません。

ラベル付けされたメッセージとドキュメントを識別するメール フロー ルールを構成する前に、使用する Azure Information Protection ラベルの GUID を把握する必要があります。 

ラベルによって格納されるメタデータと、ラベルの GUID の識別方法について詳しくは、「[メールやドキュメントに格納されるラベル情報](configure-policy.md#label-information-stored-in-emails-and-documents)」をご覧ください。

## <a name="example-configurations"></a>構成例

以下の例では、次の手順に従って新しいメール フロー ルールを作成します。

1. グローバル管理者のアクセス許可を付与されている職場または学校のアカウントを使用して、Web ブラウザーで Office 365 にサインインします。 

2. **[管理者]** タイルを選択します。

3. Microsoft 365 管理センターで、 **[管理センター]**  >  **[Exchange]** の順に選択します。

4. Exchange 管理センターで、 **[メール フロー]**  >  **[ルール]**  >  **+**  >  **[新しいルールの作成]** の順に選択します。 

> [!TIP]
> ルールを構成する際にユーザー インターフェイスの問題が発生する場合は、Internet Explorer など、別のブラウザーを試してください。

この例では、電子メールが組織の外に送信されるときに保護を適用する条件が 1 つだけ含まれています。 選択できる他の条件について詳しくは、「[Exchange Online でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/library/jj919235(v=exchg.150).aspx)」をご覧ください。


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>例 1:  **[全般]** ラベルの付いた電子メールが組織の外部に送信されるときに、それに [転送不可] オプションを適用するルール

この例では、 **[全般]** ラベルの GUID は 0e421e6d-ea17-4fdb-8f01-93a3e71333b8 です。 このルールで使用する独自のラベルまたはサブラベルの GUID で置き換えます。 

Azure Information Protection ポリシーでは、このラベルは電子メールを **[全般]** として分類する既定のラベルとして構成され、ラベルで保護は適用されません。 

1. **[名前]** に、`Apply Do Not Forward for General emails sent externally` のようなルールの名前を入力します。
 
2. **[このルールを適用する条件]** で、 **[受信者が...]** を選択し、 **[組織外]** を選択したら、 **[OK]** を選択します。

3. **[その他のオプション]** を選択し、 **[条件の追加]** を選択します。
 
4. **[and]** で、 **[メッセージ ヘッダー]** を選択し、 **[これらの単語を含む]** を選択します。
     
    a. **[テキストの入力]** を選択し、`msip_labels` と入力します。
     
    b. **[Enter words]\(単語の入力\)** を選択し、`MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;` と入力します。
    
    c. **[+]** を選択し、 **[OK]** を選択します。

5. **[実行する処理]** で、 **[メッセージのセキュリティを変更する]**  >  **[Office 365 メッセージの暗号化と権限保護を適用する]**  >  **[転送不可]** の順に選択し、 **[OK]** を選択します。
    
    これで、ルール構成は次のようになります。![Azure Information Protection ラベルに対して構成された Exchange Online メールフロールール-例1](./media/aip-exo-rule-ex1.png)

7. **[保存]** を選択します。 

[転送不可] オプションについて詳しくは、「[電子メールの [転送不可] オプション](configure-usage-rights.md#do-not-forward-option-for-emails)」をご覧ください。

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>例 2:電子メールに **Confidential \ Partners** ラベルの付いた添付ファイルが含まれ、かつ電子メールが組織の外部に送信される場合に、暗号化のみのオプションを電子メールに適用するルール

この例では、**Confidential \ Partners** サブラベルの GUID は 0e421e6d-ea17-4fdb-8f01-93a3e71333b8 です。 このルールで使用する独自のラベルまたはサブラベルの GUID で置き換えます。 

このラベルは、パートナーと共同で作業するドキュメントの分類と保護のために使用されます。   

1. **[名前]** に、`Apply Encrypt to emails sent externally if protected attachments` のようなルールの名前を入力します。
 
2. **[このルールを適用する条件]** で、 **[受信者が...]** を選択し、 **[組織外]** を選択したら、 **[OK]** を選択します。

3. **[その他のオプション]** を選択し、 **[条件の追加]** を選択します。
 
4. **[and]** で、 **[任意の添付ファイル]** を選択してから、 **[これらのプロパティが次の単語のいずれかを含む]** を選択します。
     
    a. **[+]**  >  **[カスタム添付ファイルのプロパティを指定]** を選択します。
  
    b. **[プロパティ]** に `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled` を入力します。
    
    c. **[値]** に `True` を入力します。
    
    d. **[保存]** を選択し、 **[OK]** を選択します。

5. **[実行する処理]** で、 **[メッセージのセキュリティを変更する]**  >  **[Office 365 メッセージの暗号化と権限保護を適用する]**  >  **[暗号化]** の順に選択し、 **[OK]** を選択します。
    
    これで、ルール構成は次のようになります。![Azure Information Protection ラベルに対して構成された Exchange Online メールフロールール-例2](./media/aip-exo-rule-ex2.png)

6. **[保存]** を選択します。 

暗号化オプションについて詳しくは、「[電子メールの暗号化のみオプション](configure-usage-rights.md#encrypt-only-option-for-emails)」をご覧ください。


## <a name="next-steps"></a>次の手順

Exchange Online メール フロー ルールで使用するラベルの作成と構成について詳しくは、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。

また、添付ファイルを含む電子メール メッセージの分類を楽にするために、次の Azure Information Protection [ポリシー設定](configure-policy-settings.md)の使用を検討してください: **添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します**。


