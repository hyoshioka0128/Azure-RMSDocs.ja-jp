---
title: class mip::ProtectionProfile::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionprofile クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a9138e497655dfa939a9ac9b15d7ed228331e9e0
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560713"
---
# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
ProtectionProfile に関連する通知を受信するインターフェイスです。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 void OnLoadSuccess (const std:: shared_ptr\<ProtectionProfile\>& profile、const std:: shared_ptr\<void\>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
パブリック仮想 void OnLoadFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess (const std:: vector\<std:: string\>& engineIds、const std:: shared_ptr\<void\>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  エンジンの一覧の作成中にエラーが発生すると呼び出されます。
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<ProtectionEngine\>& engine、const std:: shared_ptr\<void\>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  新しいエンジンの追加でエラーが発生すると呼び出されます。
public virtual void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  エンジンの削除でエラーが発生すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 関数
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 新しく作成された protectionprofile への参照


* **context**: ProtectionProfile::LoadAsync に渡されたものと同じコンテキスト。


アプリケーションで任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionProfile:: LoadAsync に渡すことができます。また、同じコンテキストは、そのまま、ProtectionProfile:: Observer:: OnLoadSuccess または ProtectionProfile:: Observer:: O にそのまま転送されます。nLoadFailure
  
### <a name="onloadfailure-function"></a>OnLoadFailure 関数
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **エラー**: 読み込み中にエラーが発生しました 


* **context**: ProtectionProfile::LoadAsync に渡されたものと同じコンテキスト。


アプリケーションで任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionProfile:: LoadAsync に渡すことができます。また、同じコンテキストは、そのまま、ProtectionProfile:: Observer:: OnLoadSuccess または ProtectionProfile:: Observer:: O にそのまま転送されます。nLoadFailure
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 関数
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン ID の一覧。 


* **コンテキスト**: protectionprofile:: ListEnginesAsync に渡されたものと同じコンテキスト


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 関数
エンジンの一覧の作成中にエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **コンテキスト**: protectionprofile:: ListEnginesAsync に渡されたものと同じコンテキスト


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 関数
新しいエンジンが正常に追加されたときに呼び出されます。

パラメーター:  
* **engine**: 新しく作成されたエンジン 


* **コンテキスト**: protectionprofile:: AddEngineAsync に渡されたものと同じコンテキスト


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 関数
新しいエンジンの追加でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **コンテキスト**: protectionprofile:: AddEngineAsync に渡されたものと同じコンテキスト


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 関数
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **コンテキスト**: protectionprofile に渡されたのと同じコンテキスト::D eleteengineasync


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 関数
エンジンの削除でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **コンテキスト**: protectionprofile に渡されたのと同じコンテキスト::D eleteengineasync

