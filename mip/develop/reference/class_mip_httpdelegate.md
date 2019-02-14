---
title: class mip::HttpDelegate
description: Mip::httpdelegate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 8dd81508766c65d6232c278d56f3720a98aaa9eb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256296"
---
# <a name="class-miphttpdelegate"></a>class mip::HttpDelegate 
HTTP の処理をオーバーライドするインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<HttpResponse\>送信 (const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& コンテキスト)  |  HTTP 要求を送信します。
public void SendAsync (const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& コンテキストには、const std::function\<void(std::shared_ptr\<HttpResponse\>)\>& fnCallback)  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="send-function"></a>Send 関数
HTTP 要求を送信します。

パラメーター:  
* **要求**:HTTP 要求 


* **コンテキスト**:この HTTP 要求が発生する API に渡された同じ不透明なクライアント コンテキスト



  
**返します**:HTTP 応答
  
### <a name="sendasync-function"></a>SendAsync 関数
_まだ文書化されていません。_
