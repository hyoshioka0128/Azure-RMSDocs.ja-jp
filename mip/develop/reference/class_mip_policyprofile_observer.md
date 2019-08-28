---
title: class mip::PolicyProfile::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p olicyprofile クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 1315f4c1289c63184b8fa029b3668b363b88b143
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054200"
---
# <a name="class-mippolicyprofileobserver"></a>class mip::PolicyProfile::Observer 
クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_policyprofile_observer.md) インターフェイス。
すべてのエラーは [mip::Error](class_mip_error.md) から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 void onloadsuccess (const std:: shared_ptr\<policyprofile\>& profile、const std:: shared_ptr\<void\>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
パブリック仮想 void onloadfailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess (const std:: vector\<std:: string\>& engineIds、const std:: shared_ptr\<void\>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  エラーの原因となったエンジンを一覧表示するときに呼び出されます。
public virtual void OnUnloadEngineSuccess (const std:: shared_ptr\<void\>& context)  |  エンジンが正常にアンロードされたときに呼び出されます。
public virtual void OnUnloadEngineFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  エンジンのアンロードがエラーの原因となったときに呼び出されます。
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<policyengine\>& engine、const std:: shared_ptr\<void\>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineStarting (bool requiresPolicyFetch)  |  エンジンのポリシーデータをサーバーからフェッチする必要があるかどうか、またはローカルにキャッシュされたデータから作成できるかどうかを示すために、エンジンを作成する前に呼び出されます。
public virtual void OnAddEngineFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  新しいエンジンの追加がエラーの原因となったときに呼び出されます。
public virtual void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  エンジンの削除がエラーの原因となったときに呼び出されます。
public virtual void OnPolicyChanged(const std::string& engineId)  |  指定された ID を持つエンジンに対してポリシーが変更された場合、または読み込まれたカスタム感度の種類が変更された場合に呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 関数
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 操作の開始に使用された現在のプロファイル。 


* **context**: LoadAsync 操作に渡されるコンテキスト。


  
### <a name="onloadfailure-function"></a>OnLoadFailure 関数
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **error**: 読み込み操作が失敗する原因となったエラー。 


* **context**: LoadAsync 操作に渡されるコンテキスト。


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 関数
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン ID の一覧。 


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
* **requiresPolicyFetch**:エンジンデータを HTTP 経由でフェッチする必要があるのか、それともキャッシュから読み込まれるのかを説明します。


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