---
title: class mip::PolicyProfile::Settings
description: Mip::policyprofile クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d3105bd9c13e91108c44e847c3eae74f166c5e04
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173441"
---
# <a name="class-mippolicyprofilesettings"></a>class mip::PolicyProfile::Settings 
作成時および有効期間全体にわたって [PolicyProfile](class_mip_policyprofile.md) に使用される[設定](class_mip_policyprofile_settings.md)。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック設定 (const std::string & パス、bool useinmemorystorage: const std::shared_ptr\<authdelegate:\>& authdelegate:、const std::shared_ptr\<PolicyProfile::Observer\>(& a)observer, const ApplicationInfo & applicationInfo)  |  プロファイルを構成するためのインターフェイス。
public const std::string& GetPath() const  |  保存された状態へのパスを取得します。
public bool GetUseInMemoryStorage() const  |  Use In Memory Storage フラグを取得します。
public const std::shared_ptr\<AuthDelegate\>& GetAuthDelegate() const  |  認証委任を取得します。
public const std::shared_ptr\<PolicyProfile::Observer\>& GetObserver() const  |  イベント オブザーバーを取得します。
public const ApplicationInfo GetApplicationInfo() const  |  アプリケーション情報を取得します。
public std::shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate(const std::shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  既定のロガーをオーバーライドします。
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate (const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public std::shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate() const  |  アプリケーションによって提供される TaskDispatcher デリゲート (指定されている場合) を取得します。
public void SetTaskDispatcherDelegate(const std::shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  クライアントの処理をディスパッチ既定 asynchonous タスクをオーバーライドします。
public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
public bool IsTelemetryOptedOut() const  |  テレメトリの収集を無効にする必要があるかどうかを取得します。
public void SetMinimumLogLevel(LogLevel logLevel)  |  ログ イベントをトリガーする最小のログ レベルを設定します。
public LogLevel GetMinimumLogLevel() const  |  最小のログ レベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>ポリシーの設定
プロファイルを構成するためのインターフェイス。

パラメーター:  
* **パス**:SDK がプロファイル状態を格納するディレクトリへのパス。 


* **useInMemoryStorage**:ディスクではなくメモリにキャッシュされている任意の状態を格納します。 


* **authDelegate**:認証トークンを取得する SDK によって使用される認証デリゲート。 


* **オブザーバー**:実装するクラス、 [PolicyProfile::Observer](class_mip_policyprofile_observer.md)インターフェイス。 nullptr にすることができます。 


* **applicationInfo**:サービスへのアクセスに使用されるアプリケーション識別子。


  
### <a name="getpath-function"></a>GetPath 関数
保存された状態へのパスを取得します。

  
**返します**:保存された状態へのパス。
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage 関数
Use In Memory Storage フラグを取得します。

  
**返します**:メモリでの使用が false それ以外の場合に設定されている場合は true。
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
認証委任を取得します。

  
**返します**:認証委任。
  
### <a name="getobserver-function"></a>GetObserver 関数
イベント オブザーバーを取得します。

  
**返します**:イベント オブザーバー。
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 関数
アプリケーション情報を取得します。

  
**返します**:アプリケーションの情報です。
  
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

  
**返します**:HTTP 操作に使用する http デリゲート
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 関数
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **httpDelegate**:クライアント アプリケーションによって実装される http コールバック インターフェイス


  
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

  
**返します**:テレメトリの収集を無効にする場合は true false のその他。
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 関数
ログ イベントをトリガーする最小のログ レベルを設定します。

パラメーター:  
* **logLevel**: ログ イベントをトリガーする最小のログ レベル。 



  
**返します**:True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 関数
最小のログ レベル オブジェクトを取得します。

  
**返します**:ログ イベントをトリガーするための最小ログ レベル。