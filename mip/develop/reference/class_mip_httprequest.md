---
title: class mip::HttpRequest
description: Mip::httprequest クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6e663d4083d9daa2fc744289708f4c127ffb29c2
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330697"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public HttpRequestType GetRequestType() const  |  要求の種類を取得します。
public const std::string& GetUrl() const  |  要求 URL を取得します。
public const std::string& GetBody() const  |  要求本文を取得します。
public const std::map\<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders() const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getrequesttype-function"></a>GetRequestType 関数
要求の種類を取得します。

  
**返します**:要求の種類
  
### <a name="geturl-function"></a>GetUrl 関数
要求 URL を取得します。

  
**返します**:要求 url
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
**返します**:要求本文
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
**返します**:要求ヘッダー
