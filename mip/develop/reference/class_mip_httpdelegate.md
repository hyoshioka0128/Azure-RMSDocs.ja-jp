---
title: クラス HttpDelegate
description: 'Microsoft Information Protection (MIP) SDK の httpdelegate:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: e1ddc8595e3cba2172228532a84ca68883cc0afd
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762827"
---
# <a name="class-httpdelegate"></a>クラス HttpDelegate 
HTTP の処理をオーバーライドするインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std:: shared_ptr\<HttpRequest\>& request、const std:: shared_ptr\<void\>& context)  |  HTTP 要求を送信します。
public std:: shared_ptr\<HttpOperation\> sendasync (const std:: shared_ptr\<HttpRequest\>& request、const std:: shared_ptr\<void\>& context、const std:: function\<void (std:: shared_ptr\<HttpOperation\> )  |  HTTP 要求を非同期に送信します。
public void CancelOperation (const std:: string& requestId)  |  特定の HTTP 操作をキャンセルします。
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