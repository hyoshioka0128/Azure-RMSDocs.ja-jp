---
title: "方法&#58; エラーとパフォーマンスのログを有効にする | Azure RMS"
description: "Microsoft Rights Management SDK 4.2 では、診断ログとパフォーマンス ログのアップロードを 1 つのデバイス プロパティで管理します。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 1bd4b0c2605a24cd683473b35bfaf8dd0745365a


---

# 方法: エラーとパフォーマンスのログを有効にする
Microsoft Rights Management SDK 4.2 では、診断ログとパフォーマンス ログのアップロードを 1 つのデバイス プロパティで管理します。

## 概要 ##
Microsoft への診断ログとパフォーマンス ログの自動アップロードを有効にすることで、ユーザーのエクスペリエンスとトラブルシューティングを向上させることができます。 ユーザーのプライバシーを保証するために、アプリ開発者は、自動ログ記録を有効にする前に、ユーザーに同意を求める必要があります。

ログ コントロールは、2 つのプロパティを使用して管理します。

-   ログを有効にするには、**IpcCustomerExperienceDataCollectionEnabled** プロパティを使用します。 この設定は、デバイスをリセットしても保持されます。
-   ログ記録レベルは、**IpcLogLevel** プロパティを使用して制御します。次の設定を使用します。

    * 1 - 詳細
    * 2 - 情報
    * 3 - 警告
    * 4 - エラー
    * 5 - 重大

次の各サンプル コード スニペットにおいて、呼び出し元アプリケーションは、プロパティを設定または照会できます。

### Android ###
自動更新を有効にする

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

現在のログ コントロール フラグ設定を取得する

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## iOS ##
自動更新を有効にする

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
        [prefs setBool:FALSE forKey:@&quot;IpcCustomerExperienceDataCollectionEnabled”];
        [[NSUserDefaults standardUserDefaults] synchronize];

現在のログ コントロール フラグ設定を取得する

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcCustomerExperienceDataCollectionEnabled&quot;];

ログ レベル コントロールを設定する

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
      [prefs setInteger:1 forKey:@&quot;IpcLogLevel”];
      [[NSUserDefaults standardUserDefaults] synchronize];

ログ コントロール設定を取得する

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcLogLevel&quot;];
 

## Windows ##
自動更新を有効にする

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

オプションの設定の詳細については、「[CustomerExperienceOptions](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_customerexperienceoptions)」を参照してください。

現在のログ コントロール フラグ設定を取得する

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**注**: 上記の Windows コード スニペットは C++ で記述されています。 C\# の場合は、構文の "::" を  "." に置き換えてください。

**Linux/C++** - この SDK には、他のプラットフォームほど大規模ではないいくつかの基本的なログ記録機能が含まれています。 詳細については、「[RMS SDK for portable C++ (移植可能 C++ のための RMS SDK)](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting)」の "README.md" の「**Troubleshooting (トラブルシューティング)**」セクションを参照してください。

 

 



<!--HONumber=Aug16_HO4-->


