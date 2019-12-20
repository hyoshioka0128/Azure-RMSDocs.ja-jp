---
title: class mip::ProtectionHandler::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionhandler クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8b48d6e5aacacb6f678fc7d5aea2aee531da88fa
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560097"
---
# <a name="class-mipprotectionhandlerobserver"></a>class mip::ProtectionHandler::Observer 
ProtectionHandler に関連する通知を受信するインターフェイスです。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void Oncreateprotectionハンドラ Success (const std:: shared_ptr\<ProtectionHandler\>& protectionHandler、const std:: shared_ptr\<void\>& context)  |  ProtectionHandler が正常に作成されたときに呼び出されます。
パブリック仮想 void Oncreateprotectionハンドラ Failure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  ProtectionHandler の作成に失敗したときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="oncreateprotectionhandlersuccess-function"></a>Oncreateprotectionハンドラ Success 関数
ProtectionHandler が正常に作成されたときに呼び出されます。

パラメーター:  
* **protectionhandler**: 新しく作成された protectionhandler


* **コンテキスト**: protectionengine:: Createprotectionハンドラ From記述子 async または protectionengine:: Createprotectionハンドラ Fromはっこう licenseasync に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (たとえば、std::p romise、std:: function) を ProtectionEngine:: Createprotectionハンドラ From記述子 Async または ProtectionEngine:: Createprotectionハンドラ From Licenseasync に渡すことができ、同じコンテキストになります。ProtectionEngine:: Observer:: Oncreateprotectionハンドラ Success または ProtectionEngine:: Observer:: Oncreateprotectionハンドラエラーには、その状態として転送されます。
  
### <a name="oncreateprotectionhandlerfailure-function"></a>Oncreateprotectionハンドラ Failure 関数
ProtectionHandler の作成に失敗したときに呼び出されます。

パラメーター:  
* **error**: 作成中に発生するエラー 


* **コンテキスト**: protectionengine:: Createprotectionハンドラ From記述子 async または protectionengine:: Createprotectionハンドラ Fromはっこう licenseasync に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (たとえば、std::p romise、std:: function) を ProtectionEngine:: Createprotectionハンドラ From記述子 Async または ProtectionEngine:: Createprotectionハンドラ From Licenseasync に渡すことができ、同じコンテキストになります。ProtectionEngine:: Observer:: Oncreateprotectionハンドラ Success または ProtectionEngine:: Observer:: Oncreateprotectionハンドラエラーには、その状態として転送されます。