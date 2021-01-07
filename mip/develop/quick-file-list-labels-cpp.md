---
title: クイック スタート - C++ MIP SDK を使用した Microsoft Information Protection (MIP) テナントの機密ラベルの列挙
description: Microsoft Information Protection C++ SDK を使用して、テナントの機密ラベルを列挙する方法を説明するクイック スタート。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 14b36ecee7fc49c5b50d627e6ef1ab95d436d7ee
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865265"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>クイック スタート:機密ラベルの一覧表示 (C++)

このクイック スタートでは、MIP ファイル API を使用して、ご自分の組織用に構成された機密ラベルを列挙する方法を示します。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: クライアント アプリケーションの初期化 (C++)](quick-app-initialization-cpp.md)」をまず完了し、スターター Visual Studio ソリューションを構築します。 この「機密ラベルの列挙」のクイック スタートでは、前のクイック スタートでスターター ソリューションが正しく構築されている必要があります。
- 省略可能: [分類ラベル](concept-classification-labels.md)の概念を確認します。

## <a name="add-logic-to-list-the-sensitivity-labels"></a>機密ラベルを列挙するためのロジックの追加

ファイル エンジン オブジェクトを使用して、組織の機密ラベルを列挙するロジックを追加します。

1. 前の「クイック スタート: クライアント アプリケーションの初期化 (C++)」の記事で作成した、Visual Studio ソリューションを開きます。

2. **ソリューション エクスプローラー** を使用して、`main()` メソッドの実装を含む .cpp ファイルをプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. 次の `using` ディレクティブをファイル上部の `using mip::FileEngine;` の後に追加します。

   ```cpp
   using std::endl;
   ```

4. `main()` 本文の末尾の最後の `catch` ブロックの閉じかっこ `}` の下の `return 0;` の上に (前のクイック スタートが終わった場所)、次のコードを挿入します。

   ```cpp
   // List sensitivity labels
   cout << "\nSensitivity labels for your organization:\n";
   auto labels = engine->ListSensitivityLabels();
   for (const auto& label : labels)
   {
      cout << label->GetName() << " : " << label->GetId() << endl;

      for (const auto& child : label->GetChildren())
      {
        cout << "->  " << child->GetName() << " : " << child->GetId() << endl;
      }
   }
   system("pause");
   ```

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>アクセス トークンを生成するための PowerShell スクリプトの作成

次の PowerShell スクリプトを使用すると、`AuthDelegateImpl::AcquireOAuth2Token` の実装に SDK によって求められているアクセス トークンを作成できます。 このスクリプトでは、「MIP SDK Setup and configuration」 (MIP SDK の設定と構成) で以前インストールした ADAL.PS モジュールの `Get-ADALToken` コマンドレットを使用しています。

1. PowerShell Script ファイル (.ps1 extension) を作成し、次のスクリプトをファイルにコピーして貼り付けます。

   - `$authority` と `$resourceUrl` は、後のセクションで更新します。
   - `$appId` と `$redirectUri` を Azure AD アプリ登録に指定した値と一致するように更新します。

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token()
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '0edbblll-8773-44de-b87c-b8c6276d41eb'  # App ID of the Azure AD app registration
   $redirectUri = 'bltest://authorize'              # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. クライアント アプリケーションで求められたら、後で実行できるようにスクリプト ファイルを保存します。

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

最後に、クライアント アプリケーションを構築してテストします。

1. F6 ( **[ソリューションのビルド]** ) を使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireOAuth2Token()` メソッドを呼び出すたびに、アプリケーションによりアクセス トークンが求められます。 複数回求められ、要求される値が同じ場合は、前に生成したトークンを再利用できます。

3. プロンプトのアクセス トークンを生成するには、PowerShell スクリプトに戻り、次を実行します。

   - `$authority` と `$resourceUrl` の変数を更新します。 これは、手順 2 番のコンソールの出力で指定した値と一致している必要があります。 これらの値は、MIP SDK の `AcquireOAuth2Token()` の `challenge` パラメーターによって提供されます。
   - PowerShell スクリプトを実行します。 `Get-ADALToken` コマンドレットにより、次の例と似た Azure AD 認証プロンプトがトリガーされます。 手順 2 番のコンソール出力と同じアカウントを指定します。 サインインに成功すると、アクセス トークンがクリップボードに配置されます。

     [![Visual Studio のトークンでのサインインの取得](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - サインイン アカウントで実行中に、アプリケーションが MIP API にアクセスできるようにするには、同意をする必要もあります。 これは、Azure AD のアプリケーションの登録が事前に同意されていないか (「MIP SDK setup and configuration」 (MIP SDK の設定と構成) で説明)、(アプリケーションが登録されている以外の) 別のテナントのアカウントを使用してサインインしている場合に発生します。 単純に **[承諾]** をクリックして、同意を記録します。

     [![Visual Studio での承諾](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. アクセス トークンを手順 2 番のプロンプトに貼り付けると、次の例のように、コンソール出力に機密ラベルが表示されます。

   ```console
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z

   Press any key to continue . . .
   ```

   > [!NOTE]
   > 次のクイック スタートで使用するので、(たとえば、`f42a3342-8706-4288-bd31-ebb85995028z` のように) 1 つ以上の機密ラベルの ID をコピーして保存します。

## <a name="troubleshooting"></a>トラブルシューティング
### <a name="problems-during-execution-of-c-application"></a>C++ アプリケーションの実行時の問題

| [概要] | エラー メッセージ | 解決策: |
|---------|---------------|----------|
| 不正なアクセス トークン | *例外が発生しました...正しくない/期限切れのアクセス トークンですか?<br><br>API 呼び出しが失敗しました: profile_add_engine_async が次により失敗しました: [class mip::PolicySyncException] ポリシーの取得に失敗しました。次の http 状態コードにより要求が失敗しました:401, x-ms-diagnostics: [2000001;reason="要求により送信された OAuth トークンを解析できません。";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) がコード 0 により終了しました。<br><br>このウィンドウを閉じるには、いずれかのキーを押してください . . .* | プロジェクトが正しく構成されているにもかかわらず、左と同様な出力がある場合、`AcquireOAuth2Token()` メソッドのトークンが不正であるか期限切れである可能性があります。 「[アクセス トークンを生成するための PowerShell スクリプトの作成](#create-a-powershell-script-to-generate-access-tokens)」に戻ってアクセス トークンを再生成し、`AcquireOAuth2Token()` をもう一度更新して、再構築/再テストを行います。 [jwt.ms](https://jwt.ms/) の 1 ページからなる Web アプリケーションを使用して、トークンとその要求を検証および確認することも可能です。 |
| 機密ラベルが構成されていない | 該当なし | プロジェクトが正常に構築されたにもかかわらず、コンソール ウィンドウに出力がない場合、組織の機密ラベルの構成が正しいことを確認します。 詳細については、「Define label taxonomy and protection settings」 (ラベルの分類と保護設定の定義) の「[MIP SDK setup and configuration](setup-configure-mip.md)」 (MIP SDK の設定と構成) を参照してください。  |

## <a name="next-steps"></a>次のステップ

これで組織の機密ラベルを列挙する方法を学習したので、次のクイック スタートを試してください。

> [!div class="nextstepaction"]
> [機密ラベルの設定と取得](quick-file-set-get-label-cpp.md)
