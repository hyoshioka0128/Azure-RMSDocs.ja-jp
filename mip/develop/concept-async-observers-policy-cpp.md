---
title: 概念 - MIP SDK でのポリシー API オブザーバー。
description: MIP SDK は、ほぼ完全に非同期になるように設計されています。 この記事は、ポリシー API オブザーバーの実装方法と非同期処理への使用方法を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: e8f2e2c775270f81489778ced852a7bb26b5ad1c
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175498"
---
# <a name="microsoft-information-protection-sdk---policy-api-observers"></a>Microsoft Information Protection SDK - ポリシー API オブザーバー

ポリシー API SDK には、オブザーバー クラスが 1 つ含まれます。 オブザーバー メンバーは仮想で、非同期操作のコールバックを処理するためにオーバーライドする必要があります。

- [`mip::PolicyProfile::Observer`](reference/class_mip_policyprofile_observer.md)

非同期操作が完了すると、その結果に対応する `OnXxx()` メンバー関数が呼び出されます。 例では、`mip::Profile::Observer` に対して `OnLoadSuccess()`、`OnLoadFailure()`、`OnAddEngineSuccess()` が呼び出されます。

次の例は、promise/future パターンを示しています。これは SDK サンプルでも使用され、目的のコールバック動作を実装するために拡張することもできます。 

## <a name="profile-observer-implementation"></a>プロファイル オブザーバーの実装

次の例では、`mip::Profile::Observer` から派生される `ProfileObserver` クラスを作成しています。 メンバー関数は、サンプル全体で使用される future/promise パターンを使用するためにオーバーライドされています。

**注意**:以下のサンプルのみ部分的に実装され、用の上書きを含めないでください、`mip::ProfileEngine`オブザーバーに関連します。

### <a name="profileobserverh"></a>profile_observer.h

ヘッダーで、`mip::Profile::Observer` から派生する `ProfileObserver` を定義し、各メンバー関数をオーバーライドします。

```cpp
class ProfileObserver final : public mip::Profile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement remaining members
};
```

### <a name="profileobservercpp"></a>profile_observer.cpp

それ自体の実装では、各オブザーバーのメンバー関数を実行するアクションを定義します。

各メンバーは、2 つのパラメーターを受け取ります。 最初のパラメーターは、関数で処理されるクラスへの共有ポインターです。 `ProfileObserver::OnLoadSuccess` は `mip::Profile` を受け取ることを想定しています。 `ProfileObserver::OnAddEngineSuccess` は `mip::ProfileEngine` を想定しています。

2 つ目のパラメーターは、*コンテキスト*への共有ポインターです。 この実装では、コンテキストは `std::promise` への参照で、`shared_ptr<void>` として渡されます。 関数の最初の行は、これを `std::promise` にキャストし、`promise` という名前のオブジェクトに格納されます。

最後に、`promise->set_value()` を設定し、`mip::Profile` オブジェクトに渡すことで、future の準備ができます。

```cpp
#include "profile_observer.h"
#include <future>

//Called when Profile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when Profile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement remaining observer members
```

任意の非同期操作を実行しているときに、オブザーバーの実装は設定コンストラクターまたは非同期関数そのものに渡されます。 

