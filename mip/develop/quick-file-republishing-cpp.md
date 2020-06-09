---
title: '方法: シナリオ C++ の再パブリッシュ'
description: この記事は、再パブリッシュのシナリオで保護ハンドラーを再利用する方法のシナリオを理解するのに役立ちます。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 602cc8c56d260e8399fa62367d585baae1976157
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548260"
---
# <a name="file-api-re-publishing-quickstart-c"></a>ファイル API 再発行のクイックスタート (C++)

## <a name="overview"></a>概要

このシナリオの概要と使用される場所については、「 [MIP SDK での再パブリッシュ」](concept-republishing-cpp.md)を参照してください。

## <a name="prerequisites"></a>前提条件

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 完全なクイックスタート: 最初に、Visual Studio のスタートを[設定/取得する (C++)](quick-file-set-get-label-cpp.md)まず、組織の秘密度ラベルの一覧を作成し、ファイルに対して機密ラベルを設定して読み取るための、Visual Studio の初期ソリューションを構築します。 前のクイックスタートでは、「理由 C++ を必要とするラベルをダウングレードまたは削除する方法」を説明しています。
- 必要に応じて、MIP SDK の概念の[ファイルハンドラー](concept-handler-file-cpp.md)を確認します。
- 必要に応じて、MIP SDK の概念で[保護ハンドラー](concept-handler-protection-cpp.md)をレビューします。

## <a name="add-logic-to-filehandler-observer-class"></a>FileHandler オブザーバークラスにロジックを追加する

によって公開されるメソッドを使用して保護されたファイルの暗号化解除を使用できるようにするには `GetDecryptedTemporaryFileAsync()` `mip::FileHandler` 、成功と失敗の非同期メソッドのコールバックを以下のように定義する必要があります。

1. 前の「クイックスタート: 秘密度ラベルの設定/取得 (C++)」で作成した Visual Studio ソリューションを開きます。

2. ソリューションエクスプローラーを使用して、 `filehandler_observer.h` プロジェクトののファイルを開きます。 FileHandler 定義の末尾に向かって、 `};` メソッド宣言の下に行を追加する前。

    ```cpp
        void OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) override;
        void OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
    ```

3. ソリューションエクスプローラーを使用して、 `filehandler_observer.cpp` プロジェクト内のファイルを開きます。 ファイルの末尾に向かって、次の行をメソッド定義に追加します。

    ```cpp

        void FileHandlerObserver::OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::string>>(context);
        promise->set_value(decryptedFilePath);
        }

        void FileHandlerObserver::OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::string>>(context);
        promise->set_exception(error);
        }
    ```

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>保護されたファイルを編集して再発行するためのロジックを追加する

1. ソリューションエクスプローラーを使用して、メソッドの実装を含む .cpp ファイルをプロジェクトで開きます。 `main()` これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. Main () 本体の末尾に向かって ("pause")、以上の場合は0を返します。(前のクイックスタートでは、前の手順を実行しています)。次のコードを挿入します。

    ```cpp

        //Originally protected file's path.
        std::string protectedFilePath = "<protected-file-path>";

        // Create file handler for the file
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(protectedFilePath, protectedFilePath, true, std::make_shared<FileHandlerObserver>(), handlerPromise);
        auto protectedFileHandler = handlerFuture.get();

        // retieve and store protection handler from file
        auto protectionHandler = protectedFileHandler->GetProtection();

        //Check if the user has the 'Edit' right to the file and if so decrypt the file.
        if (protectionHandler->AccessCheck("Edit")) {

            // Decrypt file to temp path using the same file handler
            auto tempPromise = std::make_shared<std::promise<string>>();
            auto tempFuture = tempPromise->get_future();
            protectedFileHandler->GetDecryptedTemporaryFileAsync(tempPromise);
            auto tempPath = tempFuture.get();

            /// Write code here to perform further operations for edit ///

            /// Follow steps below for re-protecting the edited file ///

            // Create a new file handler using the temporary file path.
            auto reprotectPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
            auto reprotectFuture = reprotectPromise->get_future();
            engine->CreateFileHandlerAsync(tempPath, tempPath, true, std::make_shared<FileHandlerObserver>(), reprotectPromise);
            auto republishHandler = reprotectFuture.get();

            // Set protection using the ProtectionHandler from the original consumption operation.
            republishHandler->SetProtection(protectionHandler);
            std::string reprotectedFilePath = "<protected-file-path>";

            // Commit changes
            auto republishPromise = std::make_shared<std::promise<bool>>();
            auto republishFuture = republishPromise->get_future();
            republishHandler->CommitAsync(reprotectedFilePath, republishPromise);

            // Validate republishing
            cout << "Protected File: " + protectedFilePath<<endl;
            cout << "Protected Label ID: " + protectedFileHandler->GetLabel()->GetLabel()->GetId() << endl;
            cout << "Protection Owner: " + protectedFileHandler->GetProtection()->GetOwner() << endl<<endl;

            cout << "Republished File: " + reprotectedFilePath<<endl;
            cout << "Republished Label ID: " + republishHandler->GetLabel()->GetLabel()->GetId() << endl;
            cout << "Republished Owner: " + republishHandler->GetProtection()->GetOwner() << endl;

        }
    ```

3. Main () の最後に向かって、前のクイックスタートで作成したアプリケーションシャットダウンブロックを見つけ、リソースを解放するために以下のハンドラー行を追加します。

    ````csharp
        protectedFileHandler = nullptr;
        protectionHandler = nullptr;

    ````

4. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | プレースホルダー | 値 |
   |:----------- |:----- |
   | \<protected-file-path\> | 前のクイックスタートから保護されたファイル。 |
   | \<reprotected-file-path\> | 再パブリッシュする変更されたファイルの出力ファイルパス。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。

1. Ctrl + Shift + B (**[ソリューションのビルド]**) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 (**[デバッグ開始]**) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireOAuth2Token()` メソッドを呼び出すたびに、アプリケーションによりアクセス トークンが求められます。 以前に "秘密ラベルの設定/取得" クイックスタートで行ったように、PowerShell スクリプトを実行して、$authority と $resourceUrl に指定された値を使用して、毎回トークンを取得します。

  ```console
    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://syncservice.o365syncservice.com/
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Sensitivity labels for your organization:
    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to C:\Test\Test.docx
    Committing changes

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Label committed to file: C:\Test\Test_labeled.docx
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Getting the label committed to file: C:\Test\Test_labeled.docx
    Name: Confidential
    Id: 074e457c-5848-4542-9a6f-34a182080e7z
    Press any key to continue . . .
    Protected File: C:\Test\Test_labeled.docx
    Protected Label ID: 074e457c-5848-4542-9a6f-34a182080e7z
    Protection Owner: user1@tenant.onmicrosoft.com

    Republished File: c:\Test\Test_republished.docx
    Republished Label ID: 074e457c-5848-4542-9a6f-34a182080e7z
    Republished Owner: user1@tenant.onmicrosoft.com

    Press any key to close this window . . .

   ```
   