---
title: 'クラス PolicyProfile:: Settings'
description: 'Microsoft Information Protection (MIP) SDK の policyprofile:: settings クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 317a6cfaaac7572ae320860a0d5a11fabce356e9
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760655"
---
# <a name="class-policyprofilesettings"></a>クラス PolicyProfile:: Settings 
作成時および有効期間全体にわたって PolicyProfile に使用される設定。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: shared_ptr\<mipContext\>& MipContext、cachestoragetype cachestoragetype、const std:: shared_ptr\<policyprofile:: observer\>& オブザーバー)  |  プロファイルを構成するためのインターフェイス。
パブリック CacheStorageType GetCacheStorageType () const  |  キャッシュをメモリまたはディスクのどちらに格納するかを取得します。
public const std:: shared_ptr\<policyprofile:: オブザーバー\>& GetObserver () const  |  イベント オブザーバーを取得します。
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。
public std:: shared_ptr\<httpdelegate\> GetHttpDelegate () const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate (const std:: shared_ptr\<httpdelegate\>& httpdelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<taskDispatcherDelegate\>& TaskDispatcherDelegate)  |  クライアント独自のを使用して、既定の非同期タスクのディスパッチ処理をオーバーライドします。
public void SetSessionId(const std::string& sessionId)  | _まだ文書化されていません。_
public const std::string& GetSessionId() const  | _まだ文書化されていません。_
public void setcustomsettings (const std:: vector\<std::p air\<std:: string, std:: string\> \>& customsettings)  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
public const std:: vector\<std::p air\<std:: string、std:: string\> \>& GetCustomSettings () const  |  機能のゲーティングとテストに使用するカスタム設定を取得します。
public ~Settings()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
プロファイルを構成するためのインターフェイス。

パラメーター:  
* **mipContext**: グローバルコンテキスト設定 


* **Cachestoragetype**: キャッシュされた状態をメモリまたはディスクに格納します。 


* **observer**: PolicyProfile::Observer インターフェイスを実装するクラス。 nullptr にすることができます。


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 関数
キャッシュをメモリまたはディスクのどちらに格納するかを取得します。

  
**戻り値**: 使用されているストレージの種類
  
### <a name="getobserver-function"></a>GetObserver 関数
イベント オブザーバーを取得します。

  
**戻り値**: イベント オブザーバー。
  
### <a name="getmipcontext-function"></a>GetMipContext 関数
すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。

  
**戻り値**: mipmap コンテキスト
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 関数
アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。

  
は、HTTP 操作に使用される http デリゲートを**返し**ます。
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 関数
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **httpDelegate**: クライアント アプリケーションによって実装される HTTP コールバック インターフェイス


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 関数
アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。

  
は、非同期タスクの実行に使用される taskdispatcher デリゲートを**返し**ます。
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 関数
クライアント独自のを使用して、既定の非同期タスクのディスパッチ処理をオーバーライドします。

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
* **Customsettings**: 名前と値のペアの一覧。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を取得します。

  
**戻り値**: 名前と値のペアのリスト。
  
### <a name="settings-function"></a>~ Settings 関数
_まだ文書化されていません。_
