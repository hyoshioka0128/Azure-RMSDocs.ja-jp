---
title: クイック スタート - Microsoft Information Protection (MIP) SDK の初期化C#クライアント
description: Microsoft Information Protection (MIP) SDK の初期化ロジックを記述する方法を示すクイック スタートC#クライアント アプリケーション。
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: 7efaaba799afa01b07a5eefc0b6798983cc590d2
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652372"
---
# <a name="quickstart-client-application-initialization-c"></a>クイック スタート:クライアント アプリケーションの初期化 (C#)

このクイック スタートでは、実行時に MIP SDK .NET ラッパーで使用される、クライアントの初期化パターンを実装する方法を示します。

> [!NOTE]
> このクイック スタートで説明する手順は、MIP .NET ラッパーのファイルまたはポリシー Api を使用するクライアント アプリケーションに必要です。 保護 API は、まだ使用できません。 このクイック スタートではファイル API の使い方を示しますが、この同じパターンをポリシーと保護 API を使用するクライアントに適用できます。 今後のクイック スタートは、それぞれが前のクイック スタートをベースにビルドされるので、連続的に実行される必要があります。このクイック スタートが最初になっています。

## <a name="prerequisites"></a>前提条件

まだ完了していない場合は、必ず次の操作を行ってください。

- 「[Microsoft Information Protection (MIP) SDK setup and configuration](setup-configure-mip.md)」 (Microsoft Information Protection (MIP) SDK のセットアップと構成) の手順を完了します。 この "クライアント アプリケーションの初期化" クイック スタートは、適切な SDK のセットアップと構成に依存します。
- 必要に応じて、次の操作を行います。
  - [プロファイル オブジェクトとエンジン オブジェクト](concept-profile-engine-cpp.md)を確認します。 プロファイル オブジェクトとエンジン オブジェクトは、MIP ファイル/ポリシー/保護 API を使用するクライアントによって必要とされる、ユニバーサルな概念です。 
  - [認証の概念](concept-authentication-cpp.md)を確認して、認証と承認が SDK とクライアント アプリケーションによってどのように実装されるかについて学習します。

## <a name="create-a-visual-studio-solution-and-project"></a>Visual Studio のソリューションとプロジェクトの作成

まず、その他のクイック スタートをビルドする対象の初期の Visual Studio ソリューションを作成して構成します。

1. Visual Studio 2017 を開いて、**[ファイル]** メニュー、**[新規]**、**[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログで次の操作を行います。
   - 左側のウィンドウで **インストール済み**、 **Visual C#** を選択します**Windows デスクトップ**します。
   - 中央のウィンドウで次のように選択します**コンソール アプリ (.NET Framework)。**
   - 下のウィンドウで、プロジェクトの **[名前]**、**[場所]**、およびそれに応じて含める **[ソリューション名]** を更新します。
   - 完了したら、右下の **[OK]** ボタンをクリックします。 

     [![Visual Studio ソリューションの作成](media/quick-app-initialization-csharp/create-vs-solution.png)](media/quick-app-initialization-csharp/create-vs-solution.png#lightbox)

2. MIP SDK ファイル API 用の Nuget パッケージをご自分のプロジェクトに追加します。
   - **ソリューション エクスプローラー**で、(最上位/ソリューション ノードの下から直接) プロジェクト ノードを右クリックして、**[NuGet パッケージの管理]** を選択します。
   - **[NuGet パッケージ マネージャー]** タブが [エディター グループ] タブ領域で開かれたら、次の操作を行います。
     - **[参照]** を選択します。
     - 検索ボックスに「Microsoft.InformationProtection」と入力します。
     - [Microsoft.InformationProtection.File] パッケージを選択します。
     - **[変更のプレビュー]** の確認ダイアログが表示されたら、[インストール]、[OK] の順にクリックします。

3. MIP SDK ファイル API パッケージを追加するための上記の手順を繰り返しますが、代わりに、アプリケーションを"Microsoft.IdentityModel.Clients.ActiveDirectory"を追加します。

## <a name="implement-an-authentication-delegate"></a>認証の委任を実装する

MIP SDK では、クラスの拡張機能を使用して認証を実装します。これにより、クライアント アプリケーションを操作する認証を共有するメカニズムが提供されます。 クライアントによって、適切な OAuth2 アクセス トークンを取得し、実行時に MIP SDK を提供する必要があります。

これで、SDK を拡張することによって認証デリゲートでは、実装を作成`Microsoft.InformationProtection.IAuthDelegate`インターフェイス、およびオーバーライド実装、`IAuthDelegate.AcquireToken()`仮想関数。 認証のデリゲートがインスタンス化され、後で使用される、`FileProfile`と`FileEngine`オブジェクト。

1. Visual Studio でプロジェクト名を右クリックして**追加**し**クラス**します。
2. "AuthDelegateImplementation"を入力、**名前**フィールド。 **[追加]** をクリックします。
3. Active Directory Authentication Library (ADAL) と MIP ライブラリの using ステートメントを追加します。

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
     ```

4. 設定`AuthDelegateImplementation`を継承する`Microsoft.InformationProtection.IAuthDelegate`のプライベート変数を実装および`Microsoft.InformationProtection.ApplicationInfo`と同じ型を受け取るコンス トラクター。

     ```csharp
     public class AuthDelegateImplementation : IAuthDelegate
     {
        private ApplicationInfo _appInfo;
        private string redirectUri = "mip-sdk-app://authorize";
        public AuthDelegateImplementation(ApplicationInfo appInfo)
        {
            _appInfo = appInfo;
        }
     }
     ```

`ApplicationInfo`オブジェクトには、2 つのプロパティが含まれています。 `_appInfo.ApplicationId`で使用される、`AuthDelegateImplementation`認証ライブラリへのクライアント ID を指定するクラス。

5. 追加、`public string AcquireToken()`クラス。 このクラスを受け入れる必要があります`Microsoft.InformationProtection.Identity`、2 つの文字列: 機関とリソース。 これらの文字列変数では、API での認証ライブラリに渡され、操作することはできません。 編集と、認証に失敗した可能性があります。

     ```csharp
     public string AcquireToken(Identity identity, string authority, string resource)
     {
          AuthenticationContext authContext = new AuthenticationContext(authority);
          var result = authContext.AcquireTokenAsync(resource, _appInfo.ApplicationId, new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, null), UserIdentifier.AnyUser).Result;
          return result.AccessToken;
     }
     ```

## <a name="implement-a-consent-delegate"></a>同意の委任を実装する

これで拡張 SDK の同意デリゲートの実装を作成`Microsoft.InformationProtection.IConsentDelegate`インターフェイス、およびオーバーライド実装`GetUserConsent()`します。 この同意の委任はインスタンス化され、ファイル プロファイルとファイル エンジン オブジェクトによって後で使用されます。 同意のデリゲートがでを使用するサービスのアドレスを持つ、ユーザーが同意する必要があります指定、`url`パラメーター。 デリゲートは一般に、ユーザーに同意すると、サービスへのアクセスを承認または拒否できるいくつかのフローを提供します。 このクイック スタートのハード コード`Consent.Accept`します。

1. 前に使用したのと同じ Visual Studio の [クラスの追加] 機能を使用して、別のクラスをご自分のプロジェクトに追加します。 今回での"ConsentDelegateImplementation"の入力、**クラス名**フィールド。 

2. 今すぐ更新**ConsentDelegateImpl.cs**新しい同意デリゲート クラスを実装します。 使用して、追加のステートメント`Microsoft.InformationProtection`設定を継承するクラスと`IConsentDelegate`します。

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. 必要に応じて、エラーなしでコンパイルすることを確認するソリューションをビルドしようとします。

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>MIP SDK のマネージ ラッパーを初期化します。

1. **ソリューション エクスプ ローラー**の実装を含むプロジェクトの .cs ファイルを開き、`Main()`メソッド。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. 生成された `main()` の実装を削除します。 

3. マネージ ラッパーには、静的クラスが含まれています。 `Microsoft.InformationProtection.MIP` 、プロファイルの読み込みとリソースを解放するときに、初期化に使用します。 ファイル API の操作のラッパーを初期化するには、MIP を呼び出します。渡して初期化`MipComponent.File`ファイル操作のために必要なライブラリを読み込みます。 

4. `Main()`で*Program.cs* 、次の追加、置換**\<アプリケーション id\>** の前に作成した Azure AD アプリケーションの登録 id。

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
            //Initialize Wrapper for File API operations 
            MIP.Initialize(MipComponent.File);
        }
    }
}
```

## <a name="construct-a-file-profile-and-engine"></a>ファイルのプロファイルとエンジンを構築します。

前述のように、プロファイルとエンジンのオブジェクトは SDK クライアントが MIP Api を使用する必要があります。 ネイティブ Dll をロードし、プロファイルとエンジンのオブジェクトをインスタンス化するためのコードを追加することで、このクイック スタートのコード部分を完了します。

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
               //Initialize Wrapper for File API operations
               MIP.Initialize(MipComponent.File);

               //Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               //Instatiate the AuthDelegateImpl object, passing in AppInfo. 
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               //Initialize and instantiate the File Profile
               //Create the FileProfileSettings object
               var profileSettings = new FileProfileSettings("mip_data", false, authDelegate, new ConsentDelegateImplementation(), appInfo, LogLevel.Trace);

               //Load the Profile async and wait for the result
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               //Create a FileEngineSettings object, then use that to add an engine to the profile
               var engineSettings = new FileEngineSettings("user1@tenant.com", "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;
          }
     }
}
``` 

3. 次の値を使用して、コピーしたソース コード内のプレース ホルダーの値に置き換えます。

   | [プレースホルダ] | [値] | 例 |
   |:----------- |:----- |:--------|
   | \<application-id\> | "MIP SDK のセットアップと構成" で登録したアプリケーションに割り当てられた Azure AD アプリケーション ID (2 つのインスタンス)。  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | ご利用のアプリケーションに対するユーザー定義のフレンドリ名。 | AppInitialization |


4. アプリケーションの最終ビルドを行い、任意のエラーを解決します。 コードが正常にビルドする必要があります。

## <a name="next-steps"></a>次の手順

これで初期化コードが完了し、MIP ファイル API の操作を開始する次のクイック スタートの準備ができました。

> [!div class="nextstepaction"]
> [機密ラベルの一覧表示](quick-file-list-labels-csharp.md)
