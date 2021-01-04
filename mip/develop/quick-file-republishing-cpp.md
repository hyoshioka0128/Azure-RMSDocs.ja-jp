---
title: 方法 - 再発行のシナリオ (C++)
description: この記事は、シナリオの再発行に保護ハンドラーを再利用する方法 (C++) のシナリオを理解するうえで役立ちます。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: e71b4c59c15f0c4435f72187006de1ecdc2bffb2
ms.sourcegitcommit: 437057990372948c9435b620052a7398360264b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2020
ms.locfileid: "97701749"
---
# <a name="file-api-re-publishing-quickstart-c"></a>ファイル API の再発行に関するクイックスタート (C++)

## <a name="overview"></a>概要

このシナリオの概要とそれを使用する場面については、[MIP SDK での再発行](concept-republishing.md)に関する記事を参照してください。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: 秘密度ラベルの設定および取得 (C++)](quick-file-set-get-label-cpp.md)」をまず完了し、組織の秘密度ラベルを一覧表示し、ファイルの秘密度ラベルを設定して読み取る、スターターとなる Visual Studio ソリューションを構築します。 この「方法: 理由を必要とするラベルのダウングレードまたは削除 (C++)」クイックスタートでは、前のものを基にしています。
- 省略可能: MIP SDK の[ファイル ハンドラー](concept-handler-file-cpp.md)の概念を確認します。
- 省略可能: MIP SDK の[保護ハンドラー](concept-handler-protection-cpp.md)の概念を確認します。

## <a name="add-logic-to-filehandler-observer-class"></a>FileHandler Observer クラスにロジックを追加する

`mip::FileHandler` によって公開されている `GetDecryptedTemporaryFileAsync()` メソッドを使用して、保護されたファイルの暗号化解除を使用できるようにするには、成功と失敗の非同期メソッドのコールバックを次のように定義する必要があります。

1. 前の「クイック スタート: 秘密度ラベルの設定および取得 (C++)」を開きます。

2. ソリューション エクスプローラーを使用して、プロジェクトの `filehandler_observer.h` ファイルを開きます。 FileHandler 定義の末尾の近くにある `};` の前に、メソッド宣言の以下の行を追加します。

    ```cpp
        void OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) override;
        void OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
    ```

3. ソリューション エクスプローラーを使用して、プロジェクトの `filehandler_observer.cpp` ファイルを開きます。 ファイルの末尾の近くに、メソッド定義の以下の行を追加します。

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

1. ソリューション エクスプローラーを使用して、`main()` メソッドの実装を含む .cpp ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. main() 本文の末尾の近くにある system ("pause") の下、return 0 の上 (前のクイックスタートで中断したところ) に次のコードを挿入します。

```cpp
//Originally protected file's path.
std::string protectedFilePath = "<protected-file-path>";

// Create file handler for the file
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
auto handlerFuture = handlerPromise->get_future();
engine->CreateFileHandlerAsync(protectedFilePath, 
                                protectedFilePath, 
                                true, 
                                std::make_shared<FileHandlerObserver>(), 
                                handlerPromise);
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
    engine->CreateFileHandlerAsync(tempPath, 
                                    tempPath, 
                                    true, 
                                    std::make_shared<FileHandlerObserver>(), 
                                    reprotectPromise);
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

3. Main() の末尾の近くで、前のクイックスタートで作成したアプリケーション シャットダウン ブロックを探し、下のハンドラーの行を追加してリソースを解放します。

    ````csharp
        protectedFileHandler = nullptr;
        protectionHandler = nullptr;

    ````

4. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<protected-file-path\> | 前のクイックスタートの保護されたファイル。 |
   | \<reprotected-file-path\> | 再発行する修正されたファイルの出力ファイル パス。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。

1. Ctrl + Shift + B ( **[ソリューションのビルド]** ) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireOAuth2Token()` メソッドを呼び出すたびに、アプリケーションによりアクセス トークンが求められます。 「秘密度ラベルの設定および取得」クイックスタートで前に実行したとおり、ご自分の PowerShell スクリプトを実行し、$authority と $resourceUrl に指定された値を使用して、都度トークンを取得します。

  ```console   
    Sensitivity labels for your organization:
    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to C:\Test\Test.docx
    Committing changes
    
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
   