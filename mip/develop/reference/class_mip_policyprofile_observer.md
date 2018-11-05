---
title: class mip PolicyProfile Observer
description: class mip PolicyProfile Observer のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5de2156f4906c14e4ebc1418df8acb092c089d7d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446904"
---
# <a name="class-mippolicyprofileobserver"></a>class mip::PolicyProfile::Observer 
クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_policyprofile_observer.md) インターフェイス。
すべてのエラーは [mip::Error](class_mip_error.md) から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<PolicyProfile>& profile, const std::shared_ptr<void>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エラーの原因となったエンジンを一覧表示するときに呼び出されます。
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  エンジンが正常にアンロードされたときに呼び出されます。
public virtual void OnUnloadEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エンジンのアンロードがエラーの原因となったときに呼び出されます。
public virtual void OnAddEngineSuccess(const std::shared_ptr<PolicyEngine>& engine, const std::shared_ptr<void>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  新しいエンジンの追加がエラーの原因となったときに呼び出されます。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エンジンの削除がエラーの原因となったときに呼び出されます。
 public virtual void OnPolicyChanged(const std::string& engineId)  |  指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess"></a>OnLoadSuccess
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 操作の開始に使用された現在のプロファイル。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onloadfailure"></a>OnLoadFailure
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **error**: 読み込み操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン ID の一覧。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
エラーの原因となったエンジンを一覧表示するときに呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
エンジンが正常にアンロードされたときに呼び出されます。

パラメーター:  
* **context**: 操作に渡されたコンテキスト。


  
### <a name="onunloadenginefailure"></a>OnUnloadEngineFailure
エンジンのアンロードがエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンのアンロード操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
新しいエンジンが正常に追加されたときに呼び出されます。
  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
新しいエンジンの追加がエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **context**: 操作に渡されたコンテキスト。


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
エンジンの削除がエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onpolicychanged"></a>OnPolicyChanged
指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。

パラメーター:  
* **engineId**: エンジン 


新しいポリシーを読み込むには、指定されたエンジン ID を使用して AddEngineAsync をもう一度呼び出す必要があります。