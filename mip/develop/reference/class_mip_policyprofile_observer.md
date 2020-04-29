---
title: 'クラス PolicyProfile:: オブザーバー'
description: 'Microsoft Information Protection (MIP) SDK の policyprofile:: observer クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 5fc8dab4c74b613ff199d16c7b39205476b87249
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760614"
---
# <a name="class-policyprofileobserver"></a>クラス PolicyProfile:: オブザーバー 
クライアントがプロファイル関連のイベントに関する通知を取得するための Observer インターフェイス。
すべてのエラーは mip::Error から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 void OnLoadSuccess (const std:: shared_ptr\<policyprofile\>& profile, const std:: shared_ptr\<void\>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
パブリック仮想 void OnLoadFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess (const std:: vector\<std:: String\>& engineIds、const std:: shared_ptr\<void\>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  エラーの原因となったエンジンを一覧表示するときに呼び出されます。
public virtual void OnUnloadEngineSuccess (const std:: shared_ptr\<void\>& context)  |  エンジンが正常にアンロードされたときに呼び出されます。
public virtual void OnUnloadEngineFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  エンジンのアンロードがエラーの原因となったときに呼び出されます。
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<policyengine\>& engine、const std:: shared_ptr\<void\>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineStarting (bool requiresPolicyFetch)  |  エンジンのポリシーデータをサーバーからフェッチする必要があるかどうか、またはローカルにキャッシュされたデータから作成できるかどうかを示すために、エンジンを作成する前に呼び出されます。
public virtual void OnAddEngineFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  新しいエンジンの追加がエラーの原因となったときに呼び出されます。
public virtual void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  エンジンの削除がエラーの原因となったときに呼び出されます。
public virtual void OnPolicyChanged(const std::string& engineId)  |  指定された ID を持つエンジンに対してポリシーが変更された場合、または読み込まれたカスタム感度の種類が変更された場合に呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 関数
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 操作を開始するために使用される現在のプロファイル。 


* **context**: LoadAsync 操作に渡されるコンテキスト。


  
### <a name="onloadfailure-function"></a>OnLoadFailure 関数
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **error**: 読み込み操作が失敗する原因となったエラー。 


* **context**: LoadAsync 操作に渡されるコンテキスト。


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 関数
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン id の一覧。 


* **context**: ListEnginesAsync 操作に渡されるコンテキスト。


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 関数
エラーの原因となったエンジンを一覧表示するときに呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **context**: ListEnginesAsync 操作に渡されるコンテキスト。


  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess 関数
エンジンが正常にアンロードされたときに呼び出されます。

パラメーター:  
* **context**: UnloadEngineAsync 操作に渡されるコンテキスト。


  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure 関数
エンジンのアンロードがエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンのアンロード操作が失敗する原因となったエラー。 


* **context**: UnloadEngineAsync 操作に渡されるコンテキスト。


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 関数
新しいエンジンが正常に追加されたときに呼び出されます。

パラメーター:  
* **engine**: 新しく追加されたエンジン 


* **context**: AddEngineAsync 操作に渡されるコンテキスト


  
### <a name="onaddenginestarting-function"></a>OnAddEngineStarting 関数
エンジンのポリシーデータをサーバーからフェッチする必要があるかどうか、またはローカルにキャッシュされたデータから作成できるかどうかを示すために、エンジンを作成する前に呼び出されます。

パラメーター:  
* **requiresPolicyFetch**: エンジンデータを HTTP 経由でフェッチする必要があるか、キャッシュから読み込まれるかを記述します


この省略可能なコールバックは、AddEngineAsync 操作の完了に HTTP 操作が必要かどうかを通知するために、アプリケーションによって使用される場合があります。
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 関数
新しいエンジンの追加がエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **context**: AddEngineAsync 操作に渡されるコンテキスト。


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 関数
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **context**: DeleteEngineAsync 操作に渡されるコンテキスト。


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 関数
エンジンの削除がエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **context**: DeleteEngineAsync 操作に渡されるコンテキスト。


  
### <a name="onpolicychanged-function"></a>OnPolicyChanged 関数
指定された ID を持つエンジンに対してポリシーが変更された場合、または読み込まれたカスタム感度の種類が変更された場合に呼び出されます。

パラメーター:  
* **engineId**: エンジン 


新しいポリシーを読み込むには、指定されたエンジン ID を使用して AddEngineAsync をもう一度呼び出す必要があります。