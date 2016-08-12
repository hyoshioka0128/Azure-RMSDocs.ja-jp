---
title: "Azure Information Protection クイック スタート チュートリアル手順 3 | Azure Rights Management"
description: "4 つの手順を実行して 15 分もかからずに組織の Microsoft Azure Information Protection を簡単に試すことができる概要チュートリアルの手順 3 です。"
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: 264f2be6c62dc7fa670171493941332fe7ff20e5
ms.openlocfilehash: 42649148e58a8ea1baab6317d181c24e6a21d709


---

# 手順 3: Azure Information Protection クライアントをインストールする 

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

この手順では、Azure Information Protection クライアントをインストールし、構成したポリシーが Windows PC にダウンロードされて、Office アプリケーションにラベルが表示されるようにします。 

1. Office がインストールされている PC で (ただし、Word は現在開かれていません)、Microsoft ダウンロード センターから [Azure Information Protection クライアントをダウンロード](https://www.microsoft.com/en-us/download/details.aspx?id=53018)します。 

2. **AZInfoProtection.exe** を実行し、指示に従ってクライアントをインストールします。

    このチュートリアルでは、デモ ポリシーをインストールするオプションを選択するかどうかは関係ありません。デモ ポリシーをインストールしても、先に構成したポリシーが Azure からダウンロードされてデモ ポリシーを置き換えます。 ただし、Azure Information Protection に接続しないで既定のラベルを試したいだけの場合は、デモ ポリシー オプションを使用してもかまいません。 

3. Word を起動して新しい空白の文書を開き、クライアントがインストールされたことを確認します (今はまだ文書を保存しないでください)。 ユーザー名とパスワードの入力を求められたら、グローバル管理者アカウントの詳細を入力します。 ドキュメントが読み込まれると、2 つの新機能が表示されます。

    - **[ホーム]** タブの新しい **[Protection]** (保護) グループと **[Protect]** (保護) ボタン。

        **[Protect]** (保護)、 > **[Help and feedback]** (ヘルプとフィードバック) の順にクリックし、**[Microsoft Azure Information Protection]** ダイアログ ボックスでクライアントのステータスを確認します。 **[Information Protection policy is installed]** (Information Protection ポリシーはインストールされています) というメッセージと最新の接続時刻が表示されます。 表示されているユーザー名がテナントの正しいものであることを確認します。

    - リボンの下に新しい Information Protection バーが表示されます。 **[Sensitivity]** (秘密度) というタイトルと、構成した既定のラベル **[Internal]** (内部) が表示されます。 
    
        ![Azure Information Protection クイック スタート チュートリアル手順 3 - クライアント インストール済み](../media/word2013-callouts2.png)

最後の手順に進んで分類、ラベル付け、および保護の動作を確認できる状態になりました。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|クライアントのインストールについて|[Azure Information Protection クライアントのインストール](info-protect-client.md)|


>[!div class="step-by-step"]
[&#171; 手順 2](infoprotect-tutorial-step2.md)
[手順 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Aug16_HO2-->


