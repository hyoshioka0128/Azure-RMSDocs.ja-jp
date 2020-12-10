---
title: File API - 電子メール .msg ファイルの処理 (C#)
description: この記事は、MIP SDK ファイル API を使用して .msg ファイルを処理する方法 (C#) のシナリオを理解するうえで役立ちます。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: 04fc40fcf5e638c6b86723c90a3880f421af8025
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535996"
---
# <a name="file-api---process-email-msg-files-c"></a>File API - 電子メール .msg ファイルの処理 (C#)

File API は、他の種類のファイルと同じ方法で .msg ファイルを保護します。ただし、SDK に MSG 機能フラグを有効にするアプリケーションが必要です。 ここでは、このフラグを設定する方法について説明します。

前に説明したとおり、`IFileEngine` のインスタンス化には、設定オブジェクト、`FileEngineSettings` が必要です。 FileEngineSettings を使用すると、アプリケーションが特定のインスタンスに設定する必要があるカスタム設定のパラメーターを渡すことができます。 `FileEngineSettings` の `CustomSettings` プロパティは、.msg ファイルの処理を可能にする `enable_msg_file_type` フラグの設定に使用します。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: File API アプリケーションの初期化 (C#)](quick-app-initialization-csharp.md) に関する説明をまず完了し、スターターとなる Visual Studio ソリューションを構築します。 この「方法: 電子メール .msg ファイルの処理 (C#)」のクイックスタートは、前のものを基にしています。
- [電子メール ファイル MIP SDK](concept-email.md) の概念に関するページをご確認ください。
- 省略可能: [MIP SDK のファイル エンジン](concept-profile-engine-file-engine-cpp.md)の概念に関するページをご確認ください。
- 省略可能: [MIP SDK のファイル ハンドラー](concept-handler-file-cpp.md)の概念を確認してください。

## <a name="set-enable_msg_file_type-and-use-file-api-for-protecting-msg-file"></a>.msg ファイルの保護に enable_msg_file_type を設定し、File API を使用する

「File API アプリケーションの初期化」のクイックスタートの続きとして、ファイル エンジンの構築コードを変更して `enable_msg_file_type flag` を設定し、ファイル エンジンを使用して .msg ファイルを保護します。

1. 前の「クイック スタート: File API アプリケーションの初期化 (C#)」で作成した Visual Studio のソリューションを開きます。

2. ソリューション エクスプローラーを使用して、`Main()` メソッドの実装を含む .cs ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. 前のクイックスタートから `Main()` 関数の実装を削除します。 `Main()` 本文に次のコードを挿入します。 次のコード ブロックでは、ファイル エンジンの作成時に `enable_msg_file_type` フラグが設定されます。これにより、ファイル エンジンを使用して作成された `IFileHandler` オブジェクトで .msg ファイルを処理できるようになります。

    ```csharp
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

        MipContext mipContext = MIP.CreateMipContext(appInfo,"mip_data",LogLevel.Trace,null,null);

        // Initialize and instantiate the File Profile.
        // Create the FileProfileSettings object.
        // Initialize file profile settings to create/use local state.
        var profileSettings = new FileProfileSettings(mipContext, 
                                    CacheStorageType.OnDiskEncrypted, 
                                    new ConsentDelegateImplementation());

        // Load the Profile async and wait for the result.
        var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

        // Create a FileEngineSettings object, then use that to add an engine to the profile.
        var customSettings = new List<KeyValuePair<string, string>>();
        customSettings.Add(new KeyValuePair<string, string>("enable_msg_file_type", "true"));

        // Create a FileEngineSettings object, then use that to add an engine to the profile.
        var engineSettings = new FileEngineSettings("user1@tenant.com", authDelegate, "", "en-US");
        engineSettings.Identity = new Identity("user1@tenant.com");
        //set custom settings for the engine
        engineSettings.CustomSettings = customSettings;

        //Add fileEngine to profile
        var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;

        //Set file paths
        string inputFilePath = "<input-file-path>"; //.msg file to be protected
        string actualFilePath = inputFilePath;
        string outputFilePath = "<output-file-path>"; //protected .msg file
        string actualOutputFilePath = outputFilePath;

        //Create a file handler for original file
        var fileHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, 
                                                                    actualFilePath, 
                                                                    true)).Result;

        // List templates available to the user and use one of them to protect the mail file.

            /// Listing of protection templates has to be performed by creating protection engine as described in protection quick start

        string templateId = "<template-id>"; //protection template retrieved using protection engine

        // Construct a protection descriptor on input file and use the same to set protection to the file
        ProtectionDescriptor descriptor = new ProtectionDescriptor(templateId);
        fileHandler.SetProtection(descriptor, new ProtectionSettings());

        // Commit changes, save as outputFilePath
        var result = Task.Run(async () => await fileHandler.CommitAsync(outputFilePath)).Result;

        // Create a new handler to read the protected file metadata
        var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, 
                                                                        actualOutputFilePath, 
                                                                        true)).Result;

        Console.WriteLine(string.Format("Original file: {0}", inputFilePath));
        Console.WriteLine(string.Format("Protected file: {0}", outputFilePath));
        Console.WriteLine(string.Format("TemplateID applied to file: {0} \r\nProtectionOwner: {1}", 
            handlerModified.Protection.ProtectionDescriptor.TemplateId,handlerModified.Protection.Owner));
        Console.WriteLine("Press a key to continue.");
        Console.ReadKey();

        // Application Shutdown
        fileHandler = null;
        handlerModified = null;
        fileEngine = null;
        fileProfile = null;
        mipContext = null;
    }

    ```

    ファイル操作の詳細については、[ファイル ハンドラーの概念](concept-handler-file-cpp.md)に関するページを参照してください。

4. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<input-file-path\> | テスト入力メッセージ ファイルへの完全なパス。たとえば、`c:\\Test\\message.msg`。 |
   | \<output-file-path\> | 入力ファイルのラベル付きコピーである出力ファイルへの完全なパス。たとえば、`c:\\Test\\message_protected.msg`。 |
   | \<template-id\> | 保護エンジンを使用して取得した templateId。たとえば、`667466bf-a01b-4b0a-8bbf-a79a3d96f720`。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

ご自分のクライアント アプリケーションをビルドするには、F6 ( **[ソリューションのビルド]** ) を使用します。 ビルド エラーがない場合は、F5 ( **[デバッグ開始]** ) を使用してご自分のアプリケーションを実行します。

```Console
    Original file: C:\Test.msg
    Protected file: C:\Test_protected.msg
    TemplateID applied to file: 667466bf-a01b-4b0a-8bbf-a79a3d96f720
    ProtectionOwner: user1@tenant.com
    Press a key to continue.
```

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="problems-during-execution-of-c-application"></a>C# アプリケーションの実行時の問題

| [概要] | エラー メッセージ | 解決策: |
|---------|---------------|----------|
| NetworkException:RMS サービスが、要求で不正な入力を検出しました。 RMS エラー コード:Microsoft.RightsManagement.Exceptions.BadInputException | * TemplateID と Policy の両方が null である場合、パラメーターは無効です。, CorrelationId=f265b189-ebf6-4b30-a191-41539cdff215, CorrelationId.Description=FileHandler, HttpRequest.Id=04990d53-cf12-4969-9c80-06e365b312f2;d5fb4794-ac84-4445-abc6-647e41df62b2, HttpRequest.SanitizedUrl=https://api.aadrm.com/my/v2/publishinglicenses, HttpResponse.StatusCode=400, NetworkError.Category=FailureResponseCode* | ご自分のプロジェクトが正しくビルドされたにもかかわらず、左と同様な出力がある場合、templateID が不正である可能性があります。 コード ブロックに戻り、保護テンプレート ID を修正し、リビルドおよび再テストします。 |
| TemplateNotFoundException | *認識できないテンプレート ID です。, CorrelationId=abb2ef59-ad09-4aa0-b731-f59a92711dad, CorrelationId.Description=FileHandler, HttpRequest.Id=8c688752-ccd2-4dca-ace3-b67b44176689;78538a57-a9fd-4717-8924-33581a04598b* | ご自分のプロジェクトが正しくビルドされたにもかかわらず、左と同様な出力がある場合、templateID が不正である可能性があります。 コード ブロックに戻り、保護テンプレート ID を修正し、リビルドおよび再テストします。 |
