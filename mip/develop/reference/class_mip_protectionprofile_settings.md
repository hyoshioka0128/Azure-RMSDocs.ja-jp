---
title: class mip ProtectionProfile Settings
description: class mip ProtectionProfile Settings のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: fe2413b2265cf4994dce0e57a7c472d59336902a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446670"
---
# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
作成時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  非同期操作に使用されるオブザーバーを指定する [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const ApplicationInfo& applicationInfo)  |  同期操作に使用される、[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
 public const std::string& GetPath() const  |  ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。
 public bool GetUseInMemoryStorage() const  |  キャッシュが (ディスク上ではなく) メモリにのみ格納されているかどうかを取得します
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  認証トークンを取得するために使用する認証委任を取得します。
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  サービスに接続するために使用する同意委任を取得します。
public std::shared_ptr<ProtectionProfile::Observer> GetObserver() const  |  [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。
 public const ApplicationInfo& GetApplicationInfo() const  |  保護 SDK を利用しているアプリケーションに関する情報を取得します。
 public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
 public bool IsTelemetryOptedOut() const  |  テレメトリの収集を無効にする必要があるかどうかを取得します。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  既定のロガーをオーバーライドします。
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
 public bool GetSkipTelemetryInit() const  |  テレメトリ初期化をスキップする必要があるかどうかを取得します。
 public void SetSkipTelemetryInit()  |  テレメトリ初期化を無効にします。
 public void SetNewFeaturesDisabled()  |  新機能を無効にします。
 public bool AreNewFeaturesDisabled() const  |  新機能が無効になっているかどうかを取得します。
 public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
 public const std::string& GetSessionId() const  |  セッション ID を取得します。
 public void SetMinimumLogLevel(LogLevel logLevel)  |  ログ イベントをトリガーする最小のログ レベルを設定します。
 public LogLevel GetMinimumLogLevel() const  |  最小のログ レベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
非同期操作に使用されるオブザーバーを指定する [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **path**: ログ、テレメトリ、その他の保護関連資料が格納されるファイル パス 


* **useInMemoryStorage**: 状態のキャッシュをディスクではなくメモリに格納します 


* **authDelegate**: 認証に使用される callback オブジェクト (クライアント アプリケーションで実装されます) 


* **observer**: [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信する [Observer](class_mip_protectionprofile_observer.md) インスタンス


* **applicationInfo**: 保護 SDK を利用しているアプリケーションに関する情報


  
### <a name="settings"></a>Settings
同期操作に使用される、[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **path**: ログ、テレメトリ、その他の保護関連資料が格納されるファイル パス 


* **useInMemoryStorage**: 状態のキャッシュをディスクではなくメモリに格納します 


* **authDelegate**: 認証に使用される callback オブジェクト (クライアント アプリケーションで実装されます) 


* **applicationInfo**: 保護 SDK を利用しているアプリケーションに関する情報


  
### <a name="getpath"></a>GetPath
ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。

  
**戻り値**: ログ、テレメトリ、その他の保護関連資料が格納されるパス
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
キャッシュが (ディスク上ではなく) メモリにのみ格納されているかどうかを取得します

  
**戻り値**: キャッシュがメモリにのみ格納される場合は true
  
### <a name="getauthdelegate"></a>GetAuthDelegate
認証トークンを取得するために使用する認証委任を取得します。

  
**戻り値**: 認証トークンを取得するために使用する認証委任
  
### <a name="consentdelegate"></a>ConsentDelegate
サービスに接続するために使用する同意委任を取得します。

  
**戻り値**: サービスに接続するために使用する同意委任
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
[ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。

  
**戻り値**: [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信する[オブザーバー](class_mip_protectionprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
保護 SDK を利用しているアプリケーションに関する情報を取得します。

  
**戻り値**: 保護 SDK を利用しているアプリケーションに関する情報
  
### <a name="optouttelemetry"></a>OptOutTelemetry
テレメトリの収集をすべて無効にします。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
テレメトリの収集を無効にする必要があるかどうかを取得します。

  
**戻り値**: テレメトリの収集を無効にする必要があるかどうか
  
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
最小のログ レベル オブジェクトを取得します。

  
**戻り値**: ログ イベントをトリガーする最小のログ レベル。