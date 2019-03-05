---
title: class mip::ProtectionHandler::Observer
description: Mip::protectionhandler クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 00d74069374850a562547cd161ad4c5f15927b0a
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333723"
---
# <a name="class-mipprotectionhandlerobserver"></a>class mip::ProtectionHandler::Observer 
[ProtectionHandler](class_mip_protectionhandler.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 void OnCreateProtectionHandlerSuccess (const std::shared_ptr\<ProtectionHandler\>& protectionHandler、const std::shared_ptr\<void\>& コンテキスト)  |  [ProtectionHandler](class_mip_protectionhandler.md) が正しく作成されると呼び出されます。
パブリック仮想 void OnCreateProtectionHandlerFailure (const std::exception_ptr & エラー、const std::shared_ptr\<void\>& コンテキスト)  |  [ProtectionHandler](class_mip_protectionhandler.md) の作成に失敗すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess 関数
[ProtectionHandler](class_mip_protectionhandler.md) が正しく作成されると呼び出されます。

パラメーター:  
* **protectionHandler**:新しく作成された[ProtectionHandler](class_mip_protectionhandler.md)


* **コンテキスト**:同じコンテキストに渡された[ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function)または[ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) または [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess または ProtectionEngine::Observer::OnCreateProtectionHandlerFailure に転送されます
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure 関数
[ProtectionHandler](class_mip_protectionhandler.md) の作成に失敗すると呼び出されます。

パラメーター:  
* **エラー**:作成時に発生したエラー 


* **コンテキスト**:同じコンテキストに渡された[ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function)または[ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) または [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess または ProtectionEngine::Observer::OnCreateProtectionHandlerFailure に転送されます
