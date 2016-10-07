---
title: "クイック スタート チュートリアル手順 3 | Azure Information Protection"
description: "約 30 分で組織の Microsoft Azure Information Protection を簡単に試すことができる概要チュートリアルの手順 3 です。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: b5c87669c965d1e67b47dcfbd8ba97f1da41d104
ms.openlocfilehash: 042e168452d2b5cbc1eeec4fc06a3b0f137a5caf


---

# 手順 3: クライアントとアプリケーションをインストールする 

>*適用対象: Azure Information Protection*

この手順では、まず、Azure Information Protection クライアントをインストールし、構成したポリシーが Windows PC にダウンロードされて、Office アプリケーションにラベルが表示されるようにします。

次に、Rights Management 共有アプリケーションをインストールし、電子メールでドキュメントを安全に共有して、その使用方法を追跡できるようにします。 

これらのインストールは両方とも Office アプリケーションと統合されます。現時点では、これらを個別にインストールする必要があります。


## Azure Information Protection クライアントのインストール

1. Office がインストールされている PC で (ただし、Word は現在開かれていません)、Microsoft ダウンロード センターから [Azure Information Protection クライアントをダウンロード](https://www.microsoft.com/en-us/download/details.aspx?id=53018)します。 

2. **AzInfoProtection.exe** を実行し、指示に従ってクライアントをインストールします。

    このチュートリアルでは、デモ ポリシーをインストールするオプションを選択するかどうかは関係ありません。デモ ポリシーをインストールしても、先に構成したポリシーが Azure からダウンロードされてデモ ポリシーを置き換えます。 ただし、Azure Information Protection に接続しないで既定のラベルを試したいだけの場合は、デモ ポリシー オプションを使用してもかまいません。 

## Rights Management 共有アプリケーションのインストール 

1. Microsoft Web サイトの [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) ページに移動します。

2. [ **コンピューター** ] セクションで、 **Windows 用 RMS アプリケーション** のアイコンをクリックして、Microsoft Rights Management 共有アプリケーションをインストールする **Setup.exe** ファイルを保存します。

3. [ **Microsoft RMS のセットアップ** ] ページで、[ **次へ**] をクリックし、インストールが完了するまで待機します。 その後、コンピューターの再起動を求められた場合は **[再起動]** をクリックします。インストールを完了する場合は、**[閉じる]** をクリックします。


## インストールを確認する

Word で新しい空白の文書を開き、これらのインストールが正常に行われたことを確認します (この時点では文書を保存しないでください)。 ユーザー名とパスワードの入力を求められたら、グローバル管理者アカウントの詳細を入力します。 

文書が読み込まれると、3 つの新機能が表示されます。

- **[ホーム]** タブの新しい **[Protection]** (保護) グループと **[Protect]** (保護) ボタン。

    **[Protect]** (保護)、 > **[Help and feedback]** (ヘルプとフィードバック) の順にクリックし、**[Microsoft Azure Information Protection]** ダイアログ ボックスでクライアントのステータスを確認します。 **[Information Protection policy is installed]** (Information Protection ポリシーはインストールされています) というメッセージと最新の接続時刻が表示されます。 表示されているユーザー名がテナントの正しいものであることを確認します。

- **[ホーム]** タブの新しい **[RMS]** グループと **[保護ファイルの共有]** というラベルが付いたボタン。

- リボンの下の新しい Information Protection バー。 **[Sensitivity]** (秘密度) というタイトルと、構成した既定のラベル **[Internal]** (内部) が表示されます。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - クライアント インストール済み](../media/word2013-callouts2.png)

これで、Azure Information Protection の動作を確認する準備ができました。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|Azure Information Protection クライアントのインストールについて|[Azure Information Protection クライアントのインストール](../rms-client/info-protect-client.md)|
|Rights Management 共有アプリケーションのインストールとユーザーの手順について|[Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)|
|Windows 用 Rights Management 共有アプリケーションのスクリプト化したインストールと技術情報の詳細について|[Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; 手順 2](infoprotect-tutorial-step2.md)
[手順 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Sep16_HO4-->


