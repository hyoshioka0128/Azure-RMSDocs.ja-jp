---
title: class mip HttpRequest
description: class mip HttpRequest のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e838eb247bc00d43da72db1de03304e89a1b1da5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445242"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public HttpRequestType GetRequestType() const  |  要求の種類を取得します。
 public const std::string& GetUrl() const  |  要求 URL を取得します。
 public const std::string& GetBody() const  |  要求本文を取得します。
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="httprequesttype"></a>HttpRequestType
要求の種類を取得します。

  
**戻り値**: 要求の種類
  
### <a name="geturl"></a>GetUrl
要求 URL を取得します。

  
**返します**: 要求 URL
  
### <a name="getbody"></a>GetBody
要求本文を取得します。

  
**戻り値**: 要求本文
  
### <a name="getheaders"></a>GetHeaders
要求ヘッダーを取得します。

  
**戻り値**: 要求ヘッダー