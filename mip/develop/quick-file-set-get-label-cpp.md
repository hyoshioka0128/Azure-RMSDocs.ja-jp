---
title: クイック スタート - C++ MIP SDK を使用したファイルの機密ラベルの設定および取得
description: Microsoft Information Protection C++ SDK を使用して、ファイルに機密ラベルを設定および取得する方法を説明するクイック スタート。
services: information-protection
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 651fc73c00f18d06ad1a824337a096331bc7e897
ms.sourcegitcommit: d677088db8588fb2cc4a5d7dd296e76d0d9a2e9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251745"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>クイック スタート: 機密ラベルの設定および取得 (C++)

このクイック スタートでは、MIP File API をさらに活用する方法について説明します。 前のクイック スタートで列挙した機密ラベルの 1 つを使用して、ファイル ハンドラーを使用し、ファイルのラベルを設定および取得します。 ファイル ハンドラー クラスでは、ラベルの設定および取得操作、またはサポートされている種類のファイルの保護のさまざまな操作を公開しています。

## <a name="prerequisites"></a>必要条件

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: 機密ラベルの列挙 (C++)](quick-file-list-labels-cpp.md)」をまず完了し、組織の機密ラベルを列挙するスターター Visual Studio ソリューションを構築します。 この「機密ラベルの設定および取得」クイック スタートは、前のものに基づいて進められます。
- オプションで「[File handlers in the MIP SDK](concept-handler-file-cpp.md)」 (MIP SDK のファイル ハンドラー) の概念を確認してください。

## <a name="implement-an-observer-class-to-monitor-the-file-handler-object"></a>ファイル ハンドラー オブジェクトを監視するためのオブザーバー クラスの実装

アプリケーションの初期化のクイック スタートで (ファイル プロファイルおよびエンジン用に) 実装したオブザーバーのように、ここでファイル ハンドラー オブジェクト用にオブザーバー クラスを実装します。

SDK の `mip::FileHandler::Observer` クラスを拡大し、オブザーバー クラスの基本の実装を作成します。 ファイル ハンドラーの操作を監視するために、オブザーバーはインスタンス化され、後で使用されます。

1. 前の「クイック スタート: 機密ラベルの列挙 (C++)」の記事で使用した Visual Studio ソリューションを開きます。

2. header/.h ファイルと implementation/.cpp ファイルの両方を作成する、新しいクラスをご自分のプロジェクトに追加します。

   - **ソリューション エクスプローラー**でもう一度プロジェクト ノードを右クリックし、**[追加]**、**[クラス]** の順に選択します。
   - **[クラスの追加]** ダイアログで以下の操作を行います。
     - **[クラス名]** フィールドに「filehandler_observer」と入力します。 入力した名前に基づき、**[.h file]\(.h ファイル\)** と **[.cpp file]\(.cpp ファイル\)** の両フィールドが自動入力されたことを確認してください。
     - 完了したら、**[OK]** ボタンをクリックします。

3. クラスの .h ファイルおよび .cpp ファイルを作成すると、両ファイルは [エディター グループ] タブに表示されます。 ここで各ファイルを更新して、新しいオブザーバー クラスを実装します。

   - 生成した `filehandler_observer` クラスを選択および削除して、「filehandler_observer.h」を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include <memory>
     #include "mip/file/file_engine.h"
     #include "mip/file/file_handler.h"

     class FileHandlerObserver final : public mip::FileHandler::Observer {
     public:
        FileHandlerObserver() { }
        // Observer implementation
        void OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) override;
        void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
        void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) override;
        void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;       
     };
     ```

   - 生成した `filehandler_observer` クラス実装を選択および削除して、「filehandler_observer.cpp」を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除**しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_value(fileHandler);
     }

     void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_exception(error);
     }

     void FileHandlerObserver::OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_value(committed);
     }

     void FileHandlerObserver::OnCommitFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_exception(error);
     }
     ```

4. 必要に応じて、F6 (**[ソリューションのビルド]**) を使用して、続行する前にソリューションのテスト コンパイル/リンクを実行し、正しくビルドされることを確認します。

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>機密ラベルを設定および取得するためのロジックの追加

ファイル エンジン オブジェクトを使用し、ファイルに機密ラベルを設定および取得するためのロジックを追加します。 

1. **ソリューション エクスプローラー**を使用して、`main()` メソッドの実装を含む .cpp ファイルをプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。 

2. 次の `#include` と `using` ディレクティブをファイルの上部の対応する既存のディレクティブの下に追加します。

   ```cpp
   #include "filehandler_observer.h" 
   #include "mip/file/file_handler.h" 

   using mip::FileHandler;
   ```
3. `main()` 本文の末尾の `system("pause");` の下の `return 0;` の上 (前のクイック スタートが終わった場所) に次のコードを挿入します。

   ```cpp
   // Set up async FileHandler for input file operations
   string filePathIn = "<input-file-path>";
   std::shared_ptr<FileHandler> handler;
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(filePathIn, mip::ContentState::REST, std::make_shared<FileHandlerObserver>(), handlerPromise);
        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid input file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Set a label on input file
   try
   {
        string labelId = "<label-id>";
        cout << "\nApplying Label ID " << labelId << " to " << filePathIn << endl;
        mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED, mip::ActionSource::MANUAL);
        handler->SetLabel(labelId, labelingOptions);
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Commit changes, save as a different/output file
   string filePathOut = "<output-file-path>";
   try
   {
        cout << "Committing changes" << endl;
        auto commitPromise = std::make_shared<std::promise<bool>>();
        auto commitFuture = commitPromise->get_future();
        handler->CommitAsync(filePathOut, commitPromise);
        if (commitFuture.get()) {
            cout << "\nLabel committed to file: " << filePathOut << endl;
        }
        else {
            cout << "Failed to label: " + filePathOut << endl;
            return 1;
        }
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid commit file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");

   // Set up async FileHandler for output file operations
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(filePathOut, mip::ContentState::REST, std::make_shared<FileHandlerObserver>(), handlerPromise);
        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid output file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Get the label from output file
   try
   {
        cout << "\nGetting the label committed to file: " << filePathOut << endl;
        auto label = handler->GetLabel();
        cout << "Name: " + label->GetLabel()->GetName() << endl;
        cout << "Id: " + label->GetLabel()->GetId() << endl;
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");
   ```

4. 貼り付けたばかりのソース コードのプレースホルダー値を、次の値で置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<input-file-path\> | テスト入力ファイルへの完全なパス。たとえば `c:\\Test\\Test.docx`。 |
   | \<label-id\> | 前のクイック スタートでコンソールの出力からコピーした機密ラベル ID。たとえば `f42a3342-8706-4288-bd31-ebb85995028z`。 |
   | \<output-file-path\> | 入力ファイルのラベル付きコピーである出力ファイルへの完全なパス。たとえば、`c:\\Test\\Test_labeled.docx`。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。 

1. F6 (**[ソリューションのビルド]**) を使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 (**[デバッグ開始]**) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireOAuth2Token()` メソッドを呼び出すたびに、アプリケーションによりアクセス トークンが求められます。 「機密ラベルの列挙」クイック スタートで前に実行したとおり、PowerShell スクリプトを実行して、指定された値を使用して、都度トークンを取得します。 `AcquireOAuth2Token()` は、要求された機関とリソースが同じである場合、以前に生成されたトークンの使用を試みます。

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
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

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

ラベルのアプリケーションは、出力ファイルを開き、ドキュメントの情報保護設定を目で確認して確認できます。

> [!NOTE]
> Office ドキュメントをラベル付けする場合で、アクセス トークンを取得済み (および機密ラベルが構成済み) の Azure Active Directory (AD) テナントのアカウントを使用してサインインしていないときは、ラベル付きのドキュメントを開く前にサインインを求められることがあります。 



