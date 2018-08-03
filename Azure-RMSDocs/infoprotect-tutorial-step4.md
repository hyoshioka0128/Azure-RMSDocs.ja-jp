---
title: クイック スタート チュートリアルの手順 4 - AIP
description: Azure Information Protection を簡単に試すためのチュートリアルの手順 4 - ラベル付けと保護の動作の確認。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
ms.openlocfilehash: 965725410fd3435f2468810b5cafcbfa91c4fa5b
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39475119"
---
# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>手順 4: 分類、ラベル付け、保護の動作を確認する 

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection クライアントをインストールして Word 文書を開いたので、構成したポリシーを使用して簡単に文書のラベル付けと保護を始められることを確認できます。

文書を保存すると分類と保護が行われますが、その前に未保存の文書を使用して、ラベルを簡単に適用および変更できるかどうかを確認しています。

## <a name="to-manually-change-our-default-label"></a>既定のラベルを手動で変更するには

Information Protection バーの最後のラベルを選択すると、次のように、表示されるサブラベルが示されます。

![Azure Information Protection クイック スタート チュートリアル手順 4 - サブラベルの選択](./media/info-protect-sub-labelsv2.png)

これらのサブラベルのいずれかを選択すると、バーには他のラベルは表示されなくなり、このドキュメントに対して選択したラベルが表示されるようになります。 **[秘密度]** の値が変わってラベル名とサブラベル名が表示され、それに応じて、次のようにラベルの色も変わります。 次に例を示します。

![Azure Information Protection クイック スタート チュートリアル手順 4 - 選択されたサブラベル](./media/info-protect-sub-label-selectedv2.png)

Information Protection バーで、現在選択しているラベルの値の横にある **[ラベルの編集]** アイコンをクリックします。

![Azure Information Protection クイック スタート チュートリアル手順 4 - [ラベルの編集] アイコン](./media/info-protect-edit-label-selectedv2.png)

使用できるラベルが再び表示されます。

最初のラベルの **[個人]** を選択します。 このドキュメントに対して、前に選択したラベルよりも低い分類のラベルを選択したため、次のように分類レベルを下げる理由の入力を求められます。

![Azure Information Protection クイック スタート チュートリアル手順 4 - レベルを下げる理由の確認要求](./media/info-protect-lower-justification.png)

**[The previous label no longer applies]** (前のラベルが適合しなくなった) を選択して、**[確認]** をクリックします。 **[秘密度]** の値が **[個人]** に変わり、他のラベルは再び非表示になります。

## <a name="to-remove-the-classification-completely"></a>分類を完全に削除するには

Information Protection バーで、**[ラベルの編集]** アイコンを再度クリックします。 ここでは、いずれかのラベルを選択するのではなく、**[ラベルの削除]** アイコンをクリックします。

![Azure Information Protection クイック スタート チュートリアル手順 4 - 削除アイコン](./media/delete-icon-from-personalv2.png)

プロンプトが表示されたら、"この文書では分類は不要" などと入力し、**[確認]** をクリックします。  

**[秘密度]** の値が **[未設定]** に変わります。既定のラベルが設定されていない場合も、最初はこのように表示されます。

## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>ラベル付けの推奨プロンプトと自動保護を確認するには

1. Word 文書で、有効なクレジット カード番号 (例: **4242-4242-4242-4242**) を入力します。 

2. 任意のファイル名でローカルにドキュメントを保存します。 

3. クレジット カード番号が検出されたときの保護用に構成したラベルを適用するためのプロンプトが表示されます。 推奨事項に同意しない場合は、ポリシー設定によって、**[無視]** を選択して拒否できます。 推奨事項を表示するが、ユーザーが設定をオーバーライドできるようにすることは、自動分類を使用する場合の誤検知を削減するのに役立ちます。 このチュートリアルでは、**[今すぐ変更]** をクリックします。

    ![Azure Information Protection クイック スタート チュートリアル手順 4 - 推奨プロンプト](./media/change-nowv2.png)

    構成済みのラベルが文書に適用されていることが表示されるようになった (たとえば、**社外秘\財務**) ことに加えて、ページ全体に組織名の透かしが表示され、**社外秘として分類**というフッターも適用されます。 

    また、文書はこのラベルに指定したアクセス許可で保護されます。 文書が保護されていることは、**[ファイル]** タブをクリックして **[文書の保護]** の情報を見ると確認できます。 文書が**社外秘\財務**およびラベルの説明によって保護されていることがわかります。 
    
    ラベルの保護構成のため、従業員のみが文書を開くことができ、一部のアクションは従業員に対して制限されます。 たとえば、印刷およびコンテンツのコピーと抽出のアクセス許可がないため、文書を印刷したりコピーしたりすることはできません。 このような制限は、データの損失を防ぐのに役立ちます。 文書の所有者は文書を印刷およびコピーできますが、組織内の別のユーザーに文書をメールで送信した場合、受信者はこれらのアクションを実行できません。

4. もうこのドキュメントを閉じてもかまいません。

これで、分類、ラベル付け、および保護の動作を確認できました。次は、別の組織の他のユーザーと共有している場合でも文書を保護できる方法を見てみましょう。 文書の使用方法を追跡し、文書へのアクセスを取り消すこともできます。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|ファイルのラベル付けと保護に関するすべての手順 |[ファイルや電子メールを分類して保護する](./rms-client/client-classify-protect.md)|
|ラベル付けアクティビティのログが記録されている場所 |[Azure Information Protection クライアントの使用状況ログ](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)|


>[!div class="step-by-step"]
[&#171; 手順 3](infoprotect-tutorial-step3.md)
[手順 5 &#187;](infoprotect-tutorial-step5.md)
