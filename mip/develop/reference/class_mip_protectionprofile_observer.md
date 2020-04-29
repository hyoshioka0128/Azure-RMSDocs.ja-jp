---
title: 'クラス ProtectionProfile:: オブザーバー'
description: 'Microsoft Information Protection (MIP) SDK の protectionprofile:: observer クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 8448f75a06bfe99debcf4c1c40ab2228c46690e6
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763931"
---
# <a name="class-protectionprofileobserver"></a>クラス ProtectionProfile:: オブザーバー 
ProtectionProfile に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 void OnLoadSuccess (const std:: shared_ptr\<protectionprofile\>& profile、const std:: shared_ptr\<void\>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
パブリック仮想 void OnLoadFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess (const std:: vector\<std:: String\>& engineIds、const std:: shared_ptr\<void\>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  エンジンの一覧の作成中にエラーが発生すると呼び出されます。
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<protectionengine\>& engine、const std:: shared_ptr\<void\>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  新しいエンジンの追加でエラーが発生すると呼び出されます。
public virtual void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  エンジンの削除でエラーが発生すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 関数
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 新しく作成された ProtectionProfile への参照


* **コンテキスト**: protectionprofile:: LoadAsync に渡されたのと同じコンテキスト。


アプリケーションは任意の種類のコンテキスト (たとえば、std::p romise, std:: function) を ProtectionProfile:: LoadAsync に渡すことができます。また、同じコンテキストは、そのまま、ProtectionProfile:: Observer:: OnLoadSuccess または ProtectionProfile:: Observer:: Onloadsuccess に転送されます。
  
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


* **context**: [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md) に渡されたものと同じコンテキスト。


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 関数
エンジンの一覧の作成中にエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **context**: ProtectionProfile::ListEnginesAsync に渡されたものと同じコンテキスト。


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 関数
新しいエンジンが正常に追加されたときに呼び出されます。

パラメーター:  
* **engine**: 新しく作成されたエンジン 


* **context**: [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md) に渡されたものと同じコンテキスト。


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 関数
新しいエンジンの追加でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **context**: ProtectionProfile::AddEngineAsync に渡されたものと同じコンテキスト。


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 関数
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **context**: [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md) に渡されたものと同じコンテキスト。


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 関数
エンジンの削除でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **context**: ProtectionProfile::DeleteEngineAsync に渡されたものと同じコンテキスト。

