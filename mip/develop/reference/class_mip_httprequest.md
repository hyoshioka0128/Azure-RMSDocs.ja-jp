---
title: class mip::HttpRequest
description: 'Microsoft Information Protection (MIP) SDK の mip:: httprequest クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 28584ffa19c2ceb00f4ab3839f945adf737bdb3b
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885571"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  要求 ID を取得します。
public HttpRequestType GetRequestType() const  |  要求の種類を取得します。
public const std::string& GetUrl() const  |  要求 URL を取得します。
public const std:: vector\<uint8_t\>& getbody () const  |  要求本文を取得します。
public const std:: map\<std:: string、std:: string、CaseInsensitiveComparator\>& GetHeaders () const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
要求 ID を取得します。

  
次の**値を返し**ます。要求 ID 対応する Httpresponse.cache は同じ ID を持ちます
  
### <a name="getrequesttype-function"></a>GetRequestType 関数
要求の種類を取得します。

  
次の**値を返し**ます。要求の種類
  
### <a name="geturl-function"></a>GetUrl 関数
要求 URL を取得します。

  
次の**値を返し**ます。要求 url
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
次の**値を返し**ます。要求本文
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
次の**値を返し**ます。要求ヘッダー