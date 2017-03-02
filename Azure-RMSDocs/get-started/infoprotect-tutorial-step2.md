---
title: "クイック スタート チュートリアルの手順 2 - AIP"
description: "約 20 分で組織の Microsoft Azure Information Protection を簡単に試すことができる概要チュートリアルの手順 2 です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 39dfa8a1c4dabf32f8b62f08a674152f41a5b96a
ms.lasthandoff: 02/24/2017


---

# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>手順 2: Azure Information Protection ポリシーを構成して公開する

>*適用対象: Azure Information Protection*

Azure Information Protection には構成しないで使用できる既定のポリシーが付属していますが、ここではそのポリシーを確認し、いくつか変更を行います。

1. 新しいブラウザー ウィンドウで、テナントのグローバル管理者として [Azure Portal](https://portal.azure.com)にサインインします。

2. ハブ メニューで、**[新規]** をクリックし、**[MARKETPLACE]** リストから **[セキュリティ + ID]** を選択します。 **[セキュリティ + ID]** ブレードで、**[おすすめアプリ]** リストから **[Azure Information Protection]** を選択します。 **[Azure Information Protection]** ブレードで** [作成]** をクリックします。

    **[Azure Information Protection]** ブレードが作成され、次にポータルにサインインするときに、ハブの **[その他のサービス]** リストからサービスを選択できるようになります。 

    > [!TIP] 
    > **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。

3.  Azure Information Protection ブレードで、**[グローバル]** をクリックして **[Policy: Global]** (ポリシー: グローバル) ブレードを確認します。このブレードには、自動的に作成される既定の Information Protection ポリシーが表示されます。
    
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

2. **[Label: Confidential]** (ラベル: 機密) ブレードで、**[Set permissions for documents and emails containing this label]** (このラベルを含むドキュメントやメールのアクセス許可の設定) セクションを見つけます。

    **保護**オプションを選択
    
    ![Azure Information Protection ラベルの保護を構成する](../media/info-protect-protection-bar.png) 
    
    この操作により、**[アクセス許可]** ブレードが開きます。
    
3. **[アクセス許可]** ブレードで **[Azure RMS]** および **[テンプレートの選択]** が選択されていることを確認し、ドロップダウン ボックスをクリックして既定のテンプレート **[\<your organization name> - Confidential]** を選択します。     
    
    たとえば、組織名が VanArsdel, Ltd の場合は、**[VanArsdel, Ltd - Confidential]** (VanArsdel, Ltd - 機密) を選択します。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - Azure RMS 保護を設定する](../media/step2-select-rms-template.png)
    
    この既定の Azure Rights Management テンプレートを無効にしてある場合は、代わりのテンプレートを選択します。 ただし、部門テンプレートを選択する場合は、アカウントがスコープに含まれることを確認します。
    
4. **[完了]** をクリックして変更を保存し、**[アクセス許可]** ブレードを閉じます。

5. **[Label: Confidential]** (ラベル: 機密) ブレードに戻り、**[視覚的なマーキングの設定] ** セクションを見つけます。
    
    **[Documents with this label have a watermark]** (このラベルのあるドキュメントに透かしを付ける) 設定では、**[On]** (オン) をクリックし、**[Text]** (テキスト) ボックスに組織の名前を入力します。 たとえば、以下のように「**VanArsdel, Ltd**」と入力します。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - Azure RMS 保護を設定する](../media/step2-configure-watermark.png)
    
    透かしのサイズ、色、レイアウトは変更できますが、ここでは既定値のままにしておきます。
    
6. **[Configure conditions for automatically applying this label]** (このラベルに自動的に適用する条件を構成する) セクションを見つけます。
    
    **[Add a new condition]** (新しい条件を追加する) をクリックし、**[Condition]** (条件) ブレードで次のように選択します。
    
    a. **[Choose the type of condition]** (条件の種類を選択): 既定値の **[組み込み]** のままにしておきます。
    
    b. **[組み込みのスタイルを選択]**: ドロップダウンから、**[クレジット カード番号]** を選択します。
    
    c. **[Minimum number of occurrences]** (最小出現回数): 既定値の **1** のままにしておきます。
    
    d. **[Count occurrences with unique values only]** (一意の値のみを持つ出現回数のカウント): 既定値の **[Off]** (オフ) のままにしておきます。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - クレジット カードの条件を構成する](../media/step2-configure-condition.png)
    
    **[Save]** (保存) をクリックして、**[Label: Confidential]** (ラベル: 機密) ブレードに戻ります。

7. **[Label: Confidential]** (ラベル: 機密) ブレードでは、以下のように、**[CONDITION NAME]** (条件名) に **[Credit Card Number]** (クレジット カード番号) と表示され、**[OCCURRENCES]** (出現回数) に **1** が設定されています。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - クレジット カードの条件を構成する](../media/step2-see-condition.png)

8. **[Select how this label is applied]** (このラベルの適用方法を選択) は既定値の **[推奨]** のままにしておきます。既定のポリシー ヒントは変更しないでください。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - [Recommended] (推奨) 分類](../media/step2-keep-recommended.png)

9. **[Enter notes for internal housekeeping]** (内部ハウスキーピング処理向けのメモを入力) ボックスに、「**For testing purposes only**」 (テスト用のみ) と入力します。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - メモを入力する](../media/step2-type-notes.png)

10. この **[Label: Confidential]** (ラベル: 機密) ブレードで **[保存]** をクリックします。 次に、**[Policy: Global]**(ポリシー: グローバル) ブレードで **[保存]** を再度クリックします。

    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー構成済み](../media/info-protect-policy-configured.png)

11. 変更を行って保存したので、ユーザーがそれを使用できるようにします。そのためには、最初の **[Azure Information Protection]** ブレードで、**[公開]** をクリックし、**[はい]** をクリックして確定します。

Azure Portal を閉じても、開いたままにしておきこのチュートリアルが終わった後でさらにオプションを構成してみてもかまいません。

既定のポリシーの確認と変更が済んだので、次の手順では Azure Information Protection をインストールします。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|ポリシーの構成オプションについて|[Azure Information Protection ポリシーの構成](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; 手順 1](infoprotect-tutorial-step1.md)
[手順 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
