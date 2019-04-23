---
title: 概念 - MIP SDK での保護 API オブザーバー。
description: MIP SDK は、ほぼ完全に非同期になるように設計されています。 この記事は、保護 API オブザーバーの実装方法と非同期処理への使用方法を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 2d1cf81e20a317ecb1eb9e71b5b4e0ab32482877
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60175549"
---
# <a name="microsoft-information-protection-sdk---protection-api-observers"></a>Microsoft Information Protection SDK - 保護 API オブザーバー

保護 API には、3 つのオブザーバー クラスが含まれています。 オブザーバー メンバーは仮想で、非同期操作のコールバックを処理するためにオーバーライドすることができます。

- [保護プロファイル: `mip::ProtectionProfile::Observer`](reference/class_mip_ProtectionProfile_observer.md)
- [保護エンジン: `mip::ProtectionEngine::Observer`](reference/class_mip_ProtectionEngine_observer.md)
- [保護ハンドラー: `mip::ProtectionHandler::Observer`](reference/class_mip_Protectionhandler_observer.md)

非同期操作が完了すると、その結果に対応する `OnXxx()` メンバー関数が呼び出されます。 例では、`mip::ProtectionProfile::Observer` に対して `OnLoadSuccess()`、`OnLoadFailure()`、`OnAddEngineSuccess()` が呼び出されます。

次の例は、promise/future パターンを示しています。これは SDK サンプルでも使用され、目的のコールバック動作を実装するために拡張することもできます。 

## <a name="protectionprofile-observer-implementation"></a>ProtectionProfile Observer の実装

次の例では、`mip::ProtectionProfile::Observer` から派生される `ProtectionProfileObserverImpl` クラスを作成しています。 メンバー関数は、サンプル全体で使用される promise/future パターンを使用するためにオーバーライドされています。

### <a name="protectionprofileobserverimpl-class-declaration"></a>ProtectionProfileObserverImpl クラス宣言

ヘッダーで、`mip::ProtectionProfile::Observer` から派生する `ProtectionProfileObserverImpl` を定義し、各メンバー関数をオーバーライドします。

```cpp
//ProtectionProfileObserverImpl.h
class ProtectionProfileObserverImpl final : public mip::ProtectionProfile::Observer {
public:
  ProtectionProfileObserverImpl() { }
  void OnLoadSuccess(const shared_ptr<mip::ProtectionProfile>& profile, const shared_ptr<void>& context) override;
  void OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) override;
  void OnAddEngineSuccess(const shared_ptr<mip::ProtectionEngine>& engine, const shared_ptr<void>& context) override;
  void OnAddEngineError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionprofileobserverimpl-implementation"></a>ProtectionProfileObserverImpl の実装

それ自体の実装では、各オブザーバーのメンバー関数を実行するアクションだけを定義します。

各メンバーは、2 つのパラメーターを受け取ります。 最初のパラメーターは、関数で処理しているクラスへの共有ポインターです。 `ProtectionObserver::OnLoadSuccess` は `mip::ProtectionProtection` を受け取ることを想定し、`ProtectionObserver::OnAddEngineSuccess` は `mip::ProtectionEngine` を想定しています。

2 つ目のパラメーターは、*コンテキスト*への共有ポインターです。 この実装では、コンテキストは `std::promise` への参照で、`shared_ptr<void>` として渡されます。 関数の最初の行は、これを `std::promise` にキャストし、`promise` という名前のオブジェクトに格納されます。

最後に、`promise->set_value()` を設定し、`mip::ProtectionProtection`オブジェクトに渡すことで、future の準備ができます。

```cpp
//protection_observers.cpp

void ProtectionProfileObserverImpl::OnLoadSuccess(
  const shared_ptr<mip::ProtectionProfile>& profile,
  const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_value(profile);
};

void ProtectionProfileObserverImpl::OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_exception(error);
};

void ProtectionProfileObserverImpl::OnAddEngineSuccess(
  const shared_ptr<mip::ProtectionEngine>& engine,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_value(engine);
};

void ProtectionProfileObserverImpl::OnAddEngineError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_exception(error);
};
```

任意の SDK クラスをインスタンス化したり、非同期操作を実行する関数を使用する場合には、オブザーバーの実装を設定コンストラクターまたは非同期関数そのものに渡します。 `mip::ProtectionProfile::Settings` オブジェクトをインスタンス化すると、コンストラクターによりパラメーターの 1 つとして `mip::ProtectionProfile::Observer` が受け入れられます。 次の例は、`mip::ProtectionProfile::Settings` コンストラクターで使用されるカスタムの `ProtectionProfileObserverImpl` を示しています。

## <a name="protectionhandler-observer-implementation"></a>ProtectionHandler オブザーバーの実装

保護オブザーバーと同じく、`mip::ProtectionHandler` も保護操作中に非同期のイベント通知を処理するために `mip::ProtectionHandler::Observer` クラスを実装します。 実装は、上記で説明したのとほぼ同じです。 `ProtectionHandlerObserverImpl` は以下で部分的に定義されます。 完全な実装は、[GitHub サンプル リポジトリ](https://azure.microsoft.com/resources/samples/?sort=0&term=mip+sdk)にあります。

### <a name="protectionhandlerobserverimpl-class-declaration"></a>ProtectionHandlerObserverImpl クラス宣言

```cpp
//protection_observers.h

class ProtectionHandlerObserverImpl final : public mip::ProtectionHandler::Observer {
public:
  ProtectionHandlerObserverImpl() { }
  void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
  void OnCreateProtectionHandlerError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionhandlerobserverimpl-partial-implementation"></a>ProtectionHandlerObserverImpl の部分実装

このサンプルは、最初の 2 つの関数だけですが、残りの関数でもこれらおよび `ProtectionObserver` と同様のパターンを使用します。

```cpp
//protection_observers.cpp

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerSuccess(
  const shared_ptr<mip::ProtectionHandler>& protectionHandler,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_value(protectionHandler);
};

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_exception(error);
};
```

