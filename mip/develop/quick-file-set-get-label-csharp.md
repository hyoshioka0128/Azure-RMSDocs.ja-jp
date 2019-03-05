---
title: クイック スタート - 設定および取得を使用してファイルの機密ラベル、 C# MIP SDK
description: Microsoft の情報保護 SDK .NET ラッパーを使用して設定およびファイルの機密ラベルを取得する方法を示すクイック スタートです。
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/09/2019
ms.author: mbaldwin
ms.openlocfilehash: 3ee178c493b99cfecd3f6cd04a680f47acf45412
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333249"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>クイック スタート:設定し、機密ラベルを取得 (C#)

このクイック スタートでは、MIP File API をさらに活用する方法について説明します。 前のクイック スタートで列挙した機密ラベルの 1 つを使用して、ファイル ハンドラーを使用し、ファイルのラベルを設定および取得します。 ファイル ハンドラー クラスでは、ラベルの設定および取得操作、またはサポートされている種類のファイルの保護のさまざまな操作を公開しています。

## <a name="prerequisites"></a>前提条件

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 完全な[クイック スタート。機密ラベルを一覧表示 (C#)](quick-file-list-labels-csharp.md) 1 つは、組織の機密ラベルを一覧表示するスターター Visual Studio のソリューションをビルドします。 この「機密ラベルの設定および取得」クイック スタートは、前のものに基づいて進められます。
- 必要に応じて、次の操作を行います。レビュー [MIP SDK ファイル ハンドラー](concept-handler-file-cpp.md)概念です。

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>機密ラベルを設定および取得するためのロジックの追加

ファイル エンジン オブジェクトを使用し、ファイルに機密ラベルを設定および取得するためのロジックを追加します。 

1. 使用して**ソリューション エクスプ ローラー**Main() の実装を含むプロジェクトの .cs ファイルを開きます ' メソッド。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。 

2. `Main()` 本文の末尾の `Console.ReadKey()` の下の `}` の上 (前のクイック スタートが終わった場所) に次のコードを挿入します。

   ```csharp
     //Set paths and label ID
     string inputFilePath = "<input-file-path>";
     string labelId = "<label-id>";
     string outputFilePath = "<output-file-path>";

     //Create a file handler for that file
     //Note: the 2nd inputFilePath is used to provide a human-readable content identifier for admin auditing. 
     var handler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, inputFilePath, ContentState.Rest, true)).Result;

     //Set Labeling Options
     LabelingOptions labelingOptions = new LabelingOptions()
     {
          ActionSource = ActionSource.Manual,
          AssignmentMethod = AssignmentMethod.Standard
     };

     // Set a label on input file
     handler.SetLabel(labelId, labelingOptions);

     // Commit changes, save as outputFilePath
     var result = Task.Run(async () => await handler.CommitAsync(outputFilePath)).Result;

     // Create a new handler to read the labeled file metadata
     var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, outputFilePath, ContentState.Rest, true)).Result;

     // Get the label from output file
     var contentLabel = handlerModified.Label;
     Console.WriteLine(string.Format("Getting the label committed to file: {0}", outputFilePath));
     Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", contentLabel.Label, contentLabel.IsProtectionAppliedFromLabel.ToString()));
     Console.WriteLine("Press a key to continue.");
     Console.ReadKey();
   ```

3. 貼り付けたばかりのソース コードのプレースホルダー値を、次の値で置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<input-file-path\> | テスト入力ファイルへの完全なパス。たとえば `c:\\Test\\Test.docx`。 |
   | \<label-id\> | 前のクイック スタートでコンソールの出力からコピーした機密ラベル ID。たとえば `f42a3342-8706-4288-bd31-ebb85995028z`。 |
   | \<output-file-path\> | 入力ファイルのラベル付きコピーである出力ファイルへの完全なパス。たとえば、`c:\\Test\\Test_labeled.docx`。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。 

1. CTRL + SHIFT+B を使用して (**ソリューションのビルド**) クライアント アプリケーションをビルドします。 ビルド エラーがない場合、F5 (**[デバッグ開始]**) を使用してアプリケーションを実行します。

2. プロジェクトがビルドされ、アプリケーションで実行が成功したかどうかは*可能性があります*各 ADAL 経由での認証用プロンプトが SDK の呼び出しを時間、`AcquireToken()`メソッド。 キャッシュされた資格情報が既に存在する場合は、後で適用されたラベル情報、およびファイルを変更するにログオンし、ラベルの一覧を参照してください。 は求められません。

  ```console   
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes
   
   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .
  
   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

ラベルのアプリケーションは、出力ファイルを開き、ドキュメントの情報保護設定を目で確認して確認できます。

> [!NOTE]
> Office ドキュメントをラベル付けする場合で、アクセス トークンを取得済み (および機密ラベルが構成済み) の Azure Active Directory (AD) テナントのアカウントを使用してサインインしていないときは、ラベル付きのドキュメントを開く前にサインインを求められることがあります。 
