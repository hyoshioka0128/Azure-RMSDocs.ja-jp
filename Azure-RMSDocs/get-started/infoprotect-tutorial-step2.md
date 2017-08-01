---
title: "クイック スタート チュートリアルの手順 2 - AIP"
description: "Azure Information Protection を簡単に試すためのチュートリアルの手順 2 - ポリシーの構成。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
ms.openlocfilehash: db87ffaa15802f081439f7983ef1060a60c0b24c
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2017
---
# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>手順 2: Azure Information Protection ポリシーを構成して公開する

>*適用対象: Azure Information Protection*

Azure Information Protection には構成しないで使用できる既定のポリシーが付属していますが、ここではそのポリシーを確認し、いくつか変更を行います。

1. 新しいブラウザー ウィンドウで、テナントの全体管理者またはセキュリティ管理者として [Azure Portal](https://portal.azure.com)にサインインします。

2. ハブ メニューで、**[新規]** をクリックし、**[MARKETPLACE]** リストから **[セキュリティ + ID]** を選択します。 **[セキュリティ + ID]** ブレードで、**[おすすめアプリ]** リストから **[Azure Information Protection]** を選択します。 **[Azure Information Protection]** ブレードで **[作成]** をクリックします。

    これによって、テナントのサービスがアクティブ化されて**[Azure Information Protection]** ブレードが作成され、次にポータルにサインインするときに、ハブの **[その他のサービス]** リストからサービスを選択できるようになります。 

    > [!TIP] 
    > **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。

3. サービスに最初に接続するときに自動的に開く **[クイック スタート]** ページに関する情報を確認します。 後でここに戻ることができます。 このチュートリアルでは、**[グローバル ポリシー]** をクリックして、**[Policy: Global]\(ポリシー: グローバル\)** ブレードを開きます。 このブレードはサービスの後続の接続のために自動的に開き、テナントに自動で作成される既定の Information Protection ポリシーが表示されます。
    
    - 分類用のラベル: **[Personal (個人)]**、**[Public (公開)]**、**[General (全般)]**、**[Confidential (社外秘)]**、**[Highly Confidential (非常に機密性の高い社外秘)]**。 最後の 2 つのラベルを展開すると、サブラベル **[すべての従業員]** と **[すべてのユーザー (未保護)]** が表示されます。これは、分類にサブカテゴリを設定できることを示す例となります。
    
       > [!NOTE]
       > 実際の既定のポリシーは、このチュートリアルの既定のポリシーとは若干異なる場合があります。 たとえば、ラベル名が **[全般]** ではなく **[内部]** である場合や、**[非常に機密性の高い社外秘]** ではなく **[秘密]** である場合があります。 この場合は、既定のポリシーの以前のバージョンを使用している可能性があります。 または、このチュートリアルを開始する前に、自分で編集した可能性があります。
       > 
       > 使用する既定のポリシーが異なる場合でも、このチュートリアルを使用することはできますが、この後に示す手順や図を参照するときに、これらの変更に注意してください。 最新の既定のポリシーに合わせて既定のポリシーを変更する場合は、「[Azure Information Protection の既定のポリシー](../deploy-use/configure-policy-default.md)」を参照してください。

    - 既定の構成では、一部のラベルには視覚的なマーキング (フッター、ヘッダー、透かしなど) が構成されており、どのラベルにも保護が設定されていないことに注意してください。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー](../media/info-protect-policy-default-labelsv2.png)
    
    また、設定されていないポリシー設定がいくつかあります。 たとえば、すべてのドキュメントと電子メールはラベルが必須ではなく、既定のラベルはなく、ユーザーがラベルを変更するときに理由を示す必要はありません。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-settings-for-a-default-label-and-prompt-for-justification"></a>既定のラベルと理由を求めるプロンプトの設定の変更

このチュートリアルでは 2 つのポリシーの設定を変更し、どのように動作するかを確認します。

1. **[既定のラベルを選択]** で、これを **[全般]** に設定します。 

    以前のバージョンのポリシーを使用しているために、このラベルがない場合は、同等のラベルとして **[内部]** を選択します。

2. **[Users must provide justification to set a lower classification label, remove a label, or remove protection]** (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります) で、これを**[On]** (オン) に設定します。

## <a name="configuring-a-label-for-protection-a-watermark-and-a-condition-to-prompt-for-classification"></a>分類に関する保護ラベル、透かし、およびプロンプトを出す条件の構成

メイン ラベル **[社外秘]** から、サブラベルの 1 つである **[すべての従業員]** の設定を変更します。 

以前のバージョンのポリシーを使用しているために、**[社外秘]** ラベルにサブラベルがない場合は、代わりに **[社外秘]** ラベルを使用できます。 構成手順は同じですが、ラベルのブレードの名前が **[すべての従業員]** ではなく、**[社外秘]** になります。

1. **[社外秘]** ラベルが展開されることを確認し、そのラベルから **[すべての従業員]** を選択します。
    
    これで、新しい **[ラベル: すべての従業員]** ブレードに、各ラベルで使用できる設定が表示されます。 

2. このラベルの **[説明]** のテキストを読みます。 これは、選択したラベルがどのような使用目的であるかを示しており、ユーザーに対してはツールヒントとして表示され、ユーザーがどのラベルを選択するかを決定するのに役立ちます。

3. **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** セクションを見つけて、**[保護]** を選択します。
    
    ![Azure Information Protection ラベルの保護を構成する](../media/info-protect-protection-barv2.png) 
    
    この操作により、**[保護]** ブレードが開きます。
    
3. **[保護]** ブレードで、**[Azure RMS]** が選択され、**[定義済みのテンプレートを選択する]** も選択されていることを確認します。 次に、ドリルダウン ボックスをクリックし、組織内のすべてのユーザーが保護されているコンテンツを表示および編集できる既定のテンプレートを選択します。 
    
    最近サブスクリプションを取得した場合、このテンプレートは **[社外秘 \ すべての従業員]** という名前です。 
    
    しばらくサブスクリプションを使用している場合、既定のテンプレートは **[\<組織名> - 社外秘]** という名前である可能性があります。 たとえば、組織名が VanArsdel, Ltd の場合は、**[VanArsdel, Ltd - Confidential]** (VanArsdel, Ltd - 機密) を選択します。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - Azure RMS 保護を設定する](../media/step2-select-rms-template.png)
    
    この既定の Azure Rights Management テンプレートを無効にしてある場合は、代わりのテンプレートを選択します。 ただし、部門テンプレートを選択する場合は、アカウントがスコープに含まれることを確認します。
    
4. **[OK]** をクリックして変更を保存すると **[保護]** ブレードが閉じます。 **[ラベル: すべての従業員]** ブレードに反映された構成が表示されます。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 構成済みの Azure RMS の保護](../media/protection-bar-configured.png)
    
5. **[ラベル: すべての従業員]** ブレードで、**[視覚的なマーキングの設定]**  セクションを見つけます。
    
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
    
    **[保存]** をクリックして、**[ラベル: すべての従業員]** ブレードに戻ります。

7. **[ラベル: すべての従業員]** ブレードでは、以下のように、**[条件名]** に **[クレジット カード番号]** と表示され、**[出現回数]** に **1** が設定されています。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - クレジット カードの条件を構成する](../media/step2-see-condition.png)

8. **[Select how this label is applied]** (このラベルの適用方法を選択) は既定値の **[推奨]** のままにしておきます。既定のポリシー ヒントは変更しないでください。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - [Recommended] (推奨) 分類](../media/step2-keep-recommendedv2.png)

9. **[Enter notes for internal housekeeping]** (内部ハウスキーピング処理向けのメモを入力) ボックスに、「**For testing purposes only**」 (テスト用のみ) と入力します。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - メモを入力する](../media/step2-type-notes.png)

10. この **[ラベル: すべての従業員]** ブレードで、**[保存]** をクリックします。 次に、**[Policy: Global]**(ポリシー: グローバル) ブレードで **[保存]** を再度クリックします。
    
    この時点で、ラベルには、構成したラベルの Azure RMS 保護が表示されます。

    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー構成済み](../media/info-protect-policy-configuredv2.png)
    
    設定は、既定のラベルと妥当性の変更内容に従って構成されます。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 設定構成済み](../media/info-protect-settings-configuredv2.png)
    
11. 変更を行って保存したので、ユーザーがそれを使用できるようにします。そのためには、最初の **[Azure Information Protection]** ブレードで、**[公開]** をクリックし、**[はい]** をクリックして確定します。

    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 構成済みポリシーの公開](../media/info-protect-publish.png)

Azure Portal を閉じても、開いたままにしておきこのチュートリアルが終わった後でさらにオプションを構成してみてもかまいません。

既定のポリシーの確認と変更が済んだので、次の手順では Azure Information Protection をインストールします。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|ポリシーの構成オプションについて|[Azure Information Protection ポリシーの構成](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; 手順 1](infoprotect-tutorial-step1.md)
[手順 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]