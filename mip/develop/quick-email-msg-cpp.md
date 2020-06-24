---
title: ファイル API - 電子メール .msg ファイルの処理 (C++)
description: この記事では、MIP SDK File API を使用して .msg ファイルを処理する方法のシナリオについて説明します。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: 44aabf8a6c822779100c3ca8c9c2eadf1831f549
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548124"
---
# <a name="file-api---process-email-msg-files-c"></a>ファイル API - 電子メール .msg ファイルの処理 (C++)

File API は、他の種類のファイルと同じ方法で .msg ファイルを保護します。ただし、SDK に MSG 機能フラグを有効にするアプリケーションが必要です。 ここでは、このフラグを設定する方法について説明します。

前に説明したとおり、`mip::FileEngine` のインスタンス化には、設定オブジェクト、`mip::FileEngineSettings` が必要です。 FileEngineSettings を使用すると、アプリケーションが特定のインスタンスに設定する必要があるカスタム設定のパラメーターを渡すことができます。 `mip::FileEngineSettings` の `CustomSettings` プロパティは、.msg ファイルの処理を可能にする `enable_msg_file_type` フラグの設定に使用します。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: File API アプリケーションの初期化 (C++)](quick-app-initialization-cpp.md) に関する説明をまず完了し、スターターとなる Visual Studio ソリューションを構築します。 この「方法: 電子メール .msg ファイルの処理 (C++)」のクイックスタートは、前のものを基にしています。
- 「[クイックスタート:秘密度ラベルの一覧表示 (C#)](quick-file-list-labels-cpp.md)」をご確認ください。
- 「[クイックスタート:秘密度ラベルの設定/取得 (C#)](quick-file-set-get-label-cpp.md)」をご確認ください。
- [電子メール ファイル MIP SDK](concept-email-cpp.md) の概念に関するページをご確認ください。
- 省略可能: [MIP SDK のファイル エンジン](concept-profile-engine-file-engine-cpp.md)の概念に関するページをご確認ください。
- 省略可能: [MIP SDK のファイル ハンドラー](concept-handler-file-cpp.md)の概念を確認してください。

## <a name="prerequisite-implementation-steps"></a>前提条件となる実装手順

1. 前の「クイック スタート: クライアント アプリケーションの初期化 (C++)」の記事で作成した、Visual Studio ソリューションを開きます。

2. [秘密度ラベルの一覧表示 ( C++ )](quick-file-list-labels-cpp.md#create-a-powershell-script-to-generate-access-tokens) に関するクイックスタートで説明したとおり、アクセス トークンを生成する PowerShell スクリプトを作成します。

3. 「[秘密度ラベルの設定/取得 (C++)](quick-file-set-get-label-cpp.md#implement-an-observer-class-to-monitor-the-file-handler-object)」のクイックスタートで説明したとおり、`mip::FileHandler` を監視するためにオブザーバー クラスを実装します。

## <a name="set-enable_msg_file_type-and-use-file-api-to-protect-msg-file"></a>.msg ファイルの保護に enable_msg_file_type を設定し、File API を使用する

次のファイル エンジンの構築コードを追加して `enable_msg_file_type flag` を設定し、ファイル エンジンを使用して .msg ファイルを保護します。

1. *ソリューション エクスプローラー*を使用して、`main()` メソッドの実装を含む .cpp ファイルをプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. 次の #include と using ディレクティブをファイルの上部の対応する既存のディレクティブの下に追加します。

    ```cpp
    #include "filehandler_observer.h" 
    #include "mip/file/file_handler.h" 
    #include <iostream>
    #include "mip/protection/protection_descriptor_builder.h"
    #include "mip/protection_descriptor.h"
    using mip::FileHandler;
    using mip::ProtectionDescriptor;
    using mip::ProtectionDescriptorBuilder;
    using mip::ProtectionSettings;
    using std::endl;
    ```

3. 前のクイックスタートから `main()` 関数の実装を削除します。 `main()` 本文に次のコードを挿入します。 次のコード ブロックでは、ファイル エンジンの作成時に `enable_msg_file_type` フラグが設定されます。これにより、ファイル エンジンを使用して作成された `mip::FileHandler` オブジェクトで .msg ファイルを処理できるようになります。

    ```cpp
    int main()
    {
        // Construct/initialize objects required by the application's profile object
        ApplicationInfo appInfo{ "<application-id>",                    // ApplicationInfo object (App ID, name, version)
                    "<application-name>", "1.0" };

        auto mipContext = mip::MipContext::Create(appInfo,"file_sample",mip::LogLevel::Trace,false,
                                                nullptr /*loggerDelegateOverride*/,nullptr /*telemetryOverride*/);

        auto profileObserver = make_shared<ProfileObserver>();                      // Observer object
        auto authDelegateImpl = make_shared<AuthDelegateImpl>("<application-id>");  // Authentication delegate object (App ID)
        auto consentDelegateImpl = make_shared<ConsentDelegateImpl>();              // Consent delegate object

        // Construct/initialize profile object
        FileProfile::Settings profileSettings(mipContext,mip::CacheStorageType::OnDisk,authDelegateImpl,
            consentDelegateImpl,profileObserver);

        // Set up promise/future connection for async profile operations; load profile asynchronously
        auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
        auto profileFuture = profilePromise->get_future();
        try
        {
            mip::FileProfile::LoadAsync(profileSettings, profilePromise);
        }
        catch (const std::exception& e)
        {
            std::cout << "An exception occurred... are the Settings and ApplicationInfo objects populated correctly?\n\n"<< e.what() << "'\n";
            system("pause");
            return 1;
        }
        auto profile = profileFuture.get();

        // Construct/initialize engine object
        FileEngine::Settings engineSettings(
            mip::Identity("<engine-account>"),    // Engine identity (account used for authentication)
            "<engine-state>",                                 // User-defined engine state
            "en-US");                                       // Locale (default = en-US)

        //Set enamble_msg_file_type flag as true
        std::vector<std::pair<string, string>> customSettings;
        customSettings.emplace_back(mip::GetCustomSettingEnableMsgFileType(), "true");
        engineSettings.SetCustomSettings(customSettings);

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
            cout << "An exception occurred... is the access token incorrect/expired?\n\n"<< e.what() << "'\n";
            system("pause");
            return 1;
        }


        //Set file paths
        string inputFilePath = "<input-file-path>"; //.msg file to be protected
        string actualFilePath = inputFilePath;
        string outputFilePath = "<output-file-path>"; //protected .msg file
        string actualOutputFilePath = outputFilePath;

        //Create a file handler for original file
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(inputFilePath,actualFilePath,true,std::make_shared<FileHandlerObserver>(),handlerPromise);
        auto fileHandler = handlerFuture.get();

        //List templates available to the user and use one of them to protect the mail file.

            ///Listing of protection templates has to be performed by creating protection engine as described in protection quick start

        string templateId = "<template-id>"; //protection template retrieved using protection engine

        //Create a protection descriptor using templateID and use it to set protection to the file
        auto descriptorBuilder = mip::ProtectionDescriptorBuilder::CreateFromTemplate(templateId);
        const std::shared_ptr<mip::ProtectionDescriptor>& descriptor = descriptorBuilder->Build();
        fileHandler->SetProtection(descriptor, ProtectionSettings());

        // Commit changes, save as outputFilePath
        auto commitPromise = std::make_shared<std::promise<bool>>();
        auto commitFuture = commitPromise->get_future();
        fileHandler->CommitAsync(outputFilePath, commitPromise);
        if (commitFuture.get()) {
            cout << "\n Protection applied to file: " << outputFilePath << endl;
        }
        else {
            cout << "Failed to protect: " + outputFilePath << endl;
            return 1;
        }

        // Create a new handler to read the protected file metadata
        auto protectedHandlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto protectedHandlerFuture = protectedHandlerPromise->get_future();
        engine->CreateFileHandlerAsync(outputFilePath, actualOutputFilePath, true, std::make_shared<FileHandlerObserver>(), protectedHandlerPromise);
        auto protectedFileHandler = protectedHandlerFuture.get();

        cout << "Original file: " << inputFilePath << endl;
        cout << "Protected file: " << outputFilePath << endl;
        cout << "TemplateID applied to protected file : " << protectedFileHandler->GetProtection()->GetProtectionDescriptor()->GetTemplateId() << endl;
        cout << "Protection Owner of protected file : " << protectedFileHandler->GetProtection()->GetProtectionDescriptor()->GetOwner() << endl;


        // Application shutdown. Null out profile and engine, call ReleaseAllResources();
        // Application may crash at shutdown if resources aren't properly released.
        protectedFileHandler = nullptr;
        fileHandler = nullptr;
        engine = nullptr;
        profile = nullptr;
        mipContext = nullptr;

        return 0;
    }

    ```

    ファイル操作の詳細については、[ファイル ハンドラーの概念](concept-handler-file-cpp.md)に関するページを参照してください。

4. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<application-id\> | Azure AD テナントに登録されているアプリケーション ID。たとえば、`0edbblll-8773-44de-b87c-b8c6276d41eb`。 |
   | \<engine-account\> | エンジンの ID に使用されるアカウント。たとえば、`user@tenant.onmicrosoft.com`。 |
   | \<engine-state\> | ユーザー定義のアプリケーションの状態。たとえば、`My engine state`。 |
   | \<input-file-path\> | テスト入力メッセージ ファイルへの完全なパス。たとえば、`c:\\Test\\message.msg`。 |
   | \<output-file-path\> | 入力ファイルのラベル付きコピーである出力ファイルへの完全なパス。たとえば、`c:\\Test\\message_protected.msg`。 |
   | \<template-id\> | 保護エンジンを使用して取得した templateId。たとえば、`667466bf-a01b-4b0a-8bbf-a79a3d96f720`。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

ご自分のクライアント アプリケーションをビルドするには、F6 ( **[ソリューションのビルド]** ) を使用します。 ビルド エラーがない場合は、F5 ( **[デバッグ開始]** ) を使用してご自分のアプリケーションを実行します。

```Console
    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://syncservice.o365syncservice.com/
    Sign in with user account: User@Contoso.onmicrosoft.com
    Enter access token: <Paste token here>
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: User@Contoso.onmicrosoft.com
    Enter access token: <Paste token here>
    Press any key to continue . . .

    Protection applied to file: C:\Test_protected.msg

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: User@Contoso.onmicrosoft.com
    Enter access token: <Paste token here>
    Press any key to continue . . .
    Original file: C:\Test.msg
    Protected file: C:\Test_protected.msg
    TemplateID applied to protected file : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
    Protection Owner of protected file : User@Contoso.OnMicrosoft.com

```

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="problems-during-execution-of-c-application"></a>C# アプリケーションの実行時の問題

| [概要] | エラー メッセージ | 解決策: |
|---------|---------------|----------|
| TemplateNotFoundException | 認識できないテンプレート ID です。, CorrelationId=abb2ef59-ad09-4aa0-b731-f59a92711dad, CorrelationId.Description=FileHandler, HttpRequest.Id=8c688752-ccd2-4dca-ace3-b67b44176689;78538a57-a9fd-4717-8924-33581a04598b| ご自分のプロジェクトが正しくビルドされたにもかかわらず、左と同様な出力がある場合、templateID が不正である可能性があります。 コード ブロックに戻り、保護テンプレート ID を修正し、リビルドおよび再テストします。 |