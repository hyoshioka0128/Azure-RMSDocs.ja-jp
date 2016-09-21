---
title: "Azure Information Protection クイック スタート チュートリアル手順 2 | Azure Information Protection"
description: "4 つの手順を実行して 15 分もかからずに組織の Microsoft Azure Information Protection を簡単に試すことができる概要チュートリアルの手順 2 です。"
author: cabailey
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: ba0f05619e1d13e16b8d4f6d86231b89e9326726
ms.openlocfilehash: 9dfbeb4c887c619d07b11be0da304ac4f4e7d4a9


---

# 手順 2: Azure Information Protection ポリシーを構成して公開する

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

Azure Information Protection には構成しないで使用できる既定のポリシーが付属していますが、ここではそのポリシーを確認し、いくつか変更を行います。

1. 新しいブラウザー ウィンドウで、[Azure ポータル](https://portal.azure.com)にサインインします。 保護だけでなく、分類とラベルもテストする場合、Azure Rights Management テンプレートを取得するためにグローバル管理者としてサインインします。
 
2. ハブ メニューの操作: **[新規]** > **[セキュリティ + ID]** > **[Azure Information Protection (プレビュー)]** > **[作成]** をクリックします。

    **[Azure Information Protection]** ブレードが作成され、次にポータルにサインインするときに、ハブの **[その他のサービス]** リストからサービスを選択できるようになります。 

    > [!TIP] 
    > **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。

3.  **Azure Information Protection** のメイン ブレードを確認します。このブレードには、自動的に作成される既定の Information Protection ポリシーが表示されます。
    
    - 分類用のラベル: **[Personal]** (個人)、**[Public]** (公開)、**[Internal]** (内部)、**[Confidential]** (機密)、**[Secret]** (社内秘) が含まれます。 各ラベルの用途については、それぞれのツール ヒントを読んでください。 **[Secret]** (社内秘) には 2 つのサブグループ **[All-Employees]** (全従業員) と **[My-Group]** (自分のグループ) があります。これらは、分類にサブカテゴリを設定する方法の例を示しています。

    - 既定の設定 **[Internal]** (内部)、**[Confidential]** (機密)、**[Secret]** (社内秘) ラベルには視覚的なマーキング (フッター、ヘッダー、透かしなど) が構成されており、どのラベルにも保護が設定されていないことに注意してください。 さらに、3 つのグローバル設定は設定されていないので、すべてのドキュメントと電子メールにラベルは必要なく、既定のラベルはなく、ユーザーが分類の秘密度を下げるときに理由を示す必要はありません。

    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー](../media/info-protect-policy.png)

このチュートリアルでは 2 つのグローバル設定を変更し、どのように動作するかを確認します。

-  **[Select the default label]** (既定のレベルを選択): これを **[Internal]** (内部) に設定します。

- **Users must provide justification to set a lower classification label, remove a label, or remove protection** (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります): これを**[On]** (オン) に設定します。

次に、ラベルの 1 つ **[Confidential]** (機密) の設定を変更します。

1. **[Confidential]** (機密) ラベルをクリックします。

2. **[Label: Confidential]** (ラベル: 機密) ブレードに、各ラベルで使用できる設定が表示されます。 次のように変更します。

    a. Azure Rights Management をアクティブ化済みの場合: **[Set RMS template for protecting documents and emails containing this label]** (このラベルを含むドキュメントおよび電子メールを保護するための RMS テンプレートを設定する) セクションで、**[Select RMS template from]** (RMS テンプレートの選択元) を、既定値の **[Azure RMS]** のままにします。 次に **[RMS テンプレートの選択]** のドロップダウン ボックスをクリックし、既定のテンプレート **[\<your organization name> - Confidential]** (<組織名> - 機密) を選択します。 たとえば、組織名が VanArsdel, Ltd の場合は、**[VanArsdel, Ltd - Confidential]** (VanArsdel, Ltd - 機密) を選択します。 この既定の Azure Rights Management テンプレートを無効にしてある場合は、代わりのテンプレートを選択します。 ただし、部門テンプレートを選択する場合は、アカウントがスコープに含まれることを確認します。
    
    Azure Rights Management をアクティブ化していない場合は、このオプションを使用することはできません。
    
    b. **[Documents with this label have a watermark]** (このラベルのあるドキュメントに透かしを付ける) : **[On]** (オン) をクリックし、**[Text]** (テキスト) ボックスに組織の名前を入力します。 この例では、「**VanArsdel, Ltd**」と入力します。 
    
    c. **[Add a new condition]** (新しい条件を追加する) をクリックし、**[Condition]** (条件) ブレードで次のように選択します。
    
    - **[Choose the type of condition]** (条件の種類を選択): **[Built-in]** (組み込み)
    
    - **[Select built-in]** (組み込みから選択): **[Credit Card Number]** (クレジット カード番号)
    
    - **[Minimum number of occurrences]** (最小出現回数): **1**
    
    - **Count occurrences with unique values only** (一意の値のみを持つ出現回数のカウント): **[On]** (オン)
    
    - **[Save]** (保存) をクリックして、**[Label: Confidential]** (ラベル: 機密) ブレードに戻ります。

3. **[Label: Confidential]** (ラベル: 機密) ブレードでは、**[CONDITION NAME]** (条件名) に **[Credit Card Number]** (クレジット カード番号) と表示され、**[OCCURRENCES]** (出現回数) に **1** が設定されています。

4. **[Select how this label is applied (このラベルの適用方法を選択)]** は **[Recommended (推奨)]** のままにします。

5. **[Enter notes for internal housekeeping]** (内部ハウスキーピング処理向けのメモを入力) ボックスに、「**For testing purposes only**」 (テスト用のみ) と入力します。

6. この **[Label: Confidential]** (ラベル: 機密) ブレードの **[Save]** (保存) をクリックし、メインの **[Azure Information Protection]** ブレードでもう一度 **[Save]** (保存) をクリックします。

7. 変更を行って保存したので、ユーザーがそれを使用できるようにします。そのためには、**[Publish]** (発行) をクリックし、**[Yes]** (はい) をクリックして確定します。

![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー構成済み](../media/info-protect-policy-configured.png)

Azure ポータルを閉じても、開いたままにしておきこのチュートリアルが終わった後でさらにオプションを構成してみてもかまいません。

既定のポリシーの確認と変更が済んだので、次の手順では Azure Information Protection をインストールします。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|ポリシーの構成オプションについて|[Azure Information Protection ポリシーの構成](configure-policy.md)|


>[!div class="step-by-step"]
[&#171; 手順 1](infoprotect-tutorial-step1.md)
[手順 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Sep16_HO3-->


