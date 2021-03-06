---
title: 概念 - ポリシー API プロファイル オブジェクト
description: この記事は、アプリケーションの初期化中に作成される、ポリシー プロファイル オブジェクトに関する概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: f9bb02dd4508b5e09761b3684a2a4e6d92224b6a
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175340"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>Microsoft Information Protection SDK - ポリシー API プロファイルの概念

ポリシー API の操作を実行する前に、`mip::Profile` を読み込む必要があります。

次の 2 つの例では、状態ストレージに対するローカル ストレージ、およびメモリ内のみを使用する profileSettings オブジェクト作成する方法を示します。 いずれも、`authDelegateImpl` オブジェクトが作成済みであると想定しています。

## <a name="load-a-profile"></a>プロファイルの読み込み

これで `ProfileObserver` と `AuthDelegateImpl` を定義したので、それらを使用して `mip::PolicyProfile` をインスタンス化します。 `mip::PolicyProfile` オブジェクトの作成には、[`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md) が必要です。

### <a name="profilesettings-parameters"></a>Profile::Settings パラメーター

- `std::string path`:ファイルのパスをログ、テレメトリ、およびその他の永続的な状態が格納されます。
- `bool useInMemoryStorage`:すべての状態をディスク上ではなくメモリに格納する必要があるかどうかを定義します。
- `std::shared_ptr<mip::AuthDelegate> authDelegate`:クラスの共有ポインター `mip::AuthDelegate` 
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`:共有へのポインター、`PolicyProfile::Observer`実装します。
- `mip::ApplicationInfo applicationInfo`: オブジェクト。 SDK を利用しているアプリケーションに関する情報を定義するために使用します。

次の 2 つの例では、状態ストレージに対するローカル ストレージ、およびメモリ内のみを使用する profileSettings オブジェクト作成する方法を示します。 いずれも、`authDelegateImpl` オブジェクトが作成済みであると想定しています。

#### <a name="store-state-in-memory-only"></a>メモリ内の状態のみを格納

```cpp
Profile::Settings profileSettings("",
    true,
    authDelegateImpl,
    std::make_shared<ProfileObserver>(),
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>ディスク上のストレージ パスからのプロファイル設定の読み取り/書き込み

```cpp
Profile::Settings profileSettings("./mip_app_data",
    false,
    authDelegateImpl,
    std::make_shared<ProfileObserver>(),
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });
```

次に、promise/future パターンを使用して `Profile` を読み込みます。

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<Profile>>>();
auto profileFuture = profilePromise->get_future();
Profile::LoadAsync(profileSettings, profilePromise);
```

プロファイルが正常に読み込まれたら、`mip::Profile::Observer::OnLoadSuccess` の実装である `ProfileObserver::OnLoadSuccess` が通知されます。 この場合は `mip::Profile` である、結果のオブジェクトおよびコンテキストは、オブザーバー関数にパラメーターとして渡されます。

この*コンテキスト*は、非同期操作を処理するために作成した `std::promise` へのポインターです。 この関数は、最初のパラメーター用に渡した Profile オブジェクトに Promise の値を単純に設定します。 メイン関数で `Future.get()` を使用する場合、結果は呼び出しスレッドの新しいオブジェクトに格納できます。

```cpp
//get the future value and store in profile. 
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>まとめ

オブザーバーおよび認証委任を完全に実装したので、プロファイルを完全に読み込めるようになりました。 以下のコードの切り取りでは、すべての必要なハンドラーが既に含まれていると想定しています。

```cpp
int main()
{
    const string userName = "MyTestUser@consoto.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    Profile::Settings profileSettings("", false, authDelegateImpl, std::make_shared<ProfileObserver>(), mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<Profile>>>();
    auto profileFuture = profilePromise->get_future();
    Profile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

最終結果は、プロファイルの読み込みが成功し、それが `profile` と呼ばれるオブジェクトに格納されます。

## <a name="next-steps"></a>次の手順

これでプロファイルが追加されました。次の手順では、エンジンをプロファイルに追加します。

[ポリシー エンジンの概念](concept-profile-engine-policy-engine-cpp.md)
