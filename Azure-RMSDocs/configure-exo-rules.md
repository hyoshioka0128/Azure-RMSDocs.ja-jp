---
title: Azure Information Protection ラベルの Exchange Online メールフロールール
description: Azure Information Protection ラベルの Exchange Online メール フロー ルールを構成するための手順と例を示します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ROBOTS: NOINDEX
ms.reviewer: shakella
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7c76e7e79acb0cd12bfcbe2d71a1fee3ce78b1ba
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164285"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>Azure Information Protection ラベルの Exchange Online メール フロー ルールの構成

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、Microsoft 365 ドキュメントから「機密ラベルと[DLP ラベル](/microsoft-365/compliance/dlp-sensitivity-label-as-condition)[について](/microsoft-365/compliance/sensitivity-labels)」を参照してください。 *

> [!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure Portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Exchange Online でメール フロー ルールを構成して Azure Information Protection ラベルを使用し、特定のシナリオに向けた追加の保護を適用するときに、次の情報を参考にしてください。 例:

- 既定のラベルは **[全般]** で、保護は適用されません。 このラベルを含む外部からの電子メールには、追加の [転送不可] 保護アクションが適用されます。

- **社外秘** の添付ファイルが組織外に電子メールで送信され、その電子メールが保護されていない場合は、追加の暗号化のみの保護アクションを適用します。

アクションとして保護を適用するメール フロー ルール は、電子メールが既に保護されている場合は無視されます。 たとえば、[転送不可] によって保護されている電子メールメッセージは、[暗号化のみ] オプションを使用するように Exchange メールフロールールで変更することはできません。  

これらの例は、変更するだけでなく拡張することもできます。 たとえば、さらに条件を追加します。 詳しくは、Exchange Online のドキュメントの「[Exchange Online のメール フロー ルール (トランスポート ルール)](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules)」をご覧ください。

電子メールメッセージを暗号化するためのメールフロールールの構成の詳細については、Office ドキュメントの「 [Microsoft 365 で電子メールメッセージを暗号化するためのメールフロールールの定義](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8) 」を参照してください。 

## <a name="prerequisite-know-your-label-guid"></a>前提条件: ラベル GUID を確認する

Azure Information Protection ラベルはメタデータに格納されるため、Exchange Online のメール フロー ルールでは、メッセージと Office ドキュメント添付ファイルに対するこの情報を読み取ることができます。 メール フロー ルールでは、PDF ドキュメントのメタデータを検査することはできません。

ラベル付けされたメッセージとドキュメントを識別するメール フロー ルールを構成する前に、使用する Azure Information Protection ラベルの GUID を把握する必要があります。 

ラベルによって格納されるメタデータと、ラベルの GUID の識別方法について詳しくは、「[メールやドキュメントに格納されるラベル情報](configure-policy.md#label-information-stored-in-emails-and-documents)」をご覧ください。

## <a name="example-configurations"></a>構成例

以下の例では、次の手順に従って新しいメール フロー ルールを作成します。

1. Web ブラウザーで、グローバル管理者のアクセス許可が付与されている職場または学校のアカウントを使用して、Microsoft 365 にサインインします。 

2. [ **管理** ] タイルを選択します。

3. Microsoft 365 管理センターで、[**管理センター**] [Exchange] の順に選択し  >  ます。

4. Exchange 管理センターでは、**メールフロー** ルールによって  >    >  **+**  >  **新しいルールが作成** されます。 

> [!TIP]
> ルールを構成する際にユーザー インターフェイスの問題が発生する場合は、Internet Explorer など、別のブラウザーを試してください。

この例では、電子メールが組織の外に送信されるときに保護を適用する条件が 1 つだけ含まれています。 選択できる他の条件について詳しくは、「[Exchange Online でのメール フロー ルールの条件と例外 (述語)](/exchange/security-and-compliance/mail-flow-rules/conditions-and-exceptions)」をご覧ください。


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>例 1: **[全般]** ラベルの付いた電子メールが組織の外部に送信されるときに [転送不可] オプションを適用するルール

この例では、**[全般]** ラベルの GUID は 0e421e6d-ea17-4fdb-8f01-93a3e71333b8 です。 このルールで使用する独自のラベルまたはサブラベルの GUID で置き換えます。 

Azure Information Protection ポリシーでは、このラベルは電子メールを **[全般]** として分類する既定のラベルとして構成され、ラベルで保護は適用されません。 

1. **[名前]** に、`Apply Do Not Forward for General emails sent externally` のようなルールの名前を入力します。
 
2. **[このルールを適用する条件]** で、**[受信者が...]** を選択し、**[組織外]** を選択したら、**[OK]** を選択します。

3. **[その他のオプション]** を選択し、**[条件の追加]** を選択します。
 
4. **[and]** で、**[メッセージ ヘッダー]** を選択し、**[これらの単語を含む]** を選択します。
     
    a. **[テキストの入力]** を選択し、`msip_labels` と入力します。
     
    b. **[Enter words]\(単語の入力\)** を選択し、`MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True` と入力します。
    
    c. を選択し **+** 、[ **OK]** を選択します。

5. **[実行する処理]** で、**[メッセージのセキュリティを変更する]** > **[Apply Office 365 Message Encryption and rights protection]\(Office 365 メッセージの暗号化と権限保護を適用する\)** > **[転送不可]** の順に選択し、**[OK]** を選択します。
    
    ルールの構成は、次のようになります。  ![ Azure Information Protection ラベルに構成されている Exchange Online メールフロールール-例1](./media/aip-exo-rule-ex1.png)

7. **[保存]** を選びます。 

[転送不可] オプションについて詳しくは、「[電子メールの [転送不可] オプション](configure-usage-rights.md#do-not-forward-option-for-emails)」をご覧ください。

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>例 2: 機密性の高い **パートナー** というラベルが付いた添付ファイルが含まれている場合に、電子メールに暗号化のみのオプションを適用する規則。これらの電子メールは組織外に送信されます。

この例では、**Confidential \ Partners** サブラベルの GUID は 0e421e6d-ea17-4fdb-8f01-93a3e71333b8 です。 このルールで使用する独自のラベルまたはサブラベルの GUID で置き換えます。 

このラベルは、パートナーと共同で作業するドキュメントの分類と保護のために使用されます。   

1. **[名前]** に、`Apply Encrypt to emails sent externally if protected attachments` のようなルールの名前を入力します。
 
2. **[このルールを適用する条件]** で、**[受信者が...]** を選択し、**[組織外]** を選択したら、**[OK]** を選択します。

3. **[その他のオプション]** を選択し、**[条件の追加]** を選択します。
 
4. **[and]** で、**[Any attachment]\(添付ファイル\)** を選択し、**[これらのプロパティが次の単語のいずれかを含む]** を選択します。
     
    a. [ **+**  >  **カスタム添付ファイルの指定] プロパティ** を選択します。
  
    b. **[プロパティ]** に `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled` を入力します。
    
    c. **[値]** に `True` を入力します。
    
    d. **[保存]** を選択し、**[OK]** を選択します。

5. **[実行する処理]** で、**[メッセージのセキュリティを変更する]** > **[Apply Office 365 Message Encryption and rights protection]\(Office 365 メッセージの暗号化と権限保護を適用する\)** > **[暗号化]** の順に選択し、**[OK]** を選択します。
    
    ルールの構成は、次のようになります。  ![ Azure Information Protection ラベルに構成された Exchange Online メールフロールール-例2](./media/aip-exo-rule-ex2.png)

6. **[保存]** を選びます。 

暗号化オプションの詳細については、「 [電子メールの暗号化専用オプション](configure-usage-rights.md#encrypt-only-option-for-emails)」を参照してください。


## <a name="next-steps"></a>次のステップ

Exchange Online メール フロー ルールで使用するラベルの作成と構成について詳しくは、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。

また、添付ファイルを含む電子メール メッセージを分類するには、次の Azure Information Protection [ポリシー設定](configure-policy-settings.md)の使用を検討してください: **添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します**。