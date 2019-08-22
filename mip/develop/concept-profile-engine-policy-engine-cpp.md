---
title: 概念 - ポリシー API エンジン オブジェクト
description: この記事は、アプリケーションの初期化中に作成される、ポリシー エンジン オブジェクトの概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 5fac6b39cb3770748336fac7264134acf2627a02
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886063"
---
# <a name="microsoft-information-protection-sdk---policy-api-engine-concepts"></a>Microsoft Information Protection SDK - ポリシー API エンジンの概念

`mip::PolicyEngine` は、ポリシー API で実行できる、プロファイルの読み込みを除くすべての操作を実装します。

## <a name="implementation-add-a-policy-engine"></a>ションポリシーエンジンを追加する

### <a name="implementation-create-policy-engine-settings"></a>ションポリシーエンジン設定の作成

プロファイルと同様に、エンジンにも設定オブジェクト `mip::PolicyEngine::Settings` が必要です。 このオブジェクトには、一意のエンジン ID、デバッグやテレメトリで使用できるカスタマイズ可能なクライアント データ、および必要に応じてロケールが格納されます。

ここでは、 `FileEngine::Settings`アプリケーションユーザーの id を使用して、 *engineSettings*という名前のオブジェクトを作成します。

```cpp
PolicyEngine::Settings engineSettings(
  mip::Identity(mUsername), // mip::Identity.
  "",                       // Client data. Customizable by developer, stored with engine.
  "en-US",                  // Locale.
  false);                   // Load sensitive information types for driving classification.
```

また、カスタムエンジン ID を指定することもできます。

```cpp
PolicyEngine::Settings engineSettings(
  "myEngineId", // string
  "",           // Client data in string format. Customizable by developer, stored with engine.
  "en-US",      // Locale. Default is en-US
  false);       // Load sensitive information types for driving classification. Default is false.
```

ベスト プラクティスとして、最初のパラメーターである **id** には、望ましくはユーザー プリンシパル名など、関連付けられているユーザーにエンジンを簡単に接続できるものにする必要があります。

### <a name="implementation-add-the-policy-engine"></a>ションポリシーエンジンを追加する

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

## <a name="implementation-list-sensitivity-labels"></a>ション機密ラベルの一覧表示

追加されたエンジンを使用すると、`engine->ListSensitivityLabels()` を呼び出すことで、認証済みユーザーが利用可能な機密ラベルをすべて一覧表示することができるようになりました。

`ListSensitivityLabels()` により、サービスの特定のユーザー用のラベルの一覧とそれらのラベルの属性がフェッチされます。 結果は `std::shared_ptr<mip::Label>` のベクターに格納されます。

### <a name="implementation-listsensitivitylabels"></a>ションListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

### <a name="implementation-print-the-labels"></a>ションラベルを印刷する

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
