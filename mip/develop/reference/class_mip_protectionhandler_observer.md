---
title: 'クラス ProtectionHandler:: オブザーバー'
description: 'Microsoft Information Protection (MIP) SDK の protectionhandler:: observer クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: bd7a2b24b5eb80b3b17c025c43b0e0b31589a00a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214543"
---
# <a name="class-protectionhandlerobserver"></a>クラス ProtectionHandler:: オブザーバー 
ProtectionHandler に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr\<ProtectionHandler\>& protectionHandler, const std::shared_ptr\<void\>& context)  |  ProtectionHandler が正しく作成されると呼び出されます。
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  ProtectionHandler の作成に失敗すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="oncreateprotectionhandlersuccess-function"></a>Oncreateprotectionハンドラ Success 関数
ProtectionHandler が正しく作成されると呼び出されます。

パラメーター:  
* **protectionHandler**: 新しく作成された ProtectionHandler


* **context**: ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync または ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync に渡されたのと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync または ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess または ProtectionEngine::Observer::OnCreateProtectionHandlerFailure に転送されます
  
### <a name="oncreateprotectionhandlerfailure-function"></a>Oncreateprotectionハンドラ Failure 関数
ProtectionHandler の作成に失敗すると呼び出されます。

パラメーター:  
* **error**: 作成中に発生するエラー 


* **context**: ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync または ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync に渡されたのと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync または ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess または ProtectionEngine::Observer::OnCreateProtectionHandlerFailure に転送されます