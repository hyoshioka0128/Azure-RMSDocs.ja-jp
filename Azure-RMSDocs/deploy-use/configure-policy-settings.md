---
title: "Azure Information Protection のポリシー設定を構成する"
description: "すべてのユーザーとデバイスに適用される Azure Information Protection ポリシーを設定します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: c5ff5a2ab0c73ad36d8fcb6062a25b9fb936f846
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Azure Information Protection のポリシー設定を構成する方法

>*適用対象: Azure Information Protection*

Information Protection バーに表示されるタイトルとツールヒントのほかに、Azure Information Protection ポリシーには、すべてのユーザーとデバイスに適用される次の設定があります。

![Azure Information Protection ポリシーのグローバル設定](../media/info-protect-policy-default-settingsv2.png)


設定を構成するには:

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は新しいブラウザーのウィンドウで全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 構成する設定をすべてのユーザーに適用する場合は、次のグローバル設定を **[Policy: Global (ポリシー: グローバル)]** ブレードで構成します。

    - **All documents and emails must have a label** (すべてのドキュメントと電子メールにラベルを設定する必要があります): このオプションを **[オン]** に設定した場合は、すべての保存されるドキュメントと送信される電子メールにラベルを適用する必要があります。 ラベル付けは、ユーザーが手動で割り当てる、[条件](configure-policy-classification.md)の結果として自動的に割り当てる、または (**[Select the default label]** (既定のラベルを選択) オプションを設定することで) 既定で割り当てることができます。 

    ユーザーがドキュメントを保存または電子メールを送信するときにラベルが割り当てられなかった場合は、ラベルの選択を求めるプロンプトが表示されます。 たとえば、

    ![ラベル付けが必須である場合の Azure Information Protection のプロンプト](../media/info-protect-enforce-labelv2.png)

    - **Select the default label** (既定のラベルを選択します): このオプションを設定した場合、ラベルを持たないドキュメントや電子メールに割り当てるラベルを選択します。 サブラベルがあるラベルは、既定値として設定することはできません。 

    - **分類ラベルを低くする、ラベルを削除する、保護を削除する場合、ユーザーは理由を提供する必要があります**: このオプションが **[オン]** に設定されているときは、ユーザーがこれらの操作を行うと (たとえば **[Public (パブリック)]** ラベルを **[Personal (個人用)]** に変更)、その操作の理由を入力する画面が表示されます。 たとえば、ユーザーは、「このドキュメントにはもう秘密情報が含まれていない」という説明を入力します。 この操作と妥当性の説明は、次のローカルの Windows イベント ログに記録されます: **[アプリケーション]**  >  **[Microsoft Azure Information Protection]**  

    ![新しい分類が下位の場合の Azure Information Protection のプロンプト](../media/info-protect-lower-justification.png)

    このオプションは、サブラベルには適用されません。

    - **For email messages with attachments, apply a label that matches the highest classification of those attachments (添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します)**: このオプションを **[推奨]** に設定すると、ユーザーは自分の電子メール メッセージにラベルを適用するよう求められます。 ラベルは、添付ファイルに適用されている分類のラベルに基づいて動的に選択され、最上位の分類のラベルが選択されます。 ユーザーは、推奨設定を受け入れるか、通知を閉じます。 このオプションを **[オン]** に設定すると、ラベルが自動的に適用されますが、ユーザーは電子メールを送信する前に、ラベルを削除することも、別のラベルを選択することもできます。  

    - **Provide a custom URL for the Azure Information Protection client "Tell me more" web page** (Azure Information Protection クライアントの "詳細情報" Web ページ用のカスタム URL を指定する): このリンクは、**[Microsoft Azure Information Protection]** ダイアログ ボックスの **[ヘルプとフィードバック]** セクションにあり、ユーザーが Office アプリケーションの **[ホーム]** タブで**[保護]** > **[ヘルプとフィードバック]** を選択したときに表示されます。 このリンクの既定のリンク先は [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection) Web サイトです。 このリンクをクリックしたときに別の Web ページが表示されるようにするには、HTTP または HTTPS (推奨) の URL を入力します。 入力されたカスタム URL がどのデバイスでもアクセス可能で正しく表示できるかどうかの確認は行われません。
        
        たとえば、ヘルプ デスク用に、クライアントのインストールと使用の方法が記載されている Microsoft のドキュメント ページ (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) や、リリース バージョン情報のページ (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**) を指定します。 あるいは、ユーザー向けの Web ページを独自に作成して、ヘルプ デスクへの連絡方法を掲載したり、ラベルを使用する手順をユーザーに説明するビデオを公開したりすることが考えられます。
        
     [スコープ ポリシー](configure-policy-scope.md)を作成した場合は、指定されたユーザーにこれらの設定を上書きすることができます。 スコープ ポリシーでこれらの設定を構成するには、最初の **[Azure Information Protection]** ブレードで該当するスコープ ポリシーを選択します。

3. 変更を保存するには、**[保存]** をクリックします。

4. ユーザーが変更を使用できるようにするには、最初の **[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
