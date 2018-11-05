---
title: 概念 - MIP SDK の保護ハンドラー。
description: この記事は、保護 API ハンドラーがどのように作成され、操作を呼び出すためにどのように使用されるかを理解するのに役立ちます。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a087f1bdef5a010718c67fbdca938ecbb62e5faa
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453494"
---
# <a name="microsoft-information-protection-sdk---protection-handler-concepts"></a>Microsoft Information Protection SDK - 保護ハンドラーの概念

MIP SDK 保護 API では、`mip::ProtectionHandler` により、保護されたストリームとバッファーの暗号化と暗号化解除、アクセス確認の実行、発行ライセンスの取得、および保護された情報からの属性の取得のための関数が示されます。 

## <a name="requirements"></a>要件

特定のファイルを操作するための `ProtectionHandler` を作成するには、以下のものが必要です。

- `ProtectionProfile`
- `ProtectionProfile` に追加された `ProtectionEngine`
- [ここ]()で概説されているパターンに似た、`mip::ProtectionHandler::Observer` を継承するクラス。
- `mip::ProtectionDescriptor` または発行ライセンス

## <a name="create-a-protection-handler"></a>保護ハンドラーを作成する

`mip::ProtectionHandler` オブジェクトは、`ProtectionDescriptor` またはシリアル化された発行ライセンスを 2 つの `ProtectionEngine` 関数のいずれかに提供することで構築されます。 まだ発行ライセンスがないプレーンテキスト情報を保護するために、保護記述子を生成する必要があります。 **発行ライセンス**は、既に保護されているコンテンツの暗号を解除する場合や、ライセンスが既に構築されているコンテンツを保護する場合に使用されます。 保護されたコンテンツは、関連付けられている発行ライセンスなしで暗号化を解除することはできません。

`mip::ProtectionEngine` では、`ProtectionHandler` を作成するための 2 つの関数が示されます。 最初のパラメーターとしての発行ライセンスまたはハンドラーを除き、パラメーターは同じです。

- `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync`
  - 最初のパラメーターとして `ProtectionDescriptor` が必要になります。
- `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync`
  - 最初のパラメーターとして `std::vector<unint8_t>` に格納される、シリアル化された発行ライセンスが必要です。

### <a name="create-from-descriptor"></a>記述子から作成する

まだ保護されていないコンテンツを保護する場合や、コンテンツに新しい保護を適用するとき (暗号化が解除されていることを意味します) には、`mip::ProtectionDescriptor` を構築する必要があります。 構築された後、`mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync()` に渡され、`mip::ProtectionHandler::Observer` を通じて結果が返されます。

```cpp
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();
auto observer = std::make_shared<ProtectionHandlerObserverImpl>();

//Refer to ProtectionDescriptor docs for details on creating the descriptor
auto descriptor = CreateProtectionDescriptor(); //Stub function

mEngine->CreateProtectionHandlerFromDescriptorAsync(
    descriptor,
    mip::ProtectionHandlerCreationOptions::None,
    observer,
    handlerPromise);

auto handler = handlerFuture.get();
```

`ProtectionHandler` オブジェクトが正常に作成されたら、ファイル操作 (取得/設定/削除/コミット) を行うことができます。

### <a name="create-from-publishing-license"></a>発行ライセンスから作成する

この例では、発行ライセンスが既にいくつかのソースから読み取られており、`std::vector<uint8_t> serializedPublishingLicense` に格納されていることが前提となります。

```cpp

//TODO: Implement GetPublishingLicense()
//Snip implies that function reads PL from source file, database, stream, etc.
std::vector<uint8_t> serializedPublishingLicense = GetPublishingLicense(filePath);

auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();

shared_ptr<ProtectionHandlerObserverImpl> handleObserver =
    std::make_shared<ProtectionHandlerObserverImpl>();

mEngine->CreateProtectionHandlerFromPublishingLicenseAsync(
    serializedPublishingLicense,
    mip::ProtectionHandlerCreationOptions::None,
    handleObserver,
    handlerPromise);

auto handler = handlerFuture.get();
```

