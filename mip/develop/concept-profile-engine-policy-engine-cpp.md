---
title: 概念 - ポリシー API エンジン オブジェクト
description: この記事は、アプリケーションの初期化中に作成される、ポリシー エンジン オブジェクトの概念を理解するのに役立ちます。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 07e0fc59e0ed5ec1fc66fe3179fce07dfcb687d1
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445276"
---
# <a name="microsoft-information-protection-sdk---policy-api-engine-concepts"></a>Microsoft Information Protection SDK - ポリシー API エンジンの概念

`mip::PolicyEngine` は、ポリシー API で実行できる、プロファイルの読み込みを除くすべての操作を実装します。 

## <a name="implementation-add-a-policy-engine"></a>実装: ポリシー エンジンを追加する

### <a name="implementation-create-policy-engine-settings"></a>実装: ポリシー エンジンの設定を作成する

プロファイルと同様に、エンジンにも設定オブジェクト `mip::PolicyEngine::Settings` が必要です。 このオブジェクトには、一意のエンジン ID、デバッグやテレメトリで使用できるカスタマイズ可能なクライアント データ、および必要に応じてロケールが格納されます。

ここでは、*engineSettings* という `PolicyEngine::Settings` オブジェクトを作成します。

```cpp
PolicyEngine::Settings engineSettings("UniqueID", "");
```

ベスト プラクティスとして、最初のパラメーターである **id** には、望ましくはユーザー プリンシパル名など、関連付けられているユーザーにエンジンを簡単に接続できるものにする必要があります。

### <a name="implementation-add-the-policy-engine"></a>実装: ポリシー エンジンを追加する

エンジンを追加するため、プロファイルの読み込みに使用した future/promise パターンに戻ります。 `mip::Profile` の promise を作成するのではなく、`mip::PolicyEngine` を使用します。

```cpp

  //auto profile will be std::shared_ptr<mip::Profile>
  auto profile = profileFuture.get();

  //Create the PolicyEngine::Settings object
  PolicyEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::PolicyEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::PolicyEngine>
  auto engine = engineFuture.get();
```

上記のコードの最終結果では、認証済みユーザーのエンジンがプロファイルに正常に追加されます。

## <a name="implementation-list-sensitivity-labels"></a>実装: 機密ラベルの列挙

追加されたエンジンを使用すると、`engine->ListSensitivityLabels()` を呼び出すことで、認証済みユーザーが利用可能な機密ラベルをすべて一覧表示することができるようになりました。

`ListSensitivityLabels()` により、サービスの特定のユーザー用のラベルの一覧とそれらのラベルの属性がフェッチされます。 結果は `std::shared_ptr<mip::Label>` のベクターに格納されます。

### <a name="implementation-listsensitivitylabels"></a>実装: ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

### <a name="implementation-print-the-labels"></a>実装: レベルの出力

```cpp
//Iterate through all labels in the vector
for (const auto& label : labels) {
  //print the label name
  cout << label->GetName() << endl;
  //Iterate through all child labels
  for (const auto& child : label->GetChildren()) {
    //Print the label with some formatting
    cout << "->  " << child->GetName() << endl;
  }
}
```

サービスからポリシーを正常にプルし、ラベルを取得できたことを示す簡単な方法は、名前を出力することです。 ラベルの適用には、ラベル識別子が必須です。 ラベル ID を返すために上述の切り取りを変更すると、次のようになります。

```cpp
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

