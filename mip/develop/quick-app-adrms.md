---
title: クイック スタート - Active Directory Rights Management Server の保護
description: Active Directory Rights Management Server (AD RMS) を使うように MIP SDK を構成する方法を示すクイック スタートです
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/17/2019
ms.author: tommos
ms.openlocfilehash: 32e2cc1cb3924c5a4181bd4cafaaf3f53f085c00
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764216"
---
# <a name="quickstart-active-directory-rights-management-server-ad-rms-protection"></a>クイック スタート:Active Directory Rights Management Server (AD RMS) の保護

このクイック スタートでは、MIP SDK を使って Active Directory Rights Management Server (AD RMS) のサポートを実装する方法について説明します。

> [!NOTE]
> このクイック スタートで説明されている手順は、C# または C++ 用のファイル API と、C++ 用の保護 API にのみ適用できます。

## <a name="prerequisites"></a>[前提条件]

まだ完了していない場合は、必ず次の操作を行ってください。

- 「[クイック スタート: クライアント アプリケーションの初期化 (C++)](quick-app-initialization-cpp.md)」をまず完了し、スターター Visual Studio ソリューションを構築します。
- 「[クイック スタート: 機密ラベルの一覧表示 (C++)](quick-file-list-labels-cpp.md)」または「[クイック スタート: 機密ラベルの一覧表示 (C#)](quick-file-list-labels-csharp.md)」を完了します
- [モバイル デバイス拡張機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11))を使って AD RMS を展開します。
- 必要に応じて、[AD RMS MDE 用の DNS SRV レコード](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn673574(v%3dws.11)#specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension)が発行されていることを確認します。

## <a name="service-discovery"></a>サービス検出

SDK では、UPN またはメール アドレスのサフィックスを使うことで、`FileEngineSettings` または `ProtectionEngineSettings` 経由で提供される `mip::Identity` に基づいてサービス検出を実行します。 まず、MDE の *_rmsdisco* レコードのドメイン階層が検索されます。 このプロセスの詳細については、「[AD RMS モバイル デバイス拡張機能用の DNS SRV レコードの指定](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn673574(v%3dws.11)#specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension)」をご確認ください。 その DNS SRV レコードが見つからない場合は、サービスの場所として Azure Information Protection サービスが規定値となります。

ID が使用できない場合、または MDE の DNS SRV レコードが発行されていない場合は、[クラウド エンドポイントの URL](https://docs.microsoft.com/information-protection/develop/reference/class_mip_fileengine_settings#setpolicycloudendpointbaseurl-function) を明示的に設定することによって、サービス検出のプロセスをオーバーライドできます。

## <a name="configuring-file-api-in-c-to-use-ad-rms"></a>AD RMS を使うように C# でファイル API を構成する

お客様のアプリケーションで C# の Active Directory 認証ライブラリ (ADAL) とファイル API が使われている場合は、わずかな変更が 2 点必要です。 `FileEngineSettings` オブジェクトと `AuthenticationContext` コンストラクターを更新して、AD RMS および Active Directory フェデレーション サービス (ADFS) と共に機能するようにする必要があります。

モバイル デバイス拡張機能の DNS SRV レコードを展開済みで、ユーザー プリンシパル名またはメール アドレスを渡すことを計画している場合は、[ID を使う場合の手順に従ってください](#update-the-file-engine-settings-to-use-ad-rms-with-an-identity)。

モバイル デバイス拡張機能の DNS SRV レコードがない場合、または実行時に ID がない場合は、[明示的なエンドポイントの指示に従ってください](#update-the-file-engine-settings-to-use-ad-rms-with-an-explicit-endpoint)。

### <a name="update-the-file-engine-settings-to-use-ad-rms-with-an-identity"></a>ID と共に AD RMS を使うようにファイル エンジン設定を更新する

MDE の DNS SRV レコードが発行済みで、エンジン設定の一部として `Microsoft.InformationProtection.Identity` が提供されている場合、必要なコード変更は `FileEngineSettings.ProtectionOnlyEngine = true` を設定することだけです。 AD RMS の保護エンドポイントではラベル付け (ポリシー) 操作がサポートされていないため、このプロパティを設定する必要があります。

```csharp
// Configure FileEngineSettings as protection only engine.
var engineSettings = new FileEngineSettings("", authDelegate, "", "en-US")
{
     // Provide the identity for service discovery.
     Identity = identity,
     // Set ProtectionOnlyEngine to true for AD RMS as labeling isn't supported
     ProtectionOnlyEngine = true
};
```

### <a name="update-the-file-engine-settings-to-use-ad-rms-with-an-explicit-endpoint"></a>明示的なエンドポイントと共に AD RMS を使うようにファイル エンジン設定を更新する

MDE の DNS SRV レコードが発行されていない場合、またはを `FileEngine` を作成するときに `Microsoft.InformationProtection.Identity` を渡すことができない場合は、コード変更を 2 点加える必要があります。 `FileEngineSettings.ProtectionOnlyEngine = true` を設定します。 AD RMS の保護エンドポイントではラベル付け (ポリシー) 操作がサポートされていないため、このプロパティを設定する必要があります。

```csharp
// Configure FileEngineSettings as protection only engine and generate a unique engine id.
var engineSettings = new FileEngineSettings("", authDelegate, "", "en-US")
{
     // Set ProtectionOnlyEngine to true for AD RMS as labeling isn't supported
     ProtectionOnlyEngine = true,
     // Provide the explicit AD RMS endpoint
     ProtectionCloudEndpointBaseUrl = "https://rms.contoso.com"
};
```

### <a name="update-the-authentication-delegate"></a>認証委任を更新する

お客様の .NET アプリケーションで ADAL を使っている場合は、`Microsoft.InformationProtection.AuthDelegate` の実装を変更して、機関の検証を無効にする必要があります。 `AuthenticationContext` コンストラクターで `validateAuthority` を **false** に設定することで、機関の検証を無効にします。

   ```csharp
   AuthenticationContext authContext = new AuthenticationContext(authority, false, tokenCache);
   ```

## <a name="configuring-file-api-in-c-to-use-ad-rms"></a>AD RMS を使うように C++ でファイル API を構成する

モバイル デバイス拡張機能の DNS SRV レコードを展開済みで、ユーザー プリンシパル名またはメール アドレスを渡すことを計画している場合は、[ID を使う場合の手順に従ってください](#update-the-fileenginesettings-to-use-ad-rms-with-an-identity)。

モバイル デバイス拡張機能の DNS SRV レコードがない場合、または実行時に ID がない場合は、[明示的なエンドポイントの指示に従ってください](#update-the-fileenginesettings-to-use-ad-rms-with-an-explicit-endpoint)。

### <a name="update-the-fileenginesettings-to-use-ad-rms-with-an-identity"></a>ID と共に AD RMS を使うように FileEngine::Settings を更新する

MDE の DNS SRV レコードが発行済みで、`FileEngine::Settings` で `mip::Identity` が提供されている場合、唯一の操作はエンジンを保護専用エンジンに設定することです。

```cpp
FileEngine::Settings engineSettings(mip::Identity(mUsername), "");
engineSettings.SetProtectionOnlyEngine = true;
```

### <a name="update-the-fileenginesettings-to-use-ad-rms-with-an-explicit-endpoint"></a>明示的なエンドポイントと共に AD RMS を使うように FileEngine::Settings を更新する

MDE の DNS SRV レコードが発行されていない場合、またはサービス検出に ID を使用できない場合は、エンジンを保護専用に、かつ `SetProtectionCloudEndpointBaseUrl()` 経由で指定される明示的なクラウド エンドポイントの URL に設定する必要があります。

```cpp
FileEngine::Settings engineSettings("", authDelegate, "");
engineSettings.SetProtectionOnlyEngine = true;
engineSettings.SetProtectionCloudEndpointBaseUrl("https://rms.contoso.com");
```

## <a name="configuring-protection-api-in-c-to-use-ad-rms"></a>AD RMS を使うように C++ で保護 API を構成する

モバイル デバイス拡張機能の DNS SRV レコードを展開済みで、ユーザー プリンシパル名またはメール アドレスを渡すことを計画している場合は、[ID を使う場合の手順に従ってください](#set-the-protectionenginesettings-to-use-ad-rms-with-an-identity)。

モバイル デバイス拡張機能の DNS SRV レコードがない場合、または実行時に ID がない場合は、[明示的なエンドポイントの指示に従ってください](#set-the-protectionenginesettings-to-use-ad-rms-with-an-explicit-endpoint)。

### <a name="set-the-protectionenginesettings-to-use-ad-rms-with-an-identity"></a>ID と共に AD RMS を使うように ProtectionEngine::Settings を設定する

モバイル デバイス拡張機能の DNS SRV レコードが発行済みで、`ProtectionEngine::Settings` で ID が提供されている場合は、AD RMS を使うために追加のコード変更を行う必要はありません。 サービス検出によって AD RMS エンドポイントが検索され、それを使って保護操作が実行されます。

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity(mUsername), authDelegate, "");
```

### <a name="set-the-protectionenginesettings-to-use-ad-rms-with-an-explicit-endpoint"></a>明示的なエンドポイントと共に AD RMS を使うように ProtectionEngine::Settings を設定する

DNS SRV レコードが発行されていない場合、または `ProtectionEngine::Settings` で ID が提供されていない場合は、`SetProtectionCloudEndpointBaseUrl()` を使って明示的に保護エンドポイントの URL を設定する必要があります。

```cpp
ProtectionEngine::Settings engineSettings("", authDelegate, "");
engineSettings.SetProtectionCloudEndpointBaseUrl("https://RMS.CONTOSO.COM");
```

## <a name="remove-or-comment-label-references"></a>ラベルの参照を削除またはコメント化する

クイック スタート ガイドのいずれかからアプリケーションを構築する場合、`fileEngine.SensitivityLabels` または `engine->ListSensitivityLabels();` という形式で、アプリケーションにラベルへの参照が含まれていることがわかります。 このアプリケーションは保護専用に設定されているため、これらのコード ブロックはコメント アウトするか、削除する必要があります。これらを実行すると例外が発生します。

## <a name="next-steps"></a>次のステップ

これで AD RMS をサポートするための変更を行ったので、お客様のアプリケーションでは、保護プロバイダーとして AD RMS サービスを使い、任意の保護専用の操作を実行できるようになりました。
