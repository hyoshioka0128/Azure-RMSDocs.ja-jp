---
title: クイック スタート - Microsoft Information Protection (MIP) SDK C++ クライアントの初期化
description: Microsoft Information Protection (MIP) SDK クライアント アプリケーションの初期化ロジックを記述する方法を示すクイック スタートです。
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: bryanla
ms.openlocfilehash: 75ca6b078275a2547cebfee3c78f8741f367c788
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255956"
---
# <a name="quickstart-client-application-initialization-c"></a>クイック スタート:クライアント アプリケーションの初期化 (C++)

このクイック スタートでは、実行時に MIP C++ SDK で使用される、クライアントの初期化パターンを実装する方法を示します。 

> [!NOTE]
> MIP ファイル、ポリシー、または保護 API を使用する任意のクライアント アプリケーションには、このクイック スタートで概説されている手順が必要です。 このクイック スタートではファイル API の使い方を示しますが、この同じパターンをポリシーと保護 API を使用するクライアントに適用できます。 直列に、残りのクイック スタートを完了する 1 つ目を次のそれぞれは、1 つ前のビルド、します。

## <a name="prerequisites"></a>前提条件

まだ完了していない場合は、必ず次の操作を行ってください。

- 「[Microsoft Information Protection (MIP) SDK setup and configuration](setup-configure-mip.md)」 (Microsoft Information Protection (MIP) SDK のセットアップと構成) の手順を完了します。 この "クライアント アプリケーションの初期化" クイック スタートは、適切な SDK のセットアップと構成に依存します。
- 必要に応じて、次の操作を行います。
  - [プロファイル オブジェクトとエンジン オブジェクト](concept-profile-engine-cpp.md)を確認します。 プロファイル オブジェクトとエンジン オブジェクトは、MIP ファイル/ポリシー/保護 API を使用するクライアントによって必要とされる、ユニバーサルな概念です。 
  - レビュー[認証の概念](concept-authentication-cpp.md)に、SDK、およびクライアント アプリケーションで認証と承認を実装する方法について説明します。
  - [オブザーバーの概念](concept-async-observers.md)を確認して、オブザーバーの詳細および実装方法について学習します。 MIP SDK では、オブザーバー パターンを使用して、非同期のイベント通知を実装します。

## <a name="create-a-visual-studio-solution-and-project"></a>Visual Studio のソリューションとプロジェクトの作成

最初に作成し、初期の Visual Studio ソリューションとの他のクイック スタートをビルドするプロジェクトを構成します。 

1. Visual Studio 2017 を開いて、**[ファイル]** メニュー、**[新規]**、**[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログで次の操作を行います。
   - 左側のウィンドウの **[インストール済み]** の下の **[その他の言語]** で、**[Visual C++]** を選択します。
   - 中央のウィンドウで、**[Windows コンソール アプリケーション]** を選択します。
   - 下のウィンドウで、プロジェクトの **[名前]**、**[場所]**、およびそれに応じて含める **[ソリューション名]** を更新します。
   - 完了したら、右下の **[OK]** ボタンをクリックします。

     [![Visual Studio ソリューションの作成](media/quick-app-initialization-cpp/create-vs-solution.png)](media/quick-app-initialization-cpp/create-vs-solution.png#lightbox)

2. MIP SDK ファイル API 用の Nuget パッケージをご自分のプロジェクトに追加します。
   - **ソリューション エクスプ ローラー**を (直接 上部/ソリューション ノード) で、プロジェクト ノードを右クリックし、 **NuGet パッケージの管理.**:
   - **[NuGet パッケージ マネージャー]** タブが [エディター グループ] タブ領域で開かれたら、次の操作を行います。
     - **[参照]** を選択します。
     - 検索ボックスに「Microsoft.InformationProtection」と入力します。
     - [Microsoft.InformationProtection.File] パッケージを選択します。
     - **[変更のプレビュー]** の確認ダイアログが表示されたら、[インストール]、[OK] の順にクリックします。
   
     [![Visual Studio による NuGet パッケージの追加](media/quick-app-initialization-cpp/add-nuget-package.png)](media/quick-app-initialization-cpp/add-nuget-package.png#lightbox)
 
## <a name="implement-an-observer-class-to-monitor-the-file-profile-and-engine-objects"></a>ファイル プロファイルとエンジン オブジェクトを監視するためのオブザーバー クラスの実装

ここで、SDK の `mip::FileProfile::Observer` クラスを拡大することで、ファイル プロファイル オブザーバー クラスの基本の実装を作成します。 このオブザーバーはインスタンス化され、ファイル プロファイルの読み込みとエンジン オブジェクトのプロファイルへの追加を監視するために、後で使用されます。

1. header/.h ファイルと implementation/.cpp ファイルの両方を作成する、新しいクラスをご自分のプロジェクトに追加します。

   - **ソリューション エクスプ ローラー**、もう一度、プロジェクト ノードを右クリックし、選択**追加**を選択し、**クラス**します。
   - **[クラスの追加]** ダイアログで以下の操作を行います。
     - **[クラス名]** フィールドに「profile_observer」と入力します。 入力した名前に基づき、**[.h file]\(.h ファイル\)** と **[.cpp file]\(.cpp ファイル\)** の両フィールドが自動入力されたことを確認してください。
     - 完了したら、**[OK]** ボタンをクリックします。

     [![Visual Studio によるクラスの追加](media/quick-app-initialization-cpp/add-class.png)](media/quick-app-initialization-cpp/add-class.png#lightbox)

2. クラスの .h ファイルおよび .cpp ファイルを作成すると、両ファイルは [エディター グループ] タブに表示されます。 ここで各ファイルを更新して、新しいオブザーバー クラスを実装します。

   - 生成した `profile_observer` クラスを選択または削除することで、"profile_observer.h" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include <memory>
     #include "mip/file/file_profile.h"

     class ProfileObserver final : public mip::FileProfile::Observer {
     public:
          ProfileObserver() { }
          void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
          void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
          void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context) override;
          void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
     };
     ```

   - 生成した `profile_observer` クラス実装を選択/削除することで、"profile_observer.cpp" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include <future>

     using std::promise;
     using std::shared_ptr;
     using std::static_pointer_cast;
     using mip::FileEngine;
     using mip::FileProfile;

     void ProfileObserver::OnLoadSuccess(const shared_ptr<FileProfile>& profile, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_value(profile);
     }

     void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_exception(error);
     }

     void ProfileObserver::OnAddEngineSuccess(const shared_ptr<FileEngine>& engine, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_value(engine);
     }

     void ProfileObserver::OnAddEngineFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_exception(error);
     }
     ```

3. 必要に応じて、F6 (**[ソリューションのビルド]**) を使用して、続行する前にソリューションのテスト コンパイル/リンクを実行し、正しくビルドされることを確認します。

## <a name="implement-an-authentication-delegate"></a>認証の委任を実装する

MIP SDK では、クラスの拡張機能を使用して認証を実装します。これにより、クライアント アプリケーションを操作する認証を共有するメカニズムが提供されます。 クライアントによって、適切な OAuth2 アクセス トークンを取得し、実行時に MIP SDK を提供する必要があります。 

SDK の `mip::AuthDelegate` クラスを拡張し、`mip::AuthDelegate::AcquireOAuth2Token()` 純粋仮想関数をオーバーライド/実装することで、認証の委任に対して実装を作成します。 この認証の委任はインスタンス化され、ファイル プロファイルとファイル エンジン オブジェクトによって後で使用されます。

1. 前のセクションの手順 1 で使用したのと同じ Visual Studio の [クラスの追加] 機能を使用して、別のクラスをご自分のプロジェクトに追加します。 ここでは、**[クラス名]** フィールドに「auth_delegate」と入力します。 

2. ここで、各ファイルを更新して、新しい認証の委任クラスを実装します。

   - 生成された `auth_delegate` クラス コードをすべて次のソースに置き換えることにより、"auth_delegate.h" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma, #include)。

     ```cpp
     #include <string>
     #include "mip/common_types.h"

     class AuthDelegateImpl final : public mip::AuthDelegate {
     public:
          AuthDelegateImpl() = delete;        // Prevents default constructor
          
          AuthDelegateImpl(
            const std::string& appId)         // AppID for registered AAD app
            : mAppId(appId) {};

          bool AcquireOAuth2Token(            // Called by MIP SDK to get a token
            const mip::Identity& identity,    // Identity of the account to be authenticated, if known
            const OAuth2Challenge& challenge, // Authority (AAD tenant issuing token), and resource (API being accessed; "aud" claim).
            OAuth2Token& token) override;     // Token handed back to MIP SDK
     private:
          std::string mAppId;
          std::string mToken;
          std::string mAuthority;
          std::string mResource;
     };
     ```

   - 生成された `auth_delegate` クラスの実装をすべて次のソースに置き換えることにより、"auth_delegate.cpp" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma、#include)。 

     > [!IMPORTANT]
     > 次のトークン取得コードは、運用環境での使用には適していません。 運用環境では、次に示すものを使用して、動的にトークンを取得するコードで置き換える必要があります。
     > - ご利用の Azure AD アプリ登録で指定されたアプリケーション ID と応答/リダイレクトの URI (応答/リダイレクトの URI は、ご利用のアプリの登録に一致する**必要があります**)
     > - `challenge` 引数の SDK によって渡された機関とリソースの URL (リソース URL はご利用のアプリ登録の API/アクセス許可に一致する**必要があります**)
     > - アカウントが SDK によって渡された `identity` 引数に一致する、有効なアプリ/ユーザーの資格情報。 OAuth2 の "ネイティブ" クライアントではユーザーの資格情報を求める確認メッセージが表示し、"認証コード" フローを使用する必要があります。 OAuth2 の "Confidential クライアント" では、"クライアントの資格情報" フロー (サービスなど) で独自のセキュリティで保護された資格情報を使用したり、"認証コード" フロー (Web アプリなど) を使用してユーザーの資格情報を求める確認メッセージを表示したりすることができます。 
     >
     > OAuth2 トークンの取得は複雑なプロトコルであり、通常はライブラリを使用することによって実現されます。 TokenAcquireOAuth2Token() は、必要に応じて MIP SDK によって**のみ**呼び出されます。

     ```cpp
     #include <iostream>
     using std::cout;
     using std::cin;
     using std::string;

     bool AuthDelegateImpl::AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) 
     {
          // Acquire a token manually, reuse previous token if same authority/resource. In production, replace with token acquisition code.
          string authority = challenge.GetAuthority();
          string resource = challenge.GetResource();
          if (mToken == "" || (authority != mAuthority || resource != mResource))
          {
              cout << "\nRun the PowerShell script to generate an access token using the following values, then copy/paste it below:\n";
              cout << "Set $authority to: " + authority + "\n";
              cout << "Set $resourceUrl to: " + resource + "\n";
              cout << "Sign in with user account: " + identity.GetEmail() + "\n";
              cout << "Enter access token: ";
              cin >> mToken;
              mAuthority = authority;
              mResource = resource;
              system("pause");
          }

          // Pass access token back to MIP SDK
          token.SetAccessToken(mToken);

          // True = successful token acquisition; False = failure
          return true;
     }
     ``` 
3. 必要に応じて、F6 (**[ソリューションのビルド]**) を使用して、続行する前にソリューションのテスト コンパイル/リンクを実行し、正しくビルドされることを確認します。

## <a name="implement-a-consent-delegate"></a>同意の委任を実装する

SDK の `mip::ConsentDelegate` クラスを拡張し、`mip::AuthDelegate::GetUserConsent()` 純粋仮想関数をオーバーライド/実装することで、同意の委任に対して実装を作成します。 この同意の委任はインスタンス化され、ファイル プロファイルとファイル エンジン オブジェクトによって後で使用されます。

1. 前に使用したのと同じ Visual Studio の [クラスの追加] 機能を使用して、別のクラスをご自分のプロジェクトに追加します。 ここでは、**[クラス名]** フィールドに「consent_delegate」と入力します。 

2. ここで各ファイルを更新して、新しい同意の委任クラスを実装します。

   - 生成された `consent_delegate` クラス コードをすべて次のソースに置き換えることにより、"consent_delegate.h" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma, #include)。

     ```cpp
     #include "mip/common_types.h"
     #include <string>

     class ConsentDelegateImpl final : public mip::ConsentDelegate {
     public:
          ConsentDelegateImpl() = default;
          virtual mip::Consent GetUserConsent(const std::string& url) override;
     };
     ```

   - 生成された `consent_delegate` クラスの実装をすべて次のソースに置き換えることにより、"consent_delegate.cpp" を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma、#include)。 

     ```cpp
     #include <iostream>
     using mip::Consent;
     using std::string;

     Consent ConsentDelegateImpl::GetUserConsent(const string& url) 
     {
          // Accept the consent to connect to the url
          std::cout << "SDK will connect to: " << url << std::endl;
          return Consent::AcceptAlways;
     }
     ``` 
3. 必要に応じて、F6 (**[ソリューションのビルド]**) を使用して、続行する前にソリューションのテスト コンパイル/リンクを実行し、正しくビルドされることを確認します。

## <a name="construct-a-file-profile-and-engine"></a>ファイルのプロファイルとエンジンを構築する

前述のように、プロファイルとエンジンのオブジェクトは SDK クライアントが MIP Api を使用する必要があります。 プロファイル オブジェクトとエンジン オブジェクトをインスタンス化するためにコードを追加することで、このクイック スタートのコード部分を完了します。 

1. **ソリューション エクスプローラー**から、`main()` メソッドの実装を含む .cpp ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. 生成された `main()` の実装を削除します。 プロジェクトの作成時に Visual Studio で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma, #include)。 任意のプリプロセッサ ディレクティブの後に次のコードを追加します。

   ```cpp
   #include "auth_delegate.h"
   #include "consent_delegate.h"
   #include "profile_observer.h"

   using std::promise;
   using std::future;
   using std::make_shared;
   using std::shared_ptr;
   using std::string;
   using std::cout;
   using mip::ApplicationInfo; 
   using mip::FileProfile;
   using mip::FileEngine;

   int main()
   {
     // Construct/initialize objects required by the application's profile object
     ApplicationInfo appInfo{"<application-id>",                    // ApplicationInfo object (App ID, name, version)
                 "<application-name>",
                 "<application-version>"};
     auto profileObserver = make_shared<ProfileObserver>();         // Observer object                  
     auto authDelegateImpl = make_shared<AuthDelegateImpl>(         // Authentication delegate object (App ID)
                 "<application-id>");
     auto consentDelegateImpl = make_shared<ConsentDelegateImpl>(); // Consent delegate object
 
     // Construct/initialize profile object
     FileProfile::Settings profileSettings("",    // Path for logging/telemetry/state
       true,                                      // true = use in-memory state storage (vs disk)
       authDelegateImpl,                            
       consentDelegateImpl,                     
       profileObserver,                         
       appInfo);                                    

     // Set up promise/future connection for async profile operations; load profile asynchronously
     auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
     auto profileFuture = profilePromise->get_future();
    try
    { 
        mip::FileProfile::LoadAsync(profileSettings, profilePromise);
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
     FileEngine::Settings engineSettings(
       mip::Identity("<engine-account>"),         // Engine identity (account used for authentication)
       "<engine-state>",                          // User-defined engine state      
       "en-US");                                  // Locale (default = en-US)

     // Set up promise/future connection for async engine operations; add engine to profile asynchronously
     auto enginePromise = make_shared<promise<shared_ptr<FileEngine>>>();
     auto engineFuture = enginePromise->get_future();
     profile->AddEngineAsync(engineSettings, enginePromise);
     std::shared_ptr<FileEngine> engine; 
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

   return 0;
   }
   ``` 

3. 貼り付けた、文字列定数を使用してソース コード内のすべてのプレース ホルダー値を置き換えます。

   | [プレースホルダ] | 値 | 例 |
   |:----------- |:----- |:--------|
   | \<application-id\> | 登録されている Azure AD アプリケーション ID (GUID)、アプリケーションに割り当てられている[手順 #2「MIP SDK のセットアップと構成」の](/information-protection/develop/setup-configure-mip#register-a-client-application-with-azure-active-directory)記事。 2 つのインスタンスを置き換えます。 | `"0edbblll-8773-44de-b87c-b8c6276d41eb"` |
   | \<application-name\> | ご利用のアプリケーションに対するユーザー定義のフレンドリ名。 有効な ASCII 文字を含める必要があります (を除く ';')、理想的には、Azure AD の登録で使用したアプリケーション名と一致するとします。 | `"AppInitialization"` |
   | \<application-version\> | アプリケーションのユーザー定義のバージョン情報です。 有効な ASCII 文字を含める必要があります (を除く ';')。 | `"1.1.0.0"` |
   | \<engine-account\> | エンジンの ID に使用されるアカウント。 トークンの取得時にユーザー アカウントを認証する場合、ユーザー アカウントはこの値に一致します。 | `"user1@tenant.onmicrosoft.com"` |
   | \<engine-state\> | エンジンに関連付けられるユーザー定義の状態。 | `"My App State"` |


4. アプリケーションの最終ビルドを行い、任意のエラーを解決します。 ご自分のコードで正常にビルドされますが、次のクイック スタートを完了するまでは、まだ正しく実行されません。 アプリケーションを実行する場合に、次のような出力を参照してください。 次のクイック スタートを完了するまで、提供するアクセス トークンはありません。

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account:
   Enter access token:
   ```

## <a name="next-steps"></a>次の手順

これで初期化コードが完了し、MIP ファイル API の操作を開始する次のクイック スタートの準備ができました。

> [!div class="nextstepaction"]
> [機密ラベルの一覧表示](quick-file-list-labels-cpp.md)
