---
title: 概念 - 保護 API プロファイル オブジェクト
description: この記事は、アプリケーションの初期化中に作成される、保護プロファイル オブジェクトの概念を理解するのに役立ちます。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ae6699212d45a6c8a2fa95f648e7f5a2be3de93e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445310"
---
# <a name="microsoft-information-protection-sdk---protection-api-profile-concepts"></a>Microsoft Information Protection SDK - 保護 API プロファイルの概念

次の 2 つの例では、状態ストレージに対するローカル ストレージ、およびメモリ内のみを使用する profileSettings オブジェクト作成する方法を示します。 いずれも、`authDelegateImpl` オブジェクトが作成済みであると想定しています。

## <a name="load-a-profile"></a>プロファイルの読み込み

これで `ProtectionProfileObserverImpl` と `AuthDelegateImpl` を定義したので、それらを使用して `mip::ProtectionProfile` をインスタンス化します。 `mip::ProtectionProfile` オブジェクトの作成には、[`mip::ProtectionProfile::Settings`](reference/class_mip_ProtectionProfile_settings.md) が必要です。

### <a name="protectionprofilesettings-parameters"></a>ProtectionProfile::Settings Parameters

- `std::string path`: ログ、テレメトリ、その他の継続状態が格納されるファイル パス。
- `bool useInMemoryStorage`: 状態を、ディスク上ではなく、すべてメモリに格納するかどうかの定義。
- `std::shared_ptr<mip::AuthDelegate> authDelegate`: クラス `mip::AuthDelegate` の共有ポインター。
- `std::shared_ptr<mip::ProtectionProfile::Observer> observer`: `ProtectionProfile::Observer` の実装への共有ポインター。
- `mip::ApplicationInfo applicationInfo`: オブジェクト。 SDK を利用しているアプリケーションに関する情報を定義するために使用します。

次の 2 つの例では、状態ストレージに対するローカル ストレージ、およびメモリ内のみを使用する profileSettings オブジェクト作成する方法を示します。 いずれも、`authDelegateImpl` オブジェクトが作成済みであると想定しています。

#### <a name="store-state-in-memory-only"></a>メモリ内の状態のみを格納

```cpp
ProtectionProfile::Settings profileSettings(
    "",                                     //path to store settings
    true,                                   //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>ディスク上のストレージ パスからのプロファイル設定の読み取り/書き込み

```cpp
ProtectionProfile::Settings profileSettings(
    "./mip_app_data",                       //path to store settings
    false,                                  //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

次に、promise/future パターンを使用して `ProtectionProfile` を読み込みます。

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<ProtectionProfile>>>();
auto profileFuture = profilePromise->get_future();
ProtectionProfile::LoadAsync(profileSettings, profilePromise);
```

プロファイルを読み込み、その操作が成功した場合、`mip::ProtectionProfile::Observer::OnLoadSuccess` の実装の `ProtectionProfileObserverImpl::OnLoadSuccess` が呼び出されます。 結果のオブジェクトまたは例外のポインターやコンテキストが、関数にパラメーターとして渡されます。 このコンテキストは、非同期操作を処理するために作成した `std::promise` へのポインターです。 この関数は、単純に約束の値を ProtectionProfile オブジェクト (コンテキスト) に設定します。 メイン関数で `Future.get()` を使用する場合、結果は新しいオブジェクトに格納できます。

```cpp
//get the future value and store in profile.
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>まとめ

オブザーバーおよび認証委任を完全に実装したので、プロファイルを完全に読み込めるようになりました。 以下のコードの切り取りでは、すべての必要なハンドラーが既に含まれていると想定しています。

```cpp
int main()
{
    const string userName = "MyTestUser@contoso.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    ProtectionProfile::Settings profileSettings("",
        false,
        authDelegateImpl,
        std::make_shared<ConsentDelegateImpl>(),
        std::make_shared<ProfileObserver>(),
        mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<ProtectionProfile>>>();
    auto profileFuture = profilePromise->get_future();
    ProtectionProfile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

最終結果は、プロファイルの読み込みが成功し、それが `profile` と呼ばれるオブジェクトに格納されます。

## <a name="next-steps"></a>次の手順

これでプロファイルが追加されました。次の手順では、エンジンをプロファイルに追加します。

[保護エンジンの概念](concept-profile-engine-protection-engine-cpp.md)