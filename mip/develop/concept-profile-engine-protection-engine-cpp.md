---
title: 概念 - 保護 API エンジン オブジェクト
description: この記事は、アプリケーションの初期化中に作成される、保護エンジン オブジェクトに関する概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 1ccfc81e4b45c6ec4e4316b748d9ccc0f73561a4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886028"
---
# <a name="microsoft-information-protection-sdk---protection-api-engine-concepts"></a>Microsoft Information Protection SDK - 保護 API エンジンの概念

## <a name="implementation-add-a-protection-engine"></a>ション保護エンジンを追加する

ファイル API では、`mip::ProtectionProfile` クラスがすべての SDK 操作のルート クラスとなります。 プロファイルは既に作成されているため、ここでプロファイルにエンジンを追加できます。

次の例では、1 人の認証済みユーザーに対する単一エンジンの使用について説明します。

### <a name="implementation-create-protection-engine-settings"></a>ション保護エンジン設定の作成

プロファイルと同様に、エンジンにも設定オブジェクト `mip::ProtectionEngine::Settings` が必要です。 このオブジェクトには、一意のエンジン ID、デバッグやテレメトリで使用できるカスタマイズ可能なクライアント データ、および必要に応じてロケールが格納されます。

ここでは、*engineSettings* という `ProtectionEngine::Settings` オブジェクトを作成します。 

```cpp
ProtectionEngine::Settings engineSettings("UniqueID", "");
```

> [!NOTE]
> この方法を使用して保護設定オブジェクトを作成する場合は、Active Directory Rights Management サービスクラスターの https://api.aadrm.com URL に手動で CloudEndpointBaseUrl を設定する必要もあります。

ベスト プラクティスとして、最初のパラメーターである **id** を、関連付けられているユーザーにエンジンを簡単に接続できるようなものにする必要があります。**または** `mip::Identity` オブジェクトを使用します。 `mip::Identity` で設定を初期化するには、次のようにします。

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity("Bob@Contoso.com", "");
```

### <a name="implementation-add-the-protection-engine"></a>ション保護エンジンを追加する

エンジンを追加するため、プロファイルの読み込みに使用した future/promise パターンに戻ります。 `mip::ProtectionProfile` の promise を作成するのではなく、`mip::ProtectionEngine` を使用します。

```cpp

  //auto profile will be std::shared_ptr<mip::ProtectionProfile>
  auto profile = profileFuture.get();

  //Create the ProtectionEngine::Settings object
  ProtectionEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::ProtectionEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::ProtectionEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::ProtectionEngine>
  auto engine = engineFuture.get();
```

上記のコードの最終結果では、認証済みユーザーのエンジンがプロファイルに正常に追加されます。

## <a name="implementation-list-templates"></a>ションリストテンプレート

追加されたエンジンを使用し、`engine->GetTemplatesAsync()` を呼び出すことで、認証済みユーザーが利用可能な機密テンプレートをすべて一覧表示することができます。 

`GetTemplatesAsync()` では、テンプレート ID の一覧が取り込まれます。 結果は `std::shared_ptr<std::string>` のベクターに格納されます。

### <a name="implementation-listsensitivitytemplates"></a>ションListSensitivityTemplates()

```cpp
auto loadPromise = std::make_shared<std::promise<shared_ptr<vector<string>>>>();
std::future<std::shared_ptr<std::vector<std::string>>> loadFuture = loadPromise->get_future();
mEngine->GetTemplatesAsync(engineObserver, loadPromise);
auto templates = loadFuture.get();
```

### <a name="implementation-print-the-template-ids"></a>ションテンプレート Id を印刷する

```cpp
//Iterate through all template IDs in the vector
for (const auto& temp : *templates) {
  cout << "Template:" << "\n\tId: " << temp << endl;
}
```

サービスからポリシーを正常にプルし、テンプレートを取得できたことを表示する簡単な方法は、名前を印刷することです。 テンプレートを適用するには、テンプレート ID が必要です。

ポリシー API を使用して `ComputeActions()` の結果を調べることでのみ、テンプレートをラベルにマッピングすることができます。

## <a name="next-steps"></a>次の手順

これでプロファイルが読み込まれ、エンジンが追加され、テンプレートの準備ができたため、ハンドラーを追加して、ファイルに対するテンプレートの読み取り、書き込み、削除を開始できます。 [保護ハンドラーの概念](concept-handler-protection-cpp.md)に関するページを参照してください。
