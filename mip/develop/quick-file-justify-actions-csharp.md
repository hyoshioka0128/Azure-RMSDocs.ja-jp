---
title: '方法: 理由を必要とするラベルのダウングレードまたは削除 (C#)'
description: この記事では、理由を必要とするラベルをダウングレードまたは削除する方法のシナリオについて説明します。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 666b0c7fdbc483f638f76def37ec3082c9eb7377
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316519"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>Microsoft Information Protection SDK File API - ファイルの秘密度ラベルをダウングレードするアクションの理由 (C#)

このクイック スタートでは、理由が必要なラベル ポリシーで、ラベルのダウングレード操作を処理する方法について説明します。ここでは、ファイルのラベルの変更に `IFileHandler` インターフェイスを使用します。 詳細については、[API リファレンス](/dotnet/api/?term=microsoft.informationprotection)に関するページを参照してください。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: 秘密度ラベルの設定および取得 (C#)](quick-file-set-get-label-csharp.md)」を完了し、組織の秘密度ラベルを一覧表示し、ファイルの秘密度ラベルを設定して読み取る、スターターとなる Visual Studio ソリューションを構築します。 この「方法: 理由を必要とするラベルのダウングレードまたは削除 (C#)」クイック スタートでは、前のものを基にしています。
- 省略可能: MIP SDK の概念の[ファイル ハンドラーの概念](concept-handler-file-cpp.md)に関する記事を確認してください。

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>保護されているファイルに低いラベルを設定してロジックを追加する

ファイル ハンドラー オブジェクトを使用し、ファイルに秘密度ラベルを設定してロジックを追加できます。

1. 前の「クイック スタート: 秘密度ラベルの設定および取得 (C#)」で作成した Visual Studio ソリューションを開きます。

2. ソリューション エクスプローラーを使用して、`Main()` メソッドの実装を含む .cs ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. 前のクイックスタートからの `<label-id>` 値を、低くする理由が必要な秘密度ラベルに更新します。 このクイックスタートでは、まずこのラベルを設定し、後続の手順でコード スニペットを使用してそれを下げます。

4. `Main()` 本文の末尾の `Console.ReadKey()` の下のアプリケーション シャットダウン ブロックの上 (前のクイック スタートが終わった場所) に次のコードを挿入します。

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

5. Main() の末尾で、前のクイック スタートで作成したアプリケーション シャットダウン ブロックを探し、下のハンドラーの行を追加してリソースを解放します。

    ````csharp
    downgradeHandler = null;
    commitHandler = null;
    ````

6. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<downgraded-labled-output\> | 変更したファイルの保存先の出力ファイル パス。 |
   | \<new-label-id\> | 前のクイック スタートでコンソールの出力からコピーしたテンプレート ID (例: `bb7ed207-046a-4caf-9826-647cff56b990`)。 以前に保護していたファイル ラベルよりも秘密度が低いことを確認します。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。

1. Ctrl + Shift + B ( **[ソリューションのビルド]** ) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireToken()` メソッドを呼び出すたびに、アプリケーションから ADAL を使用した認証が求められる *場合があります*。 キャッシュされた資格情報が既に存在する場合は、サインインが求められることはなく、ラベルの一覧と、適用されたラベルおよび修正されたファイルに関する情報が表示されます。

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

なお、ファイルから削除するラベルの各ラベル ポリシーで理由が必要な場合、`DeleteLabel()` 操作にも同様のアプローチが適用されます。`DeleteLabel()` 関数では `JustificationRequiredException` 例外がスローされ、ラベルを正常に削除するには、その前に例外処理で `IsDowngradeJustified` フラグを true に設定する必要があります。