---
title: class mip ProtectionProfile Observer
description: class mip ProtectionProfile Observer のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3678e6c1e1659f28b2f1dcc36f61295a8d29393e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446432"
---
# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
[ProtectionProfile](class_mip_protectionprofile.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エンジンの一覧の作成中にエラーが発生すると呼び出されます。
public virtual void OnAddEngineSuccess(const std::shared_ptr<ProtectionEngine>& engine, const std::shared_ptr<void>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  新しいエンジンの追加でエラーが発生すると呼び出されます。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エンジンの削除でエラーが発生すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess"></a>OnLoadSuccess
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 新しく作成された [ProtectionProfile](class_mip_protectionprofile.md) への参照


* **context**: [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) に渡されたものと同じコンテキスト。


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) または [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure) に転送されます
  
### <a name="onloadfailure"></a>OnLoadFailure
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **error**: 読み込み中に発生した[エラー](class_mip_error.md) 


* **context**: [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) に渡されたものと同じコンテキスト。


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) または [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure) に転送されます
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン ID の一覧。 


* **context**: [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync) に渡されたものと同じコンテキスト。


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
エンジンの一覧の作成中にエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **context**: [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync) に渡されたものと同じコンテキスト。


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
新しいエンジンが正常に追加されたときに呼び出されます。

パラメーター:  
* **engine**: 新しく作成されたエンジン 


* **context**: [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync) に渡されたものと同じコンテキスト。


  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
新しいエンジンの追加でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **context**: [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync) に渡されたものと同じコンテキスト。


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **context**: [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync) に渡されたものと同じコンテキスト。


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
エンジンの削除でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **context**: [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync) に渡されたものと同じコンテキスト。

