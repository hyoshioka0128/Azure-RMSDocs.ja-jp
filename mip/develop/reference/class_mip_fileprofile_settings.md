---
title: class mip FileProfile Settings
description: class mip FileProfile Settings のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 4b79d8eb75a54a56f1b3e48645bdd5eec0afaa19
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446381"
---
# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
作成時および有効期間全体にわたって [FileProfile](class_mip_fileprofile.md) に使用される[設定](class_mip_fileprofile_settings.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  [FileProfile::Settings](class_mip_fileprofile_settings.md) コンストラクター。
 public const std::string& GetPath() const  |  ログ、テレメトリ、その他の継続状態が格納されるファイル パスを取得します。
 public bool GetUseInMemoryStorage() const  |  状態がすべて (ディスク上ではなく) メモリに格納されるかどうかを取得します。
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  認証トークンを取得するために使用する認証委任を取得します。
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  サービスに接続しているユーザーの同意を要求するために使用する同意委任を取得します。
public std::shared_ptr<Observer> GetObserver() const  |  [FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。
 public const ApplicationInfo GetApplicationInfo() const  |  SDK を利用しているアプリケーションに関する情報を取得します。
 public bool GetSkipTelemetryInit() const  |  テレメトリ初期化をスキップする必要があるかどうかを取得します。
 public void SetSkipTelemetryInit()  |  テレメトリ初期化を無効にします。
 public void SetNewFeaturesDisabled()  |  新機能を無効にします。
 public bool AreNewFeaturesDisabled() const  |  新機能が無効になっているかどうかを取得します。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  既定のロガーをオーバーライドします。
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
 public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
 public bool IsTelemetryOptedOut() const  |  テレメトリの収集を無効にする必要があるかどうかを取得します。
 public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
 public const std::string& GetSessionId() const  |  セッション ID を取得します。
 public void SetMinimumLogLevel(LogLevel logLevel)  |  ログ イベントをトリガーする最小のログ レベルを設定します。
 public LogLevel GetMinimumLogLevel() const  |  ログ イベントをトリガーする最小のログ レベルを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
[FileProfile::Settings](class_mip_fileprofile_settings.md) コンストラクター。

パラメーター:  
* **path**: ログ、テレメトリ、その他の継続状態が格納されるファイル パス 


* **useInMemoryStorage**: すべての状態がメモリ内に格納される必要がある場合は true、状態をディスクにキャッシュできる場合は false 


* **authDelegate**: 認証トークンを取得するために使用する認証委任 


* **observer**: [FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信する[オブザーバー](class_mip_fileprofile_observer.md) インスタンス


* **applicationInfo**: SDK を利用しているアプリケーションに関する情報


  
### <a name="getpath"></a>GetPath
ログ、テレメトリ、その他の継続状態が格納されるファイル パスを取得します。

  
**戻り値**: ログ、テレメトリ、その他の継続状態が格納されるファイル パス
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
状態がすべて (ディスク上ではなく) メモリに格納されるかどうかを取得します。

  
**戻り値**: 状態がすべて (ディスク上ではなく) メモリに格納されるかどうか
  
### <a name="getauthdelegate"></a>GetAuthDelegate
認証トークンを取得するために使用する認証委任を取得します。

  
**戻り値**: 認証トークンを取得するために使用する認証委任
  
### <a name="consentdelegate"></a>ConsentDelegate
サービスに接続しているユーザーの同意を要求するために使用する同意委任を取得します。

  
**戻り値**: ユーザーの同意を要求するために使用する同意委任
  
### <a name="observer"></a>オブザーバー
[FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。

  
**戻り値**: [FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信する[オブザーバー](class_mip_fileprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
SDK を利用しているアプリケーションに関する情報を取得します。

  
**戻り値**: SDK を利用しているアプリケーションに関する情報
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
テレメトリ初期化をスキップする必要があるかどうかを取得します。

  
**戻り値**: テレメトリ初期化をスキップする必要があるかどうか
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
テレメトリ初期化を無効にします。
このメソッドは、通常、クライアント アプリケーションによっては呼び出されず、初期化の重複を防ぐためにファイル SDK によって使用されます
  
### <a name="setnewfeaturesdisabled"></a>SetNewFeaturesDisabled
新機能を無効にします。
新機能を試さないアプリケーションの場合
  
### <a name="arenewfeaturesdisabled"></a>AreNewFeaturesDisabled
新機能が無効になっているかどうかを取得します。

  
**戻り値**: 新機能が無効になっているかどうか
  
### <a name="loggerdelegate"></a>LoggerDelegate
アプリケーションによって提供されるロガー委任を取得します (提供される場合)。

  
**戻り値**: ロガー
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
既定のロガーをオーバーライドします。

パラメーター:  
* **loggerDelegate**: クライアント アプリケーションによって実装されるログ コールバック インターフェイス


このメソッドは、独自のロガー実装を使用するクライアント アプリケーションによって呼び出される必要があります
  
### <a name="httpdelegate"></a>HttpDelegate
アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。

  
**戻り値**: HTTP 操作に使用される HTTP 委任
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **httpDelegate**: クライアント アプリケーションによって実装される HTTP コールバック インターフェイス


  
### <a name="optouttelemetry"></a>OptOutTelemetry
テレメトリの収集をすべて無効にします。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
テレメトリの収集を無効にする必要があるかどうかを取得します。

  
**戻り値**: テレメトリの収集を無効にする必要があるかどうか
  
### <a name="setsessionid"></a>SetSessionId
セッション ID を設定します。

パラメーター:  
* **sessionId**: ログ/テレメトリを関連付けるために使用されるセッション ID


  
### <a name="getsessionid"></a>GetSessionId
セッション ID を取得します。

  
**戻り値**: ログ/テレメトリを関連付けるために使用されるセッション ID
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
ログ イベントをトリガーする最小のログ レベルを設定します。

パラメーター:  
* **logLevel**: ログ イベントをトリガーする最小のログ レベル。 



  
**戻り値**: True
  
### <a name="loglevel"></a>ログ レベル
ログ イベントをトリガーする最小のログ レベルを取得します。

  
**戻り値**: ログ イベントをトリガーする最小のログ レベル。