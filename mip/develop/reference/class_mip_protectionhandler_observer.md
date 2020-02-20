---
title: class mip::ProtectionHandler::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionhandler クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 8f661f3ebf9bc657a4dd6f6356b26cd582d4aa2e
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486819"
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

パラメータ:  
* **protectionhandler**: 新しく作成された protectionhandler


* **コンテキスト**: protectionengine:: Createprotectionハンドラ From記述子 async または protectionengine:: Createprotectionハンドラ Fromはっこう licenseasync に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (たとえば、std::p romise、std:: function) を ProtectionEngine:: Createprotectionハンドラ From記述子 Async または ProtectionEngine:: Createprotectionハンドラ From Licenseasync に渡すことができ、同じコンテキストになります。ProtectionEngine:: Observer:: Oncreateprotectionハンドラ Success または ProtectionEngine:: Observer:: Oncreateprotectionハンドラエラーには、その状態として転送されます。
  
### <a name="oncreateprotectionhandlerfailure-function"></a>Oncreateprotectionハンドラ Failure 関数
ProtectionHandler の作成に失敗したときに呼び出されます。

パラメータ:  
* **error**: 作成中に発生するエラー 


* **コンテキスト**: protectionengine:: Createprotectionハンドラ From記述子 async または protectionengine:: Createprotectionハンドラ Fromはっこう licenseasync に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (たとえば、std::p romise、std:: function) を ProtectionEngine:: Createprotectionハンドラ From記述子 Async または ProtectionEngine:: Createprotectionハンドラ From Licenseasync に渡すことができ、同じコンテキストになります。ProtectionEngine:: Observer:: Oncreateprotectionハンドラ Success または ProtectionEngine:: Observer:: Oncreateprotectionハンドラエラーには、その状態として転送されます。