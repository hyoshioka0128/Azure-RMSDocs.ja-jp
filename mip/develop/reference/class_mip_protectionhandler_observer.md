---
title: 'クラス ProtectionHandler:: オブザーバー'
description: 'Microsoft Information Protection (MIP) SDK の protectionhandler:: observer クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 66453d343505cc57427e177eac258b83a2663eb0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764437"
---
# <a name="class-protectionhandlerobserver"></a>クラス ProtectionHandler:: オブザーバー 
ProtectionHandler に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void Oncreateprotectionハンドラ Success (const std:: shared_ptr\<protectionhandler\>& protectionhandler、const std:: shared_ptr\<void\>& context)  |  ProtectionHandler が正しく作成されると呼び出されます。
パブリック仮想 void Oncreateprotectionハンドラ Failure (const std:: exception_ptr& error、const std:: shared_ptr\<void\>& context)  |  ProtectionHandler の作成に失敗すると呼び出されます。
  
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