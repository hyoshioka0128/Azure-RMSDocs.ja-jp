---
title: class mip::ProtectionEngine::Observer
description: Mip::protectionengine クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2473e4bc1e64e3e8de498d2976d07b5324346a53
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573498"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
[ProtectionEngine](class_mip_protectionengine.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック仮想 void OnGetTemplatesSuccess (const std::shared_ptr\<std::vector\<std::string\>\>& templateIds、const std::shared_ptr\<void\>& コンテキスト)  |  テンプレートが正しく取得されると呼び出されます。
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  テンプレートの取得でエラーが発生すると呼び出されます。
パブリック仮想 void OnGetRightsForLabelIdSuccess (const std::shared_ptr\<std::vector\<std::string\>\>& rights、const std::shared_ptr\<void\>& コンテキスト)  |  権限が正しく取得されると呼び出されます。
public virtual void OnGetRightsForLabelIdFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  ユーザーのラベル ID に対する権限を取得するときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 関数
テンプレートが正しく取得されると呼び出されます。

パラメーター:  
* **templateIds**:テンプレートの一覧への参照を取得 


* **コンテキスト**:同じコンテキストに渡された[ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function) に転送されます
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure 関数
テンプレートの取得でエラーが発生すると呼び出されます。

パラメーター:  
* **エラー**:[エラー](class_mip_error.md)テンプレートを取得中に発生しました。 


* **コンテキスト**:同じコンテキストに渡された[ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function) に転送されます
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess 関数
権限が正しく取得されると呼び出されます。

パラメーター:  
* **rights**:権限の一覧への参照を取得 


* **コンテキスト**:同じコンテキストに渡された[ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function)


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) または [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function) に転送されます
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 関数
ユーザーのラベル ID に対する権限を取得するときに呼び出されます。

パラメーター:  
* **エラー**:[エラー](class_mip_error.md)権利を取得中に発生しました。 


* **コンテキスト**:同じコンテキストに渡された[ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function)


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) または [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function) に転送されます