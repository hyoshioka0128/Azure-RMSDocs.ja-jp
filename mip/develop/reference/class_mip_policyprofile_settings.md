---
title: 'クラス PolicyProfile:: Settings'
description: 'Microsoft Information Protection (MIP) SDK の policyprofile:: settings クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2ec38a34f2522448704f1be91d03c62761cafdf6
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566661"
---
# <a name="class-policyprofilesettings"></a>クラス PolicyProfile:: Settings 
作成時および有効期間全体にわたって PolicyProfile に使用される設定。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: shared_ptr \<MipContext\>& mipContext、cacheStorageType cachestoragetype、const std:: shared_ptr \<PolicyProfile::Observer\>& オブザーバー)  |  プロファイルを構成するためのインターフェイス。
パブリック CacheStorageType GetCacheStorageType () const  |  キャッシュをメモリまたはディスクのどちらに格納するかを取得します。
public const std:: shared_ptr \<PolicyProfile::Observer\>& GetObserver () const  |  イベント オブザーバーを取得します。
public std:: shared_ptr \<MipContext\> GetMipContext () const  |  すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public std:: shared_ptr \<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。
public void SetTaskDispatcherDelegate (const std:: shared_ptr \<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  クライアント独自のを使用して、既定の非同期タスクのディスパッチ処理をオーバーライドします。
public void SetSessionId(const std::string& sessionId)  | _まだ文書化されていません。_
public const std::string& GetSessionId() const  | _まだ文書化されていません。_
public void SetCustomSettings (const std:: vector \<std::pair\<std::string, std::string\> \>& customsettings)  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
public const std:: vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  機能のゲーティングとテストに使用するカスタム設定を取得します。
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

  
は、HTTP 操作に使用される http デリゲートを **返し** ます。
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 関数
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **httpDelegate**: クライアント アプリケーションによって実装される HTTP コールバック インターフェイス


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 関数
アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。

  
は、非同期タスクの実行に使用される taskdispatcher デリゲートを **返し** ます。
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 関数
クライアント独自のを使用して、既定の非同期タスクのディスパッチ処理をオーバーライドします。

パラメーター:  
* **taskDispatcherDelegate**: クライアントアプリケーションによって実装されたタスクのディスパッチコールバックインターフェイス


タスクはプロファイルオブジェクトを参照することができるため、結果としてその破棄が妨げられます。 taskdispatcher キューは共有しないでください。
  
### <a name="setsessionid-function"></a>SetSessionId 関数
まだ文書化されていません。

  
### <a name="getsessionid-function"></a>GetSessionId 関数
まだ文書化されていません。

  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を設定します。

パラメーター:  
* **Customsettings**: 名前と値のペアの一覧。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を取得します。

  
**戻り値**: 名前と値のペアのリスト。
  
### <a name="settings-function"></a>~ Settings 関数
まだ文書化されていません。
