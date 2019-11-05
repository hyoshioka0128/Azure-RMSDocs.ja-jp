---
title: class mip::HttpDelegate
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpdelegate クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a29673c71aaa0357ebb52bc4cab3b3fef74a21d1
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560193"
---
# <a name="class-miphttpdelegate"></a>class mip::HttpDelegate 
HTTP の処理をオーバーライドするインターフェイス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std:: shared_ptr\<HttpRequest\>& request、const std:: shared_ptr\<void\>& context)  |  HTTP 要求を送信します。
public std:: shared_ptr\<HttpOperation\> SendAsync (const std:: shared_ptr\<HttpRequest\>& request、const std:: shared_ptr\<void\>& context、const std:: function\<void (std:: shared_ptr\<HttpOperation\>)  |  HTTP 要求を非同期に送信します。
public void CancelOperation (const std:: string & requestId)  |  特定の HTTP 操作をキャンセルします。
public void CancelAllOperations ()  |  進行中の HTTP 要求を取り消します。
  
## <a name="members"></a>メンバー
  
### <a name="send-function"></a>Send 関数
HTTP 要求を送信します。

パラメーター:  
* **要求**: HTTP 要求 


* **コンテキスト**: HTTP 要求となった、API に渡された同じ不透明なクライアント コンテキスト



  
**戻り値**: HTTP 操作コンテナー
  
### <a name="sendasync-function"></a>SendAsync 関数
HTTP 要求を非同期に送信します。

パラメーター:  
* **要求**: HTTP 要求 


* **コンテキスト**: HTTP 要求となった、API に渡された同じ不透明なクライアント コンテキスト 


* の**実行が**完了したときに実行される関数



  
**戻り値**: HTTP 操作コンテナー
  
### <a name="canceloperation-function"></a>CancelOperation 関数
特定の HTTP 操作をキャンセルします。

パラメーター:  
* **requestId**: 取り消す要求の ID


  
### <a name="cancelalloperations-function"></a>CancelAllOperations 関数
進行中の HTTP 要求を取り消します。