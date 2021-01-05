---
title: クイック スタート - C++ MIP SDK を利用し、Microsoft Information Protection (MIP) テナントの認証ユーザーが利用できる保護テンプレートを一覧表示する
description: Microsoft Information Protection C++ SDK 保護 API を使用し、ユーザーが利用できる保護テンプレートを一覧表示する方法 (C++) について説明するクイック スタート
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: v-anikep
ms.custom: has-adal-ref
ms.openlocfilehash: d319af8e65e2eae958ef215d30dfa84c09ae7145
ms.sourcegitcommit: 437057990372948c9435b620052a7398360264b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2020
ms.locfileid: "97701647"
---
# <a name="quickstart-list-protection-templates-c"></a>クイック スタート:保護テンプレートを一覧表示する (C++)

このクイック スタートでは、MIP 保護 API を使用し、ユーザーが利用できる保護テンプレートを一覧表示する方法を紹介します。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート - クライアント アプリケーション初期化 - 保護 API (C++)](quick-protection-app-initialization-cpp.md)」をまず完了し、スターター Visual Studio ソリューションを構築します。 この「保護テンプレートを一覧表示する」クイック スタートでは、前のクイック スタートでスターター ソリューションが正しく構築されている必要があります。
- 省略可能: 「[RMS テンプレート](/azure/information-protection/configure-policy-templates)」概念を確認します。

## <a name="add-logic-to-list-the-protection-templates"></a>保護テンプレートを一覧表示するロジックを追加する

保護エンジン オブジェクトを使用し、ユーザーが利用できる保護テンプレートを一覧表示するロジックを追加します。

1. 前の「クイック スタート - クライアント アプリケーション初期化 - 保護 API (C++)」の記事で作成した Visual Studio ソリューションを開きます。

2. **ソリューション エクスプローラー** を使用して、`main()` メソッドの実装を含む .cpp ファイルをプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. 次の `using` ディレクティブをファイル上部の `using mip::ProtectionEngine;` の後に追加します。

   ```cpp
   using std::endl;
   ```

4. `main()` 本文の末尾の最後の `catch` ブロックの閉じかっこ `}` の下の `return 0;` の上に (前のクイック スタートが終わった場所)、次のコードを挿入します。

   ```cpp
    // List protection templates
    const shared_ptr<ProtectionEngineObserver> engineObserver = std::make_shared<ProtectionEngineObserver>();
    // Create a context to pass to 'ProtectionEngine::GetTemplateListAsync'. That context will be forwarded to the
    // corresponding ProtectionEngine::Observer methods. In this case, we use promises/futures as a simple way to detect
    // the async operation completes synchronously.
    auto loadPromise = std::make_shared<std::promise<vector<shared_ptr<mip::TemplateDescriptor>>>>();
    std::future<vector<shared_ptr<mip::TemplateDescriptor>>> loadFuture = loadPromise->get_future();
    engine->GetTemplatesAsync(engineObserver, loadPromise);
    auto templates = loadFuture.get();

    cout << "**_ Template List: " << endl;

    for (const auto& protectionTemplate : templates) {
        cout << "Name: " << protectionTemplate->GetName() << " : " << protectionTemplate->GetId() << endl;
    }

   ```

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>アクセス トークンを生成するための PowerShell スクリプトの作成

次の PowerShell スクリプトを使用すると、`AuthDelegateImpl::AcquireOAuth2Token` の実装に SDK によって求められているアクセス トークンを作成できます。 このスクリプトでは、「MIP SDK Setup and configuration」 (MIP SDK の設定と構成) で以前インストールした ADAL.PS モジュールの `Get-ADALToken` コマンドレットを使用しています。

1. PowerShell Script ファイル (.ps1 extension) を作成し、次のスクリプトをファイルにコピーして貼り付けます。

   - `$authority` と `$resourceUrl` は、後のセクションで更新します。
   - `$appId` と `$redirectUri` を Azure AD アプリ登録に指定した値と一致するように更新します。

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token()
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '<app-ID>'                              # App ID of the Azure AD app registration
   $redirectUri = '<redirect-uri>'                  # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. クライアント アプリケーションで求められたら、後で実行できるようにスクリプト ファイルを保存します。

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

最後に、クライアント アプリケーションを構築してテストします。

1. Ctrl+Shift+b (*[ソリューションのビルド] **) キーを使用して、クライアント アプリケーションを構築します。ビルド エラーがない場合は、F5 (** [デバッグ開始]**) を使用してご自分のアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireOAuth2Token()` メソッドを呼び出すたびに、アプリケーションによりアクセス トークンが求められます。 複数回求められ、要求される値が同じ場合は、前に生成したトークンを再利用できます。

3. プロンプトのアクセス トークンを生成するには、PowerShell スクリプトに戻り、次を実行します。

   - `$authority` と `$resourceUrl` の変数を更新します。 これは、手順 2 番のコンソールの出力で指定した値と一致している必要があります。
   - PowerShell スクリプトを実行します。 `Get-ADALToken` コマンドレットにより、次の例と似た Azure AD 認証プロンプトがトリガーされます。 手順 2 番のコンソール出力と同じアカウントを指定します。 サインインに成功すると、アクセス トークンがクリップボードに配置されます。

     [![Visual Studio のトークンでのサインインの取得](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - サインイン アカウントで実行中に、アプリケーションが MIP API にアクセスできるようにするには、同意をする必要もあります。 これは、Azure AD のアプリケーションの登録が事前に同意されていないか (「MIP SDK setup and configuration」 (MIP SDK の設定と構成) で説明)、(アプリケーションが登録されている以外の) 別のテナントのアカウントを使用してサインインしている場合に発生します。 単純に **[承諾]** をクリックして、同意を記録します。

     [![Visual Studio での承諾](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. アクセス トークンを手順 2 番のプロンプトに貼り付けると、次の例のように、コンソール出力に保護テンプレートが表示されます。

   ```console
   **_ Template List:
   Name: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
   Name: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
   Name: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
   Name: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720

   C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
   To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.

   Press any key to continue . . .
   ```

   > [!NOTE]
   > 次のクイック スタートで使用するので、(たとえば、`f42a3342-8706-4288-bd31-ebb85995028z` のように) 1 つ以上の保護テンプレートの ID をコピーして保存します。

## <a name="troubleshooting"></a>トラブルシューティング
### <a name="problems-during-execution-of-c-application"></a>C++ アプリケーションの実行時の問題

| [概要] | エラー メッセージ | 解決策: |
|---------|---------------|----------|
| 不正なアクセス トークン | _例外が発生しました...正しくない/期限切れのアクセス トークンですか?<br><br>API 呼び出しが失敗しました: profile_add_engine_async が次により失敗しました: [class mip::PolicySyncException] ポリシーの取得に失敗しました。次の http 状態コードにより要求が失敗しました:401, x-ms-diagnostics: [2000001;reason="要求により送信された OAuth トークンを解析できません。";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) がコード 0 により終了しました。<br><br>このウィンドウを閉じるには、いずれかのキーを押してください . . .* | プロジェクトが正しく構成されているにもかかわらず、左と同様な出力がある場合、`AcquireOAuth2Token()` メソッドのトークンが不正であるか期限切れである可能性があります。 「[アクセス トークンを生成するための PowerShell スクリプトの作成](#create-a-powershell-script-to-generate-access-tokens)」に戻ってアクセス トークンを再生成し、`AcquireOAuth2Token()` をもう一度更新して、再構築/再テストを行います。 [jwt.ms](https://jwt.ms/) の 1 ページからなる Web アプリケーションを使用して、トークンとその要求を検証および確認することも可能です。 |

## <a name="next-steps"></a>次の手順

認証ユーザーが利用できる保護テンプレートを一覧表示する方法を覚えたところで、次のクイック スタートをお試しください。

> [!div class="nextstepaction"]
> [テキストの暗号化と暗号化解除](quick-protection-encrypt-decrypt text-cpp.md)