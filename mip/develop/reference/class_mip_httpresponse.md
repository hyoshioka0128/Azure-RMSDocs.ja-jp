---
title: class mip::HttpResponse
description: Mip::httpresponse クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 06bc3f52bdecd85412dc0c35df46c7847167aa1b
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573762"
---
# <a name="class-miphttpresponse"></a>class mip::HttpResponse 
[HttpDelegate](class_mip_httpdelegate.md) をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  応答 ID を取得します
public int32_t GetStatusCode() const  |  応答の状態コードを取得します。
public const std::vector\<uint8_t\>& GetBody() const  |  要求本文を取得します。
public const std::map\<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders() const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
応答 ID を取得します

  
**返します**:応答 ID、対応する[HttpRequest](class_mip_httprequest.md)同じ ID が必要がありました
  
### <a name="getstatuscode-function"></a>GetStatusCode 関数
応答の状態コードを取得します。

  
**返します**:状態コード
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
**返します**:[要求本文]
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
**返します**:要求ヘッダー