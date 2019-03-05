---
title: class mip::PolicyProfile::Observer
description: Mip::policyprofile クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3f98e106bb7fcc30e333b70345687260add6bd22
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333616"
---
# <a name="class-mippolicyprofileobserver"></a>class mip::PolicyProfile::Observer 
クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_policyprofile_observer.md) インターフェイス。
すべてのエラーは [mip::Error](class_mip_error.md) から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 void OnLoadSuccess (const std::shared_ptr\<PolicyProfile\>(& a) プロファイル、const std::shared_ptr\<void\>& コンテキスト)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
パブリック仮想 void OnListEnginesSuccess (const std::vector\<std::string\>& engineids:、const std::shared_ptr\<void\>& コンテキスト)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  エラーの原因となったエンジンを一覧表示するときに呼び出されます。
パブリック仮想 void OnUnloadEngineSuccess (const std::shared_ptr\<void\>& コンテキスト)  |  エンジンが正常にアンロードされたときに呼び出されます。
パブリック仮想 void OnUnloadEngineFailure (const std::exception_ptr & エラー、const std::shared_ptr\<void\>& コンテキスト)  |  エンジンのアンロードがエラーの原因となったときに呼び出されます。
パブリック仮想 void OnAddEngineSuccess (const std::shared_ptr\<PolicyEngine\>& エンジン, const std::shared_ptr\<void\>& コンテキスト)  |  新しいエンジンが正常に追加されたときに呼び出されます。
パブリック仮想 void OnAddEngineStarting (bool requiresPolicyFetch)  |  サーバーからそのエンジンのポリシーのデータをフェッチする必要があるかどうか、またはローカルにキャッシュされたデータから作成するかどうかを示すエンジンを作成する前に呼び出されます。
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  新しいエンジンの追加がエラーの原因となったときに呼び出されます。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  エンジンの削除がエラーの原因となったときに呼び出されます。
public virtual void OnPolicyChanged(const std::string& engineId)  |  指定した ID を使用してエンジンのポリシーが変更されたとき、または読み込まれたカスタム機密の種類が変更されたときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 関数
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 操作の開始に使用された現在のプロファイル。 


* **コンテキスト**: LoadAsync 操作に、コンテキストが渡されます。


  
### <a name="onloadfailure-function"></a>OnLoadFailure 関数
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **error**: 読み込み操作が失敗する原因となったエラー。 


* **コンテキスト**: LoadAsync 操作に、コンテキストが渡されます。


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 関数
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン ID の一覧。 


* **コンテキスト**: ListEnginesAsync 操作に、コンテキストが渡されます。


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 関数
エラーの原因となったエンジンを一覧表示するときに呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **コンテキスト**: ListEnginesAsync 操作に、コンテキストが渡されます。


  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess 関数
エンジンが正常にアンロードされたときに呼び出されます。

パラメーター:  
* **コンテキスト**: UnloadEngineAsync 操作に、コンテキストが渡されます。


  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure 関数
エンジンのアンロードがエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンのアンロード操作が失敗する原因となったエラー。 


* **コンテキスト**: UnloadEngineAsync 操作に、コンテキストが渡されます。


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 関数
新しいエンジンが正常に追加されたときに呼び出されます。

パラメーター:  
* **エンジン**: 新しく追加されたエンジン 


* **コンテキスト**: AddEngineAsync 操作に渡されるコンテキスト


  
### <a name="onaddenginestarting-function"></a>OnAddEngineStarting 関数
サーバーからそのエンジンのポリシーのデータをフェッチする必要があるかどうか、またはローカルにキャッシュされたデータから作成するかどうかを示すエンジンを作成する前に呼び出されます。

パラメーター:  
* **requiresPolicyFetch**:エンジンのデータを HTTP 経由でフェッチする必要があるかどうか、またはキャッシュから読み込まれるかどうかについて説明します


この省略可能なコールバックをアプリケーションにできない形式であるかどうか、AddEngineAsync 操作が必要になります (その関連付けられている遅延) で HTTP 操作を完了することができます。
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 関数
新しいエンジンの追加がエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **コンテキスト**: AddEngineAsync 操作に、コンテキストが渡されます。


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 関数
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **コンテキスト**: DeleteEngineAsync 操作に、コンテキストが渡されます。


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 関数
エンジンの削除がエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **コンテキスト**: DeleteEngineAsync 操作に、コンテキストが渡されます。


  
### <a name="onpolicychanged-function"></a>OnPolicyChanged 関数
指定した ID を使用してエンジンのポリシーが変更されたとき、または読み込まれたカスタム機密の種類が変更されたときに呼び出されます。

パラメーター:  
* **engineId**: エンジン 


新しいポリシーを読み込むには、指定されたエンジン ID を使用して AddEngineAsync をもう一度呼び出す必要があります。
