---
title: class mip ProtectionEngine Observer
description: class mip ProtectionEngine Observer のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 9999b450d614b4465f151f0b2df80892a83bc143
ms.sourcegitcommit: 4cd90fcf94ac6e2543d8be10e6e29e8218d5fd9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49651347"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
[ProtectionEngine](class_mip_protectionengine.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  テンプレートが正しく取得されると呼び出されます。
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  テンプレートの取得でエラーが発生すると呼び出されます。
public virtual void OnGetRightsForLabelIdSuccess(const std::shared_ptr<std::vector<std::string>>& rights, const std::shared_ptr<void>& context)  |  権限が正しく取得されると呼び出されます。
public virtual void OnGetRightsForLabelIdFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  ユーザーのラベル ID に対する権限を取得するときに呼び出されます。
public virtual void OnGetGrantingLabelIdsSuccess(const std::shared_ptr<std::vector<std::string>>& labelIds, const std::shared_ptr<void>& context)  |  ラベル ID が正しく取得されると呼び出されます。
public virtual void OnGetGrantingLabelIdsFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  ユーザーのラベル ID を取得するときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
テンプレートが正しく取得されると呼び出されます。

パラメーター:  
* **templateIds**: 取得したテンプレートのリストへの参照 


* **context**: [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure) に転送されます
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
テンプレートの取得でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: テンプレートの取得中に発生した[エラー](class_mip_error.md) 


* **context**: [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure) に転送されます
  
### <a name="ongetrightsforlabelidsuccess"></a>OnGetRightsForLabelIdSuccess
権限が正しく取得されると呼び出されます。

パラメーター:  
* **rights**: 取得する権限の一覧への参照 


* **context**: [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) または [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure) に転送されます
  
### <a name="ongetrightsforlabelidfailure"></a>OnGetRightsForLabelIdFailure
ユーザーのラベル ID に対する権限を取得するときに呼び出されます。

パラメーター:  
* **error**: 権限の取得中に発生した[エラー](class_mip_error.md) 


* **context**: [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) または [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure) に転送されます
  
### <a name="ongetgrantinglabelidssuccess"></a>OnGetGrantingLabelIdsSuccess
ラベル ID が正しく取得されると呼び出されます。

パラメーター:  
* **labelIds**: 取得したラベル ID の一覧への参照 


* **context**: [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) または [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure) に転送されます
  
### <a name="ongetgrantinglabelidsfailure"></a>OnGetGrantingLabelIdsFailure
ユーザーのラベル ID を取得するときに呼び出されます。

パラメーター:  
* **error**: ラベル ID の取得中に発生した[エラー](class_mip_error.md) 


* **context**: [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) または [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure) に転送されます
