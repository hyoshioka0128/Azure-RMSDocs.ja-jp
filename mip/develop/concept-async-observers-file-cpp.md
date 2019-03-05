---
title: 概念 - MIP SDK でのファイル API オブザーバー。
description: MIP SDK は、ほぼ完全に非同期になるように設計されています。 この記事は、ファイル API オブザーバーの実装方法と非同期処理への使用方法を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: baa62e34e10de3fb4cacc3eb7cb21c0b3e2ebf75
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329959"
---
# <a name="microsoft-information-protection-sdk---file-api-observers"></a>Microsoft Information Protection SDK - ファイル API オブザーバー

ファイル API には、2 つのオブザーバー クラスが含まれます。 オブザーバー メンバーは仮想で、イベントのコールバックを処理するためにオーバーライドすることができます。

- [`mip::FileProfile::Observer`](reference/class_mip_fileprofile_observer.md)
- [`mip::FileHandler::Observer`](reference/class_mip_filehandler_observer.md)

非同期操作が完了すると、その結果に対応する `OnXxx()` メンバー関数が呼び出されます。 例では、`mip::FileProfile::Observer` に対して `OnLoadSuccess()`、`OnLoadFailure()`、`OnAddEngineSuccess()` が呼び出されます。

次の例は、promise/future パターンを示しています。これは SDK サンプルでも使用され、目的のコールバック動作を実装するために拡張することもできます。 

## <a name="file-profile-observer-implementation"></a>ファイル プロファイル オブザーバーの実装

次の例では、`mip::FileProfile::Observer` から派生される `ProfileObserver` クラスを作成しています。 メンバー関数は、サンプル全体で使用される future/promise パターンを使用するためにオーバーライドされています。

**注**:以下のサンプルのみ部分的に実装され、用の上書きを含めないでください、`mip::FileEngine`オブザーバーに関連します。

### <a name="profileobserverh"></a>profile_observer.h

ヘッダーで、`mip::FileProfile::Observer` から派生する `ProfileObserver` を定義し、各メンバー関数をオーバーライドします。

```cpp
class ProfileObserver final : public mip::FileProfile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement mip::FileEngine related observers.
};
```

### <a name="profileobservercpp"></a>profile_observer.cpp

それ自体の実装では、各オブザーバーのメンバー関数を実行するアクションを定義します。

各メンバーは、2 つのパラメーターを受け取ります。 最初のパラメーターは、関数で処理しているクラスへの共有ポインターです。 `ProfileObserver::OnLoadSuccess` は `mip::FileProfile` を受け取ることを想定しています。 `ProfileObserver::OnAddEngineSuccess` は `mip::FileEngine` を想定しています。

2 つ目のパラメーターは、*コンテキスト*への共有ポインターです。 この実装では、コンテキストは `std::promise` への参照で、`std::shared_ptr<void>` として参照によって渡されます。 関数の最初の行は、これを `std::promise` にキャストし、`promise` という名前のオブジェクトに格納されます。

最後に、`promise->set_value()` を設定し、`mip::FileProfile`オブジェクトに渡すことで、future の準備ができます。

```cpp
#include "profile_observer.h"
#include <future>

//Called when FileProfile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = 
  std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when FileProfile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement mip::FileEngine related observers.
```

任意の SDK クラスをインスタンス化したり、非同期操作を実行する関数を使用する場合には、オブザーバーの実装を設定コンストラクターまたは非同期関数そのものに渡します。 `mip::FileProfile::Settings` オブジェクトをインスタンス化すると、コンストラクターによりパラメーターの 1 つとして `mip::FileProfile::Observer` が受け入れられます。 次の例は、`mip::FileProfile::Settings` コンストラクターで使用されるカスタムの `ProfileObserver` を示しています。

## <a name="filehandler-observer-implementation"></a>FileHandler オブザーバーの実装

プロファイル オブザーバーと同じく、`mip::FileHandler` もファイル操作中に非同期のイベント通知を処理するために `mip::FileHandler::Observers` クラスを実装します。 実装は、上記で説明したのとほぼ同じです。 `FileHandlerObserver` は以下で部分的に定義されます。 

### <a name="filehandlerobserverh"></a>file_handler_observer.h

```cpp
#include "mip/file/file_handler.h"

class FileHandlerObserver final : public mip::FileHandler::Observer {
public:
  void OnCreateFileHandlerSuccess(
      const std::shared_ptr<mip::FileHandler>& fileHandler,
      const std::shared_ptr<void>& context) override;

  void OnCreateFileHandlerFailure(
      const std::exception_ptr& error,
      const std::shared_ptr<void>& context) override;

  //TODO: override remaining member functions inherited from mip::FileHandler::Observer
};
```

### <a name="filehandlerobservercpp"></a>file_handler_observer.cpp

このサンプルは、最初の 2 つの関数だけですが、残りの関数でもこれらおよび `ProfileObserver` と同様のパターンを使用します。

```cpp
#include "file_handler_observer.h"

void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_value(fileHandler);
}

void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_exception(error);
}

//TODO: override remaining member functions inherited from mip::FileHandler::Observer
```

