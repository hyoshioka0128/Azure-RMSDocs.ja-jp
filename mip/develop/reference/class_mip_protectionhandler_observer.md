---
title: class mip::ProtectionHandler::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionhandler クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: a02e84a7be2071340a0ffef6310788823b768de3
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057555"
---
# <a name="class-mipprotectionhandlerobserver"></a>class mip::ProtectionHandler::Observer 
[ProtectionHandler](class_mip_protectionhandler.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void oncreateprotectionハンドラ success (const std:: shared_ptr\<protectionhandler\>& protectionhandler、const std:: shared_ptr\<void\>& context)  |  [ProtectionHandler](class_mip_protectionhandler.md) が正しく作成されると呼び出されます。
public virtual void oncreateprotectionハンドラ failure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  [ProtectionHandler](class_mip_protectionhandler.md) の作成に失敗すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="oncreateprotectionhandlersuccess-function"></a>Oncreateprotectionハンドラ Success 関数
[ProtectionHandler](class_mip_protectionhandler.md) が正しく作成されると呼び出されます。

パラメーター:  
* **Protectionhandler**:新しく作成された[Protectionhandler](class_mip_protectionhandler.md)


* **コンテキスト**:[Protectionengine:: Createprotectionハンドラ From記述子 async](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function)または[protectionengine:: Createprotectionハンドラ fromはっこう licenseasync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) または [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess または ProtectionEngine::Observer::OnCreateProtectionHandlerFailure に転送されます
  
### <a name="oncreateprotectionhandlerfailure-function"></a>Oncreateprotectionハンドラ Failure 関数
[ProtectionHandler](class_mip_protectionhandler.md) の作成に失敗すると呼び出されます。

パラメーター:  
* **エラー**:作成中に発生したエラー 


* **コンテキスト**:[Protectionengine:: Createprotectionハンドラ From記述子 async](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function)または[protectionengine:: Createprotectionハンドラ fromはっこう licenseasync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) または [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess または ProtectionEngine::Observer::OnCreateProtectionHandlerFailure に転送されます