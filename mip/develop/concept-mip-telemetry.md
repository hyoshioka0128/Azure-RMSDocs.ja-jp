---
title: 概念-MIP SDK-テレメトリコントロールの主要な概念
description: この記事は、テレメトリを無効にする方法と、オプトアウト時に送信されるイベントを理解するのに役立ちます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 10/01/2019
ms.author: tommos
ms.openlocfilehash: 3d97bdbf5307d7f0faefe6b6434b1df1ebc67798
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74484855"
---
# <a name="microsoft-information-protection-sdk---telemetry-configuration"></a>Microsoft Information Protection SDK-テレメトリ構成

## <a name="telemetry"></a>製品利用統計情報

既定では、Microsoft Information Protection SDK はテレメトリデータを Microsoft に送信します。 このテレメトリデータは、内部テストではキャプチャされない可能性がある SDK インストールベース全体のバグ、品質、およびパフォーマンスの問題のトラブルシューティングに役立ちます。 SDK を使用してアプリケーションを実装する場合は、必要に応じて、ユーザーと管理者にテレメトリをオプトアウトする機能を提供することが重要です。

## <a name="telemetry-configuration"></a>テレメトリの構成

MIP SDK のテレメトリオプションは、 [TelemetryConfiguration](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.telemetryconfiguration?view=mipsdk-dotnet)を使用して制御できます。 このクラスのインスタンスを作成し、 **IsTelemetryOptedOut**を true に設定します。 **MipContext**を作成するために使用される関数に、 **TelemetryConfiguration**クラスのオブジェクトを指定します。 これにより、テレメトリデータが完全に削除されるわけではありませんが、エンドユーザーを特定できるすべての情報スキャンされを使用して最小限のセットに減らすことができます。

### <a name="minimum-telemetry-events"></a>最小テレメトリイベント

テレメトリが*オプトアウト*に設定されている場合、データの最小セットが Microsoft に送信されます。 個人を特定できる情報はすべて、この情報からスキャンされます。 このデータには、SDK が使用されていること、およびシステムメタデータを理解するためのハートビート情報が含まれています。 **ユーザーのコンテンツまたはエンドユーザーを特定できる情報がサービスに設定されていません。**

以下の表を確認して、最小テレメトリセットと共に送信されるイベントとデータを正確に確認してください。

#### <a name="event-heartbeat"></a>イベント: ハートビート

| 名前                                 | [説明]                                                                            | スキャンされ |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| アプリケーションの ApplicationId                    | Mip:: ApplicationInfo を使用して指定されたアプリケーション id。                          | [いいえ]       |
| App.xaml                  | Mip:: ApplicationInfo を使用して指定されたアプリケーション名。                                | [いいえ]       |
| App.config バージョン               | Mip:: ApplicationInfo を使用してアプリケーションのバージョンを示します。                             | [いいえ]       |
| ApplicationId                        | Mip:: ApplicationInfo を使用してアプリケーションのバージョンを示します。                             | [いいえ]       |
| ApplicationName                      | Mip:: ApplicationInfo を使用して指定されたアプリケーション名。                                | [いいえ]       |
| CreationTime                         | タイムイベントが生成されました。                                                              | [いいえ]       |
| DefaultLabel.Id                      | テナントの既定のラベル ID。                                                               | [いいえ]       |
| エンジン TenantId                      | 認証されたユーザーのホームテナント GUID。                                            | [いいえ]       |
| エンジン. UserObjectId                  | Azure Active Directory のユーザーオブジェクト ID。                                              | [いいえ]       |
| イベント id                  | イベントをトリガーしたオブジェクトに関連付けられている一意の ID が生成されました。                   | [いいえ]       |
| イベント. CorrelationIdDescription       | C++イベントを発生させたオブジェクトのクラス名。                                     | [いいえ]       |
| イベント ParentCorrelationId            | 親イベントの相関 ID。                                                           | [いいえ]       |
| イベント ParentCorrelationIdDescription | イベントをトリガーしたオブジェクトの親に関連付けられた一意の ID が生成されます。 | [いいえ]       |
| イベント UniqueId                       | イベントに割り当てられた一意の ID が生成されます。                                             | [いいえ]       |
| MachineName                          | イベントを生成したシステムの名前。                                           | **はい**  |
| MIP.バージョン                          | MIP SDK のバージョン。                                                                | [いいえ]       |
| 操作                            | ハートビート                                                                              | [いいえ]       |
| OrganizationId                       | 認証されたユーザーのホームテナント GUID。                                            | [いいえ]       |
| プラットフォーム                             | オペレーティング システムのバージョン。                                                              | [いいえ]       |
| ProcessName                          | SDK を使用したプロセスの名前。                                                     | [いいえ]       |
| ProductVersion                       | "App.config バージョン" と同じです。                                                      | [いいえ]       |
| SDKVersion                           | MIP と同じです。バージョン。                                                                   | [いいえ]       |
| UserId                               | ユーザーの電子メール アドレス。                                                             | **はい**  |
| UserObjectId                         | ユーザーのオブジェクト ID Azure AD ます。                                                        | [いいえ]       |
| バージョン                              | 監査バージョンスキーマ ("1.1")。                                                          | [いいえ]       |

#### <a name="event-discovery"></a>イベント: 検出

| 名前                                 | [説明]                                                                            | スキャンされ |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | イベントの関連付けに使用される、このイベントの一意のアクション ID。                           | [いいえ]       |
| アプリケーションの ApplicationId                    | Mip:: ApplicationInfo を使用して指定されたアプリケーション id。                          | [いいえ]       |
| App.xaml                  | Mip:: ApplicationInfo を使用して指定されたアプリケーション名。                                | [いいえ]       |
| App.config バージョン               | Mip:: ApplicationInfo を使用してアプリケーションのバージョンを示します。                             | [いいえ]       |
| ApplicationId                        | Mip:: ApplicationInfo を使用してアプリケーションのバージョンを示します。                             | [いいえ]       |
| ApplicationName                      | Mip:: ApplicationInfo を使用して指定されたアプリケーション名。                                | [いいえ]       |
| CreationTime                         | タイムイベントが生成されました。                                                              | [いいえ]       |
| dataState                            | アプリケーションとしてのデータの状態は、"REST"、"MOTION"、"USE" に対して動作します。           | [いいえ]       |
| DefaultLabel.Id                      | テナントの既定のラベル識別子。                                                       | [いいえ]       |
| エンジン TenantId                      | 認証されたユーザーのホームテナント GUID。                                            | [いいえ]       |
| エンジン. UserObjectId                  | Azure Active Directory のユーザーオブジェクト識別子。                                      | [いいえ]       |
| イベント id                  | イベントをトリガーしたオブジェクトに関連付けられている一意の ID が生成されました。                   | [いいえ]       |
| イベント. CorrelationIdDescription       | C++イベントを発生させたオブジェクトのクラス名。                                     | [いいえ]       |
| イベント ParentCorrelationId            | 親イベントの相関 ID。                                                           | [いいえ]       |
| イベント ParentCorrelationIdDescription | イベントをトリガーしたオブジェクトの親に関連付けられた一意の ID が生成されます。 | [いいえ]       |
| イベント UniqueId                       | イベントに割り当てられた一意の ID が生成されます。                                             | [いいえ]       |
| LabelId                              | 開いているファイルまたはデータのコンテンツラベル識別子。                                   | [いいえ]       |
| MachineName                          | イベントを生成したシステムの名前。                                           | **はい**  |
| MIP.バージョン                          | MIP SDK のバージョン。                                                                | [いいえ]       |
| ObjectId                             | ファイルのパスとファイルの説明。                                             | **はい**  |
| 操作                            | "検出"。                                                                           | [いいえ]       |
| OrganizationId                       | 認証されたユーザーのホームテナント GUID。                                            | [いいえ]       |
| プラットフォーム                             | オペレーティング システムのバージョン。                                                              | [いいえ]       |
| ProcessName                          | SDK を使用したプロセスの名前。                                                     | [いいえ]       |
| 保護                            | ファイルが保護されているかどうかを示すブール値。                                       | [いいえ]       |
| Protection                           | 保護テンプレート識別子。                                                    | **はい**  |
| ProtectionOwner                      | 保護所有者の電子メールアドレス。                                                 | **はい**  |
| SDKVersion                           | MIP と同じです。バージョン。                                                                   | [いいえ]       |
| UserId                               | ユーザーの電子メール アドレス。                                                             | **はい**  |
| UserObjectId                         | ユーザーのオブジェクト ID Azure AD ます。                                                        | [いいえ]       |
| バージョン                              | 監査バージョンスキーマ ("1.1")。                                                          | [いいえ]       |

#### <a name="event-label-change"></a>イベント: ラベルの変更

| 名前                                 | [説明]                                                                            | スキャンされ |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | イベントの関連付けに使用される、このイベントの一意のアクション ID。                           | [いいえ]       |
| ActionIdBefore                       | 以前のアクション ID。 新しいアクション ID にチェーンするために使用されます。                                    | [いいえ]       |
| ActionSource                         | MIP:: ActionSource の値。                                                            | [いいえ]       |
| アプリケーションの ApplicationId                    | Mip:: ApplicationInfo を使用して提供されたアプリケーション ID。                                  | [いいえ]       |
| App.xaml                  | Mip:: ApplicationInfo を使用して指定されたアプリケーション名。                                | [いいえ]       |
| App.config バージョン               | Mip:: ApplicationInfo を使用してアプリケーションのバージョンを示します。                             | [いいえ]       |
| ApplicationId                        | Mip:: ApplicationInfo を使用して提供されたアプリケーション ID。                                  | [いいえ]       |
| ApplicationName                      | Mip:: ApplicationInfo を使用して指定されたアプリケーション名。                                | [いいえ]       |
| CreationTime                         | イベントが生成された時刻。                                                          | [いいえ]       |
| dataState                            | アプリケーションとしてのデータの状態は、"REST"、"MOTION"、"USE" に対して動作します。           | [いいえ]       |
| DefaultLabel.Id                      | テナントの既定のラベル識別子。                                                       | [いいえ]       |
| エンジン TenantId                      | 認証されたユーザーのホームテナント GUID。                                            | [いいえ]       |
| エンジン. UserObjectId                  | Azure Active Directory のユーザーオブジェクト識別子。                                      | [いいえ]       |
| イベント id                  | イベントをトリガーしたオブジェクトに関連付けられている一意の ID が生成されました。                   | [いいえ]       |
| イベント. CorrelationIdDescription       | C++イベントを発生させたオブジェクトのクラス名。                                     | [いいえ]       |
| イベント ParentCorrelationId            | 親イベントの相関 ID。                                                           | [いいえ]       |
| イベント ParentCorrelationIdDescription | イベントをトリガーしたオブジェクトの親に関連付けられた一意の ID が生成されます。 | [いいえ]       |
| イベント UniqueId                       | イベントに割り当てられた一意の ID が生成されます。                                             | [いいえ]       |
| IsLabelChanged                       | ラベルが変更されたかどうかを示すブール値。                                                  | [いいえ]       |
| IsProtectionChanged                  | 保護が変更されたかどうかを示すブール値。                                                 | [いいえ]       |
| LabelId                              | ファイルまたはデータに適用されるラベル ID。                                    | [いいえ]       |
| Labの前に                        | ファイルまたはデータに対する以前のラベル ID。                                        | [いいえ]       |
| MachineName                          | イベントを生成したシステムの名前。                                           | **はい**  |
| MIP.バージョン                          | MIP SDK のバージョン。                                                                | [いいえ]       |
| ObjectId                             | ファイルのパスとファイルの説明。                                             | **はい**  |
| 操作                            | "変更"。                                                                              | [いいえ]       |
| OrganizationId                       | 認証されたユーザーのホームテナント GUID。                                            | [いいえ]       |
| プラットフォーム                             | オペレーティング システムのバージョン。                                                              | [いいえ]       |
| ProcessName                          | SDK を使用したプロセスの名前。                                                     | [いいえ]       |
| 製品バージョン                      |                                                                                        | [いいえ]       |
| 保護                            | ファイルが保護されているかどうかを示すブール値。                                       | [いいえ]       |
| 保護前                     | ファイルが既に保護されているかどうかを示すブール値。                           | [いいえ]       |
| Protection                           | 保護テンプレート識別子。                                                    | [いいえ]       |
| 以前の保護                    | 以前の保護テンプレート識別子。                                           | [いいえ]       |
| ProtectionContentId                  | 新しいコンテンツ識別子 (GUID)。                                                     | [いいえ]       |
| ProtectionContentIdBefore            | 以前のコンテンツ識別子 (GUID)。                                                | [いいえ]       |
| ProtectionOwner                      | 保護所有者の電子メールアドレス。                                                 | **はい**  |
| ProtectionOwnerBefore                | 保護所有者の前の電子メールアドレス。                                        | **はい**  |
| SDKVersion                           | MIP と同じです。バージョン。                                                                   | [いいえ]       |
| UserId                               | ユーザーの電子メール アドレス。                                                             | **はい**  |
| UserObjectId                         | ユーザーのオブジェクト ID Azure AD ます。                                                        | [いいえ]       |
| バージョン                              | 監査バージョンスキーマ ("1.1")。                                                          | [いいえ]       |


### <a name="opting-out-in-c"></a>オプトインC++

テレメトリを [最小のみ] に設定するには、 **mip:: TelemetryConfiguration ()** の共有ポインターを作成し、 **isTelemetryOptedOut**を true に設定します。 構成オブジェクトを**MipContent:: Create ()** に渡します。

```cpp
auto telemetryConfig = std::make_shared<mip::TelemetryConfiguration>();                                     
telemetryConfig->isTelemetryOptedOut = true;
                       
// Create MipContext, passing in mip::TelemetryConfiguration object.
mMipContext = mip::MipContext::Create(
    mAppInfo,
    "mip_data",
    mip::LogLevel::Trace,
    false,
    nullptr /*loggerDelegateOverride*/,
    telemetryConfig /*telemetryOverride*/
);
```

### <a name="opting-out-in-net"></a>.NET でのオプトイン

テレメトリを最小値のみに設定するには、 **TelemetryConfiguration ()** オブジェクトを作成し、 **isTelemetryOptedOut**を true に設定します。 構成オブジェクトを MIP に渡し**ます。CreateMipContext ()** 。

```csharp
TelemetryConfiguration telemetryConfiguration = new TelemetryConfiguration();
telemetryConfiguration.IsTelemetryOptedOut = true;

// Create MipContext, passing in TelemetryConfiguration object.
mipContext = MIP.CreateMipContext(appInfo, 
    "mip_data", 
    LogLevel.Trace, 
    null, 
    telemetryConfiguration);
```

