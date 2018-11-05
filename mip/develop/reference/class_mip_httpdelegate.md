---
title: class mip HttpDelegate
description: class mip HttpDelegate のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3e55f9aff5a9ebd97731ec21e408a33f22905648
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445372"
---
# <a name="class-miphttpdelegate"></a>class mip::HttpDelegate 
HTTP の処理をオーバーライドするインターフェイス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::shared_ptr<HttpResponse> Send(const std::shared_ptr<HttpRequest>& request, const std::shared_ptr<void>& context)  |  HTTP 要求を送信します。
  
## <a name="members"></a>メンバー
  
### <a name="httpresponse"></a>HttpResponse
HTTP 要求を送信します。

パラメーター:  
* **要求**: HTTP 要求 


* **コンテキスト**: HTTP 要求となった、API に渡された同じ不透明なクライアント コンテキスト



  
**戻り値**: HTTP 応答