---
title: クイック スタート チュートリアルの手順 3 - AIP
description: Azure Information Protection を簡単に試すためのチュートリアルの手順 3 - クライアントのインストール。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/28/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
ms.openlocfilehash: 203964dfb153b45c515fa93c8cb6b69ebe3fbd37
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2018
ms.locfileid: "44151641"
---
# <a name="step-3-install-the-client"></a>手順 3: クライアントのインストール

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

この手順では、Azure Information Protection クライアントをインストールし、構成したポリシーが Windows PC にダウンロードされて、Office アプリケーションにラベルが表示されるようにします。


## <a name="install-the-azure-information-protection-client"></a>Azure Information Protection クライアントのインストール

1. Office がインストールされていて、Word は開いていない状態の PC で、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)にアクセスし、**AzInfoProtection.exe** をダウンロードします。
    
2. ダウンロードした実行可能ファイルを実行し、指示に従ってクライアントをインストールします。
    
    このチュートリアルでは、デモ ポリシーをインストールするオプションを選択するかどうかは関係ありません。デモ ポリシーをインストールしても、先に構成したポリシーが Azure からダウンロードされてデモ ポリシーを置き換えます。 ただし、Azure Information Protection に接続しないで既定のラベルを試したいだけの場合は、デモ ポリシー オプションを使用してもかまいません。 

## <a name="verify-the-installation"></a>インストールの確認

Word で新しい空白の文書を開き、インストールが正常に行われたことを確認します (この時点では文書を保存しないでください)。 ユーザー名とパスワードの入力を求められたら、グローバル管理者アカウントの詳細を入力します。 

クライアントをインストールしたのが今回が初めての場合は、**[完了しました]** というページ表示され、基本的な手順が示されます。 それを読み終えたら、**[閉じる]** をクリックします。

ドキュメントが読み込まれると、2 つの新機能が表示されます。

![Azure Information Protection クイック スタート チュートリアル手順 3 - クライアント インストール済み](./media/word2016-calloutsv2.png)

- **[ホーム]** タブの新しい **[保護]** グループと **[保護]** ボタン。
    
    **[保護]** > **[ヘルプとフィードバック]** の順にクリックして、**[Microsoft Azure Information Protection]** ダイアログ ボックスでクライアントのステータスを確認します。 **[接続ユーザー]** とユーザー名が表示されているはずです。 さらに、最終接続日時と Information Protection ポリシーのインストール日時も表示されているはずです。 表示されているユーザー名がテナントの正しいものであることを確認します。

- リボンの下の新しい Information Protection バー。 **[秘密度]** というタイトルと、Azure Portal で確認したラベルが表示されます。 

これで、Azure Information Protection の動作を確認する準備ができました。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|Azure Information Protection クライアントのインストールについて|[Azure Information Protection クライアントをダウンロードしてインストールする](./rms-client/install-client-app.md)|
|Azure Information Protection クライアントの管理者向けの手順|[Azure Information Protection クライアント管理者ガイド](./rms-client/client-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; 手順 2](infoprotect-tutorial-step2.md)
[手順 4 &#187;](infoprotect-tutorial-step4.md)
