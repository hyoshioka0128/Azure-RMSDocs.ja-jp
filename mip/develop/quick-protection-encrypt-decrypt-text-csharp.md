---
title: クイック スタート - C# MIP SDK 保護 API を使用してテキストを暗号化し、復号する
description: Microsoft Information Protection SDK .NET ラッパーを使用し、保護テンプレートでアドホック テキストを暗号化し、復号する方法について説明するクイック スタート。
services: information-protection
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.custom: has-adal-ref
ms.openlocfilehash: 85c3575aad9315155b2fbfaad991e586435edb37
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82972154"
---
# <a name="quickstart-encryptdecrypt-text-using-mip-sdk-c"></a>クイック スタート:MIP SDK (C#) を使用して暗号化し、復号する

このクイック スタートでは、MIP 保護 API をさらに活用する方法について説明します。 前のクイック スタートで一覧に挙げた保護テンプレートの 1 つを使用し、保護ハンドラーでアドホック テキストを暗号化します。 保護ハンドラー クラスからは、保護を適用し、削除するためのさまざまな演算が公開されます。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: 保護テンプレートを一覧表示する (C#)](quick-protection-list-templates-csharp.md)」をまず完了し、認証されたユーザーが利用できる保護テンプレートを一覧表示します。これにより、スターターとなる Visual Studio ソリューションが構築されます。 この "テキストの暗号化と暗号化解除" クイック スタートは前のクイック スタートを基盤とします。
- 省略可能: 「[MIP SDK の保護ハンドラー](concept-handler-protection-cpp.md)」の概念を確認します。

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>機密ラベルを設定および取得するためのロジックの追加

保護エンジン オブジェクトを使用し、アドホック テキストを暗号化するロジックを追加する

1. **ソリューション エクスプローラー**を使用して、Main()` メソッドの実装を含む .cs ファイルをプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

2. `Main()` 本文の末尾 (前のクイック スタートが終わった場所) に次のコードを挿入します。

   ```csharp
   //Set text to encrypt and template ID
   string inputText = "<Sample-text>";
   string templateId = "<template-id>";
   //Create a template based publishing descriptor
   ProtectionDescriptor protectionDescriptor = new ProtectionDescriptor(templateId);

   //Create publishing settings using protection descriptor
   PublishingSettings publishingSettings = new PublishingSettings(protectionDescriptor);

   //Generate Protection Handler for publishing
   var publishingHandler = Task.Run(async() => await protectionEngine.CreateProtectionHandlerForPublishingAsync(publishingSettings)).Result;

   //Encrypt text using Publishing handler
   long bufferSize = publishingHandler.GetProtectedContentLength(inputText.Length, true);
   byte[] inputTextBuffer = Encoding.ASCII.GetBytes(inputText);
   byte[] encryptedTextBuffer = new byte[bufferSize];
   publishingHandler.EncryptBuffer(0, inputTextBuffer, encryptedTextBuffer, true);
   Console.WriteLine("Original text: {0}", inputText);
   Console.WriteLine("Encrypted text: {0}", Encoding.UTF8.GetString(encryptedTextBuffer));

   //Create a Protection handler for consumption using the same publishing licence
   var serializedPublishingLicense = publishingHandler.GetSerializedPublishingLicense();
   PublishingLicenseInfo plInfo = PublishingLicenseInfo.GetPublishingLicenseInfo(serializedPublishingLicense);
   ConsumptionSettings consumptionSettings = new ConsumptionSettings(plInfo);
   var consumptionHandler = protectionEngine.CreateProtectionHandlerForConsumption(consumptionSettings);

   //Use the handler to decrypt the encrypted text
   long buffersize = encryptedTextBuffer.Length;
   byte[] decryptedBuffer = new byte[bufferSize];
   var bytesDecrypted = consumptionHandler.DecryptBuffer(0, encryptedTextBuffer, decryptedBuffer, true);
   byte[] OutputBuffer = new byte[bytesDecrypted];
   for (int i = 0; i < bytesDecrypted; i++){
      OutputBuffer[i] = decryptedBuffer[i];
   }

   Console.WriteLine("Decrypted content: {0}", Encoding.UTF8.GetString(OutputBuffer));
   Console.WriteLine("Press a key to quit.");
   Console.ReadKey();

   ```

3. `Main()` の末尾で、最初のクイック スタートで作成したアプリケーション シャットダウンのブロックを探し、ハンドラーの行を追加します。

   ```csharp
   // Application Shutdown
   publishingHandler = null;
   consumptionHandler = null;
   protectionEngine = null;
   protectionProfile = null;
   mipContext = null;
   ```

4. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<sample-text\> | 暗号化するサンプル テキスト (例: `My secure text`)。 |
   | \<template-id\> | 前のクイック スタートでコンソールの出力からコピーしたテンプレート ID (例: `bb7ed207-046a-4caf-9826-647cff56b990`)。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。

1. Ctrl + Shift + B ( **[ソリューションのビルド]** ) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireToken()` メソッドを呼び出すたびに、アプリケーションから ADAL を使用した認証が求められる*場合があります*。 キャッシュされた資格情報が既に存在する場合は、サインインが求められることはなく、ラベルの一覧と、適用されたラベルおよび修正されたファイルに関する情報が表示されます。

  ```console
   Original content: My secure text
   Encrypted content: c?_hp???Q??+<?
   Decrypted content: My secure text
   Press a key to quit.
   ```
