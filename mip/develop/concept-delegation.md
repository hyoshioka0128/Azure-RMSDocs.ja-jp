---
title: 概念-委任
description: この記事は、MIP SDK での委任に関する概念を理解するのに役立ちます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 848b0752f6158ade4fd61b562163e2e641454773
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225021"
---
# <a name="concept---delegation-in-the-mip-sdk"></a>概念-MIP SDK での委任

Microsoft Information Protection SDK には、サービスベースのアプリケーションが別のユーザーの代理として動作するための2つのパスが用意されています。 サービス id とは異なるユーザー id のコンテキストで、ファイルのラベル付け、保護、または使用を行う必要がある場合は、委任が必要になることがあります。 この委任された id は、 **エンジン** レベルまたは **ハンドラー** レベルで設定できます。設定される場所は、ユースケースによって異なります。

## <a name="engine-settings-based-delegation"></a>エンジン設定ベースの委任

MIP SDK は、すべての Sdk の設定オブジェクトに、委任されたユーザーの電子メールアドレスを提供することをサポートしています。ファイル、保護、およびポリシー。 これを実現するには、設定オブジェクトのプロパティを設定し `DelegatedUserEmail` ます。 結果として、その設定オブジェクトを使用して初期化されたエンジンは、プロパティにユーザーが指定した場合と同じように、 **すべての MIP 操作** を実行し `DelegatedUserEmail` ます。 特定のユーザーに対してポリシーがフェッチされ、保護されているファイルの所有者であることを含め、すべての保護操作がそのユーザーとして実行されます。

このパターンは、サービスベースのアプリケーションをユーザーとして完全に動作させる必要がある場合に役立ちます。ポリシーは、指定されたユーザーに対してのみフェッチする必要があり、復号化操作はユーザー id のコンテキストで実行する必要があります。 このエンジンを作成するときは、アプリケーションがそのユーザーに固有のエンジン ID (多くの場合、メールアドレス) を指定することが重要です。 これにより、キャッシュの利点が確実に実現されます。 一意のエンジン ID が指定されていない場合、アプリケーションのパフォーマンスが低下する可能性があります。

### <a name="file-sdk"></a>ファイル SDK

次のサンプルは、C++ および C# でファイル SDK アプリケーションの委任された id を設定する方法を示しています。 ポリシー SDK でも同じパターンを使用できます。

このサンプルでは、.NET の File SDK で **デリゲートエンジン** を作成する方法を示します。

```csharp
// C# Example for creating a delegated file engine
string delegatedUserEmail = "alice@contoso.com";
var engineSettings = new PolicyEngineSettings(delegatedUserEmail, authDelegate, "", "en-US")
{
    // Provide the identity for service discovery.
    Identity = identity,
    // Set the identity for which all MIP operations will be performed.
    DelegatedUserEmail = delegatedUserEmail
};

var engine = Task.Run(async () => await profile.AddEngineAsync(engineSettings)).Result;
```

このサンプルでは、C++ の File SDK で **デリゲートエンジン** を作成する方法を示します。

```c++
// C++ Example for creating a delegated file engine
std::string delegatedUserEmail = "alice@contoso.com";
FileEngine::Settings engineSettings(delegatedUserEmail, mAuthDelegate, "", "en-US", false);
// Set the identity for which all MIP operations will be performed. 
engineSettings.SetDelegatedUserEmail(delegatedUserEmail);

auto enginePromise = std::make_shared<std::promise<std::shared_ptr<FileEngine>>>();
auto engineFuture = enginePromise->get_future();

mProfile->AddEngineAsync(engineSettings, enginePromise);
mEngine = engineFuture.get();
```

結果として、指定したユーザーの代わりにすべてのファイルエンジンが作成されます。


## <a name="handler-based-delegation"></a>ハンドラーベースの委任

特定のユーザー id のコンテキストでのみファイルを **保護** する必要があるシナリオでは、は、 `FileHandler` オブジェクトを介してユーザー id を渡すためのメソッドを提供し `ProtectionSettings` ます。 ポリシーと暗号化解除操作は、認証済みの **サービス id** として実行されます。 保護アクションは、指定されたユーザーの代わりに実行されます。そのユーザーは、ドキュメントの MIP 保護の **所有者** になります。

### <a name="file-sdk"></a>ファイル SDK

オブジェクトに対して指定されたユーザーとして、直接または via のラベルを使用して保護を適用する操作のみが実行され `ProtectionSettings` ます。 このオブジェクトは、 `SetLabel()` `SetProtection()` File SDK の関数または関数に渡されます。

このサンプルでは、.NET で File SDK に対して **委任保護操作** を実行する方法を示します。

```csharp
string delegatedUserEmail = "bob@contoso.com";
ProtectionSettings protectionSettings = new ProtectionSettings()
{
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};
handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, protectionSettings);
// Similar pattern for SetProtection()
// handler.SetProtection(protectionDescriptor, protectionSettings);
```

このサンプルでは、C++ の File SDK での **デリゲート保護操作** を実行する方法を示します。

```c++
mip::ProtectionSettings protectionSettings;
// Set the delegated mail address 
protectionSettings.SetDelegatedUserEmail(delegatedUserEmail);
handler->SetLabel(mEngine->GetLabelById(labelId), labelingOptions, protectionSettings);
```

その結果、保護が適用されるすべてのハンドラー **書き込み** 操作が委任されたユーザーとして実行されます。 

### <a name="protection-sdk"></a>保護 SDK

保護 SDK の機能は、File SDK とは異なります。 作成できる **ハンドラーに** は、発行用と使用用の2種類があります。 ファイル SDK と同様に、委任されたメールアドレスは、ハンドラーの種類ごとに設定オブジェクトを使用して設定します。

#### <a name="net"></a>.NET

このサンプルでは、委任された **発行** を実行する方法を示します。

```csharp
string delegatedUserEmail = "bob@contoso.com";
PublishingSettings publishingSettings = new PublishingSettings(protectionDescriptor)
{
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};          
var protectionHandler = engine.CreateProtectionHandlerForPublishing(publishingSettings);
```

このサンプルでは、委任された使用 **量** を実行する方法を示します。

```csharp
string delegatedUserEmail = "bob@contoso.com";
ConsumptionSettings consumptionSettings = new ConsumptionSettings(plInfo)
{                
    ContentName = "A few bytes.",
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};
var protectionHandler = engine.CreateProtectionHandlerForConsumption(consumptionSettings);
```

#### <a name="c"></a>C++

このサンプルでは、委任された使用 **量** を実行する方法を示します。

```c++
string delegatedUserEmail = "bob@contoso.com";
mip::ProtectionHandler::PublishingSettings publishingSettings = mip::ProtectionHandler::PublishingSettings(descriptor);
// Set the delegated mail address 
publishingSettings.SetDelegatedUserEmail(delegatedUserEmail);
mEngine->CreateProtectionHandlerForPublishingAsync(publishingSettings, handlerObserver, handlerPromise);
auto handler = handlerFuture.get(); 
```

このサンプルでは、委任された **発行** を実行する方法を示します。

```c++
string delegatedUserEmail = "bob@contoso.com";
mip::ProtectionHandler::ConsumptionSettings consumptionSettings = mip::ProtectionHandler::ConsumptionSettings(serializedPublishingLicense);
// Set the delegated mail address 
consumptionSettings.SetDelegatedUserEmail(delegatedUserEmail);
mEngine->CreateProtectionHandlerForConsumptionAsync(consumptionSettings, handlerObserver, handlerPromise);
auto handler = handlerFuture.get(); 
```

## <a name="required-permissions"></a>必要なアクセス許可

上記の各シナリオでは、異なるアクセス許可のセットが必要です。 

| シナリオ                             | 必要な権限                                                             |
| ------------------------------------ | ------------------------------------------------------------------------------- |
| ファイル SDK の委任されたエンジン            | UnifiedPolicy<br>DelegatedReader<br>DelegatedWriter |
| ポリシー SDK の委任されたエンジン          | UnifiedPolicy                                                       |
| File SDK の委任されたハンドラー           | DelegatedWriter                                                         |
| 保護 SDK の委任された発行     | DelegatedWriter                                                         |
| 保護 SDK の委任された使用量 | DelegatedReader                                                         |

アクセス許可の詳細および設定場所については、「 [Microsoft INFORMATION PROTECTION SDK の API アクセス許可](concept-api-permissions.md)」を参照してください。

## <a name="next-steps"></a>次の手順

- [Microsoft INFORMATION PROTECTION SDK の API アクセス許可](concept-api-permissions.md)を確認する
- <TODO>サービスプリンシパルの追加認証の参照を確認します。