---
title: class mip ProtectionHandler Observer
description: class mip ProtectionHandler Observer のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 7fed286dec42f16d7dfa8e375ec739264bd365ba
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446181"
---
# <a name="class-mipprotectionhandlerobserver"></a>class mip::ProtectionHandler::Observer 
[ProtectionHandler](class_mip_protectionhandler.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  [ProtectionHandler](class_mip_protectionhandler.md) が正しく作成されると呼び出されます。
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  [ProtectionHandler](class_mip_protectionhandler.md) の作成に失敗すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="oncreateprotectionhandlersuccess"></a>OnCreateProtectionHandlerSuccess
[ProtectionHandler](class_mip_protectionhandler.md) が正しく作成されると呼び出されます。

パラメーター:  
* **protectionHandler**: 新しく作成された [ProtectionHandler](class_mip_protectionhandler.md)


* **context**: [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) または [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) に渡されたのと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) または [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess または ProtectionEngine::Observer::OnCreateProtectionHandlerFailure に転送されます
  
### <a name="oncreateprotectionhandlerfailure"></a>OnCreateProtectionHandlerFailure
[ProtectionHandler](class_mip_protectionhandler.md) の作成に失敗すると呼び出されます。

パラメーター:  
* **error**: 作成中に発生するエラー 


* **context**: [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) または [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) に渡されたのと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) または [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess または ProtectionEngine::Observer::OnCreateProtectionHandlerFailure に転送されます