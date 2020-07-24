---
title: '方法: 理由を必要とするラベルのダウングレードまたは削除 ( C++ )'
description: この記事では、理由を必要とするラベルをダウングレードまたは削除する方法のシナリオについて説明します。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/14/2020
ms.author: v-anikep
ms.openlocfilehash: f50613340cc4c977239910d5047943d25239b1bc
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86403291"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>Microsoft Information Protection SDK File API - ファイルの秘密度ラベルを下げるアクションの理由 (C++)

このクイックスタートでは、理由が必要なラベル ポリシーで、ラベルのダウングレード操作を処理する方法について説明します。 ここでは、ファイルのラベルの変更に `mip::FileHandler` クラスを使用します。 詳細については、[API リファレンス](./reference/mip-sdk-reference.md)に関するページを参照してください。

## <a name="prerequisites"></a>[前提条件]

まだ行っていない場合、続行する前に、必ず以下の前提条件を完了してください。

- 「[クイック スタート: 秘密度ラベルの設定および取得 (C++)](quick-file-set-get-label-cpp.md)」をまず完了し、組織の秘密度ラベルを一覧表示し、ファイルの秘密度ラベルを設定して読み取る、スターターとなる Visual Studio ソリューションを構築します。 この「方法: 理由を必要とするラベルのダウングレードまたは削除 ( C++ )」クイックスタートでは、前のものを基にしています。
- 省略可能: MIP SDK の概念の[ファイル ハンドラーの概念](concept-handler-file-cpp.md)に関する記事を確認してください。

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>保護されているファイルに低いラベルを設定してロジックを追加する

`mip::FileHandler` オブジェクトを使用し、ファイルに秘密度ラベルを設定してロジックを追加できます。

1. 前の「[クイック スタート: 秘密度ラベルの設定および取得 (C++)](quick-file-set-get-label-cpp.md)」で作成した Visual Studio ソリューションを開きます。

2. ソリューション エクスプローラーを使用して、`main()` メソッドの実装を含む .cpp ファイルをご自分のプロジェクトで開きます。 これの既定の名前は、プロジェクトの作成時に指定した、それを含むプロジェクトと同じ名前です。

3. 次の #include と using ディレクティブをファイルの上部の対応する既存のディレクティブの下に追加します。

    ```cpp

        #include "mip/file/file_error.h"

        using mip::JustificationRequiredError;
        using std::cin;

    ```

4. 前のクイックスタートからの `<label-id>` 値を、低くする理由が必要な秘密度ラベルに更新します。 このクイックスタートでは、まずこのラベルを設定し、後続の手順でコード スニペットを使用してそれを下げます。

5. `main()` 本文の末尾の `system("pause");` の下のシャットダウン ブロックの上 (前のクイック スタートが終わった場所) に次のコードを挿入します。

```cpp

// Downgrade label
// Set paths and lower label ID
// Set a new label on input file.

string lowerlabelId = "<lower-label-id>";
cout << "\nApplying new Label ID " << lowerlabelId << " to " << filePathOut << endl;
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);

// Try to apply a label with lower sensitivity.
try
{
    handler->SetLabel(engine->GetLabelById(lowerlabelId), labelingOptions, mip::ProtectionSettings());
}

catch (const mip::JustificationRequiredError& e)
{
    // Request justification from user.
    cout<<"Please provide justification for downgrading a label: "<<endl;
    string justification;
    cin >> justification;

    // Set Justification provided flag
    bool isDowngradeJustified = true;
    mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);
    labelingOptions.SetDowngradeJustification(isDowngradeJustified,justification);

    //Set new label.
    handler->SetLabel(engine->GetLabelById(lowerlabelId), labelingOptions, mip::ProtectionSettings());
}

catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}

// Commit changes, save as a different output file
string lowerFilePathOut = "<lower-output-file-path>";
try
{
    cout << "Committing changes" << endl;
    auto commitPromise = std::make_shared<std::promise<bool>>();
    auto commitFuture = commitPromise->get_future();
    handler->CommitAsync(lowerFilePathOut, commitPromise);
    if (commitFuture.get()) {
        cout << "\nLabel committed to file: " << lowerFilePathOut << endl;
    }
    else {
        cout << "Failed to label: " + lowerFilePathOut << endl;
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
string lowerActualFilePath = "<lower-content-identifier>";
try
{
    auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto handlerFuture = handlerPromise->get_future();
    engine->CreateFileHandlerAsync(
        lowerFilePathOut,
        lowerActualFilePath,
        true,
        std::make_shared<FileHandlerObserver>(),
        handlerPromise);

    handler = handlerFuture.get();
}
catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid output file path?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}

// Get the lowered label from output file
try
{
    cout << "\nGetting the label committed to file: " << lowerFilePathOut << endl;
    auto lowerLabel = handler->GetLabel();
    cout << "Name: " + lowerLabel->GetLabel()->GetName() << endl;
    cout << "Id: " + lowerLabel->GetLabel()->GetId() << endl;
}
catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}
system("pause");

```

6. ソース コードのプレースホルダー値を、次の値を使って置き換えます。

   | [プレースホルダ] | 値 |
   |:----------- |:----- |
   | \<lower-label-id\> | 前のクイック スタートでコンソールの出力からコピーしたラベル ID。たとえば、`bb7ed207-046a-4caf-9826-647cff56b990`。 以前に保護していたファイル ラベルよりも秘密度が低いことを確認します。 |
   | \<lower-output-file-path\> | 変更したファイルの保存先の出力ファイル パス。 |
   | \<lower-content-identifier\> | コンテンツに対する人間が判読できる識別子。 |

## <a name="build-and-test-the-application"></a>アプリケーションの構築とテスト

クライアント アプリケーションを構築してテストします。

1. Ctrl + Shift + B ( **[ソリューションのビルド]** ) キーを使用して、クライアント アプリケーションを構築します。 ビルド エラーがない場合、F5 ( **[デバッグ開始]** ) を使用してアプリケーションを実行します。

2. プロジェクトが構築され、正しく実行されたら、SDK が `AcquireOAuth2Token()` メソッドを呼び出すたびに、アプリケーションによりアクセス トークンが求められます。 「秘密度ラベルの設定および取得」クイック スタートで前に実行したとおり、ご自分の PowerShell スクリプトを実行し、$authority と $resourceUrl に指定された値を使用して、都度トークンを取得します。

  ```console
    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://syncservice.o365syncservice.com/
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID f55c2dea-db0f-47cd-8520-a52e1590fb6z to c:\Test\Test.docx
    Committing changes

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Label committed to file: c:\Test\Test.docx
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Getting the label committed to file: c:\Test\Test_labeled.docx
    Name: Highly Confidential
    Id: f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying new Label ID f42a3342-8706-4288-bd31-ebb85995028z to c:\Test\Test_labeled.docx
    Please provide justification for downgrading a label:
    Need for sharing with wider audience.
    Committing changes

    Label committed to file: c:\Test\Test_downgraded.docx
    Press any key to continue . . .

    Getting the label committed to file: c:\Test\Test_downgraded.docx
    Name: General
    Id: f42a3342-8706-4288-bd31-ebb85995028z
    Press any key to continue . . .
   ```

なお、ファイルから削除するラベルの各ラベル ポリシーで理由が必要な場合、`DeleteLabel()` 操作で同様のアプローチをとる必要があります。`DeleteLabel()` 関数は、`mip::JustificationRequiredError` の例外をスローします。 ラベルを正常に削除するには、その前に例外処理で `isDowngradeJustified` フラグを true に設定する必要があります。