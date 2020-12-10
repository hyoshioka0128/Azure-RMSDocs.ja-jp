---
title: クイック スタート - クライアント アプリケーション初期化 - 保護 API (C#)
description: Microsoft Information Protection (MIP) SDK - 保護 API C# クライアント アプリケーション (C#) の初期化ロジックを記述する方法を示すクイック スタート
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 0f8ed60420b5a0c4fcc0f8264d54f696f5c439a2
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535894"
---
# <a name="quickstart-client-application-initialization-for-protection-apis-c"></a>クイック スタート:保護 API のためのクライアント アプリケーション初期化 (C#)

このクイック スタートでは、実行時に MIP SDK .NET ラッパーによって使用される、クライアントの初期化パターンを実装する方法を示します。

> [!NOTE]
> MIP .NET ラッパーの保護 API を使用するすべてのクライアント アプリケーションには、このクイック スタートで概説されている手順が必要です。 このクイック スタートは、アプリケーションを初期化し、認証委任クラスと同意委任クラスを実装した直後に順次行ってください。

## <a name="prerequisites"></a>[前提条件]

まだ完了していない場合は、必ず次の操作を行ってください。

- 「[Microsoft Information Protection (MIP) SDK setup and configuration](setup-configure-mip.md)」 (Microsoft Information Protection (MIP) SDK のセットアップと構成) の手順を完了します。 この "保護のプロファイルとエンジンの設定" クイック スタートを始めるには、SDK の設定と構成が正しく行われている必要があります。
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
   - **ソリューション エクスプローラー** で、(最上位/ソリューション ノードの下から直接) プロジェクト ノードを右クリックして、 **[NuGet パッケージの管理]** を選択します。
   - **[NuGet パッケージ マネージャー]** タブが [エディター グループ] タブ領域で開かれたら、次の操作を行います。
     - **[参照]** を選択します。
     - 検索ボックスに「Microsoft.InformationProtection」と入力します。
     - [Microsoft.InformationProtection.File] パッケージを選択します。
     - **[変更のプレビュー]** の確認ダイアログが表示されたら、[インストール]、[OK] の順にクリックします。

3. 上記の手順を繰り返して MIP SDK 保護の API パッケージを追加します。ただし代わりに "Microsoft.IdentityModel.Clients.ActiveDirectory" をアプリケーションに追加します。

## <a name="implement-an-authentication-delegate-and-a-consent-delegate"></a>認証委任と同意委任を実装する

まだ実装されていない場合、「[ファイル API アプリケーション初期化](quick-app-initialization-csharp.md)」の手順に従い、認証と同意の委任を実装します。

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>MIP SDK のマネージド ラッパーを初期化する

1. **ソリューション エクスプローラー** から、`Main()` メソッドの実装を含む .cs ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. 生成された `main()` の実装を削除します。

3. マネージド ラッパーには、初期化、`MipContext` の作成、プロファイルの読み込み、リソースのリリースに使用された静的クラス `Microsoft.InformationProtection.MIP` が含まれています。 ファイル API の操作のためにラッパーを初期化するには、`MIP.Initialize()` を呼び出し、`MipComponent.Protection` を渡して、保護操作に必要なライブラリを読み込みます。

4. *Program.cs* の `Main()` で次を追加し、 **\<application-id\>** を前に作成した Azure AD アプリケーションの登録の ID と置き換えます。

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for Protection API operations
            MIP.Initialize(MipComponent.Protection);
        }
    }
}
```

## <a name="construct-a-protection-profile-and-engine"></a>保護のプロファイルとエンジンを構築する

前述のように、MIP API を使用する SDK クライアントには、プロファイル オブジェクトとエンジン オブジェクトが必要です。 ネイティブの DLL を読み込んでプロファイル オブジェクトとエンジン オブジェクトをインスタンス化するためのコードを追加することで、このクイック スタートのコード部分を完了します。

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

          static void Main(string[] args)
          {
               // Initialize Wrapper for Protection API operations.
               MIP.Initialize(MipComponent.Protection);

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

               // Initialize and instantiate the ProtectionProfile.
               // Create the ProtectionProfileSettings object.
               // Initialize protection profile settings to create/use local state.
               var profileSettings = new ProtectionProfileSettings(mipContext,
                                        CacheStorageType.OnDiskEncrypted,                                        
                                        new ConsentDelegateImplementation());

               // Load the Profile async and wait for the result.
               var protectionProfile = Task.Run(async () => await MIP.LoadProtectionProfileAsync(profileSettings)).Result;

               // Create a ProtectionEngineSettings object, then use that to add an engine to the profile.
               var engineSettings = new ProtectionEngineSettings("user1@tenant.com", authDelegate, "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var protectionEngine = Task.Run(async () => await protectionProfile.AddEngineAsync(engineSettings)).Result;

               // Application Shutdown
               // handler = null; // This will be used in later quick starts.
               protectionEngine = null;
               protectionProfile = null;
               mipContext = null;
          }
     }
}
```

3. 貼り付けたソース コードのプレースホルダー値を、次の値で置き換えます。

   | [プレースホルダ] | 値 | 例 |
   |:----------- |:----- |:--------|
   | \<application-id\> | "MIP SDK のセットアップと構成" で登録したアプリケーションに割り当てられた Azure AD アプリケーション ID (2 つのインスタンス)。  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | ご利用のアプリケーションに対するユーザー定義のフレンドリ名。 | AppInitialization |


4. アプリケーションの最終ビルドを行い、任意のエラーを解決します。 コードは正常にビルドされるはずです。

## <a name="next-steps"></a>次の手順

これで初期化コードが完了し、MIP 保護 API の操作を開始する次のクイック スタートの準備ができました。

> [!div class="nextstepaction"]
> [保護テンプレートを一覧表示する](quick-protection-list-templates-csharp.md)
