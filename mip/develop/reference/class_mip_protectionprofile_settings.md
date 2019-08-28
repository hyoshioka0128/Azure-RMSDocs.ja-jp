---
title: class mip::ProtectionProfile::Settings
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionprofile クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f5c9d9fcd72f65b029c0a1af582b0f0cd498186e
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057483"
---
# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
作成時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: string & path、cachestoragetype cachestoragetype、const std:: shared_ptr\<authdelegate\>& authdelegate、const std:: shared_ptr\<conて delegate\>&conのデリゲート、const std:: shared_ptr\<protectionprofile:: オブザーバー\>& オブザーバー、const applicationinfo & applicationinfo)  |  非同期操作に使用されるオブザーバーを指定する [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
パブリック設定 (const std:: shared_ptr\<MipContext\>& MipContext、cachestoragetype cachestoragetype、const std:: shared_ptr\<authdelegate\>& authdelegate、const std:: shared_ptr\<Con& delegate\>& conのデリゲート、const std:: shared_ptr\<protectionprofile:: observer\>オブザーバー)  |  非同期操作に使用されるオブザーバーを指定する [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
パブリック設定 (const std:: string & path、cachestoragetype cachestoragetype、const std:: shared_ptr\<authdelegate\>& authdelegate、const std:: shared_ptr\<conて delegate\>&Coninsights Delegate、const ApplicationInfo & applicationInfo)  |  同期操作に使用される、[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
パブリック設定 (const std:: shared_ptr\<MipContext\>& MipContext、cachestoragetype cachestoragetype、const std:: shared_ptr\<authdelegate\>& authdelegate、const std:: shared_ptr\<Conのデリゲート\>& conのデリゲート)  |  同期操作に使用される、[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
public const std::string& GetPath() const  |  ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。
パブリック CacheStorageType GetCacheStorageType () const  |  キャッシュをメモリまたはディスクのどちらに格納するかを取得します。
public std:: shared_ptr\<authdelegate\> getauthdelegate () const  |  認証トークンを取得するために使用する認証委任を取得します。
public std:: shared_ptr\<conのデリゲート\> getconの delegate () const  |  サービスに接続するために使用する同意委任を取得します。
public std:: shared_ptr\<protectionprofile:: オブザーバー\> GetObserver () const  |  [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。
public const ApplicationInfo& GetApplicationInfo() const  |  保護 SDK を利用しているアプリケーションに関する情報を取得します。
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。
public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
public bool IsTelemetryOptedOut() const  |  テレメトリの収集を無効にする必要があるかどうかを取得します。
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate () const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate (const std:: shared_ptr\<LoggerDelegate\>& LoggerDelegate)  |  既定のロガーをオーバーライドします。
public std:: shared_ptr\<httpdelegate\> GetHttpDelegate () const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate (const std:: shared_ptr\<httpdelegate\>& httpdelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& TaskDispatcherDelegate)  |  クライアント独自のを使用して、既定の asynchonous タスクのディスパッチ処理をオーバーライドします。
public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
public const std::string& GetSessionId() const  |  セッション ID を取得します。
public void SetMinimumLogLevel(LogLevel logLevel)  |  ログ イベントをトリガーする最小のログ レベルを設定します。
public LogLevel GetMinimumLogLevel() const  |  最小のログ レベル オブジェクトを取得します。
public void SetCanCacheLicenses (bool canCacheLicenses)  |  エンドユーザーライセンス (Eul) がローカルにキャッシュされるかどうかを構成します。
public bool CanCacheLicenses () const  |  エンドユーザーライセンス (Eul) がローカルにキャッシュされているかどうかを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
非同期操作に使用されるオブザーバーを指定する [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **パス**:ログ記録、テレメトリ、その他の保護関連資料が格納されるファイルパス 


* **Cachestoragetype**:キャッシュされた状態をメモリまたはディスクに格納する 


* **Authdelegate**:クライアントアプリケーションによって実装される認証に使用されるコールバックオブジェクト 


* **Conのデリゲート**:外部リソースにアクセスするためのユーザーアクセス許可を取得するために使用されるデリゲート 


* **オブザーバー**:[Protectionprofile](class_mip_protectionprofile.md)に関連するイベントの通知を受信する[オブザーバー](class_mip_protectionprofile_observer.md)インスタンス


* **Applicationinfo**:保護 SDK を使用しているアプリケーションに関する情報


> れこのコンストラクターは、mip:: MipContext パラメーターを必要とするものを優先して、間もなく非推奨となります。
  
### <a name="settings-function"></a>Settings 関数
非同期操作に使用されるオブザーバーを指定する [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **mipContext**:グローバルコンテキスト設定 


* **Cachestoragetype**:キャッシュされた状態をメモリまたはディスクに格納する 


* **Authdelegate**:クライアントアプリケーションによって実装される認証に使用されるコールバックオブジェクト 


* **Conのデリゲート**:外部リソースにアクセスするためのユーザーアクセス許可を取得するために使用されるデリゲート 


* **オブザーバー**:[Protectionprofile](class_mip_protectionprofile.md)に関連するイベントの通知を受信する[オブザーバー](class_mip_protectionprofile_observer.md)インスタンス


* **Applicationinfo**:保護 SDK を使用しているアプリケーションに関する情報


  
### <a name="settings-function"></a>Settings 関数
同期操作に使用される、[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **パス**:ログ記録、テレメトリ、その他の保護関連資料が格納されるファイルパス 


* **Cachestoragetype**:キャッシュされた状態をメモリまたはディスクに格納する 


* **Authdelegate**:クライアントアプリケーションによって実装される認証に使用されるコールバックオブジェクト 


* **Conのデリゲート**:外部リソースにアクセスするためのユーザーアクセス許可を取得するために使用されるデリゲート 


* **Applicationinfo**:保護 SDK を使用しているアプリケーションに関する情報


このコンストラクターは、mip:: MipContext パラメーターを必要とするものを優先して、間もなく非推奨となります。
  
### <a name="settings-function"></a>Settings 関数
同期操作に使用される、[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **mipContext**:グローバルコンテキスト設定 


* **Cachestoragetype**:キャッシュされた状態をメモリまたはディスクに格納する 


* **Authdelegate**:クライアントアプリケーションによって実装される認証に使用されるコールバックオブジェクト 


* **Conのデリゲート**:外部リソースにアクセスするためのユーザーアクセス許可を取得するために使用されるデリゲート 


* **Applicationinfo**:保護 SDK を使用しているアプリケーションに関する情報


  
### <a name="getpath-function"></a>GetPath 関数
ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。

  
次の**値を返し**ます。ログ、テレメトリ、その他の保護関連資料が格納されるパス
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 関数
キャッシュをメモリまたはディスクのどちらに格納するかを取得します。

  
次の**値を返し**ます。使用されたストレージの種類
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
認証トークンを取得するために使用する認証委任を取得します。

  
次の**値を返し**ます。認証トークンを取得するために使用される Auth delegate
  
### <a name="getconsentdelegate-function"></a>Getconのデリゲート関数
サービスに接続するために使用する同意委任を取得します。

  
次の**値を返し**ます。サービスへの接続に使用される同意デリゲート
  
### <a name="getobserver-function"></a>GetObserver 関数
[ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。

  
次の**値を返し**ます。[Protectionprofile](class_mip_protectionprofile.md)に関連するイベントの通知を受信する[オブザーバー](class_mip_protectionprofile_observer.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 関数
保護 SDK を利用しているアプリケーションに関する情報を取得します。

  
次の**値を返し**ます。保護 SDK を使用しているアプリケーションに関する情報
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="getmipcontext-function"></a>GetMipContext 関数
すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。

  
次の**値を返し**ます。Mipmap コンテキスト
  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 関数
テレメトリの収集をすべて無効にします。
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 関数
テレメトリの収集を無効にする必要があるかどうかを取得します。

  
次の**値を返し**ます。テレメトリ収集を無効にする必要がある場合
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 関数
アプリケーションによって提供されるロガー委任を取得します (提供される場合)。

  
次の**値を返し**ます。Lnm
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate 関数
既定のロガーをオーバーライドします。

パラメーター:  
* **loggerDelegate**:クライアントアプリケーションによって実装されるログコールバックインターフェイス


このメソッドは、独自のロガー実装を使用するクライアント アプリケーションによって呼び出される必要があります 
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 関数
アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。

  
次の**値を返し**ます。HTTP 操作に使用する HTTP デリゲート
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 関数
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **Httpdelegate**:クライアントアプリケーションによって実装される HTTP コールバックインターフェイス


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 関数
アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。

  
次の**値を返し**ます。非同期タスクの実行に使用される TaskDispatcher デリゲート
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 関数
クライアント独自のを使用して、既定の asynchonous タスクのディスパッチ処理をオーバーライドします。

パラメーター:  
* **taskDispatcherDelegate**:クライアントアプリケーションによって実装されたタスクのディスパッチコールバックインターフェイス


  
### <a name="setsessionid-function"></a>SetSessionId 関数
セッション ID を設定します。

パラメーター:  
* **sessionId**:ログ/テレメトリを関連付けるために使用されるセッション ID


  
### <a name="getsessionid-function"></a>GetSessionId 関数
セッション ID を取得します。

  
次の**値を返し**ます。ログ/テレメトリを関連付けるために使用されるセッション ID
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 関数
ログ イベントをトリガーする最小のログ レベルを設定します。

パラメーター:  
* **logLevel**: ログ イベントをトリガーする最小のログ レベル。


> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 関数
最小のログ レベル オブジェクトを取得します。

  
次の**値を返し**ます。ログイベントをトリガーする最小ログレベル。
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses 関数
エンドユーザーライセンス (Eul) がローカルにキャッシュされるかどうかを構成します。

パラメーター:  
* **canCacheLicenses**:保護されたコンテンツを開くときにエンジンがライセンスをキャッシュする必要があるかどうか


True の場合、保護されたコンテンツを開くと、関連付けられているライセンスがローカルにキャッシュされます。 False の場合、保護されたコンテンツを開くと、常に RMS サービスからライセンスを取得するための HTTP 操作が実行されます。
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses 関数
エンドユーザーライセンス (Eul) がローカルにキャッシュされているかどうかを取得します。

  
次の**値を返し**ます。ライセンスキャッシュの構成