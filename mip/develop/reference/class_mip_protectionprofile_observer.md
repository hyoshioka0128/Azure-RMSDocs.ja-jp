---
title: 'クラス ProtectionProfile:: オブザーバー'
description: 'Microsoft Information Protection (MIP) SDK の protectionprofile:: observer クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 38f578991ed9409aed6ea87622d8db79dcd78b06
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214441"
---
# <a name="class-protectionprofileobserver"></a>クラス ProtectionProfile:: オブザーバー 
ProtectionProfile に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr\<ProtectionProfile\>& profile, const std::shared_ptr\<void\>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess (const std:: vector \<std::string\>& engineIds、const std:: shared_ptr \<void\>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  エンジンの一覧の作成中にエラーが発生すると呼び出されます。
public virtual void OnAddEngineSuccess(const std::shared_ptr\<ProtectionEngine\>& engine, const std::shared_ptr\<void\>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  新しいエンジンの追加でエラーが発生すると呼び出されます。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  エンジンの削除でエラーが発生すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 関数
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 新しく作成された ProtectionProfile への参照


* **context**: ProtectionProfile::LoadAsync に渡されたものと同じコンテキスト。


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を ProtectionProfile::LoadAsync に渡すことができ、その同じコンテキストがそのまま ProtectionProfile::Observer::OnLoadSuccess または ProtectionProfile::Observer::OnLoadFailure に転送されます
  
### <a name="onloadfailure-function"></a>OnLoadFailure 関数
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **エラー**: 読み込み中にエラーが発生しました 


* **context**: ProtectionProfile::LoadAsync に渡されたものと同じコンテキスト。


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を ProtectionProfile::LoadAsync に渡すことができ、その同じコンテキストがそのまま ProtectionProfile::Observer::OnLoadSuccess または ProtectionProfile::Observer::OnLoadFailure に転送されます
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 関数
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン id の一覧。 


* **context**: ProtectionProfile::ListEnginesAsync に渡されたものと同じコンテキスト。


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 関数
エンジンの一覧の作成中にエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **context**: ProtectionProfile::ListEnginesAsync に渡されたものと同じコンテキスト。


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 関数
新しいエンジンが正常に追加されたときに呼び出されます。

パラメーター:  
* **engine**: 新しく作成されたエンジン 


* **context**: ProtectionProfile::AddEngineAsync に渡されたものと同じコンテキスト。


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 関数
新しいエンジンの追加でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **context**: ProtectionProfile::AddEngineAsync に渡されたものと同じコンテキスト。


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 関数
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **context**: ProtectionProfile::DeleteEngineAsync に渡されたものと同じコンテキスト。


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 関数
エンジンの削除でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **context**: ProtectionProfile::DeleteEngineAsync に渡されたものと同じコンテキスト。

