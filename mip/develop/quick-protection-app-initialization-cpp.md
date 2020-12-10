---
title: クイックスタート - 保護 API を使用した MIP SDK C++ クライアントの初期化
description: 保護 API を使用して Microsoft Information Protection (MIP) SDK クライアント アプリケーションの初期化ロジックを記述する方法 (C++) を示すクイック スタート
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 1dd25f0239d158c6c88b5b0c96d437fae38ff844
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535962"
---
# <a name="quickstart-client-application-initialization-for-protection-apis-c"></a>クイック スタート:保護 API のためのクライアント アプリケーション初期化 (C++)

このクイック スタートでは、実行時に MIP C++ SDK によって使用される、クライアントの初期化パターンを実装する方法を示します。

> [!NOTE]
> MIP 保護 API を使用する任意のクライアント アプリケーションには、このクイック スタートで概説されている手順が必要です。 これらのクイック スタートは、アプリケーションを初期化し、認証委任クラスと同意委任クラスを実装した直後に順次行ってください。

## <a name="prerequisites"></a>[前提条件]

まだ完了していない場合は、必ず次の操作を行ってください。

- 「[Microsoft Information Protection (MIP) SDK setup and configuration](setup-configure-mip.md)」 (Microsoft Information Protection (MIP) SDK のセットアップと構成) の手順を完了します。 この "クライアント アプリケーションの初期化" クイック スタートは、適切な SDK のセットアップと構成に依存します。
- 省略可能:
  - [プロファイル オブジェクトとエンジン オブジェクト](concept-profile-engine-cpp.md)を確認します。 プロファイル オブジェクトとエンジン オブジェクトは、MIP ファイル/ポリシー/保護 API を使用するクライアントによって必要とされる、ユニバーサルな概念です。
  - [認証の概念](concept-authentication-cpp.md)を確認して、認証と同意が SDK とクライアント アプリケーションによってどのように実装されるかについて学習します。
  - [オブザーバーの概念](concept-async-observers.md)を確認して、オブザーバーの詳細および実装方法について学習します。 MIP SDK では、非同期イベントの通知を実装するために、オブザーバー パターンを使用します。

## <a name="create-a-visual-studio-solution-and-project"></a>Visual Studio のソリューションとプロジェクトの作成

まず、その他のクイック スタートをビルドする対象の初期の Visual Studio ソリューションを作成して構成します。

1. Visual Studio 2017 を開いて、 **[ファイル]** メニュー、 **[新規]** 、 **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログで次の操作を行います。
   - 左側のウィンドウの **[インストール済み]** の下の **[その他の言語]** で、 **[Visual C++]** を選択します。
   - 中央のウィンドウで、 **[Windows コンソール アプリケーション]** を選択します。
   - 下のウィンドウで、プロジェクトの **[名前]** 、 **[場所]** 、およびそれに応じて含める **[ソリューション名]** を更新します。
   - 完了したら、右下の **[OK]** ボタンをクリックします。

     [![Visual Studio ソリューションの作成](media/quick-app-initialization-cpp/create-vs-solution.png)](media/quick-app-initialization-cpp/create-vs-solution.png#lightbox)

2. MIP SDK 保護 API 用の Nuget パッケージをご自分のプロジェクトに追加します。
   - **ソリューション エクスプローラー** で、(最上位/ソリューション ノードの下から直接) プロジェクト ノードを右クリックして、 **[NuGet パッケージの管理]** を選択します。
   - **[NuGet パッケージ マネージャー]** タブが [エディター グループ] タブ領域で開かれたら、次の操作を行います。
     - **[参照]** を選択します。
     - 検索ボックスに「Microsoft.InformationProtection」と入力します。
     - [Microsoft.InformationProtection.Protection] パッケージを選択します。
     - **[変更のプレビュー]** の確認ダイアログが表示されたら、[インストール]、[OK] の順にクリックします。

     [![Visual Studio による NuGet パッケージの追加](media/quick-app-initialization-cpp/add-nuget-package.png)](media/quick-app-initialization-cpp/add-nuget-package.png#lightbox)

## <a name="implement-observer-classes-to-monitor-the-protection-profile-and-engine-objects"></a>保護プロファイルとエンジン オブジェクトを監視するためのオブザーバー クラスの実装

ここで、SDK の `mip::ProtectionProfile::Observer` クラスを拡大することで、保護プロファイル オブザーバー クラスの基本の実装を作成します。 このオブザーバーはインスタンス化され、保護プロファイルの読み込みとエンジン オブジェクトのプロファイルへの追加を監視するために、後で使用されます。

1. header/.h ファイルと implementation/.cpp ファイルの両方を作成する、新しいクラスをご自分のプロジェクトに追加します。

   - **ソリューション エクスプローラー** でもう一度プロジェクト ノードを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。
   - **[クラスの追加]** ダイアログで以下の操作を行います。
     - **[クラス名]** フィールドに「profile_observer」と入力します。 入力した名前に基づき、 **[.h file]\(.h ファイル\)** と **[.cpp file]\(.cpp ファイル\)** の両フィールドが自動入力されたことを確認してください。
     - 完了したら、 **[OK]** ボタンをクリックします。

     [![Visual Studio によるクラスの追加](media/quick-app-initialization-cpp/add-class.png)](media/quick-app-initialization-cpp/add-class.png#lightbox)

2. クラスの .h ファイルおよび .cpp ファイルを作成すると、両ファイルは [エディター グループ] タブに表示されます。 ここで各ファイルを更新して、新しいオブザーバー クラスを実装します。

   - 生成した `profile_observer` クラスを選択または削除することで、"profile_observer.h" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除 **しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include <memory>
     #include "mip/protection/protection_profile.h"
     using std::exception_ptr;
     using std::shared_ptr;


     class ProtectionProfileObserver final : public mip::ProtectionProfile::Observer {
     public:
          ProtectionProfileObserver() { }
          void OnLoadSuccess(const std::shared_ptr<mip::ProtectionProfile>& profile, const std::shared_ptr<void>& context) override;
          void OnLoadFailure(const std::exception_ptr& Failure, const std::shared_ptr<void>& context) override;
          void OnAddEngineSuccess(const std::shared_ptr<mip::ProtectionEngine>& engine, const std::shared_ptr<void>& context) override;
          void OnAddEngineFailure(const std::exception_ptr& Failure, const std::shared_ptr<void>& context) override;
     };
     ```

   - 生成した `profile_observer` クラス実装を選択/削除することで、"profile_observer.cpp" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除 **しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include <future>

     using std::promise;
     using std::shared_ptr;
     using std::static_pointer_cast;
     using mip::ProtectionEngine;
     using mip::ProtectionProfile;

     void ProtectionProfileObserver::OnLoadSuccess(const shared_ptr<ProtectionProfile>& profile, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionProfile>>>(context);
          promise->set_value(profile);
     }

     void ProtectionProfileObserver::OnLoadFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionProfile>>>(context);
          promise->set_exception(error);
     }

     void ProtectionProfileObserver::OnAddEngineSuccess(const shared_ptr<ProtectionEngine>& engine, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionEngine>>>(context);
          promise->set_value(engine);
     }

     void ProtectionProfileObserver::OnAddEngineFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionEngine>>>(context);
          promise->set_exception(error);
     }
     ```

3. 1 の手順に従う。 保護エンジン オブザーバーの新しいクラス "engine_observer" をプロジェクトに追加します。それにより header/.h ファイルと implementation/.cpp ファイルの両方が自動的に生成されます。

4. クラスの .h ファイルおよび .cpp ファイルを作成すると、両ファイルは [エディター グループ] タブに表示されます。 ここで各ファイルを更新して、新しいオブザーバー クラスを実装します。

   - 生成した `engine_observer` クラスを選択または削除することで、"engine_observer.h" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除 **しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include <memory>
     #include "mip/protection/protection_engine.h"
     using std::vector;
     using std::exception_ptr;
     using std::shared_ptr;

     class ProtectionEngineObserver final : public mip::ProtectionEngine::Observer {
       public:
       ProtectionEngineObserver() {}
       void OnGetTemplatesSuccess(const vector<std::shared_ptr<mip::TemplateDescriptor>>& templateDescriptors, const shared_ptr<void>& context) override;
       void OnGetTemplatesFailure(const exception_ptr& Failure, const shared_ptr<void>& context) override;

     };
     ```

   - 生成した `engine_observer` クラス実装を選択/削除することで、"engine_observer.cpp" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除 **しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include "mip/protection/protection_profile.h"
     #include "engine_observer.h"

     using std::promise;
     void ProtectionEngineObserver::OnGetTemplatesSuccess(const vector<shared_ptr<mip::TemplateDescriptor>>& templateDescriptors,const shared_ptr<void>& context) {
         auto loadPromise = static_cast<promise<vector<shared_ptr<mip::TemplateDescriptor>>>*>(context.get());
         loadPromise->set_value(templateDescriptors);
       };

       void ProtectionEngineObserver::OnGetTemplatesFailure(const exception_ptr& Failure, const shared_ptr<void>& context) {
         auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
         loadPromise->set_exception(Failure);
       };
     ```

5. 必要に応じて、Ctrl+Shift+B ( **[ソリューションのビルド]** ) を使用して、続行する前にソリューションのテスト コンパイル/リンクを実行し、正しくビルドされることを確認します。

## <a name="implement-an-authentication-delegate-and-a-consent-delegate"></a>認証委任と同意委任を実装する

MIP SDK では、クラスの拡張機能を使用して認証を実装します。これにより、クライアント アプリケーションを操作する認証を共有するメカニズムが提供されます。 クライアントによって、適切な OAuth2 アクセス トークンを取得し、実行時に MIP SDK を提供する必要があります。

SDK の `mip::AuthDelegate` クラスを拡張し、`mip::AuthDelegate::AcquireOAuth2Token()` 純粋仮想関数をオーバーライド/実装することで、認証の委任に対して実装を作成します。 **[ファイル API アプリケーション初期化クイック スタート](quick-app-initialization-cpp.md)に詳細が記されている手順に従います。** この認証の委任はインスタンス化され、保護プロファイルと保護エンジン オブジェクトによって後で使用されます。

## <a name="implement-a-consent-delegate"></a>同意の委任を実装する

SDK の `mip::ConsentDelegate` クラスを拡張し、`mip::AuthDelegate::GetUserConsent()` 純粋仮想関数をオーバーライド/実装することで、同意の委任に対して実装を作成します。  **[ファイル API アプリケーション初期化クイック スタート](quick-app-initialization-cpp.md)に詳細が記されている手順に従います。** この同意の委任はインスタンス化され、保護プロファイルと保護エンジン オブジェクトによって後で使用されます。

## <a name="construct-a-protection-profile-and-engine"></a>保護のプロファイルとエンジンを構築する

前述のように、MIP API を使用する SDK クライアントには、プロファイル オブジェクトとエンジン オブジェクトが必要です。 プロファイル オブジェクトとエンジン オブジェクトをインスタンス化するためにコードを追加することで、このクイック スタートのコード部分を完了します。

1. **ソリューション エクスプローラー** から、`main()` メソッドの実装を含む .cpp ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. 生成された `main()` の実装を削除します。 プロジェクトの作成時に Visual Studio で生成された、プリプロセッサ ディレクティブは削除 **しないでください** (#pragma, #include)。 任意のプリプロセッサ ディレクティブの後に次のコードを追加します。

  ```cpp
  #include "mip/mip_init.h"
  #include "mip/mip_context.h"  
  #include "auth_delegate.h"
  #include "consent_delegate.h"
  #include "profile_observer.h"
  #include"engine_observer.h"

  using std::promise;
  using std::future;
  using std::make_shared;
  using std::shared_ptr;
  using std::string;
  using std::cout;
  using mip::ApplicationInfo;
  using mip::ProtectionProfile;
  using mip::ProtectionEngine;

  int main(){
    // Construct/initialize objects required by the application's profile object
    ApplicationInfo appInfo{"<application-id>",                    // ApplicationInfo object (App ID, name, version)
                            "<application-name>",
                            "<application-version>"};

    auto mipContext = mip::MipContext::Create(appInfo,
                                              "file_sample",
                                              mip::LogLevel::Trace,
                                              false,
                                              nullptr /*loggerDelegateOverride*/,
                                              nullptr /*telemetryOverride*/);


    auto profileObserver = make_shared<ProtectionProfileObserver>(); // Observer object
    auto authDelegateImpl = make_shared<AuthDelegateImpl>("<application-id>"); // Authentication delegate object (App ID)
    auto consentDelegateImpl = make_shared<ConsentDelegateImpl>(); // Consent delegate object

    // Construct/initialize profile object
    ProtectionProfile::Settings profileSettings(
      mipContext,
      mip::CacheStorageType::OnDisk,      
      consentDelegateImpl,
      profileObserver);

    // Set up promise/future connection for async profile operations; load profile asynchronously
    auto profilePromise = make_shared<promise<shared_ptr<ProtectionProfile>>>();
    auto profileFuture = profilePromise->get_future();
    try
    {
      mip::ProtectionProfile::LoadAsync(profileSettings, profilePromise);
    }
    catch (const std::exception& e)
    {
      cout << "An exception occurred... are the Settings and ApplicationInfo objects populated correctly?\n\n"
            << e.what() << "'\n";
      system("pause");
      return 1;
    }

    auto profile = profileFuture.get();

    // Construct/initialize engine object
    ProtectionEngine::Settings engineSettings(
       authDelegateImpl,                          // Reference to mip::AuthDelegate implementation
       mip::Identity("<engine-account>"),         // Engine identity (account used for authentication)
       "<engine-state>",                          // User-defined engine state
       "en-US");                                  // Locale (default = en-US)

    // Set up promise/future connection for async engine operations; add engine to profile asynchronously
    auto enginePromise = make_shared<promise<shared_ptr<ProtectionEngine>>>();
    auto engineFuture = enginePromise->get_future();
    profile->AddEngineAsync(engineSettings, enginePromise);
    std::shared_ptr<ProtectionEngine> engine;

    try
    {
      engine = engineFuture.get();
    }
    catch (const std::exception& e)
    {
      cout << "An exception occurred... is the access token incorrect/expired?\n\n"
           << e.what() << "'\n";
      system("pause");
      return 1;
    }

    // Application shutdown. Null out profile and engine, call ReleaseAllResources();
    // Application may crash at shutdown if resources aren't properly released.
    engine = nullptr;
    profile = nullptr;
    mipContext = nullptr;

    return 0;
  }
   ```

3. 貼り付けたばかりのソース コードのすべてのプレースホルダー値を、次の文字列定数を使って置き換えます。

   | [プレースホルダ] | 値 | 例 |
   |:----------- |:----- |:--------|
   | \<application-id\> | "MIP SDK の設定と構成" (setup-configure-mip.md) に関する記事の手順 2 番で登録したアプリケーションに割り当てられた Azure AD アプリケーション ID (GUID)。 2 つのインスタンスを置き換えます。 | `"0edbblll-8773-44de-b87c-b8c6276d41eb"` |
   | \<application-name\> | ご利用のアプリケーションに対するユーザー定義のフレンドリ名。 有効な ASCII 文字が含まれている必要があります (';' を除く)。Azure AD 登録で使用したアプリケーション名と一致するものが理想的です。 | `"AppInitialization"` |
   | \<application-version\> | アプリケーションのユーザー定義のバージョン情報。 有効な ASCII 文字が含まれている必要があります (';' を除く)。 | `"1.1.0.0"` |
   | \<engine-account\> | エンジンの ID に使用されるアカウント。 トークンの取得時にユーザー アカウントを認証する場合、ユーザー アカウントはこの値に一致します。 | `"user1@tenant.onmicrosoft.com"` |
   | \<engine-state\> | エンジンに関連付けられるユーザー定義の状態。 | `"My App State"` |

4. アプリケーションの最終ビルドを行い、任意のエラーを解決します。 ご自分のコードで正常にビルドされますが、次のクイック スタートを完了するまでは、まだ正しく実行されません。 アプリケーションを実行すると、次のような出力が表示されます。 このアプリケーションでは保護プロファイルと保護エンジンが正しく構築されますが、次のクイック スタートを完了するまでは認証モジュールが起動しないことがあり、アクセス トークンが与えられません。

   ```console
    C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
    To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
    Press any key to close this window . . .
   ```

## <a name="next-steps"></a>次の手順

これで初期化コードが完了し、MIP 保護 API の操作を開始する次のクイック スタートの準備ができました。

> [!div class="nextstepaction"]
> [保護テンプレートを一覧表示する](quick-protection-list-templates-cpp.md)
