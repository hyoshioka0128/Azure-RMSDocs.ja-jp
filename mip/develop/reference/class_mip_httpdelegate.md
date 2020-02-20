---
title: class mip::HttpDelegate
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpdelegate クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e629e15ed3a4754123f8ca71adee04d32bc3785f
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488111"
---
# <a name="class-miphttpdelegate"></a>class mip::HttpDelegate 
HTTP の処理をオーバーライドするインターフェイス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std:: shared_ptr\<HttpRequest\>& request、const std:: shared_ptr\<void\>& context)  |  HTTP 要求を送信します。
public std:: shared_ptr\<HttpOperation\> SendAsync (const std:: shared_ptr\<HttpRequest\>& request、const std:: shared_ptr\<void\>& context、const std:: function\<void (std:: shared_ptr\<HttpOperation\>)  |  HTTP 要求を非同期に送信します。
public void CancelOperation (const std:: string & requestId)  |  特定の HTTP 操作をキャンセルします。
public void CancelAllOperations ()  |  進行中の HTTP 要求を取り消します。
  
## <a name="members"></a>Members
  
### <a name="send-function"></a>Send 関数
HTTP 要求を送信します。

パラメータ:  
* **要求**: HTTP 要求 


* **コンテキスト**: HTTP 要求となった、API に渡された同じ不透明なクライアント コンテキスト



  
**戻り値**: HTTP 操作コンテナー
  
### <a name="sendasync-function"></a>SendAsync 関数
HTTP 要求を非同期に送信します。

パラメータ:  
* **要求**: HTTP 要求 


* **コンテキスト**: HTTP 要求となった、API に渡された同じ不透明なクライアント コンテキスト 


* の**実行が**完了したときに実行される関数



  
**戻り値**: HTTP 操作コンテナー
  
### <a name="canceloperation-function"></a>CancelOperation 関数
特定の HTTP 操作をキャンセルします。

パラメータ:  
* **requestId**: 取り消す要求の ID


  
### <a name="cancelalloperations-function"></a>CancelAllOperations 関数
進行中の HTTP 要求を取り消します。