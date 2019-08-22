---
title: class mip::HttpDelegate
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpdelegate クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: d2b01c53b44d6884f47cf48c431ee7359f64b9c4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885598"
---
# <a name="class-miphttpdelegate"></a>class mip::HttpDelegate 
HTTP の処理をオーバーライドするインターフェイス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std:: shared_ptr\<HttpRequest\>& request、const std:: shared_ptr\<void\>& context)  |  HTTP 要求を送信します。
public std:: shared_ptr\<HttpOperation\> sendasync (const std:: shared_ptr\<HttpRequest\>& request、const std:: shared_ptr\<void\>& context、const std::関数\<void (std:: shared_ptr\<HttpOperation\>)\>& を返します。  |  HTTP 要求を非同期に送信します。
public void CancelOperation (const std:: string & requestId)  |  特定の HTTP 操作をキャンセルします。
public void CancelAllOperations ()  |  進行中の HTTP 要求を取り消します。
  
## <a name="members"></a>メンバー
  
### <a name="send-function"></a>Send 関数
HTTP 要求を送信します。

パラメーター:  
* **要求**:HTTP 要求 


* **コンテキスト**:この HTTP 要求を生成した API に渡された、同じ非透過クライアントコンテキスト。



  
次の**値を返し**ます。HTTP 操作コンテナー
  
### <a name="sendasync-function"></a>SendAsync 関数
HTTP 要求を非同期に送信します。

パラメーター:  
* **要求**:HTTP 要求 


* **コンテキスト**:この HTTP 要求を生成した API に渡された、同じ非透過クライアントコンテキスト。 


* "/":完了時に実行される関数



  
次の**値を返し**ます。HTTP 操作コンテナー
  
### <a name="canceloperation-function"></a>CancelOperation 関数
特定の HTTP 操作をキャンセルします。

パラメーター:  
* **requestId**:取り消す要求の ID


  
### <a name="cancelalloperations-function"></a>CancelAllOperations 関数
進行中の HTTP 要求を取り消します。