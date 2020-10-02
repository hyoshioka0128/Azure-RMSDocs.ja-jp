---
title: クイック スタート - Microsoft Information Protection (MIP) SDK C# クライアントの初期化
description: Microsoft Information Protection (MIP) SDK C# クライアント アプリケーションの初期化ロジックを記述する方法を示すクイック スタート。
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 09/15/2020
ms.author: tommos
ms.custom: has-adal-ref
ms.openlocfilehash: 406068f5770f489c66963fc34a462ec7e205765b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91108954"
---
# <a name="quickstart-client-application-initialization-c"></a>クイック スタート:クライアント アプリケーションの初期化 (C#)

このクイック スタートでは、実行時に MIP SDK .NET ラッパーによって使用される、クライアントの初期化パターンを実装する方法を示します。

> [!NOTE]
> MIP .NET ラッパーのファイルまたはポリシー API を使用するすべてのクライアント アプリケーションには、このクイック スタートで概説されている手順が必要です。 保護 API はまだ使用できません。 このクイック スタートではファイル API の使い方を示しますが、この同じパターンをポリシーと保護 API を使用するクライアントに適用できます。 今後のクイック スタートは、それぞれが前のクイック スタートをベースにビルドされるので、連続的に実行される必要があります。このクイック スタートが最初になっています。

## <a name="prerequisites"></a>[前提条件]

まだ完了していない場合は、必ず次の操作を行ってください。

- 「[Microsoft Information Protection (MIP) SDK setup and configuration](setup-configure-mip.md)」 (Microsoft Information Protection (MIP) SDK のセットアップと構成) の手順を完了します。 この "クライアント アプリケーションの初期化" クイック スタートは、適切な SDK のセットアップと構成に依存します。
- 省略可能:
  - [プロファイル オブジェクトとエンジン オブジェクト](concept-profile-engine-cpp.md)を確認します。 プロファイル オブジェクトとエンジン オブジェクトは、MIP ファイル/ポリシー/保護 API を使用するクライアントによって必要とされる、ユニバーサルな概念です。
  - [認証の概念](concept-authentication-cpp.md)を確認して、認証と承認が SDK とクライアント アプリケーションによってどのように実装されるかについて学習します。

## <a name="create-a-visual-studio-solution-and-project"></a>Visual Studio のソリューションとプロジェクトの作成

まず、その他のクイック スタートをビルドする対象の初期の Visual Studio ソリューションを作成して構成します。

1. Visual Studio 2017 を開いて、 **[ファイル]** メニュー、 **[新規]** 、 **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログで次の操作を行います。
   - 左側のウィンドウの **[インストール済み]** 、 **[Visual C#]** の下で **[Windows Desktop]** を選択します。
   - 中央のウィンドウで、 **[コンソール アプリ (.NET Framework)]** を選択します。
   - 下のウィンドウで、プロジェクトの **[名前]** 、 **[場所]** 、およびそれに応じて含める **[ソリューション名]** を更新します。
   - 完了したら、右下の **[OK]** ボタンをクリックします。

     [![Visual Studio ソリューションの作成](media/quick-app-initialization-csharp/create-vs-solution.png)](media/quick-app-initialization-csharp/create-vs-solution.png#lightbox)

2. MIP SDK ファイル API 用の Nuget パッケージをご自分のプロジェクトに追加します。
   - **ソリューション エクスプローラー**で、(最上位/ソリューション ノードの下から直接) プロジェクト ノードを右クリックして、 **[NuGet パッケージの管理]** を選択します。
   - **[NuGet パッケージ マネージャー]** タブが [エディター グループ] タブ領域で開かれたら、次の操作を行います。
     - **[参照]** を選択します。
     - 検索ボックスに「Microsoft.InformationProtection」と入力します。
     - [Microsoft.InformationProtection.File] パッケージを選択します。
     - **[変更のプレビュー]** の確認ダイアログが表示されたら、[インストール]、[OK] の順にクリックします。

3. MIP SDK File API パッケージを追加する上記のステップを繰り返します。ただし、アプリケーションには "Microsoft.Identity.Client" を追加します。

## <a name="implement-an-authentication-delegate"></a>認証の委任を実装する

MIP SDK では、クラスの拡張機能を使用して認証を実装します。これにより、クライアント アプリケーションを操作する認証を共有するメカニズムが提供されます。 クライアントによって、適切な OAuth2 アクセス トークンを取得し、実行時に MIP SDK を提供する必要があります。

SDK の `Microsoft.InformationProtection.IAuthDelegate` インターフェイスを拡張し、`IAuthDelegate.AcquireToken()` 仮想関数をオーバーライド/実装することで、認証の委任に対して実装を作成します。 この認証の委任はインスタンス化され、`FileProfile` オブジェクトと `FileEngine` オブジェクトによって後で使用されます。

1. Visual Studio でプロジェクト名を右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。
2. **[名前]** フィールドに「AuthDelegateImplementation」と入力します。 **[追加]** をクリックします。
3. Microsoft Authentication Library (ADAL) および MIP ライブラリに using ステートメントを追加します。

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.Identity.Client;
     ```

4. `AuthDelegateImplementation` を設定して `Microsoft.InformationProtection.IAuthDelegate` を継承し、`Microsoft.InformationProtection.ApplicationInfo` のプライベート変数と、同じ型を受け入れるコンストラクターを実装します。

     ```csharp
     public class AuthDelegateImplementation : IAuthDelegate
    {
        private ApplicationInfo _appInfo;
        // Microsoft Authentication Library IPublicClientApplication
        private IPublicClientApplication _app;
        public AuthDelegateImplementation(ApplicationInfo appInfo)
        {
            _appInfo = appInfo;
        }

    }
     ```

    `ApplicationInfo` オブジェクトには 3 つのプロパティが含まれています。 `_appInfo.ApplicationId` は認証ライブラリにクライアント ID を提供するために `AuthDelegateImplementation` クラスで使用されます。 `ApplicationName` と `ApplicationVersion` は Azure Information Protection Analytics レポートに表示されます。

5. `public string AcquireToken()` メソッドを追加します。 このメソッドには、`Microsoft.InformationProtection.Identity` と、必要に応じて 3 つの文字列: 権限 URL、リソース URI、および要求を指定することができます。 これらの文字列変数は API によって認証ライブラリに渡されるため、操作することはできません。 テナントの Azure portal からテナント GUID を入力してください。 テナント GUID 以外の文字列を編集すると、認証に失敗する可能性があります。

     ```csharp
    public string AcquireToken(Identity identity, string authority, string resource, string claims)
    {
        var authorityUri = new Uri(authority);
        authority = String.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

        _app = PublicClientApplicationBuilder.Create(_appInfo.ApplicationId).WithAuthority(authority).WithDefaultRedirectUri().Build();
        var accounts = (_app.GetAccountsAsync()).GetAwaiter().GetResult();

        // Append .default to the resource passed in to AcquireToken().
        string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
        var result = _app.AcquireTokenInteractive(scopes).WithAccount(accounts.FirstOrDefault()).WithPrompt(Prompt.SelectAccount)
                   .ExecuteAsync().ConfigureAwait(false).GetAwaiter().GetResult();

        return result.AccessToken;
    }

     ```

## <a name="implement-a-consent-delegate"></a>同意の委任を実装する

SDK の `Microsoft.InformationProtection.IConsentDelegate` インターフェイスを拡張し、`GetUserConsent()` をオーバーライド/実装することで、同意の委任に対して実装を作成します。 この同意の委任はインスタンス化され、ファイル プロファイルとファイル エンジン オブジェクトによって後で使用されます。 同意の委任によりサービスのアドレスが提供され、これを `url` パラメーターで使用することをユーザーが同意する必要があります。 委任では一般に、サービスへのアクセスに同意することをユーザーが許可/拒否できるようにするフローがいくつか提供されます。 このクイック スタートでは `Consent.Accept` をハードコーディングします。

1. 前に使用したのと同じ Visual Studio の [クラスの追加] 機能を使用して、別のクラスをご自分のプロジェクトに追加します。 ここでは、**[クラス名]** フィールドに「ConsentDelegateImplementation」と入力します。

2. ここで **ConsentDelegateImpl.cs** を更新して、新しい同意の委任クラスを実装します。 `Microsoft.InformationProtection` に using ステートメントを追加し、`IConsentDelegate` を継承するようにクラスを設定します。

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. 必要に応じて、ソリューションのビルドを試し、エラーなしでコンパイルされることを確認してください。

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>MIP SDK のマネージド ラッパーを初期化する

1. **ソリューション エクスプローラー**から、`Main()` メソッドの実装を含む .cs ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. 生成された `main()` の実装を削除します。

3. マネージド ラッパーには、初期化、`MipContext` の作成、プロファイルの読み込み、リソースのリリースに使用された静的クラス `Microsoft.InformationProtection.MIP` が含まれています。 ファイル API の操作のためにラッパーを初期化するには、`MIP.Initialize()` を呼び出し、`MipComponent.File` を渡して、ファイル操作に必要なライブラリを読み込みます。

4. *Program.cs* の `Main()` で次を追加し、 **\<application-id\>** を前に作成した Azure AD アプリケーションの登録の ID と置き換えます。

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.File;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for File API operations
            MIP.Initialize(MipComponent.File);
        }
    }
}
```

## <a name="construct-a-file-profile-and-engine"></a>ファイルのプロファイルとエンジンを構築する

前述のように、MIP API を使用する SDK クライアントには、プロファイル オブジェクトとエンジン オブジェクトが必要です。 ネイティブの DLL を読み込んでプロファイル オブジェクトとエンジン オブジェクトをインスタンス化するためのコードを追加することで、このクイック スタートのコード部分を完了します。


   ```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.File;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

          static void Main(string[] args)
          {
               // Initialize Wrapper for File API operations.
               MIP.Initialize(MipComponent.File);

               // Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId.
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               // Instantiate the AuthDelegateImpl object, passing in AppInfo.
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               MipContext mipContext = MIP.CreateMipContext(appInfo,
                                        "mip_data",
                                        LogLevel.Trace,
                                        null,
                                        null);

               // Initialize and instantiate the File Profile.
               // Create the FileProfileSettings object.
               // Initialize file profile settings to create/use local state.
               var profileSettings = new FileProfileSettings(mipContext,
                                        CacheStorageType.OnDiskEncrypted,
                                        new ConsentDelegateImplementation());

               // Load the Profile async and wait for the result.
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               // Create a FileEngineSettings object, then use that to add an engine to the profile.
               var engineSettings = new FileEngineSettings("user1@tenant.com", authDelegate "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;

               // Application Shutdown
               // handler = null; // This will be used in later quick starts.
               fileEngine = null;
               fileProfile = null;
               mipContext = null;
          }
     }
}
```

3. 貼り付けたソース コードのプレースホルダー値を、次の値で置き換えます。

   | プレースホルダー | 値 | 例 |
   |:----------- |:----- |:--------|
   | \<application-id\> | "MIP SDK のセットアップと構成" で登録したアプリケーションに割り当てられた Azure AD アプリケーション ID (2 つのインスタンス)。  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | ご利用のアプリケーションに対するユーザー定義のフレンドリ名。 | AppInitialization |
   | \<Tenant-GUID\> | Azure AD テナントのテナント ID | TenantId |


4. アプリケーションの最終ビルドを行い、任意のエラーを解決します。 コードは正常にビルドされるはずです。

## <a name="next-steps"></a>次の手順

これで初期化コードが完了し、MIP ファイル API の操作を開始する次のクイック スタートの準備ができました。

> [!div class="nextstepaction"]
> [秘密度ラベルの一覧表示](quick-file-list-labels-csharp.md)
