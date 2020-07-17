---
title: 理由が必要なラベルをダウングレードまたは削除する方法 (C#)
description: この記事では、理由を必要とするラベルをダウングレードまたは削除する方法のシナリオについて説明します。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 88c55d973dde25e1571750e51e36f5fa726770f5
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86403223"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>Microsoft Information Protection SDK File API-ファイルの秘密度ラベルを下げるためのアクションの理由 (C#)

このクイックスタートでは、ラベルポリシーで理由が必要な場合のダウングレードラベル操作の処理について説明します。ここでは、 `IFileHandler` ファイルのラベルを変更するためにインターフェイスを使用します。 詳細については、[API リファレンス](/dotnet/api/?term=microsoft.informationprotection)に関するページを参照してください。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 完全なクイックスタート: 組織の秘密度ラベルを一覧表示したり、ファイルに対して機密ラベルを設定したり読み取りたりするためのスタート Visual Studio ソリューションを構築する、[感度ラベルを設定/取得](quick-file-set-get-label-csharp.md)します。 この「理由 C#」クイックスタートでは、前のクイックスタートを基にして、このようなラベルをダウングレードまたは削除することができます。
- 省略可能: MIP SDK の概念の[ファイル ハンドラーの概念](concept-handler-file-cpp.md)に関する記事を確認してください。

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>保護されているファイルに低いラベルを設定してロジックを追加する

ファイルハンドラーオブジェクトを使用して、ファイルに機密ラベルを設定するロジックを追加します。

1. 前の「クイックスタート: 秘密度ラベルの設定/取得 (C#)」で作成した Visual Studio ソリューションを開きます。

2. ソリューション エクスプローラーを使用して、`Main()` メソッドの実装を含む .cs ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. 前のクイックスタートからの `<label-id>` 値を、低くする理由が必要な秘密度ラベルに更新します。 このクイックスタートでは、まずこのラベルを設定し、後続の手順でコード スニペットを使用してそれを下げます。

4. 本文の末尾に向かっ `Main()` `Console.ReadKey()` て、アプリケーションのシャットダウンブロックの下 (前のクイックスタートでは、前のクイックスタートで終了したもの) の下に、次のコードを挿入します。

    ```csharp
    //Set paths and label ID
    string lowerInput = actualOutputFilePath;
    string lowerActualInput = lowerInput;
    string newLabelId = "<new-label-id>";
    string lowerOutput = "<downgraded-labled-output>";
    string lowerActualOutput = lowerOutput;

    //Create a file handler for that file
    var downgradeHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(lowerInput, lowerActualInput, true)).Result;

    //Set Labeling Options
    LabelingOptions options = new LabelingOptions()
    {
        AssignmentMethod = AssignmentMethod.Standard
    };

    try
    {
        //Try to set new label
        downgradeHandler.SetLabel(fileEngine.GetLabelById(newLabelId), options, new ProtectionSettings());
    }

    catch (Microsoft.InformationProtection.Exceptions.JustificationRequiredException)
    {
        //Request justification from user
        Console.Write("Please provide justification for downgrading a label: ");
        string justification = Console.ReadLine();

        options.IsDowngradeJustified = true;
        options.JustificationMessage = justification;

        //Set new label
        downgradeHandler.SetLabel(fileEngine.GetLabelById(newLabelId), options, new ProtectionSettings());
    }

    // Commit changes, save as outputFilePath
    var downgradedResult = Task.Run(async () => await downgradeHandler.CommitAsync(lowerActualOutput)).Result;

    // Create a new handler to read the labeled file metadata
    var commitHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(lowerOutput, lowerActualOutput, true)).Result;

    // Get the label from output file
    var newContentLabel = commitHandler.Label;
    Console.WriteLine(string.Format("Getting the new label committed to file: {0}", lowerOutput));
    Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", newContentLabel.Label.Name, newContentLabel.IsProtectionAppliedFromLabel.ToString()));
    Console.WriteLine("Press a key to continue.");
    Console.ReadKey();

    ```

5. Main () の最後に向かって、前のクイックスタートで作成したアプリケーションシャットダウンブロックを見つけ、リソースを解放するために以下のハンドラー行を追加します。

    ````csharp
    downgradeHandler = null;
    commitHandler = null;
    ````

6. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<downgraded-labled-output\> | 変更したファイルの保存先の出力ファイル パス。 |
   | \<new-label-id\> | 前のクイックスタートでコンソール出力からコピーされたテンプレート ID (例:) `bb7ed207-046a-4caf-9826-647cff56b990` 。 以前に保護していたファイル ラベルよりも秘密度が低いことを確認します。 |

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

    Getting the label committed to file: c:\Test\Test_labeled.docx
    Name: Confidential
    IsProtected: True
    Press any key to continue . . .

    Please provide justification for downgrading a label: Lower label approved.
    Getting the new label committed to file: c:\Test\Test_downgraded.docx
    File Label: General
    IsProtected: False
    Press a key to continue.
   ```

ただし、同様のアプローチは、 `DeleteLabel()` ファイルから削除されるラベルにラベルポリシーごとの理由が必要な場合にも操作に適用されることに注意してください。`DeleteLabel()` 関数は例外をスロー `JustificationRequiredException` し、 `IsDowngradeJustified` ラベルを正常に削除する前に例外処理でフラグを true に設定する必要があります。