---
title: class mip::FileProfile::Settings
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileprofile クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 21bbda3424f5c436324ce97137082200ee8d9837
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73561097"
---
# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
作成時および有効期間全体にわたって FileProfile によって使用される設定。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: shared_ptr\<MipContext\>& mipContext、CacheStorageType cacheStorageType、std:: shared_ptr\<AuthDelegate\> authDelegate、std:: shared_ptr\<Con Delegate\> Con Delegate、std:: shared_ptr\<オブザーバー\> オブザーバー)  |  FileProfile:: Settings コンストラクター。
パブリック CacheStorageType GetCacheStorageType () const  |  キャッシュをメモリまたはディスクのどちらに格納するかを取得します。
public std:: shared_ptr\<AuthDelegate\> GetAuthDelegate () const  |  認証トークンを取得するために使用する認証委任を取得します。
public std:: shared_ptr\<Con\> Getconの Delegate () const  |  サービスに接続しているユーザーの同意を要求するために使用する同意委任を取得します。
public std:: shared_ptr\<オブザーバー\> GetObserver () const  |  FileProfile に関連するイベントの通知を受け取るオブザーバーを取得します。
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  すべてのプロファイルで共有状態を表す mipmap コンテキストを取得します。
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  アプリケーションによって提供される TaskDispatcher デリゲート (存在する場合) を取得します。
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  クライアント独自のを使用して、既定の asynchonous タスクのディスパッチ処理をオーバーライドします。
public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
public const std::string& GetSessionId() const  |  セッション ID を取得します。
public void SetCanCacheLicenses (bool canCacheLicenses)  |  エンドユーザーライセンス (Eul) がローカルにキャッシュされるかどうかを構成します。
public bool CanCacheLicenses () const  |  エンドユーザーライセンス (Eul) がローカルにキャッシュされているかどうかを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
FileProfile:: Settings コンストラクター。

パラメーター:  
* **mipContext**: グローバルコンテキスト設定 


* **Cachestoragetype**: キャッシュされた状態をメモリまたはディスクに格納します。 


* **authDelegate**: 認証トークンを取得するために使用する認証委任 


* **Conのデリゲート**: 外部リソースにアクセスするためのユーザーアクセス許可を取得するために使用されるデリゲート 


* **オブザーバー**: fileprofile に関連するイベントの通知を受け取るオブザーバーインスタンス


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 関数
キャッシュをメモリまたはディスクのどちらに格納するかを取得します。

  
**戻り値**: 使用されているストレージの種類
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
認証トークンを取得するために使用する認証委任を取得します。

  
**戻り値**: 認証トークンを取得するために使用する認証委任
  
### <a name="getconsentdelegate-function"></a>Getconのデリゲート関数
サービスに接続しているユーザーの同意を要求するために使用する同意委任を取得します。

  
**戻り値**: ユーザーの同意を要求するために使用する同意委任
  
### <a name="getobserver-function"></a>GetObserver 関数
FileProfile に関連するイベントの通知を受け取るオブザーバーを取得します。

  
**戻り値**: fileprofile に関連するイベントの通知を受け取るオブザーバー
  
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
セッション ID を設定します。

パラメーター:  
* **sessionId**: ログ/テレメトリを関連付けるために使用されるセッション ID


  
### <a name="getsessionid-function"></a>GetSessionId 関数
セッション ID を取得します。

  
**戻り値**: ログ/テレメトリを関連付けるために使用されるセッション ID
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses 関数
エンドユーザーライセンス (Eul) がローカルにキャッシュされるかどうかを構成します。

パラメーター:  
* **canCacheLicenses**: エンジンが保護されたコンテンツを開くときにライセンスをキャッシュする必要があるかどうか


True の場合、保護されたコンテンツを開くと、関連付けられているライセンスがローカルにキャッシュされます。 False の場合、保護されたコンテンツを開くと、常に RMS サービスからライセンスを取得するための HTTP 操作が実行されます。
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses 関数
エンドユーザーライセンス (Eul) がローカルにキャッシュされているかどうかを取得します。

  
**戻り値**: ライセンスキャッシュの構成