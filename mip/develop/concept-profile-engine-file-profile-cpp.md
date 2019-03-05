---
title: 概念 - ファイル API プロファイル オブジェクト
description: この記事は、アプリケーションの初期化中に作成される、ファイル プロファイル オブジェクトに関する概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 19b283017929858299bd1c9af0662b170b4206f0
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333012"
---
# <a name="microsoft-information-protection-sdk---file-api-profile-concepts"></a>Microsoft Information Protection SDK - ファイル API プロファイルの概念

プロファイルは、MIP SDK のすべての操作のルート クラスです。 ファイル API 機能のいずれかを使用する前に、`FileProfile` を作成する必要があり、今後の操作はすべて、プロファイルまたはプロファイルに*追加された*その他のオブジェクトによって実行されます。

プロファイルをインスタンス化しようとする前に、満たす必要があるいくつかのコード条件があります。

- `AuthDelegateImpl` は `mip::AuthDelegate` を拡張するために実装されます。
- `ConsentDelegateImpl` は `mip::ConsentDelegate` を拡張するために実装されます。
- アプリケーションが [Azure Active Directory に登録されており](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md)、クライアント ID がアプリケーションまたは構成ファイルにハードコードされています。 
- `mip::FileProfile::Observer` を継承しているクラスは適切に実装されています。

## <a name="load-a-profile"></a>プロファイルの読み込み

`ProfileObserver`、`ConsentDelegateImpl`、および `AuthDelegateImpl` が定義されると、`mip::FileProfile` はインスタンス化できるようになります。 `mip::FileProfile` オブジェクトを作成するには、`FileProfile` に関する設定情報をすべて格納するために [`mip::FileProfile::Settings`](reference/class_mip_fileprofile_settings.md) が必要です。

### <a name="fileprofilesettings-parameters"></a>FileProfile::Settings パラメーター

`FileProfile::Settings` コンストラクターでは、以下に一覧された 5 つのパラメーターを受け取ります。

- `std::string path`:ファイルのパスをログ、テレメトリ、およびその他の永続的な状態が格納されます。
- `bool useInMemoryStorage`:すべての状態をディスク上ではなくメモリに格納する必要があるかどうかを定義します。
- `std::shared_ptr<mip::AuthDelegate> authDelegate`:クラスの共有ポインター `mip::AuthDelegate` 
- `std::shared_ptr<mip::ConsentDelegate>`: 
- `std::shared_ptr<mip::FileProfile::Observer> observer`:共有へのポインター、`FileProfile::Observer`実装します。
- `mip::ApplicationInfo applicationInfo`: オブジェクト。 SDK を利用しているアプリケーションに関する情報を定義するために使用します。

次の例では、状態ストレージに対するローカル ストレージ、およびメモリ内のみを使用する `profileSettings` オブジェクトを作成する方法を示します。 いずれも、`authDelegateImpl` オブジェクトが作成済みであると想定しています。

#### <a name="store-state-in-memory-only"></a>メモリ内の状態のみを格納

```cpp
FileProfile::Settings profileSettings(
    "",                                          //path to store settings
    true,                                        //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>ディスク上のストレージ パスからのプロファイル設定の読み取り/書き込み

次のコードの切り取りでは、`FileProfile` に `./mip_app_data` でアプリの状態データをすべて格納するように指示します。

```cpp
FileProfile::Settings profileSettings(
    "./mip_app_data",                            //path to store settings
    false,                                       //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="load-the-profile"></a>プロファイルの読み込み

上記いずれかの方法の詳細を使用して、promise/future パターンを使用して `FileProfile` を読み込みます。

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<FileProfile>>>();
auto profileFuture = profilePromise->get_future();
FileProfile::LoadAsync(profileSettings, profilePromise);
```

プロファイルを読み込み、その操作が成功した場合、`mip::FileProfile::Observer::OnLoadSuccess` の実装の `ProfileObserver::OnLoadSuccess` が呼び出されます。 結果のオブジェクトまたは例外のポインターやコンテキストが、関数にパラメーターとして渡されます。 このコンテキストは、非同期操作を処理するために作成した `std::promise` へのポインターです。 関数では最初のパラメーターに渡した FileProfile オブジェクトへの promise の値を設定するだけです。 メイン関数で `Future.get()` を使用する場合、結果は新しいオブジェクトに格納できます。

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

    FileProfile::Settings profileSettings("",
            false,
            authDelegateImpl,
            std::make_shared<ConsentDelegateImpl>(),
            std::make_shared<ProfileObserver>(),
            mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<FileProfile>>>();
    auto profileFuture = profilePromise->get_future();
    FileProfile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

最終結果は、プロファイルの読み込みが成功し、それが `profile` と呼ばれるオブジェクトに格納されます。

## <a name="next-steps"></a>次の手順

これでプロファイルが追加されました。次の手順では、エンジンをプロファイルに追加します。 

- [ファイル エンジンの概念](concept-profile-engine-file-engine-cpp.md)
