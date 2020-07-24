---
title: 方法&#58; エラーとパフォーマンスのログを有効にする | Azure RMS
description: Microsoft Rights Management SDK 4.2 では、診断ログとパフォーマンス ログのアップロードが 1 つのデバイス プロパティで管理されます。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 4a9f0b375f9e152d44f4d5b5251a9259456db53c
ms.sourcegitcommit: 84b45c949d85a7291c088a050d2a66d356fc9af2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2020
ms.locfileid: "87135710"
---
# <a name="how-to-enable-error-and-performance-logging"></a>方法: エラーとパフォーマンスのログを有効にする
Microsoft Rights Management SDK 4.2 では、診断ログとパフォーマンス ログのアップロードが 1 つのデバイス プロパティで管理されます。

## <a name="overview"></a>概要 ##
診断、パフォーマンス、およびテレメトリに関するデータ ログの Microsoft への自動アップロードを有効にすると、ユーザーのエクスペリエンスとトラブルシューティングを改善できます。 

> [!IMPORTANT] 
> ユーザーのプライバシーを保証するために、アプリ開発者は、自動ログ記録を有効にする前に、ユーザーに同意を求める必要があります。

> [!NOTE]
> たとえば、Microsoft の標準のメッセージでは、ログ記録について次のように通知しています。 
>
> *エラーとパフォーマンスのログ記録をオンにすると、エラーとパフォーマンスのデータを Microsoft に送信することに同意したことになります。 マイクロソフトは、インターネット経由でエラーとパフォーマンスのデータを収集します ("データ")。 Microsoft はこのデータを使用して、Microsoft の製品およびサービスの品質、セキュリティ、および整合性を提供し、改善します。 たとえば、使用する機能、機能の反応速度、デバイスのパフォーマンス、ユーザーインターフェイスの操作、製品で発生した問題など、パフォーマンスと信頼性を分析します。 データには、現在実行しているソフトウェアや IP アドレスなど、ソフトウェアの構成に関する情報も含まれます。*  

ログ コントロールは、2 つのプロパティを使用して管理します。

-   ログを有効にするには、**IpcCustomerExperienceDataCollectionEnabled** プロパティを使用します。 この設定は、デバイスをリセットしても保持されます。
-   ログ記録レベルは、**IpcLogLevel** プロパティを使用して制御します。次の設定を使用します。

    * 1 - 詳細
    * 2 - 情報
    * 3 - 警告
    * 4 - エラー
    * 5 - 重大

次の各サンプル コード スニペットにおいて、呼び出し元アプリケーションは、プロパティを設定または照会できます。

### <a name="android"></a>Android ###
自動更新を有効にする

```java
SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
SharedPreferences.Editor editor = preferences.edit();
editor.putBoolean("IpcCustomerExperienceDataCollectionEnabled", true);
editor.commit();
```

現在のログ コントロール フラグ設定を取得する

```java
SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);
```

## <a name="ios"></a>iOS ##
自動更新を有効にする

```objectivec
NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
    [prefs setBool:FALSE forKey:@"IpcCustomerExperienceDataCollectionEnabled"];
    [[NSUserDefaults standardUserDefaults] synchronize];
```

現在のログ コントロール フラグ設定を取得する

```java
[[NSUserDefaults standardUserDefaults] boolForKey:@"IpcCustomerExperienceDataCollectionEnabled"];
```

ログ レベル コントロールを設定する

```java
NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
    [prefs setInteger:1 forKey:@"IpcLogLevel"];
    [[NSUserDefaults standardUserDefaults] synchronize];
```

ログ コントロール設定を取得する

```java
[[NSUserDefaults standardUserDefaults] boolForKey:@"IpcLogLevel"];
```

## <a name="windows"></a>Windows ##
自動更新を有効にする

```cpp
CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;
```

オプションの設定の詳細については、「[CustomerExperienceOptions](https://msdn.microsoft.com/library/microsoft.rightsmanagement.customerexperienceoptions.aspx)」を参照してください。

現在のログ コントロール フラグ設定を取得する

```cpp
CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;
```

**注**: 上記の Windows コード スニペットは C++ で記述されています。 C\# の場合は、構文の "::" を  "." に置き換えてください。

**Linux/C++** - この SDK には、他のプラットフォームほど大規模ではないいくつかの基本的なログ記録機能が含まれています。 詳細については、「[RMS SDK for portable C++ (移植可能 C++ のための RMS SDK)](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting)」の "README.md" の「**Troubleshooting (トラブルシューティング)**」セクションを参照してください。
