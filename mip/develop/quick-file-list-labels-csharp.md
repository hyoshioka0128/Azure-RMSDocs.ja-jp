---
title: MIP SDK を使用して Microsoft Information Protection (MIP) テナントに機密ラベルのリストのクイック スタート -C#ラッパー
description: Microsoft の Information Protection SDK を使用する方法を示すクイック スタートC#ラッパーをテナント内の機密ラベルを一覧表示します。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: mbaldwin
ms.openlocfilehash: 0b1b110fe3b2e96c258c7b94a3d356b9404d6e7e
ms.sourcegitcommit: 1d444b17e3d096f3e867e0240182ae3143fc1b71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59892410"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>クイック スタート: 機密ラベルの一覧表示 (C#)

このクイック スタートでは、MIP SDK のファイル API を使用して、組織用に構成された機密ラベルを一覧表示する方法を示しています。

## <a name="prerequisites"></a>前提条件

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 完全な[クイック スタート。クライアント アプリケーションの初期化 (C#)](quick-app-initialization-csharp.md) 1 つは、starter Visual Studio ソリューションをビルドします。 この「機密ラベルの列挙」のクイック スタートでは、前のクイック スタートでスターター ソリューションが正しく構築されている必要があります。
- 必要に応じて、次の操作を行います。レビュー[分類ラベル](concept-classification-labels.md)概念です。

## <a name="add-logic-to-list-the-sensitivity-labels"></a>機密ラベルを列挙するためのロジックの追加

ファイル エンジン オブジェクトを使用して、組織の機密ラベルを列挙するロジックを追加します。 

1. 以前で作成した Visual Studio ソリューションを開く"クイック スタート。クライアント アプリケーションの初期化 (C#)"記事。

2. 使用して**ソリューション エクスプ ローラー**の実装を含むプロジェクトの .cs ファイルを開き、`Main()`メソッド。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。 

3. 末尾に向かって、`Main()`右中かっこの下の本文`}`の`Main()`関数 (中断したところから前のクイック スタートでは)、次のコード挿入します。

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

1. CTRL + SHIFT+B を使用して (**ソリューションのビルド**) クライアント アプリケーションをビルドします。 ビルド エラーがない場合、F5 (**[デバッグ開始]**) を使用してアプリケーションを実行します。

2. プロジェクトがビルドされ、アプリケーションで実行が成功したかどうかは*可能性があります*各 ADAL 経由での認証用プロンプトが SDK の呼び出しを時間、`AcquireToken()`メソッド。 キャッシュされた資格情報が既に存在する場合にログオンし、ラベルの一覧を表示する求めるはありません。 

     [![Visual Studio のトークンでのサインインの取得](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - サインイン アカウントで実行中に、アプリケーションが MIP API にアクセスできるようにするには、同意をする必要もあります。 これは、Azure AD のアプリケーションの登録が事前に同意されていないか (「MIP SDK setup and configuration」 (MIP SDK の設定と構成) で説明)、(アプリケーションが登録されている以外の) 別のテナントのアカウントを使用してサインインしている場合に発生します。 単純に **[承諾]** をクリックして、同意を記録します。

     [![Visual Studio での承諾](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. 認証後、コンソール出力次の例のような機密ラベルが表示されます。

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

### <a name="problems-during-execution-of-c-application"></a>実行中に問題C#アプリケーション

| まとめ | エラー メッセージ | ソリューション |
|---------|---------------|----------|
| 不正なアクセス トークン | *例外が発生しました.正しくない/有効期限切れ、アクセス トークンですか。<br><br>失敗の API 呼び出し: profile_add_engine_async に失敗しました: [クラス mip::PolicySyncException] ポリシーの取得に失敗しました、要求は http 状態コードで失敗しました。401、x: ms 診断: [2000001; 理由 =「、要求と共に送信される OAuth トークンを解析できません」;。error_category ="invalid_token"]、関連付け Id: [35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (プロセス 29924) は、コード 0 で終了しました<br>。<br>このウィンドウを閉じますすべてのキーを押します.* | プロジェクトが正しく構成されているにもかかわらず、左と同様な出力がある場合、`AcquireOAuth2Token()` メソッドのトークンが不正であるか期限切れである可能性があります。 戻り[のビルドし、アプリケーションをテスト](#build-and-test-the-application)アクセス トークン、更新プログラムを再生成と`AcquireOAuth2Token()`、もう一度と再構築/再テストします。 [jwt.ms](https://jwt.ms/) の 1 ページからなる Web アプリケーションを使用して、トークンとその要求を検証および確認することも可能です。 |
| 機密ラベルが構成されていない | n/a | プロジェクトが正常に構築されたにもかかわらず、コンソール ウィンドウに出力がない場合、組織の機密ラベルの構成が正しいことを確認します。 詳細については、「Define label taxonomy and protection settings」 (ラベルの分類と保護設定の定義) の「[MIP SDK setup and configuration](setup-configure-mip.md)」 (MIP SDK の設定と構成) を参照してください。  |

## <a name="next-steps"></a>次の手順

これで組織の機密ラベルを列挙する方法を学習したので、次のクイック スタートを試してください。

> [!div class="nextstepaction"]
> [機密ラベルの設定と取得](quick-file-set-get-label-csharp.md)
