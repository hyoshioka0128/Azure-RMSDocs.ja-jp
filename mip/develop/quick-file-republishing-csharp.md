---
title: '方法: シナリオ C を再発行する#'
description: この記事は、再パブリッシュのシナリオで保護ハンドラーを再利用する方法のシナリオを理解するのに役立ちます。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 2b6e0b866144c4883ece29936c1a23cc946c5976
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86403342"
---
# <a name="microsoft-information-protection-sdk---file-api-republishing-quickstart-c"></a>Microsoft Information Protection SDK-ファイル API の再パブリッシュのクイックスタート (C#)

## <a name="overview"></a>概要

このシナリオの概要と使用される場所については、「 [MIP SDK での再パブリッシュ」](concept-republishing.md)を参照してください。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 完全な[クイックスタート: "秘密度ラベルを設定/取得する (C#)](quick-file-set-get-label-csharp.md) first": 最初に、Visual Studio のスタートボタンを構築します。これにより、組織の秘密度ラベルの一覧が作成され、ファイルに対して機密ラベルを設定して読み取ることができます。 この「保護されたファイルを再発行する方法-C#」は、前のクイックスタートで作成したものです。
- 必要に応じて、MIP SDK の概念の[ファイルハンドラー](concept-handler-file-cpp.md)を確認します。
- 必要に応じて、MIP SDK の概念で[保護ハンドラー](concept-handler-protection-cpp.md)をレビューします。

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>保護されたファイルを編集して再発行するためのロジックを追加する

1. 前の「クイックスタート: 秘密ラベルの設定/取得 (C#)」で作成した Visual Studio ソリューションを開きます。

2. ソリューション エクスプローラーを使用して、`Main()` メソッドの実装を含む .cs ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. 本文の末尾に向かっ `Main()` `Console.ReadKey()` て、アプリケーションのシャットダウンブロックの下 (前のクイックスタートでは、前のクイックスタートで終了したもの) の下に、次のコードを挿入します。

```csharp
string protectedFilePath = "<protected-file-path>" // Originally protected file's path from previous quickstart.

//Create a fileHandler for consumption for the Protected File.
var protectedFileHandler = Task.Run(async () => 
                            await fileEngine.CreateFileHandlerAsync(protectedFilePath,// inputFilePath
                                                                    protectedFilePath,// actualFilePath
                                                                    false, //isAuditDiscoveryEnabled
                                                                    null)).Result; // fileExecutionState

// Store protection handler from file
var protectionHandler = protectedFileHandler.Protection;

//Check if the user has the 'Edit' right to the file
if (protectionHandler.AccessCheck("Edit"))
{
    // Decrypt file to temp path
    var tempPath = Task.Run(async () => await protectedFileHandler.GetDecryptedTemporaryFileAsync()).Result;

    /*
        Your own application code to edit the decrypted file belongs here. 
    */

    /// Follow steps below for re-protecting the edited file. ///
    // Create a new file handler using the temporary file path.
    var republishHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(tempPath, tempPath, false)).Result;

    // Set protection using the ProtectionHandler from the original consumption operation.
    republishHandler.SetProtection(protectionHandler);

    // New file path to save the edited file
    string reprotectedFilePath = "<reprotected-file-path>" // New file path for saving reprotected file.

    // Write changes
    var reprotectedResult = Task.Run(async () => await republishHandler.CommitAsync(reprotectedFilePath)).Result;

    var protectedLabel = protectedFileHandler.Label;
    Console.WriteLine(string.Format("Originally protected file: {0}", protectedFilePath));
    Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", 
                        protectedLabel.Label.Id, 
                        protectedFileHandler.Protection.Owner, 
                        protectedLabel.IsProtectionAppliedFromLabel.ToString()));
    var reprotectedLabel = republishHandler.Label;
    Console.WriteLine(string.Format("Reprotected file: {0}", reprotectedFilePath));
    Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", 
                        reprotectedLabel.Label.Id, 
                        republishHandler.Protection.Owner, 
                        reprotectedLabel.IsProtectionAppliedFromLabel.ToString()));
    Console.WriteLine("Press a key to continue.");
    Console.ReadKey();
}
```

4. Main () の最後に向かって、前のクイックスタートで作成したアプリケーションシャットダウンブロックを見つけ、リソースを解放するために以下のハンドラー行を追加します。

    ````csharp
        protectedFileHandler = null;
        protectionHandler = null;
    ````

5. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<protected-file-path\> | 前のクイックスタートから保護されたファイル。 |
   | \<reprotected-file-path\> | 再パブリッシュする変更されたファイルの出力ファイルパス。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。

1. Ctrl + Shift + B ( **[ソリューションのビルド]** ) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireToken()` メソッドを呼び出すたびに、アプリケーションから ADAL を使用した認証が求められる*場合があります*。 キャッシュされた資格情報が既に存在する場合は、サインインが求められることはなく、ラベルの一覧と、適用されたラベルおよび修正されたファイルに関する情報が表示されます。

  ```console
    Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
    Public : 73254501-3d5b-4426-979a-657881dfcb1e
    General : da480625-e536-430a-9a9e-028d16a29c59
    Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
    Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
    Press a key to continue.

    Getting the label committed to file: C:\Test\Test_protected.docx
    File Label: Confidential
    IsProtected: True
    Press a key to continue.
    Originally protected file: C:\Test\Test_protected.docx
    File LabelID: 569af77e-61ea-4deb-b7e6-79dc73653959
    ProtectionOwner: User1@Contoso.OnMicrosoft.com
    IsProtected: True
    Reprotected file: C:\Test\Test_reprotected.docx
    File LabelID: 569af77e-61ea-4deb-b7e6-79dc73653959
    ProtectionOwner: User1@Contoso.OnMicrosoft.com
    IsProtected: True
    Press a key to continue.
   ```