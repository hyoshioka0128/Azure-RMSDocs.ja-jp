---
title: クイック スタート - MIP SDK C# ラッパーを使用した Microsoft Information Protection (MIP) テナントの機密ラベルの列挙
description: Microsoft Information Protection SDK C# ラッパーを使用して、テナントの秘密度ラベルを列挙する方法 (C#) を説明するクイック スタート。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 607e721ad941901b83e37de7e20949da2a9ab936
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535945"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>クイック スタート:機密ラベルの一覧表示 (C#)

このクイック スタートでは、MIP SDK ファイル API を使用して、ご自分の組織用に構成された機密ラベルを列挙する方法を示します。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: クライアント アプリケーションの初期化 (C#)](quick-app-initialization-csharp.md)」をまず完了し、スターター Visual Studio ソリューションを構築します。 この「機密ラベルの列挙」のクイック スタートでは、前のクイック スタートでスターター ソリューションが正しく構築されている必要があります。
- 省略可能: [分類ラベル](concept-classification-labels.md)の概念を確認します。

## <a name="add-logic-to-list-the-sensitivity-labels"></a>機密ラベルを列挙するためのロジックの追加

ファイル エンジン オブジェクトを使用して、組織の機密ラベルを列挙するロジックを追加します。

1. 前の「クイック スタート: クライアント アプリケーションの初期化 (C#)」の記事で作成した、Visual Studio ソリューションを開きます。

2. **ソリューション エクスプローラー** を使用して、`Main()` メソッドの実装を含む .cs ファイルをプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. `Main()` 本文の末尾の、`Main()` 関数のアプリケーション シャットダウンのセクションの上 (前のクイック スタートが終わった場所) に、次のコードを挿入します。

  ```csharp
  // List sensitivity labels from fileEngine and display name and id
  foreach(var label in fileEngine.SensitivityLabels)
  {
      Console.WriteLine(string.Format("{0} : {1}", label.Name, label.Id));

      if (label.Children.Count != 0)
      {
          foreach (var child in label.Children)
          {
              Console.WriteLine(string.Format("{0}{1} : {2}", "\t",child.Name, child.Id));
          }
      }
  }
  ```

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

最後に、クライアント アプリケーションを構築してテストします。

1. Ctrl + Shift + B ( **[ソリューションのビルド]** ) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireToken()` メソッドを呼び出すたびに、アプリケーションから ADAL を使用した認証が求められる *場合があります*。 キャッシュされた資格情報が既に存在する場合は、サインインを求められることはなく、ラベルの一覧が表示されます。

     [![Visual Studio のトークンでのサインインの取得](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - サインイン アカウントで実行中に、アプリケーションが MIP API にアクセスできるようにするには、同意をする必要もあります。 これは、Azure AD のアプリケーションの登録が事前に同意されていないか (「MIP SDK setup and configuration」 (MIP SDK の設定と構成) で説明)、(アプリケーションが登録されている以外の) 別のテナントのアカウントを使用してサインインしている場合に発生します。 単純に **[承諾]** をクリックして、同意を記録します。

     [![Visual Studio での承諾](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. 認証後、次の例のように、コンソールに機密ラベルが出力されます。

  ```console
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.
  ```

   > [!NOTE]
   > 次のクイック スタートで使用するので、(たとえば、`f42a3342-8706-4288-bd31-ebb85995028z` のように) 1 つ以上の機密ラベルの ID をコピーして保存します。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="problems-during-execution-of-c-application"></a>C# アプリケーションの実行時の問題

| [概要] | エラー メッセージ | 解決策: |
|---------|---------------|----------|
| 不正なアクセス トークン | *例外が発生しました...正しくない/期限切れのアクセス トークンですか?<br><br>API 呼び出しが失敗しました: profile_add_engine_async が次により失敗しました: [class mip::PolicySyncException] ポリシーの取得に失敗しました。次の http 状態コードにより要求が失敗しました:401, x-ms-diagnostics: [2000001;reason="要求により送信された OAuth トークンを解析できません。";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) がコード 0 により終了しました。<br><br>このウィンドウを閉じるには、いずれかのキーを押してください . . .* | プロジェクトが正しく構成されているにもかかわらず、左と同様な出力がある場合、`AcquireOAuth2Token()` メソッドのトークンが不正であるか期限切れである可能性があります。 「[アプリケーションの構築とテスト](#build-and-test-the-application)」に戻り、アクセス トークンを再生成し、`AcquireOAuth2Token()` を再度更新して、再構築/再テストを行います。 [jwt.ms](https://jwt.ms/) の 1 ページからなる Web アプリケーションを使用して、トークンとその要求を検証および確認することも可能です。 |
| 機密ラベルが構成されていない | 該当なし | プロジェクトが正常に構築されたにもかかわらず、コンソール ウィンドウに出力がない場合、組織の機密ラベルの構成が正しいことを確認します。 詳細については、「Define label taxonomy and protection settings」 (ラベルの分類と保護設定の定義) の「[MIP SDK setup and configuration](setup-configure-mip.md)」 (MIP SDK の設定と構成) を参照してください。  |

## <a name="next-steps"></a>次のステップ

これで組織の機密ラベルを列挙する方法を学習したので、次のクイック スタートを試してください。

> [!div class="nextstepaction"]
> [機密ラベルの設定と取得](quick-file-set-get-label-csharp.md)
