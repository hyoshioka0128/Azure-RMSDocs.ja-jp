---
title: "クイック スタート チュートリアルの手順 4 - AIP"
description: "Azure Information Protection を簡単に試すためのチュートリアルの手順 4 - ラベル付けと保護の動作の確認。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
ms.openlocfilehash: fb1334a2ee345125db6e2637a59a5ab1a69e62d8
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>手順 4: 分類、ラベル付け、保護の動作を確認する 

>*適用対象: Azure Information Protection*

Azure Information Protection クライアントをインストールして Word 文書を開いたので、構成したポリシーを使用して簡単に文書のラベル付けと保護を始められることを確認できます。

文書を保存すると分類と保護が行われますが、その前に、未保存の文書を使用して簡単にラベルを適用および変更できることを見てみます。

## <a name="to-manually-change-our-default-label"></a>既定のラベルを手動で変更するには

Information Protection バーの **[秘密]** ラベルを選択すると、次のように、表示されるサブラベルが示されます。

![Azure Information Protection クイック スタート チュートリアル手順 4 - サブラベルの選択](../media/info-protect-sub-labels.png)

**[会社全体]** を選択すると、バーには他のラベルは表示されなくなり、このドキュメントに対して選択したラベルが表示されるようになります。 **[秘密度]** の値が **[秘密 \ 会社全体]** に変わり、それに応じて、次のようにラベルの色も変わります。

![Azure Information Protection クイック スタート チュートリアル手順 4 - 選択されたサブラベル](../media/info-protect-sub-label-selected.png)

Information Protection バーで、**[秘密 \ 会社全体]** の横にある **[ラベルの編集]** アイコンをクリックします。

![Azure Information Protection クイック スタート チュートリアル手順 4 - [ラベルの編集] アイコン](../media/info-protect-edit-label-selected.png)

使用できるラベルが再び表示されます。

ここで、**[個人]** ラベルを選択します。 このドキュメントに対して前に選択したラベルよりも低い分類であるラベルを選択したため、次のように、分類レベルを下げる理由の入力を求められます。

![Azure Information Protection クイック スタート チュートリアル手順 4 - レベルを下げる理由の確認要求](../media/info-protect-lower-justification.png)

**[The previous label no longer applies]** (前のラベルが適合しなくなった) を選択して、**[確認]** をクリックします。 **[秘密度]** の値が **[個人]** に変わり、他のラベルは再び非表示になります。

## <a name="to-remove-the-classification-completely"></a>分類を完全に削除するには

Information Protection バーで、**[ラベルの編集]** アイコンを再度クリックします。 ここでは、いずれかのラベルを選択するのではなく、**[ラベルの削除]** アイコンをクリックします。

![Azure Information Protection クイック スタート チュートリアル手順 4 - 削除アイコン](../media/delete-icon-from-personal.png)

プロンプトが表示されたら、"この文書では分類は不要" などと入力し、**[確認]** をクリックします。  

**[Sensitivity]** (秘密度) の値が **[Not set]** (非設定) に変わります。既定のラベルが設定されていない場合も、最初はこのように表示されます。

![Azure Information Protection クイック スタート チュートリアル手順 4 - 分類の削除](../media/sensitivity-not-set.png)


## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>ラベル付けの推奨プロンプトと自動保護を確認するには

1. Word 文書で、有効なクレジット カード番号 (例: **4242-4242-4242-4242**) を入力します。 

2. 文書を保存します (ファイル名と場所は任意)。 

3. **[It is recommended to label this file as Confidential]** (このファイルには機密というラベルを付けることが推奨されます) というプロンプトが表示されます。 **[Change now]** (今すぐ変更) をクリックします。

    ![Azure Information Protection クイック スタート チュートリアル手順 4 - 推奨プロンプト](../media/change-now.png)

    ラベルが 「Confidential」 (機密) に設定されている文書に加え、ページ全体に組織名の透かしがすぐに表示されます。また、**「Sensitivity: Confidential」** (秘密度: 機密) のフッターも適用されます。 

    文書は指定した Azure Rights Management テンプレートによっても保護されます。これは、**[ファイル]** タブをクリックして **[文書の保護]** の情報を見ることで確認できます。 既定の機密テンプレートを使用した場合は、文書が内部ユーザーに制限され (組織外のユーザーは文書を開けません)、内容をコピーまたは印刷できないという情報が表示されます。 文書の所有者は文書をコピーおよび印刷できますが、組織内の別のユーザーに文書をメール送信した場合、受信者はこれらの操作を実行できません。

4. もうこのドキュメントを閉じてもかまいません。

これで、分類、ラベル付け、および保護の動作を確認できました。次は、別の組織の他のユーザーと共有している場合でも文書を保護できる方法を見てみましょう。 文書の使用方法を追跡し、文書へのアクセスを取り消すこともできます。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|ファイルのラベル付けと保護に関するすべての手順 |[ファイルや電子メールを分類して保護する](../rms-client/client-classify-protect.md)|





>[!div class="step-by-step"]
[&#171; 手順 3](infoprotect-tutorial-step3.md)
[手順 5 &#187;](infoprotect-tutorial-step5.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]