---
title: クイック スタート - C++ MIP SDK 保護 API を使用してテキストを暗号化し、復号する
description: C++ Microsoft Information Protection SDK 保護 API を使用し、保護テンプレートでアドホック テキストを暗号化し、復号する方法 (C++) について説明するクイック スタート
services: information-protection
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 1258bfcd6c47611b439a29406ed0e78b644a5803
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535843"
---
# <a name="quickstart-encryptdecrypt-text-using-mip-sdk-c"></a>クイック スタート:MIP SDK (C++) を使用して暗号化し、復号する

このクイック スタートでは、MIP 保護 API をさらに活用する方法について説明します。 前のクイック スタートで一覧に挙げた保護テンプレートの 1 つを使用し、保護ハンドラーでアドホック テキストを暗号化します。 保護ハンドラー クラスからは、保護を適用し、削除するためのさまざまな演算が公開されます。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: 保護テンプレートを一覧表示する (C++)](quick-protection-list-templates-cpp.md)」をまず完了し、認証されたユーザーが利用できる保護テンプレートを一覧表示します。これにより、スターターとなる Visual Studio ソリューションが構築されます。 この "テキストの暗号化と暗号化解除" クイック スタートは前のクイック スタートを基盤とします。
- 省略可能: 「[MIP SDK の保護ハンドラー](concept-handler-protection-cpp.md)」の概念を確認します。

## <a name="implement-an-observer-class-to-monitor-the-protection-handler-object"></a>保護ハンドラー オブジェクトを監視するためのオブザーバー クラスの実装

アプリケーションの初期化のクイック スタートで (保護プロファイルおよびエンジン用に) 実装したオブザーバーのように、ここで保護ハンドラー オブジェクト用にオブザーバー クラスを実装します。

SDK の `mip::ProtectionHandler::Observer` クラスを拡大し、保護ハンドラー オブザーバーの基本実装を作成します。 保護ハンドラーの操作を監視するために、オブザーバーはインスタンス化され、後で使用されます。

1. 前の「クイック スタート: 保護テンプレートを一覧表示する (C++)」 記事で取り組んだ Visual Studio ソリューションを開きます。

2. header/.h ファイルと implementation/.cpp ファイルの両方を作成する、新しいクラスをご自分のプロジェクトに追加します。

   - **ソリューション エクスプローラー** でもう一度プロジェクト ノードを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。
   - **[クラスの追加]** ダイアログで以下の操作を行います。
     - **[クラス名]** フィールドに「handler_observer」と入力します。 入力した名前に基づき、 **[.h file]\(.h ファイル\)** と **[.cpp file]\(.cpp ファイル\)** の両フィールドが自動入力されたことを確認してください。
     - 完了したら、 **[OK]** ボタンをクリックします。

3. クラスの .h ファイルおよび .cpp ファイルを作成すると、両ファイルは [エディター グループ] タブに表示されます。 ここで各ファイルを更新して、新しいオブザーバー クラスを実装します。

   - 生成した `handler_observer` クラスを選択および削除して、「handler_observer.h」を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除 **しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include <memory>
     #include "mip/protection/protection_engine.h"
     using std::shared_ptr;
     using std::exception_ptr;

     class ProtectionHandlerObserver final : public mip::ProtectionHandler::Observer {
          public:
          ProtectionHandlerObserver() { }
          void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
          void OnCreateProtectionHandlerFailure(const exception_ptr& Failure, const shared_ptr<void>& context) override;
          };

     ```

   - 生成した `handler_observer` クラス実装を選択および削除して、「handler_observer.cpp」を更新します。 前の手順で生成された、プリプロセッサ ディレクティブは削除 **しないでください** (#pragma、#include)。 次に、ファイルの既存の任意のプリプロセッサ ディレクティブの後に、次のソースをコピーし、貼り付けます。

     ```cpp
     #include "handler_observer.h"
     using std::shared_ptr;
     using std::promise;
     using std::exception_ptr;

     void ProtectionHandlerObserver::OnCreateProtectionHandlerSuccess(
          const shared_ptr<mip::ProtectionHandler>& protectionHandler,const shared_ptr<void>& context) {
               auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
               createProtectionHandlerPromise->set_value(protectionHandler);
               };

     void ProtectionHandlerObserver::OnCreateProtectionHandlerFailure(
          const exception_ptr& Failure, const shared_ptr<void>& context) {
               auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get())
               createProtectionHandlerPromise->set_exception(Failure);
               };

     ```

4. 必要に応じて、Ctrl+Shift+B ( **[ソリューションのビルド]** ) を使用して、続行する前にソリューションのテスト コンパイル/リンクを実行し、正しくビルドされることを確認します。

## <a name="add-logic-to-encrypt-and-decrypt-ad-hoc-text"></a>アドホック テキストを暗号化し、復号するロジックを追加する

保護エンジン オブジェクトを使用し、アドホック テキストを暗号化し、復号するロジックを追加する

1. **ソリューション エクスプローラー** を使用して、`main()` メソッドの実装を含む .cpp ファイルをプロジェクトで開きます。

2. 次の #include と using ディレクティブをファイルの上部の対応する既存のディレクティブの下に追加します。

   ```cpp
     #include "mip/protection/protection_descriptor_builder.h"
     #include "mip/protection_descriptor.h"
     #include "handler_observer.h"

     using mip::ProtectionDescriptor;
     using mip::ProtectionDescriptorBuilder;
     using mip::ProtectionHandler;
   ```

3. `Main()` 本文の末尾 (前のクイック スタートが終わった場所) に次のコードを挿入します。

   ```cpp
   //Encrypt/Decrypt text:
   string templateId = "<Template-ID>";//Template ID from previous QuickStart e.g. "bb7ed207-046a-4caf-9826-647cff56b990"
   string inputText = "<Sample-Text>";//Sample Text

   //Refer to ProtectionDescriptor docs for details on creating the descriptor
   auto descriptorBuilder = mip::ProtectionDescriptorBuilder::CreateFromTemplate(templateId);
   const std::shared_ptr<mip::ProtectionDescriptor>& descriptor = descriptorBuilder->Build();

   //Create Publishing settings using a descriptor
   mip::ProtectionHandler::PublishingSettings publishingSettings = mip::ProtectionHandler::PublishingSettings(descriptor);

   //Create a publishing protection handler using Protection Descriptor
   auto handlerObserver = std::make_shared<ProtectionHandlerObserver>();
   engine->CreateProtectionHandlerForPublishingAsync(publishingSettings, handlerObserver, pHandlerPromise);
   auto publishingHandler = pHandlerFuture.get();

   std::vector<uint8_t> inputBuffer(inputText.begin(), inputText.end());

   //Show action plan
   cout << "Applying Template ID " + templateId + " to: " << endl << inputText << endl;

   //Encrypt buffer using Publishing Handler
   std::vector<uint8_t> encryptedBuffer;
   encryptedBuffer.resize(static_cast<size_t>(publishingHandler->GetProtectedContentLength(inputText.size(), true)));

   publishingHandler->EncryptBuffer(0,
                         &inputBuffer[0],
                         static_cast<int64_t>(inputBuffer.size()),
                         &encryptedBuffer[0],
                         static_cast<int64_t>(encryptedBuffer.size()),
                         true);

   std::string encryptedText(encryptedBuffer.begin(), encryptedBuffer.end());
   cout << "Encrypted Text :" + encryptedText;

   //Show action plan
   cout << endl << "Decrypting string: " << endl << endl;

   //Generate publishing licence, so it can be used later to decrypt text.
   auto serializedPublishingLicense = publishingHandler->GetSerializedPublishingLicense();

   //Use same PL to decrypt the encryptedText.
   auto cHandlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
   auto cHandlerFuture = cHandlerPromise->get_future();
   shared_ptr<ProtectionHandlerObserver> cHandlerObserver = std::make_shared<ProtectionHandlerObserver>();

   //Create consumption settings using serialised publishing licence.
   mip::ProtectionHandler::ConsumptionSettings consumptionSettings = mip::ProtectionHandler::ConsumptionSettings(serializedPublishingLicense);
   engine->CreateProtectionHandlerForConsumptionAsync(consumptionSettings, cHandlerObserver, cHandlerPromise);

   auto consumptionHandler = cHandlerFuture.get();

   //Use consumption handler to decrypt the text.
   std::vector<uint8_t> decryptedBuffer(static_cast<size_t>(encryptedText.size()));

   int64_t decryptedSize = consumptionHandler->DecryptBuffer(
        0,
        &encryptedBuffer[0],
        static_cast<int64_t>(encryptedBuffer.size()),
        &decryptedBuffer[0],
        static_cast<int64_t>(decryptedBuffer.size()),
        true);

   decryptedBuffer.resize(static_cast<size_t>(decryptedSize));

   std::string decryptedText(decryptedBuffer.begin(), decryptedBuffer.end());

   // Output decrypted content. Should match original input text.
   cout << "Decrypted Text :" + decryptedText << endl;

   ```

4. `main()` の末尾で、最初のクイック スタートで作成したアプリケーション シャットダウンのブロックを探し、下の行を追加してハンドラー リソースを解放します。

   ```cpp
    publishingHandler = nullptr;
    consumptionHandler = nullptr;
   ```

5. ソース コードのプレースホルダー値を、次の文字列定数を使って以下のように置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<sample-text\> | 保護するサンプル テキスト (例: `"cipher text"`)。 |
   | \<Template-Id\> | テキストを保護するために使用するテンプレート ID。 例: `"bb7ed207-046a-4caf-9826-647cff56b990"` |
  
## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。

1. Ctrl+Shift+B ( **[ソリューションのビルド]** ) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireOAuth2Token()` メソッドを呼び出すたびに、アプリケーションによりアクセス トークンが求められます。 「保護テンプレートを一覧表示する」クイック スタートで前に実行したとおり、PowerShell スクリプトを実行し、$authority と $resourceUrl に指定された値を使用して、都度トークンを取得します。

   ```console
   *** Template List:
   Name: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
   Name: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
   Name: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
   Name: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
   Applying Template ID bb7ed207-046a-4caf-9826-647cff56b990 to:
   <Sample-Text>
   Encrypted Text :y¬╩$Ops7Γ╢╖¢t
   Decrypting string:

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Decrypted Text :<Sample-Text>
   C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
   To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
   Press any key to close this window . . .
   ```
