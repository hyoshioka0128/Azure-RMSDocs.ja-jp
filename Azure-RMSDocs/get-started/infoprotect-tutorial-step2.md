---
title: "クイック スタート チュートリアル手順 1 | Azure Information Protection"
description: "約 30 分で組織の Microsoft Azure Information Protection を簡単に試すことができる概要チュートリアルの手順 2 です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 00d78bf12a7f400b3dfa7e35ada25177170e2d23


---

# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>手順 2: Azure Information Protection ポリシーを構成して公開する

>*適用対象: Azure Information Protection*

Azure Information Protection には構成しないで使用できる既定のポリシーが付属していますが、ここではそのポリシーを確認し、いくつか変更を行います。

1. 新しいブラウザー ウィンドウで、テナントのグローバル管理者として [Azure ポータル](https://portal.azure.com)にサインインします。

2. ハブ メニューで、**[新規]** をクリックし、**[MARKETPLACE]** リストから **[セキュリティ + ID]** を選択します。 **[セキュリティ + ID]** ブレードで、**[おすすめアプリ]** リストから **[Azure Information Protection]** を選択します。 **[Azure Information Protection]** ブレードで** [作成]** をクリックします。

    **[Azure Information Protection]** ブレードが作成され、次にポータルにサインインするときに、ハブの **[その他のサービス]** リストからサービスを選択できるようになります。 

    > [!TIP] 
    > **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。

3.  自動的に表示される **[Policy: Global]**(ポリシー:グローバル) ブレードを確認します。このブレードには、自動的に作成される既定の Information Protection ポリシーが表示されます。
    
    - 分類用のラベル: **[Personal]** (個人)、**[Public]** (公開)、**[Internal]** (内部)、**[Confidential]** (機密)、**[Secret]** (社内秘) が含まれます。 各ラベルの用途については、それぞれのツール ヒントを読んでください。 **[Secret]** (社内秘) には&2; つのサブグループ **[All-Employees]** (全従業員) と **[My-Group]** (自分のグループ) があります。これらは、分類にサブカテゴリを設定する方法の例を示しています。

    - 既定の設定 **[Internal]** (内部)、**[Confidential]** (機密)、**[Secret]** (社内秘) ラベルには視覚的なマーキング (フッター、ヘッダー、透かしなど) が構成されており、どのラベルにも保護が設定されていないことに注意してください。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー](../media/info-protect-policy-default-labels.png)
    
    さらに、一部のグローバル ポリシーの設定は設定されていません。つまり、すべてのドキュメントと電子メールはラベルが必須ではなく、既定のラベルはなく、ユーザーがラベルを変更するときに理由を示す必要はなく、クライアントのカスタム ヘルプ リンクも設定されていません。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-global-settings-for-a-default-template-and-prompt-for-justification"></a>既定のテンプレートと理由を求めるプロンプトのグローバル設定の変更

このチュートリアルでは&2; つのグローバル ポリシーの設定を変更し、どのように動作するかを確認します。

1. **[Select the default label]** (既定のレベルを選択) で、これを **[Internal]** (内部) に設定します。

2. **[Users must provide justification to set a lower classification label, remove a label, or remove protection]** (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります) で、これを**[On]** (オン) に設定します。

## <a name="configuring-a-label-for-protection-a-watermark-and-a-condition-to-prompt-for-classification"></a>分類に関する保護ラベル、透かし、およびプロンプトを出す条件の構成

次に、ラベルの&1; つ **[Confidential]** (機密) の設定を変更します。

1. **[Confidential]** (機密) ラベルをクリックします。 
    
    これで、新しい **[Label: Confidential]** (ラベル: 機密) ブレードに、各ラベルで使用できる設定が表示されます。 

2. **[Label: Confidential]** (ラベル: 機密) ブレードで、**[Set RMS template for protecting documents and emails containing this label]** (このラベルを含むドキュメントおよび電子メールを保護するための RMS テンプレートを設定する) セクションを見つけます。
    
    **[Select RMS template from]** (RMS テンプレートの選択) オプションについては、既定値の **Azure RMS** のままにします。 次に **[RMS テンプレートの選択]** のドロップダウン ボックスをクリックし、既定のテンプレート **[\<your organization name> - Confidential]** (<組織名> - 機密) を選択します。 
    
    たとえば、組織名が VanArsdel, Ltd の場合は、**[VanArsdel, Ltd - Confidential]** (VanArsdel, Ltd - 機密) を選択します。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - Azure RMS 保護を設定する](../media/step2-select-rms-template.png)
    
    この既定の Azure Rights Management テンプレートを無効にしてある場合は、代わりのテンプレートを選択します。 ただし、部門テンプレートを選択する場合は、アカウントがスコープに含まれることを確認します。
    
3. **[Set visual marking]** (視覚的なマーキングの設定) セクションを見つけます。
    
    **[Documents with this label have a watermark]** (このラベルのあるドキュメントに透かしを付ける) 設定では、**[On]** (オン) をクリックし、**[Text]** (テキスト) ボックスに組織の名前を入力します。 たとえば、以下のように「**VanArsdel, Ltd**」と入力します。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - Azure RMS 保護を設定する](../media/step2-configure-watermark.png)
    
    透かしのサイズ、色、レイアウトは変更できますが、ここでは既定値のままにしておきます。
    
4. **[Configure conditions for automatically applying this label]** (このラベルに自動的に適用する条件を構成する) セクションを見つけます。
    
    **[Add a new condition]** (新しい条件を追加する) をクリックし、**[Condition]** (条件) ブレードで次のように選択します。
    
    a. **[Choose the type of condition]** (条件の種類を選択): 既定値の **[組み込み]** のままにしておきます。
    
    b. **[組み込みのスタイルを選択]**: ドロップダウンから、**[クレジット カード番号]** を選択します。
    
    c. **[Minimum number of occurrences]** (最小出現回数): 既定値の **1** のままにしておきます。
    
    d. **[Count occurrences with unique values only]** (一意の値のみを持つ出現回数のカウント): 既定値の **[Off]** (オフ) のままにしておきます。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - クレジット カードの条件を構成する](../media/step2-configure-condition.png)
    
    **[Save]** (保存) をクリックして、**[Label: Confidential]** (ラベル: 機密) ブレードに戻ります。

5. **[Label: Confidential]** (ラベル: 機密) ブレードでは、以下のように、**[CONDITION NAME]** (条件名) に **[Credit Card Number]** (クレジット カード番号) と表示され、**[OCCURRENCES]** (出現回数) に **1** が設定されています。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - クレジット カードの条件を構成する](../media/step2-see-condition.png)

6. **[Select how this label is applied]** (このラベルの適用方法を選択) は既定値の **[推奨]** のままにしておきます。既定のポリシー ヒントは変更しないでください。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - [Recommended] (推奨) 分類](../media/step2-keep-recommended.png)

7. **[Enter notes for internal housekeeping]** (内部ハウスキーピング処理向けのメモを入力) ボックスに、「**For testing purposes only**」 (テスト用のみ) と入力します。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - メモを入力する](../media/step2-type-notes.png)

8. この **[Label: Confidential]** (ラベル: 機密) ブレードで **[保存]** をクリックします。 次に、**[Policy: Global]**(ポリシー: グローバル) ブレードで **[保存]** を再度クリックします。

    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー構成済み](../media/info-protect-policy-configured.png)

9. 変更を行って保存したので、ユーザーがそれを使用できるようにします。そのためには、最初の **[Azure Information Protection]** ブレードで、**[公開]** をクリックし、**[はい]** をクリックして確定します。

Azure ポータルを閉じても、開いたままにしておきこのチュートリアルが終わった後でさらにオプションを構成してみてもかまいません。

これで既定のポリシーの確認と変更が終わりました。次の手順では Azure Information Protection クライアントと Rights Management 共有アプリケーションをインストールします。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|ポリシーの構成オプションについて|[Azure Information Protection ポリシーの構成](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; 手順 1](infoprotect-tutorial-step1.md)
[手順 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


