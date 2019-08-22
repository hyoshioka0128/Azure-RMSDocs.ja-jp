---
title: 概念 - ポリシー API プロファイル オブジェクト
description: この記事は、アプリケーションの初期化中に作成される、ポリシー プロファイル オブジェクトに関する概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 9b3b32464cae35560c74a05b28506ca60dc963d2
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886050"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>Microsoft Information Protection SDK - ポリシー API プロファイルの概念

ポリシー API の操作を実行する前に、`mip::Profile` を読み込む必要があります。

次の 2 つの例では、状態ストレージに対するローカル ストレージ、およびメモリ内のみを使用する profileSettings オブジェクト作成する方法を示します。 いずれも、`authDelegateImpl` オブジェクトが作成済みであると想定しています。

## <a name="load-a-profile"></a>プロファイルの読み込み

、、および`mip::PolicyProfile`が定義されたので、それらを使用してインスタンス化します。 `AuthDelegateImpl` `ProfileObserver` `MipContext` オブジェクトを`mip::PolicyProfile`作成する[`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md)に`mip::MipContext`は、とが必要です。

### <a name="profilesettings-parameters"></a>Profile::Settings パラメーター

コンストラクター `PolicyProfile::Settings`は、次に示す4つのパラメーターを受け取ります。

- `const std::shared_ptr<MipContext>`:アプリケーション情報や状態パスなどを格納するために初期化されたオブジェクト。`mip::MipContext`
- `mip::CacheStorageType`:状態を格納する方法を定義します。メモリ内、ディスク上、またはディスク上で暗号化されます。 詳細については、「[キャッシュストレージの概念](concept-cache-storage.md)」を参照してください。
- `std::shared_ptr<mip::AuthDelegate>`:クラス`mip::AuthDelegate`の共有ポインター。
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`:プロファイル`Observer`の実装[`PolicyProfile`](reference/class_mip_policyprofile_observer.md)(、 [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)、および[`FileProfile`](reference/class_mip_fileprofile_observer.md)) への共有ポインター。

次の 2 つの例では、状態ストレージに対するローカル ストレージ、およびメモリ内のみを使用する profileSettings オブジェクト作成する方法を示します。 いずれも、`authDelegateImpl` オブジェクトが作成済みであると想定しています。

#### <a name="store-state-in-memory-only"></a>メモリ内の状態のみを格納

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

PolicyProfile::Settings profileSettings(
    mipContext,                                   // mipContext object
    mip::CacheStorageType::InMemory,              // use in memory storage
    authDelegateImpl,                             // auth delegate object
    std::make_shared<PolicyProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>ディスク上のストレージ パスからのプロファイル設定の読み取り/書き込み

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

PolicyProfile::Settings profileSettings(
    mipContext,                                    // mipContext object
    mip::CacheStorageType::OnDisk,                 // use on disk storage
    authDelegateImpl,                              // auth delegate object
    std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer
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

    mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

    auto authDelegateImpl = std::make_shared<sample::auth::AuthDelegateImpl>(appInfo, userName, password);

    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    PolicyProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
        authDelegateImpl,                              // auth delegate object
        std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer

    auto profilePromise = std::make_shared<promise<shared_ptr<PolicyProfile>>>();
    auto profileFuture = profilePromise->get_future();
    Profile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

最終結果は、プロファイルの読み込みが成功し、それが `profile` と呼ばれるオブジェクトに格納されます。

## <a name="next-steps"></a>次の手順

これでプロファイルが追加されました。次の手順では、エンジンをプロファイルに追加します。

[ポリシー エンジンの概念](concept-profile-engine-policy-engine-cpp.md)
