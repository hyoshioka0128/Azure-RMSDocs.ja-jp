---
title: class mip::ProtectionEngine::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionengine クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 8985b5646849338213855017da042538a27c935b
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057634"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
[ProtectionEngine](class_mip_protectionengine.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std:: shared_ptr\<std:: vector\<std:: string\>\>& templateids、const std:: shared_ptr\<void\>& context)  |  テンプレートが正しく取得されると呼び出されます。
public virtual void OnGetTemplatesFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  テンプレートの取得でエラーが発生すると呼び出されます。
public virtual void OnGetRightsForLabelIdSuccess (const std:: shared_ptr\<std:: vector\<std:: string\>\>& 権限、const std:: shared_ptr\<void\>& context)  |  権限が正しく取得されると呼び出されます。
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  ユーザーのラベル ID に対する権限を取得するときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 関数
テンプレートが正しく取得されると呼び出されます。

パラメーター:  
* **Templateids**:取得したテンプレートのリストへの参照 


* **コンテキスト**:[Protectionengine:: Gettemplates async](class_mip_protectionengine.md#gettemplatesasync-function)に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function) に転送されます
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure 関数
テンプレートの取得でエラーが発生すると呼び出されます。

パラメーター:  
* **エラー**:テンプレートの取得中に発生した[エラー](class_mip_error.md) 


* **コンテキスト**:[Protectionengine:: Gettemplates async](class_mip_protectionengine.md#gettemplatesasync-function)に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function) に転送されます
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess 関数
権限が正しく取得されると呼び出されます。

パラメーター:  
* **権限**:取得した権限の一覧への参照 


* **コンテキスト**:ProtectionEngine:: GetRightsForLabelIdAsync に渡されたものと同じコンテキスト。


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: GetRightsForLabelIdAsync に渡すことができます。 同じコンテキストは、 [Protectionengine:: オブザーバー:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function)または[Protectionengine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)にそのように転送されます。
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 関数
ユーザーのラベル ID に対する権限を取得するときに呼び出されます。

パラメーター:  
* **エラー**:権限の取得中に[エラー](class_mip_error.md)が発生しました 


* **コンテキスト**:ProtectionEngine:: GetRightsForLabelIdAsync に渡されたものと同じコンテキスト。


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: GetRightsForLabelIdAsync に渡すことができ、同じコンテキストは[Protectionengine:: Observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function)にそのまま転送されます。または[Protectionengine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)