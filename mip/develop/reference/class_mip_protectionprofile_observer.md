---
title: class mip::ProtectionProfile::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionprofile クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: bf3a43f28c4a445a5e2040108152832d2bffcfcd
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885105"
---
# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
[ProtectionProfile](class_mip_protectionprofile.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 void onloadsuccess (const std:: shared_ptr\<protectionprofile\>& profile、const std:: shared_ptr\<void\>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
パブリック仮想 void onloadfailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess (const std:: vector\<std:: string\>& engineIds、const std:: shared_ptr\<void\>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  エンジンの一覧の作成中にエラーが発生すると呼び出されます。
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<protectionengine\>& engine、const std:: shared_ptr\<void\>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  新しいエンジンの追加でエラーが発生すると呼び出されます。
public virtual void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  エンジンの削除でエラーが発生すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 関数
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **プロファイル**:新しく作成された[Protectionprofile](class_mip_protectionprofile.md)への参照


* **コンテキスト**:[Protectionprofile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function) に渡すことができ、その同じコンテキストがそのまま [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) または [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function) に転送されます
  
### <a name="onloadfailure-function"></a>OnLoadFailure 関数
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **エラー**:読み込み中に発生した[エラー](class_mip_error.md) 


* **コンテキスト**:[Protectionprofile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function) に渡すことができ、その同じコンテキストがそのまま [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) または [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function) に転送されます
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 関数
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン ID の一覧。 


* **コンテキスト**:[Protectionprofile:: ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)に渡されたものと同じコンテキスト


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 関数
エンジンの一覧の作成中にエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **コンテキスト**:[Protectionprofile:: ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)に渡されたものと同じコンテキスト


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 関数
新しいエンジンが正常に追加されたときに呼び出されます。

パラメーター:  
* **エンジン**:新しく作成されたエンジン 


* **コンテキスト**:[Protectionprofile:: AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)に渡されたものと同じコンテキスト


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 関数
新しいエンジンの追加でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **コンテキスト**:[Protectionprofile:: AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)に渡されたものと同じコンテキスト


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 関数
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **コンテキスト**:Protectionprofile に渡されたのと同じコンテキスト[::D eleteengineasync](class_mip_protectionprofile.md#deleteengineasync-function)


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 関数
エンジンの削除でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **コンテキスト**:Protectionprofile に渡されたのと同じコンテキスト[::D eleteengineasync](class_mip_protectionprofile.md#deleteengineasync-function)

