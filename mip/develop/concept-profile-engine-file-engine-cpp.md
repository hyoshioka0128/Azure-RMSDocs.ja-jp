---
title: 概念 - ファイル API エンジン オブジェクト
description: この記事は、アプリケーションの初期化中に作成される、ファイル エンジン オブジェクトの概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: fcdcb5c11646fd7d32284b6df31cda33abbfde4a
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175515"
---
# <a name="microsoft-information-protection-sdk---file-api-engine-concepts"></a>Microsoft Information Protection SDK - ファイル API エンジンの概念

MIP SDK のファイル API の `mip::FileEngine` では、指定した ID の代わりに実行されるすべての操作へのインターフェイスを提供します。 アプリケーションにサインインするユーザーごとにエンジンが 1 つ追加され、エンジンで実行される操作がすべてその ID のコンテキストで実行されます。

`FileEngine`が 2 つの主な責務。認証されたユーザーのラベルを一覧表示するユーザーの代理としてのファイル操作を実行するファイルのハンドラーを作成しています。 

- [`mip::FileEngine`](reference/class_mip_fileengine.md)
- `ListSensitivityLabels()`:読み込まれたエンジンのラベルの一覧を取得します。
- `CreateFileHandler()`:作成、`mip::FileHandler`特定のファイルまたはストリームにします。

## <a name="add-a-file-engine"></a>ファイル エンジンの追加

[プロファイルとエンジン オブジェクト](concept-profile-engine-cpp.md)に関するページで説明されているように、エンジンでは 2 つの状態 (`CREATED` または `LOADED`) を持つことができます。 これらの 2 つの状態のいずれかではない場合、これは存在しません。 状態の作成と読み込みの両方を行うには、`FileProfile::LoadAsync` を 1 回呼び出す必要があるだけです。 エンジンが既にキャッシュされた状態に存在する場合は、`LOADED` になります。 存在しない場合は、`CREATED`、`LOADED` になります。 `CREATED` は、アプリケーションにはエンジンの読み取りに必要なサービスからの情報をすべて含むことを意味します。 `LOADED` は、エンジンを活用するのに必要なデータ構造はすべてメモリ内で作成されていることを意味します。

### <a name="create-file-engine-settings"></a>ファイル エンジン設定の作成

プロファイルと同様に、エンジンにも設定オブジェクト `mip::FileEngine::Settings` が必要です。 このオブジェクトには、一意のエンジン ID、デバッグやテレメトリで使用できるカスタマイズ可能なクライアント データ、および必要に応じてロケールが格納されます。

ここでは、*engineSettings* という `FileEngine::Settings` オブジェクトを作成します。 

```cpp
FileEngine::Settings engineSettings("UniqueID", "");
```

ベスト プラクティスとして、最初のパラメーターである `id` を、関連付けられているユーザーにエンジンを簡単に接続できるようなものにする必要があります。 電子メール アドレス、UPN、または AAD オブジェクト GUID などは、その ID がどちらも一意で、サービスを呼び出すことなく、ローカルの状態から読み込むことができることが確認されます。

### <a name="add-the-file-engine"></a>ファイル エンジンの追加

エンジンを追加するには、プロファイルの読み込みに使用した promise/future パターンに戻ります。 `mip::FileProfile` に対して promise を作成するのではなく、これは `mip::FileEngine` を使用して作成されます。

```cpp
  //auto profile will be std::shared_ptr<mip::FileProfile>
  auto profile = profileFuture.get();

  //Create the FileEngine::Settings object
  FileEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::FileEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::FileEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::FileEngine>
  auto engine = engineFuture.get();
```

上記のコードの最終結果では、認証済みユーザーのエンジンがプロファイルに追加されます。

## <a name="list-sensitivity-labels"></a>機密ラベルの一覧表示

追加されたエンジンを使用すると、`engine->ListSensitivityLabels()` を呼び出すことで、認証済みユーザーが利用可能な機密ラベルをすべて一覧表示することができるようになりました。

`ListSensitivityLabels()` により、サービスの特定のユーザー用のラベルの一覧とそれらのラベルの属性がフェッチされます。 結果は `std::shared_ptr<mip::Label>` のベクターに格納されます。

`mip::Label` の詳細については、[こちら]()をご覧ください。

### <a name="listsensitivitylabels"></a>ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

または、簡略化すると、次のようになります。

```cpp
auto labels = engine->ListSensitivityLabels();
```

### <a name="print-the-labels-and-ids"></a>ラベルと ID の出力

サービスからポリシーを正常にプルし、ラベルを取得できたことを示す簡単な方法は、名前を出力することです。 ラベルの適用には、ラベル識別子が必須です。 以下のコードはすべてのラベルから繰り返され、親と子ラベルごとに `name` と `id` を表示します。

```cpp
//Iterate through all labels in the vector
for (const auto& label : labels) {
  //Print label name and GUID
  cout << label->GetName() << " : " << label->GetId() << endl;

  //Print child label name and GUID
  for (const auto& child : label->GetChildren()) {
    cout << "->  " << child->GetName() <<  " : " << child->GetId() << endl;
  }
}
```

`GetSensitivityLabels()` によって返される `mip::Label` のコレクションは、ユーザーが利用可能なすべてのラベルを表示するために使用できます。そして選択されたら、ファイルにラベルを適用するのに ID を使用できます。

## <a name="next-steps"></a>次の手順

これでプロファイルが読み込まれ、エンジンが追加され、ラベルの準備ができたため、ハンドラーを追加して、ファイルに対するラベルの読み取り、書き込み、削除を開始できます。 「[File handlers in the MIP SDK](concept-handler-file-cpp.md)」 (MIP SDK でのファイル ハンドラー) を参照してください。

