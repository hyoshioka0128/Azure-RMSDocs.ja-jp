---
title: class mip::FileProfile::Settings
description: Mip::fileprofile クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d85fe9f4b3de485ab966a38b2c41358a6ba091e0
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173295"
---
# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
作成時および有効期間全体にわたって [FileProfile](class_mip_fileprofile.md) に使用される[設定](class_mip_fileprofile_settings.md)。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック設定 (const std::string & パス、bool useinmemorystorage: std::shared_ptr\<authdelegate:\> authdelegate:、std::shared_ptr\<ConsentDelegate\> consentDelegate、std::shared_ptr\<オブザーバー\> observer, const ApplicationInfo & applicationInfo)  |  [FileProfile::Settings](class_mip_fileprofile_settings.md) コンストラクター。
public const std::string& GetPath() const  |  ログ、テレメトリ、その他の継続状態が格納されるファイル パスを取得します。
public bool GetUseInMemoryStorage() const  |  状態がすべて (ディスク上ではなく) メモリに格納されるかどうかを取得します。
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  認証トークンを取得するために使用する認証委任を取得します。
public std::shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  サービスに接続しているユーザーの同意を要求するために使用する同意委任を取得します。
public std::shared_ptr\<Observer\> GetObserver() const  |  [FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。
public const ApplicationInfo GetApplicationInfo() const  |  SDK を利用しているアプリケーションに関する情報を取得します。
public void SetNewFeaturesDisabled()  |  新機能を無効にします。
public bool AreNewFeaturesDisabled() const  |  新機能が無効になっているかどうかを取得します。
public std::shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate(const std::shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  既定のロガーをオーバーライドします。
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate (const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public std::shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate() const  |  アプリケーションによって提供される TaskDispatcher デリゲート (指定されている場合) を取得します。
public void SetTaskDispatcherDelegate(const std::shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  クライアントの処理をディスパッチ既定 asynchonous タスクをオーバーライドします。
public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
public bool IsTelemetryOptedOut() const  |  テレメトリの収集を無効にする必要があるかどうかを取得します。
public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
public const std::string& GetSessionId() const  |  セッション ID を取得します。
public void SetMinimumLogLevel(LogLevel logLevel)  |  ログ イベントをトリガーする最小のログ レベルを設定します。
public LogLevel GetMinimumLogLevel() const  |  ログ イベントをトリガーする最小のログ レベルを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>ポリシーの設定
[FileProfile::Settings](class_mip_fileprofile_settings.md) コンストラクター。

パラメーター:  
* **パス**:ログ、テレメトリ、およびその他のファイル パスは、永続的な状態の格納 


* **useInMemoryStorage**: すべての状態がメモリ内に格納される必要がある場合は true、状態をディスクにキャッシュできる場合は false 


* **authDelegate**:認証トークンを取得するために使用される認証委任 


* **オブザーバー**:[オブザーバー](class_mip_fileprofile_observer.md)イベントの通知を受信するインスタンスに関連する[FileProfile](class_mip_fileprofile.md)


* **applicationInfo**:SDK を利用するアプリケーションに関する情報


  
### <a name="getpath-function"></a>GetPath 関数
ログ、テレメトリ、その他の継続状態が格納されるファイル パスを取得します。

  
**返します**:ログ、テレメトリ、およびその他のパスは、永続的な状態の格納
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage 関数
状態がすべて (ディスク上ではなく) メモリに格納されるかどうかを取得します。

  
**返します**:はなく、ディスク上) に、すべての状態がメモリに格納するかどうか
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
認証トークンを取得するために使用する認証委任を取得します。

  
**返します**:認証トークンを取得するために使用される認証委任
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate 関数
サービスに接続しているユーザーの同意を要求するために使用する同意委任を取得します。

  
**返します**:ユーザーの同意を要求するために使用されるデリゲートを同意します。
  
### <a name="getobserver-function"></a>GetObserver 関数
[FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。

  
**返します**:[オブザーバー](class_mip_fileprofile_observer.md)に関連するイベントの通知を受け取る[FileProfile](class_mip_fileprofile.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 関数
SDK を利用しているアプリケーションに関する情報を取得します。

  
**返します**:SDK を利用するアプリケーションに関する情報
  
### <a name="setnewfeaturesdisabled-function"></a>SetNewFeaturesDisabled 関数
新機能を無効にします。
新機能を試さないアプリケーションの場合
  
### <a name="arenewfeaturesdisabled-function"></a>AreNewFeaturesDisabled 関数
新機能が無効になっているかどうかを取得します。

  
**返します**:かどうかの新機能が無効な場合
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 関数
アプリケーションによって提供されるロガー委任を取得します (提供される場合)。

  
**返します**:ロガー
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate 関数
既定のロガーをオーバーライドします。

パラメーター:  
* **loggerDelegate**:クライアント アプリケーションによって実装されるコールバック インターフェイスをログ記録


このメソッドは、独自のロガー実装を使用するクライアント アプリケーションによって呼び出される必要があります
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 関数
アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。

  
**返します**:HTTP 操作に使用する HTTP デリゲート
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 関数
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **httpDelegate**:クライアント アプリケーションによって実装される HTTP コールバック インターフェイス


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 関数
アプリケーションによって提供される TaskDispatcher デリゲート (指定されている場合) を取得します。

  
**返します**:非同期タスクの実行に使用する TaskDispatcher デリゲート
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 関数
クライアントの処理をディスパッチ既定 asynchonous タスクをオーバーライドします。

パラメーター:  
* **taskDispatcherDelegate**:クライアント アプリケーションによって実装されるコールバック インターフェイスをディスパッチするタスク


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 関数
テレメトリの収集をすべて無効にします。
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 関数
テレメトリの収集を無効にする必要があるかどうかを取得します。

  
**返します**:かどうか、テレメトリの収集を無効にする場合
  
### <a name="setsessionid-function"></a>SetSessionId 関数
セッション ID を設定します。

パラメーター:  
* **sessionId**:ログ/テレメトリを関連付けるために使用されるセッション ID


  
### <a name="getsessionid-function"></a>GetSessionId 関数
セッション ID を取得します。

  
**返します**:ログ/テレメトリを関連付けるために使用されるセッション ID
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 関数
ログ イベントをトリガーする最小のログ レベルを設定します。

パラメーター:  
* **logLevel**: ログ イベントをトリガーする最小のログ レベル。 



  
**返します**:True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 関数
ログ イベントをトリガーする最小のログ レベルを取得します。

  
**返します**:ログ イベントをトリガーする最小のログ レベル。