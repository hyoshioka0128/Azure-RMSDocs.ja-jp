---
title: class mip::PolicyProfile::Settings
description: Microsoft Information Protection (MIP) SDK の mip::p olicyprofile クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: b4992f5af27cb6e3a2ca1b906e7983ec037ab186
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883705"
---
# <a name="class-mippolicyprofilesettings"></a>class mip::PolicyProfile::Settings 
作成時および有効期間全体にわたって [PolicyProfile](class_mip_policyprofile.md) に使用される[設定](class_mip_policyprofile_settings.md)。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: string & path、cachestoragetype cachestoragetype、const std:: shared_ptr\<authdelegate\>& authdelegate、const std:: shared_ptr\<policyprofile:: オブザーバー\>& オブザーバー、const ApplicationInfo & applicationInfo)  |  プロファイルを構成するためのインターフェイス。
パブリック設定 (const std:: shared_ptr\<MipContext\>& MipContext、cachestoragetype cachestoragetype、const std:: shared_ptr\<authdelegate\>& authdelegate、const std:: shared_ptr\<Policyprofile:: オブザーバー\>& オブザーバー)  |  プロファイルを構成するためのインターフェイス。
public const std::string& GetPath() const  |  保存された状態へのパスを取得します。
パブリック CacheStorageType GetCacheStorageType () const  |  キャッシュをメモリまたはディスクのどちらに格納するかを取得します。
public const std::shared_ptr\<AuthDelegate\>& GetAuthDelegate() const  |  認証委任を取得します。
public const std:: shared_ptr\<policyprofile:: オブザーバー\>& GetObserver () const  |  イベント オブザーバーを取得します。
public const ApplicationInfo& GetApplicationInfo() const  |  アプリケーション情報を取得します。
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate () const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate (const std:: shared_ptr\<LoggerDelegate\>& LoggerDelegate)  |  既定のロガーをオーバーライドします。
public std:: shared_ptr\<httpdelegate\> GetHttpDelegate () const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate (const std:: shared_ptr\<httpdelegate\>& httpdelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& TaskDispatcherDelegate)  |  クライアント独自のを使用して、既定の asynchonous タスクのディスパッチ処理をオーバーライドします。
public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
public bool IsTelemetryOptedOut() const  |  テレメトリの収集を無効にする必要があるかどうかを取得します。
public void SetMinimumLogLevel(LogLevel logLevel)  |  ログ イベントをトリガーする最小のログ レベルを設定します。
public LogLevel GetMinimumLogLevel() const  |  最小のログ レベル オブジェクトを取得します。
public void SetSessionId(const std::string& sessionId)  | _まだ文書化されていません。_
public const std::string& GetSessionId() const  | _まだ文書化されていません。_
public ~Settings()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
プロファイルを構成するためのインターフェイス。

パラメーター:  
* **パス**:SDK がプロファイルの状態を格納するディレクトリへのパス。 


* **Cachestoragetype**:キャッシュされた状態をメモリまたはディスクに格納する 


* **Authdelegate**:認証トークンを取得するために SDK によって使用される認証デリゲート。 


* **オブザーバー**:[Policyprofile:: Observer](class_mip_policyprofile_observer.md)インターフェイスを実装するクラス。 nullptr にすることができます。 


* **Applicationinfo**:サービスアクセスに使用されるアプリケーション識別子。


> れこのコンストラクターは、mip:: MipContext パラメーターを必要とするものを優先して、間もなく非推奨となります。
  
### <a name="settings-function"></a>Settings 関数
プロファイルを構成するためのインターフェイス。

パラメーター:  
* **mipContext**:グローバルコンテキスト設定 


* **Cachestoragetype**:キャッシュされた状態をメモリまたはディスクに格納する 


* **Authdelegate**:認証トークンを取得するために SDK によって使用される認証デリゲート。 


* **オブザーバー**:[Policyprofile:: Observer](class_mip_policyprofile_observer.md)インターフェイスを実装するクラス。 nullptr にすることができます。


  
### <a name="getpath-function"></a>GetPath 関数
保存された状態へのパスを取得します。

  
次の**値を返し**ます。保存された状態へのパス。
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 関数
キャッシュをメモリまたはディスクのどちらに格納するかを取得します。

  
次の**値を返し**ます。使用されたストレージの種類
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
認証委任を取得します。

  
次の**値を返し**ます。認証デリゲート。
  
### <a name="getobserver-function"></a>GetObserver 関数
イベント オブザーバーを取得します。

  
次の**値を返し**ます。イベントオブザーバー。
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 関数
アプリケーション情報を取得します。

  
次の**値を返し**ます。アプリケーション情報。
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="getmipcontext-function"></a>GetMipContext 関数
すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。

  
次の**値を返し**ます。Mipmap コンテキスト
  
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

  
次の**値を返し**ます。HTTP 操作に使用する http デリゲート
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 関数
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **Httpdelegate**:クライアントアプリケーションによって実装される Http コールバックインターフェイス


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 関数
アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。

  
次の**値を返し**ます。非同期タスクの実行に使用される TaskDispatcher デリゲート
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 関数
クライアント独自のを使用して、既定の asynchonous タスクのディスパッチ処理をオーバーライドします。

パラメーター:  
* **taskDispatcherDelegate**:クライアントアプリケーションによって実装されたタスクのディスパッチコールバックインターフェイス


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 関数
テレメトリの収集をすべて無効にします。
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 関数
テレメトリの収集を無効にする必要があるかどうかを取得します。

  
次の**値を返し**ます。テレメトリ収集を無効にする必要がある場合は True、それ以外の場合は false
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 関数
ログ イベントをトリガーする最小のログ レベルを設定します。

パラメーター:  
* **logLevel**: ログ イベントをトリガーする最小のログ レベル。


> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 関数
最小のログ レベル オブジェクトを取得します。

  
次の**値を返し**ます。ログイベントをトリガーする最小ログレベル。
> れこのメソッドは、mip:: MipContext を使用して共通コンテキストデータを取得/設定することを優先して、間もなく非推奨となります。
  
### <a name="setsessionid-function"></a>SetSessionId 関数
_まだ文書化されていません。_

  
### <a name="getsessionid-function"></a>GetSessionId 関数
_まだ文書化されていません。_

  
### <a name="settings-function"></a>~ Settings 関数
_まだ文書化されていません。_
