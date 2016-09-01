---
title: "Azure Information Protection クイック スタート チュートリアル手順 4 | Azure Rights Management"
description: "4 つの手順を実行して 15 分もかからずに組織の Microsoft Azure Information Protection を簡単に試すことができる概要チュートリアルの手順 4 です。"
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: d17bacf8e148622db0e2393f40d3fd37c8f086eb
ms.openlocfilehash: a36433167462275e91059f9eb3a2141ffa2797d5


---

# 手順 4: 分類、ラベル付け、保護の動作を確認する 

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

Azure Information Protection クライアントをインストールして Word 文書を開いたので、構成したポリシーを使用して簡単に文書のラベル付けと保護を始められることを確認できます。

文書を保存すると分類と保護が行われますが、その前に、未保存の文書を使用して簡単にラベルを適用および変更できることを見てみます。

### 既定のラベルを手動で変更するには:

- Information Protection バーで **[Personal]** (個人) を選択すると、分類レベルを下げる理由の入力を求められます。 **[This file no longer requires that classification]** (このファイルをこの分類にする必要がなくなりました) を選択し、**[Confirm]** (確認) をクリックします。  

    **[Sensitivity]** (秘密度) の値が **[Personal]** (個人) に変わります。

    ![Azure Information Protection クイック スタート チュートリアル手順 4 - レベルを下げる理由の確認要求](../media/confirm-lowering.png)

### 分類を完全に削除するには:

- Information Protection バーで、**[Personal]** (個人) の横にある **[Edit label]** (ラベルの編集) アイコンをクリックします。 使用できるラベルが表示されます。 今度は、いずれかのラベルを選択するのではなく、**[Remove label]** (ラベルの削除) アイコンをクリックします。 **[OK]** をクリックして確認し、このアクションの理由を入力します。  

    **[Sensitivity]** (秘密度) の値が **[Not set]** (非設定) に変わります。既定のラベルが設定されていない場合も、最初はこのように表示されます。

    ![Azure Information Protection クイック スタート チュートリアル手順 4 - 分類の削除](../media/sensitivity-not-set.png)


### ラベル付けの推奨プロンプトと自動保護を確認するには:

1. Word 文書で、有効なクレジット カード番号 (例: **4242-4242-4242-4242**) を入力します。 

2. 文書を保存します (ファイル名と場所は任意)。 

3. **[It is recommended to label this file as Confidential]** (このファイルには機密というラベルを付けることが推奨されます) というプロンプトが表示されます。 **[Change now]** (今すぐ変更) をクリックします。

    ![Azure Information Protection クイック スタート チュートリアル手順 4 - 推奨プロンプト](../media/change-now.png)

    すぐに、組織名の透かしと、**[Sensitivity: Confidential]** (秘密度: 機密) というフッターがページに表示されます。 

    RMS テンプレートを適用するオプションを選択すると、文書は指定した Azure Rights Management テンプレートによっても保護されます。これは、**[ファイル]** タブをクリックして **[文書の保護]** の情報を見ることで確認できます。 既定の機密テンプレートを使用した場合は、文書が内部ユーザーに制限され (組織外のユーザーは文書を開けません)、内容をコピーまたは印刷できないという情報が表示されます。 文書の所有者は文書をコピーおよび印刷できますが、組織内の別のユーザーに文書をメール送信した場合、受信者はこれらの操作を実行できません。

> [!NOTE]
>以上の手順の実行で問題がある場合は、**[ホーム]** タブの **[Protection]** (保護) グループの **[Protect]** (保護) をクリックし、**[Help and feedback]** (ヘルプとフィードバック) をクリックします。 
>
>**[Microsoft Azure Information Protection]** ダイアログ ボックスで、**[フィードバックの送信]** をクリックします。 これにより、Information Protection チームに電子メールが送信され、問題の診断に役立つ PC のログ ファイルが自動的に添付されます。

##  次のステップ

既定の Azure Information Protection ポリシーとそのカスタマイズ方法、および Word 文書でのラベル付けの動作を確認したので、他の設定を試し、Azure Information Protection をサポートする他の Office アプリケーション (Excel、PowerPoint、Outlook) での動作を確認してください。 Azure Information Protection クライアントをインストールしたときにこれらのアプリケーションが開かれていた場合は、いったん閉じて開き直してから、Azure Information Protection で使用してみてください。

たとえば、Information Protection バーの既定のタイトル **[Sensitivity]** (秘密度) を別のタイトルに変更できます。 ツール ヒント、ラベルの色、ラベルの順序、ラベルの名前を変更できます。 新しいラベルを作成し、独自の自動規則を定義できます。 サイズと色を構成したり、方向を斜めから水平に変更したりして、透かしを微調整できます。

Excel で透かしを使用する場合は、ページ レイアウト モードと印刷プレビュー モードおよび印刷時にのみ表示されることに注意してください。

Azure ポータルで Information Protection ポリシーの設定を変更するたびに、忘れずにポリシーを**保存**し、**公開**してください。 複数のブレードで変更を行うことができるので、すべてのブレードで **[Save]** (保存) ボタンが有効になっていないことを確認するのがよい方法です。有効になっていると、変更が保存されていないことを示します。 新しい変更を公開したときに Office アプリケーションが開かれていた場合は、アプリケーションを閉じて開きなおすと最新のポリシーがダウンロードされます。

独自のテストが完了した後は、必要に応じて [Azure Information Protection のよく寄せられる質問](faq.md)を参照してください。




<!--HONumber=Aug16_HO2-->


