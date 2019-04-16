---
title: class mip::HttpDelegate
description: Mip::httpdelegate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6dedd5e52b0599a58acabd85f7bd076169b3758e
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574195"
---
# <a name="class-miphttpdelegate"></a>class mip::HttpDelegate 
HTTP の処理をオーバーライドするインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<HttpOperation\>送信 (const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& コンテキスト)  |  HTTP 要求を送信します。
public std::shared_ptr\<HttpOperation\> SendAsync (const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& コンテキストには、const std:。関数\<void (std::shared_ptr\<HttpOperation\>)\>& callbackFn)  |  HTTP 要求を非同期的に送信します。
public void CancelOperation(const std::string& requestId)  |  特定の HTTP 操作をキャンセルします。
public void CancelAllOperations()  |  実行中の HTTP 要求をキャンセルします。
  
## <a name="members"></a>メンバー
  
### <a name="send-function"></a>Send 関数
HTTP 要求を送信します。

パラメーター:  
* **要求**:HTTP 要求 


* **コンテキスト**:この HTTP 要求が発生する API に渡された同じ不透明なクライアント コンテキスト



  
**返します**:HTTP 操作のコンテナー
  
### <a name="sendasync-function"></a>SendAsync 関数
HTTP 要求を非同期的に送信します。

パラメーター:  
* **要求**:HTTP 要求 


* **コンテキスト**:この HTTP 要求が発生する API に渡された同じ不透明なクライアント コンテキスト 


* **callbackFn**:完了時に実行される関数



  
**返します**:HTTP 操作のコンテナー
  
### <a name="canceloperation-function"></a>CancelOperation 関数
特定の HTTP 操作をキャンセルします。

パラメーター:  
* **requestId**:取り消し要求の ID


  
### <a name="cancelalloperations-function"></a>CancelAllOperations 関数
実行中の HTTP 要求をキャンセルします。