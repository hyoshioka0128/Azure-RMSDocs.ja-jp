---
title: class mip::HttpRequest
description: Mip::httprequest クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 3c23d37836b241a416cbaf5ee5cd22f8c726794d
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650087"
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