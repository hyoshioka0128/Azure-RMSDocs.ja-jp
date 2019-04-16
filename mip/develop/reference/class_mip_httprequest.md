---
title: class mip::HttpRequest
description: Mip::httprequest クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 8b0349db2e985d6fb015e1a2698187089483fbe3
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573073"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  取得要求の id です。
public HttpRequestType GetRequestType() const  |  要求の種類を取得します。
public const std::string& GetUrl() const  |  要求 URL を取得します。
public const std::vector\<uint8_t\>& GetBody() const  |  要求本文を取得します。
public const std::map\<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders() const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
取得要求の id です。

  
**返します**:要求対応 ID [HttpResponse](class_mip_httpresponse.md)同じ ID を持つ
  
### <a name="getrequesttype-function"></a>GetRequestType 関数
要求の種類を取得します。

  
**返します**:要求の種類
  
### <a name="geturl-function"></a>GetUrl 関数
要求 URL を取得します。

  
**返します**:要求 url
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
**返します**:[要求本文]
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
**返します**:要求ヘッダー