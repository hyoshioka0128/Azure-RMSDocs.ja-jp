---
title: 構造体 TelemetryConfiguration
description: Microsoft Information Protection (MIP) SDK に関連付けられているドキュメント構造。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 0599dfb9fdc5d37849c19c9284b2d6fd27cec606
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566746"
---
# <a name="struct-telemetryconfiguration"></a>構造体 TelemetryConfiguration 
カスタムテレメトリ設定 (一般的には使用されません)
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: string hostNameOverride  |  ホストテレメトリのインスタンス名。 設定されていない場合、MIP は独自のホストとして機能します。
public std:: string libraryNameOverride  |  代替テレメトリライブラリ (DLL) ファイル名。
public std:: shared_ptr \<HttpDelegate\> httpDelegateOverride  |  設定すると、このインスタンスによって HTTP 処理が管理されます
public std:: shared_ptr \<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  設定した場合、非同期タスクの処理はこのインスタンスによって管理されます。テレメトリオブジェクトを保持できるため、taskDispatcherDelegateOverides を共有することはできません。また、taskDispatcher が解放されるまで、リリースを防ぐ必要があります。
public bool isNetworkDetectionEnabled  |  設定すると、テレメトリコンポーネントによってバックグラウンドスレッドでネットワークの状態が ping されます。
public bool isLocalCachingEnabled  |  設定すると、テレメトリコンポーネントはディスク上のキャッシュを使用します。
public bool isTraceLoggingEnabled  |  設定すると、テレメトリコンポーネントによって警告/エラーログがディスクに書き込まれます
public bool isTelemetryOptedOut  |  設定すると、必要なサービスデータテレメトリのみが送信されます
public bool isFastShutdownEnabled  |  設定した場合、シャットダウン時にイベントはアップロードされません。監査イベントはログ記録時に直ちにアップロードされます
public std:: map \<std::string, std::string\> customsettings  |  カスタムテレメトリ設定 >
public std:: map \<std::string, std::vector\<std::string\> \> maskedProperties  |  マスクする必要があるテレメトリイベント/プロパティ
  
## <a name="members"></a>メンバー
  
### <a name="hostnameoverride-struct-member"></a>hostNameOverride struct メンバー
ホストテレメトリのインスタンス名。 設定されていない場合、MIP は独自のホストとして機能します。
  
### <a name="librarynameoverride-struct-member"></a>libraryNameOverride 構造体メンバー
代替テレメトリライブラリ (DLL) ファイル名。
  
### <a name="httpdelegate"></a>HttpDelegate
設定すると、このインスタンスによって HTTP 処理が管理されます
  
### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
設定した場合、非同期タスクの処理はこのインスタンスによって管理されます。テレメトリオブジェクトを保持できるため、taskDispatcherDelegateOverides を共有することはできません。また、taskDispatcher が解放されるまで、リリースを防ぐ必要があります。
  
### <a name="isnetworkdetectionenabled-struct-member"></a>isNetworkDetectionEnabled struct メンバー
設定すると、テレメトリコンポーネントによってバックグラウンドスレッドでネットワークの状態が ping されます。
  
### <a name="islocalcachingenabled-struct-member"></a>isLocalCachingEnabled 構造体メンバー
設定すると、テレメトリコンポーネントはディスク上のキャッシュを使用します。
  
### <a name="istraceloggingenabled-struct-member"></a>isTraceLoggingEnabled struct メンバー
設定すると、テレメトリコンポーネントによって警告/エラーログがディスクに書き込まれます
  
### <a name="istelemetryoptedout-struct-member"></a>isTelemetryOptedOut struct メンバー
設定すると、必要なサービスデータテレメトリのみが送信されます
  
### <a name="isfastshutdownenabled-struct-member"></a>isFastShutdownEnabled 構造体メンバー
設定した場合、シャットダウン時にイベントはアップロードされません。監査イベントはログ記録時に直ちにアップロードされます
  
### <a name="customsettings-struct-member"></a>customSettings 構造体メンバー
カスタムテレメトリ設定 >
  
### <a name="maskedproperties-struct-member"></a>maskedProperties struct メンバー
マスクする必要があるテレメトリイベント/プロパティ