---
title: Concepts - The core concepts in the MIP SDK - Telemetry Control
description: This article will help you understand how to opt out of telemetry and which events are still sent when opted out.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 10/01/2019
ms.author: tommos
ms.openlocfilehash: 3d97bdbf5307d7f0faefe6b6434b1df1ebc67798
ms.sourcegitcommit: 487e681c9683b8adb7ae6fcfb374830bf0e5ad72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2019
ms.locfileid: "74484855"
---
# <a name="microsoft-information-protection-sdk---telemetry-configuration"></a>Microsoft Information Protection SDK - Telemetry Configuration

## <a name="telemetry"></a>製品利用統計情報

By default, the Microsoft Information Protection SDK sends telemetry data to Microsoft. This telemetry data is useful for troubleshooting bugs, quality, and performance issues across the SDK install base that we may not capture in our internal testing. When implementing your application with the SDK, it's important to give users and admins the ability to opt out of telemetry if required.

## <a name="telemetry-configuration"></a>Telemetry Configuration

Telemetry options in the MIP SDK can be controlled via [TelemetryConfiguration](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.telemetryconfiguration?view=mipsdk-dotnet). Create an instance of this class, then set **IsTelemetryOptedOut** to true. Provide the object of class **TelemetryConfiguration** to the function used to create **MipContext**. This doesn't completely eliminate telemetry data, but reduces to a minimum set with all end-user identifiable information scrubbed.

### <a name="minimum-telemetry-events"></a>Minimum Telemetry Events

When telemetry is set to *opted out*, a minimum set of data is sent to Microsoft. All personally identifiable information is scrubbed from this information. This data includes heartbeat information to understand that the SDK is being used, and system metadata. **No user content or end user identifiable information is set to the service.**

Review the tables below to see exactly what events and data are sent with minimum telemetry set.

#### <a name="event-heartbeat"></a>Event: Heartbeat

| 名前                                 | [説明]                                                                            | Scrubbed |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| App.ApplicationId                    | The application identifier provided via mip::ApplicationInfo.                          | [いいえ]       |
| App.ApplicationName                  | The application name provided via mip::ApplicationInfo.                                | [いいえ]       |
| App.ApplicationVersion               | The application version profided via mip::ApplicationInfo.                             | [いいえ]       |
| ApplicationId                        | The application version profided via mip::ApplicationInfo.                             | [いいえ]       |
| ApplicationName                      | The application name provided via mip::ApplicationInfo.                                | [いいえ]       |
| CreationTime                         | Time event was generated.                                                              | [いいえ]       |
| DefaultLabel.Id                      | Tenant default label ID.                                                               | [いいえ]       |
| Engine.TenantId                      | Home tenant GUID of the authenticated user.                                            | [いいえ]       |
| Engine.UserObjectId                  | User object ID in Azure Active Directory.                                              | [いいえ]       |
| Event.CorrelationId                  | Generated unique ID associated with object that triggered the event.                   | [いいえ]       |
| Event.CorrelationIdDescription       | C++ class name of object that triggered the event.                                     | [いいえ]       |
| Event.ParentCorrelationId            | Parent event correlation ID.                                                           | [いいえ]       |
| Event.ParentCorrelationIdDescription | Generated Unique ID associated with the parent of the object that triggered the event. | [いいえ]       |
| Event.UniqueId                       | Generated unique ID assigned to the event.                                             | [いいえ]       |
| MachineName                          | Name of the system that generated the event.                                           | **はい**  |
| MIP.Version                          | Version of the MIP SDK.                                                                | [いいえ]       |
| 操作                            | ハートビート                                                                              | [いいえ]       |
| OrganizationId                       | Home tenant GUID of the authenticated user.                                            | [いいえ]       |
| プラットフォーム                             | Operating system version.                                                              | [いいえ]       |
| ProcessName                          | Name of the process using the SDK.                                                     | [いいえ]       |
| ProductVersion                       | Same as “App.ApplicationVersion”.                                                      | [いいえ]       |
| SDKVersion                           | Same as MIP.Version.                                                                   | [いいえ]       |
| UserId                               | ユーザーの電子メール アドレス。                                                             | **はい**  |
| UserObjectId                         | Azure AD object ID of the user.                                                        | [いいえ]       |
| バージョン                              | Audit version schema (“1.1”).                                                          | [いいえ]       |

#### <a name="event-discovery"></a>Event: Discovery

| 名前                                 | [説明]                                                                            | Scrubbed |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | Unique action ID for this event, used for event correlation.                           | [いいえ]       |
| App.ApplicationId                    | The application identifier provided via mip::ApplicationInfo.                          | [いいえ]       |
| App.ApplicationName                  | The application name provided via mip::ApplicationInfo.                                | [いいえ]       |
| App.ApplicationVersion               | The application version profided via mip::ApplicationInfo.                             | [いいえ]       |
| ApplicationId                        | The application version profided via mip::ApplicationInfo.                             | [いいえ]       |
| ApplicationName                      | The application name provided via mip::ApplicationInfo.                                | [いいえ]       |
| CreationTime                         | Time event was generated.                                                              | [いいえ]       |
| DataState                            | The state of the data as the application acts on it “REST”, “MOTION”, “USE”.           | [いいえ]       |
| DefaultLabel.Id                      | Tenant default label identifier.                                                       | [いいえ]       |
| Engine.TenantId                      | Home tenant GUID of the authenticated user.                                            | [いいえ]       |
| Engine.UserObjectId                  | User object identifier in Azure Active Directory.                                      | [いいえ]       |
| Event.CorrelationId                  | Generated unique ID associated with object that triggered the event.                   | [いいえ]       |
| Event.CorrelationIdDescription       | C++ class name of object that triggered the event.                                     | [いいえ]       |
| Event.ParentCorrelationId            | Parent event correlation ID.                                                           | [いいえ]       |
| Event.ParentCorrelationIdDescription | Generated Unique ID associated with the parent of the object that triggered the event. | [いいえ]       |
| Event.UniqueId                       | Generated unique ID assigned to the event.                                             | [いいえ]       |
| LabelId                              | Content label identifier on the opened file or data.                                   | [いいえ]       |
| MachineName                          | Name of the system that generated the event.                                           | **はい**  |
| MIP.Version                          | Version of the MIP SDK.                                                                | [いいえ]       |
| ObjectId                             | File path/description of the file or data.                                             | **はい**  |
| 操作                            | "Discovery".                                                                           | [いいえ]       |
| OrganizationId                       | Home tenant GUID of the authenticated user.                                            | [いいえ]       |
| プラットフォーム                             | Operating system version.                                                              | [いいえ]       |
| ProcessName                          | Name of the process using the SDK.                                                     | [いいえ]       |
| 保護                            | Bool indicating if the file is protected or not.                                       | [いいえ]       |
| Protection                           | The protection template identifier.                                                    | **はい**  |
| ProtectionOwner                      | Email address of the protection owner.                                                 | **はい**  |
| SDKVersion                           | Same as MIP.Version.                                                                   | [いいえ]       |
| UserId                               | ユーザーの電子メール アドレス。                                                             | **はい**  |
| UserObjectId                         | Azure AD object ID of the user.                                                        | [いいえ]       |
| バージョン                              | Audit version schema (“1.1”).                                                          | [いいえ]       |

#### <a name="event-label-change"></a>Event: Label Change

| 名前                                 | [説明]                                                                            | Scrubbed |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | Unique action ID for this event, used for event correlation.                           | [いいえ]       |
| ActionIdBefore                       | Previous action ID. Used to chain to new action ID.                                    | [いいえ]       |
| ActionSource                         | Value of MIP::ActionSource.                                                            | [いいえ]       |
| App.ApplicationId                    | The application ID provided via mip::ApplicationInfo.                                  | [いいえ]       |
| App.ApplicationName                  | The application name provided via mip::ApplicationInfo.                                | [いいえ]       |
| App.ApplicationVersion               | The application version profided via mip::ApplicationInfo.                             | [いいえ]       |
| ApplicationId                        | The application ID provided via mip::ApplicationInfo.                                  | [いいえ]       |
| ApplicationName                      | The application name provided via mip::ApplicationInfo.                                | [いいえ]       |
| CreationTime                         | Time the event was generated.                                                          | [いいえ]       |
| DataState                            | The state of the data as the application acts on it “REST”, “MOTION”, “USE”.           | [いいえ]       |
| DefaultLabel.Id                      | Tenant default label identifier.                                                       | [いいえ]       |
| Engine.TenantId                      | Home tenant GUID of the authenticated user.                                            | [いいえ]       |
| Engine.UserObjectId                  | User object identifier in Azure Active Directory.                                      | [いいえ]       |
| Event.CorrelationId                  | Generated unique ID associated with object that triggered the event.                   | [いいえ]       |
| Event.CorrelationIdDescription       | C++ class name of object that triggered the event.                                     | [いいえ]       |
| Event.ParentCorrelationId            | Parent event correlation ID.                                                           | [いいえ]       |
| Event.ParentCorrelationIdDescription | Generated Unique ID associated with the parent of the object that triggered the event. | [いいえ]       |
| Event.UniqueId                       | Generated unique ID assigned to the event.                                             | [いいえ]       |
| IsLabelChanged                       | Bool indicating if the label changed.                                                  | [いいえ]       |
| IsProtectionChanged                  | Bool indicating if protection changed.                                                 | [いいえ]       |
| LabelId                              | Label ID that is to be applied to the file or data.                                    | [いいえ]       |
| LabelIdBefore                        | Previous label ID that was on the file or data.                                        | [いいえ]       |
| MachineName                          | Name of the system that generated the event.                                           | **はい**  |
| MIP.Version                          | Version of the MIP SDK.                                                                | [いいえ]       |
| ObjectId                             | File path/description of the file or data.                                             | **はい**  |
| 操作                            | "Change".                                                                              | [いいえ]       |
| OrganizationId                       | Home tenant GUID of the authenticated user.                                            | [いいえ]       |
| プラットフォーム                             | Operating system version.                                                              | [いいえ]       |
| ProcessName                          | Name of the process using the SDK.                                                     | [いいえ]       |
| 製品バージョン                      |                                                                                        | [いいえ]       |
| 保護                            | Bool indicating if the file is protected or not.                                       | [いいえ]       |
| Protected Before                     | Bool indicating if the file was previously protected or not.                           | [いいえ]       |
| Protection                           | The protection template identifier.                                                    | [いいえ]       |
| Protection Before                    | The previous protection template identifier.                                           | [いいえ]       |
| ProtectionContentId                  | The new content identifier (GUID).                                                     | [いいえ]       |
| ProtectionContentIdBefore            | The previous content identifier (GUID).                                                | [いいえ]       |
| ProtectionOwner                      | Email address of the protection owner.                                                 | **はい**  |
| ProtectionOwnerBefore                | Previous email address of the protection owner.                                        | **はい**  |
| SDKVersion                           | Same as MIP.Version.                                                                   | [いいえ]       |
| UserId                               | ユーザーの電子メール アドレス。                                                             | **はい**  |
| UserObjectId                         | Azure AD object ID of the user.                                                        | [いいえ]       |
| バージョン                              | Audit version schema (“1.1”).                                                          | [いいえ]       |


### <a name="opting-out-in-c"></a>Opting out in C++

To set telemetry to minimum only, create a shared pointer of **mip::TelemetryConfiguration()** and set **isTelemetryOptedOut** to true. Pass the configuration object in to **MipContent::Create()** .

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

### <a name="opting-out-in-net"></a>Opting out in .NET

To set telemetry to minimum only, create a **TelemetryConfiguration()** object and set **isTelemetryOptedOut** to true. Pass the configuration object in to **MIP.CreateMipContext()** .

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

