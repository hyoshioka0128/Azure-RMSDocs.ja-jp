---
title: 概念 - MIP SDK のファイル ハンドラー。
description: この記事は、ファイル API ハンドラーがどのように作成され、操作を呼び出すためにどのように使用されるかを理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: f94f885f77d15ec5c38894a4801b08908e65a166
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555808"
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

## <a name="requirements"></a>［要件］

特定のファイルを操作するための `FileHandler` を作成するには、以下のものが必要です。

- `FileProfile`
- `FileProfile` に追加された `FileEngine`
- `mip::FileHandler::Observer` を継承するクラス

## <a name="create-a-file-handler"></a>ファイル ハンドラーを作成する

ファイル API でファイルを管理するために必要な最初の手順は、`FileHandler` オブジェクトの作成です。 このクラスでは、ファイルの取得、設定、更新、削除、およびファイルに対するラベル変更のコミットに必要なすべての機能が実装されます。

`FileHandler` の作成は、promise/future パターンを使用して `FileEngine` の `CreateFileHandlerAsync` 関数を呼び出すのと同じくらい簡単です。

`CreateFileHandlerAsync` では 3 つのパラメーターが受け入れられます。つまり、読み取りまたは変更が必要なファイルへのパス、非同期イベント通知のための `mip::FileHandler::Observer`、および `FileHandler` の promise です。

**注:** `mip::FileHandler::Observer` クラスは派生クラスで実装する必要があります。これは、`CreateFileHandler` に `Observer` オブジェクトが必要であるためです。 

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

ラベルの設定は、2 つの部分からなるプロセスになります。 まず、問題のファイルを指すハンドラーを作成し、`mip::Label`、`mip::LabelingOptions`、および `mip::ProtectionOptions`のいくつかのパラメーターを指定して `FileHandler->SetLabel()` を呼び出すことによって、ラベルを設定できます。 まず、ラベル id をラベルに解決して、ラベル付けオプションを定義する必要があります。 

### <a name="resolve-label-id-to-miplabel"></a>ラベル id を mip:: Label に解決します

**Setlabel**関数の最初のパラメーターは、`mip::Label`です。 多くの場合、アプリケーションはラベルではなくラベル識別子を使用します。 ファイルまたはポリシーエンジンで**GetLabelById**を呼び出すことによって、ラベル識別子を `mip::Label` に解決できます。

```cpp
mip::Label label = mEngine->GetLabelById(labelId);
```

### <a name="labeling-options"></a>ラベル オプション

ラベルを設定するために必要な2番目のパラメーターは `mip::LabelingOptions`です。 

`LabelingOptions` では、`AssignmentMethod` などのラベルに関する追加情報と、アクションの理由を指定します。

- `mip::AssignmentMethod` は単なる列挙子であり、`STANDARD`、`PRIVILEGED`、`AUTO` という 3 つの値があります。 詳細については、`mip::AssignmentMethod` のリファレンスを確認してください。
- 理由が必要になるのは、サービス ポリシーで要求され、*かつ*、ファイルの*既存の*機密度を下げる場合のみです。

この領域切り取りは、`mip::LabelingOptions` オブジェクトを作成し、ダウングレードの理由とメッセージを設定する方法を示しています。

```cpp
auto labelingOptions = mip::LabelingOptions(mip::AssignmentMethod::STANDARD);
labelingOptions.SetDowngradeJustification(true, "Because I made an educated decision based upon the contents of this file.");
```

### <a name="protection-settings"></a>保護設定

アプリケーションによっては、委任されたユーザー id の代わりに操作を実行することが必要になる場合があります。 `mip::ProtectionSettings` クラスを使用すると、アプリケーションで*ハンドラーごと*に委任された id を定義できます。 以前は、この委任はエンジンクラスによって実行されていました。 これには、アプリケーションのオーバーヘッドとサービスのラウンドトリップに大きな欠点がありました。 委任されたユーザー設定を `mip::ProtectionSettings` に移動し、ハンドラークラスのその部分を作成することにより、このオーバーヘッドが解消されるため、さまざまなユーザー id のセットに代わって多くの操作を実行するアプリケーションのパフォーマンスが向上します。 

委任が不要な場合は、単に**Setlabel**関数に `mip::ProtectionSettings()` を渡します。 委任が必要な場合は、`mip::ProtectionSettings` オブジェクトを作成し、委任されたメールアドレスを設定することで実現できます。

```cpp
mip::ProtectionSettings protectionSettings; 
protectionSettings.SetDelegatedUserEmail("alice@contoso.com");
```

### <a name="set-the-label"></a>ラベルを設定する

Id から `mip::Label` をフェッチし、ラベル付けオプションを設定し、必要に応じて保護設定を設定して、ラベルを設定できるようになりました。

保護設定を設定していない場合は、ハンドラーで `SetLabel` を呼び出してラベルを設定します。

```cpp
handler->SetLabel(label, labelingOptions, mip::ProtectionSettings());
```

委任された操作を実行するために保護設定が必要な場合は、次の手順を実行します。

```cpp
handler->SetLabel(label, labelingOptions, protectionSettings);
```

これでハンドラーによって参照されるファイルにラベルが設定されましたが、変更をコミットし、ファイルをディスクに書き込むか、出力ストリームを作成する手順がまだもう 1 つあります。

### <a name="commit-changes"></a>変更をコミットする

MIP SDK のファイルに対する変更をコミットする最後の手順は、変更の**コミット**です。 これは、`FileHandler->CommitAsync()` 関数を使用して行われます。 

コミットメント関数を実装するため、promise/future に戻り、`bool` の promise を作成します。 `CommitAsync()` 関数では、操作が成功した場合は true、何らかの理由で失敗した場合は false が返されます。 

`promise` と `future` を作成した後、`CommitAsync()` が呼び出され、2 つのパラメーター、つまり、出力ファイル パス (`std::string`)、と promise が指定されます。 最後に、`future` オブジェクトの値を取得することで、結果が得られます。

```cpp
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
auto wasCommitted = commitFuture.get();
```

**重要:** `FileHandler` では、既存のファイルの更新や上書きは行われません。 ラベルが付けられるファイルを**置き換える**のは開発者の責任です。 

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
