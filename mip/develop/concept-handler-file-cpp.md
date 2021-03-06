---
title: 概念 - MIP SDK のファイル ハンドラー。
description: この記事は、ファイル API ハンドラーがどのように作成され、操作を呼び出すためにどのように使用されるかを理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 7e436d27ae48ee6d3589faaf55943b8ffd314450
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175978"
---
# <a name="microsoft-information-protection-sdk---file-handler-concepts"></a>Microsoft Information Protection SDK - ファイル ハンドラーの概念

MIP SDK ファイル API では、`mip::FileHandler` によって、さまざまな操作がすべて示されます。これらの操作は、サポートが組み込まれている種類の一連のファイル全体で、ラベル (つまり、保護) の読み取りと書き込みのために使用できます。 

## <a name="supported-file-types"></a>サポートされているファイルの種類

- OCP に基づく Office ファイル形式 (Office 2010 以降)
- 従来の Office ファイル形式 (Office 2007)
- PDF
- 一般的な PFILE のサポート
- Adobe XMP をサポートするファイル

## <a name="file-handler-functions"></a>ファイル ハンドラー関数

`mip::FileHandler` では、ラベルと保護情報の両方を読み取り、書き込み、および削除するためのメソッドが示されます。 完全な一覧については、[API リファレンス](reference/class_mip_filehandler.md)を参照してください。

この記事では、次のメソッドについて説明します。

- `GetLabelAsync()`
- `SetLabel()`
- `DeleteLabel()`
- `CommitAsync()`

## <a name="requirements"></a>必要条件

特定のファイルを操作するための `FileHandler` を作成するには、以下のものが必要です。

- `FileProfile`
- `FileProfile` に追加された `FileEngine`
- `mip::FileHandler::Observer` を継承するクラス

## <a name="create-a-file-handler"></a>ファイル ハンドラーを作成する

ファイル API でファイルを管理するために必要な最初の手順は、`FileHandler` オブジェクトの作成です。 このクラスでは、ファイルの取得、設定、更新、削除、およびファイルに対するラベル変更のコミットに必要なすべての機能が実装されます。

`FileHandler` の作成は、promise/future パターンを使用して `FileEngine` の `CreateFileHandlerAsync` 関数を呼び出すのと同じくらい簡単です。

`CreateFileHandlerAsync` 次の 3 つのパラメーターを受け取ります。読み取りまたは変更する必要がありますファイルへのパス、`mip::FileHandler::Observer`非同期イベントの通知との約束、`FileHandler`します。

**注:**`mip::FileHandler::Observer` クラスは派生クラスで実装する必要があります。これは、`CreateFileHandler` に `Observer` オブジェクトが必要であるためです。 

```cpp
auto createFileHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::FileHandler>>>();
auto createFileHandlerFuture = createFileHandlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(filePath, std::make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = createFileHandlerFuture.get();
```

`FileHandler` オブジェクトが正常に作成されたら、ファイル操作 (取得/設定/削除/コミット) を行うことができます。

## <a name="read-a-label"></a>ラベルを読み取る

### <a name="metadata-requirements"></a>メタデータの要件

ファイルからメタデータを正常に読み取り、アプリケーションで使用できるように変換するには、いくつかの要件があります。

- 読み取られるラベルは、O365 サービスにまだ存在している必要があります。 完全に削除された場合、SDK では、そのラベルに関する情報を取得できず、エラーが返されます。
- ファイル メタデータはそのままにしておく必要があります。 このメタデータには以下のものが含まれます。
  - Attribute1
  - Attribute2

### <a name="getlabelasync"></a>GetLabelAsync()

特定のファイルを指すハンドラーを作成したため、ラベルを非同期的に読み取るための promise/future パターンに戻ります。 promise は、適用されたラベルに関するすべての情報を含む `mip::ContentLabel` オブジェクトのためのものです。

`promise` オブジェクトと `future` オブジェクトをインスタンス化した後、`handler->GetLabelAsync()` を呼び出して、唯一のパラメーターとして `promise` を指定し、ラベルを読み取ります。 最後に、ラベルを `mip::ContentLabel` オブジェクトに格納できます。このオブジェクトは `future` から取得します。

```cpp
auto loadPromise = std::make_shared<std::promise<std::shared_ptr<mip::ContentLabel>>>();
auto loadFuture = loadPromise->get_future();
handler->GetLabelAsync(loadPromise);
auto label = loadFuture.get();
```

ラベル データは `label` オブジェクトから読み取ることができ、アプリケーションの他のコンポーネントまたは機能に渡すことができます。

***

## <a name="set-a-label"></a>ラベルを設定する

ラベルの設定は、2 つの部分からなるプロセスになります。 最初に、対象のファイルを指すハンドラーを作成したため、パラメーターをいくつか指定して `FileHandler->SetLabel()` を呼び出すことで、ラベルを設定できます。

```cpp
handler->SetLabel(label->GetId(), mip::LabelingOptions{ mip::AssignmentMethod::PRIVILEGED, "" });
```

最初のパラメーターは、`ListLabelsAsync()` からの単なるラベル ID です。 この値は、専用の変数に、または `mip::Label->GetId()` を読み取ることで格納できます。

上記の例では、`label` というオブジェクトに必要な `mip::Label` が格納されていることを前提としています。

### <a name="labeling-options"></a>ラベル オプション

ラベルを設定するために必要な 2 番目のパラメーターは、`mip::LabelingOptions` オブジェクトです。これは、`SetLabel()` 関数を呼び出すときにインラインで作成します。 事前に作成することもできます。

`LabelingOptions` では、`AssignmentMethod` などのラベルに関する追加情報と、アクションの理由を指定します。

- `mip::AssignmentMethod` は単なる列挙子であり、`STANDARD`、`PRIVILEGED`、`AUTO` という 3 つの値があります。 詳細については、`mip::AssignmentMethod` のリファレンスを確認してください。
- 理由が必要になるのは、サービス ポリシーで要求され、*かつ*、ファイルの*既存の*機密度を下げる場合のみです。

```cpp
auto labelingOptions = mip::LabelingOptions();
labelingOptions.SetMethod(mip::AssignmentMethod::STANDARD);
labelingOptions.SetJustificationMessage("Because I made an educated decision based upon the contents of this file.");
```

ここでラベル オプションをインラインで作成するのではなく、`SetLabel()` 関数に渡すことができます。

```cpp
handler->SetLabel(label->GetId(), labelingOptions);
```

これでハンドラーによって参照されるファイルにラベルが設定されましたが、変更をコミットし、ファイルをディスクに書き込むか、出力ストリームを作成する手順がまだもう 1 つあります。

### <a name="commit-changes"></a>変更をコミットする

MIP SDK のファイルに対する変更をコミットする最後の手順は、変更の**コミット**です。 これは、`FileHandler->CommitAsync()` 関数を使用して行われます。 

コミットメント関数を実装するため、promise/future に戻り、`bool` の promise を作成します。 `CommitAsync()` 関数では、操作が成功した場合は true、何らかの理由で失敗した場合は false が返されます。 

作成した後、`promise`と`future`、`CommitAsync()`呼びますと指定した 2 つのパラメーター。出力ファイルのパス (`std::string`)、および約束。 最後に、`future` オブジェクトの値を取得することで、結果が得られます。

```cpp
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
auto wasCommitted = commitFuture.get();
```

**重要:**`FileHandler`更新または既存のファイルを上書きされません。 ラベルが付けられるファイルを**置き換える**のは開発者の責任です。 

ラベルを **FileA.docx** に書き込む場合、ラベルを適用して、**FileB.docx** ファイルのコピーを作成する必要があります。 **FileA.docx**の削除/名前変更、および**FileB.docx** の名前変更を行う場合は、コードを記述する必要があります。

***

## <a name="delete-a-label"></a>ラベルを削除する

```cpp
auto handler = mEngine->CreateFileHandler(filePath, std::make_shared<FileHandlerObserverImpl>());
handler->DeleteLabel(mip::AssignmentMethod::PRIVILEGED, "Label unnecessary.");
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
```
