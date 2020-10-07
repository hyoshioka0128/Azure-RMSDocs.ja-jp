---
title: クイック スタート - MIP SDK C# ラッパーを利用し、Microsoft Information Protection (MIP) テナントの認証ユーザーが利用できる保護テンプレートを一覧表示する
description: Microsoft Information Protection SDK 保護 API C# ラッパーを使用し、ユーザーが利用できる保護テンプレートを一覧表示する方法について説明するクイック スタート。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.custom: has-adal-ref
ms.openlocfilehash: 7b9a8d916b0c3c4b8aaa006abdf27cd8c02a7f6e
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91588259"
---
# <a name="quickstart-list-templates-c"></a>クイック スタート:テンプレートを一覧表示する (C#)

このクイック スタートでは、MIP SDK 保護 API を使用し、ユーザーが利用できる保護テンプレートを一覧表示する方法を紹介します。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: クライアント アプリケーションの初期化 - Protection API (C#)](quick-protection-app-initialization-csharp.md)」をまず完了し、スターター Visual Studio ソリューションを構築します。 この「保護テンプレートを一覧表示する」クイック スタートでは、前のクイック スタートでスターター ソリューションが正しく構築されている必要があります。
- 省略可能: 「[RMS テンプレート](/azure/information-protection/configure-policy-templates)」概念を確認します。

## <a name="add-logic-to-list-the-protection-templates"></a>保護テンプレートを一覧表示するロジックを追加する

保護エンジン オブジェクトを使用し、ユーザーが利用できる保護テンプレートを一覧表示するロジックを追加します。

1. 前の「クイック スタート - クライアント アプリケーション初期化 - 保護 API (C#)」の記事で作成した Visual Studio ソリューションを開きます。

2. **ソリューション エクスプローラー**を使用して、`Main()` メソッドの実装を含む .cs ファイルをプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. `Main()` 本文の末尾の、`Main()` 関数のアプリケーション シャットダウンのセクションの上 (前のクイック スタートが終わった場所) に、次のコードを挿入します。

  ```csharp
  // List protection templates using protectionEngine and display the list

  var templates=protectionEngine.GetTemplates();

  for(int i = 0; i < templates.Count; i++)
  {
      Console.WriteLine("{0}: {1}", i.ToString(), templates[i].Name + " : " + templates[i].Id);
  }

  Console.WriteLine("Press a key to continue...");
  ```

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

最後に、クライアント アプリケーションを構築してテストします。

1. Ctrl + Shift + B ( **[ソリューションのビルド]** ) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireToken()` メソッドを呼び出すたびに、アプリケーションから ADAL を使用した認証が求められる*場合があります*。 キャッシュされた資格情報が既に存在する場合は、サインインを求められることはなく、ラベルの一覧が表示されます。

     [![Visual Studio のトークンでのサインインの取得](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - サインイン アカウントで実行中に、アプリケーションが MIP API にアクセスできるようにするには、同意をする必要もあります。 これは、Azure AD のアプリケーションの登録が事前に同意されていないか (「MIP SDK setup and configuration」 (MIP SDK の設定と構成) で説明)、(アプリケーションが登録されている以外の) 別のテナントのアカウントを使用してサインインしている場合に発生します。 単純に **[承諾]** をクリックして、同意を記録します。

     [![Visual Studio での承諾](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. 認証後、次の例のように、認証ユーザーの保護テンプレートがコンソールに出力されます。

  ```console
  0: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
  1: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
  2: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
  3: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
  Press a key to continue.
  ```

   > [!NOTE]
   > 次のクイック スタートで使用するので、(たとえば、`bb7ed207-046a-4caf-9826-647cff56b990` のように) 1 つ以上の保護テンプレートの ID をコピーして保存します。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="problems-during-execution-of-c-application"></a>C# アプリケーションの実行時の問題

| [概要] | エラー メッセージ | 解決策: |
|---------|---------------|----------|
| 不正なアクセス トークン | *例外が発生しました...正しくない/期限切れのアクセス トークンですか?<br><br>API 呼び出しが失敗しました: profile_add_engine_async が次により失敗しました: [class mip::PolicySyncException] ポリシーの取得に失敗しました。次の http 状態コードにより要求が失敗しました:401, x-ms-diagnostics: [2000001;reason="要求により送信された OAuth トークンを解析できません。";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) がコード 0 により終了しました。<br><br>このウィンドウを閉じるには、いずれかのキーを押してください . . .* | プロジェクトが正しく構成されているにもかかわらず、左と同様な出力がある場合、`AcquireOAuth2Token()` メソッドのトークンが不正であるか期限切れである可能性があります。 「[アプリケーションの構築とテスト](#build-and-test-the-application)」に戻り、アクセス トークンを再生成し、`AcquireOAuth2Token()` を再度更新して、再構築/再テストを行います。 [jwt.ms](https://jwt.ms/) の 1 ページからなる Web アプリケーションを使用して、トークンとその要求を検証および確認することも可能です。 |

## <a name="next-steps"></a>次のステップ

認証ユーザーが利用できる保護テンプレートを一覧表示する方法を覚えたところで、次のクイック スタートをお試しください。

> [!div class="nextstepaction"]
> [クイック スタート - テキストの暗号化と暗号化解除](quick-protection-encrypt-decrypt-text-csharp.md)