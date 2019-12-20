---
title: class mip::PolicyProfile::Settings
description: Microsoft Information Protection (MIP) SDK の mip::p olicyprofile クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 324b31a9589cff75a758da2936a3aba242fd63c2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560880"
---
# <a name="class-mippolicyprofilesettings"></a>class mip::PolicyProfile::Settings 
作成時および有効期間全体にわたって PolicyProfile によって使用される設定。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: shared_ptr\<MipContext\>& mipContext、CacheStorageType cacheStorageType、const std:: shared_ptr\<AuthDelegate\>& authDelegate、const std:: shared_ptr\<PolicyProfile:: Observer\>& オブザーバー)  |  プロファイルを構成するためのインターフェイス。
パブリック CacheStorageType GetCacheStorageType () const  |  キャッシュをメモリまたはディスクのどちらに格納するかを取得します。
public const std::shared_ptr\<AuthDelegate\>& GetAuthDelegate() const  |  認証委任を取得します。
public const std:: shared_ptr\<PolicyProfile:: オブザーバー\>& GetObserver () const  |  イベント オブザーバーを取得します。
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  クライアント独自のを使用して、既定の asynchonous タスクのディスパッチ処理をオーバーライドします。
public void SetSessionId(const std::string& sessionId)  | まだ文書化されていません。
public const std::string& GetSessionId() const  | まだ文書化されていません。
public void SetCustomSettings (const std:: vector\<std::p air\<std:: string、std:: string\>\>& customSettings)  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  機能のゲーティングとテストに使用するカスタム設定を取得します。
public ~Settings()  | まだ文書化されていません。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
プロファイルを構成するためのインターフェイス。

パラメーター:  
* **mipContext**: グローバルコンテキスト設定 


* **Cachestoragetype**: キャッシュされた状態をメモリまたはディスクに格納します。 


* **authDelegate**: 認証トークンを取得するために SDK によって使用される認証委任。 


* **オブザーバー**: policyprofile:: observer インターフェイスを実装するクラス。 nullptr にすることができます。


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 関数
キャッシュをメモリまたはディスクのどちらに格納するかを取得します。

  
**戻り値**: 使用されているストレージの種類
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
認証委任を取得します。

  
**戻り値**: 認証委任。
  
### <a name="getobserver-function"></a>GetObserver 関数
イベント オブザーバーを取得します。

  
**戻り値**: イベント オブザーバー。
  
### <a name="getmipcontext-function"></a>GetMipContext 関数
すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。

  
**戻り値**: mipmap コンテキスト
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 関数
アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。

  
**戻り値**: HTTP 操作に使用される HTTP 委任
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 関数
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **httpDelegate**: クライアント アプリケーションによって実装される HTTP コールバック インターフェイス


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 関数
アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。

  
は、非同期タスクの実行に使用される taskdispatcher デリゲートを**返し**ます。
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 関数
クライアント独自のを使用して、既定の asynchonous タスクのディスパッチ処理をオーバーライドします。

パラメーター:  
* **taskDispatcherDelegate**: クライアントアプリケーションによって実装されたタスクのディスパッチコールバックインターフェイス


タスクはプロファイルオブジェクトを参照することができるため、結果としてその破棄が妨げられます。 taskdispatcher キューは共有しないでください。
  
### <a name="setsessionid-function"></a>SetSessionId 関数
_まだ文書化されていません。_

  
### <a name="getsessionid-function"></a>GetSessionId 関数
_まだ文書化されていません。_

  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を設定します。

パラメーター:  
* **customSettings**: 名前と値のペアの一覧。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を取得します。

  
**戻り値**: 名前と値のペアのリスト。
  
### <a name="settings-function"></a>~ Settings 関数
_まだ文書化されていません。_
