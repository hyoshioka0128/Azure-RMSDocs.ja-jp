---
title: class mip HttpResponse
description: class mip HttpResponse のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a19ea78b048cafe94501d452bb9c7409237f6ffd
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445358"
---
# <a name="class-miphttpresponse"></a>class mip::HttpResponse 
[HttpDelegate](class_mip_httpdelegate.md) をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public int32_t GetStatusCode() const  |  応答の状態コードを取得します。
 public const std::string& GetBody() const  |  要求本文を取得します。
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getstatuscode"></a>GetStatusCode
応答の状態コードを取得します。

  
**戻り値**: 状態コード
  
### <a name="getbody"></a>GetBody
要求本文を取得します。

  
**戻り値**: 要求本文
  
### <a name="getheaders"></a>GetHeaders
要求ヘッダーを取得します。

  
**戻り値**: 要求ヘッダー