---
title: class mip::HttpRequest
description: 'Microsoft Information Protection (MIP) SDK の mip:: httprequest クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 92cf2bc3840e3cb38210c42c1e1b2d43db1e8bd4
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054824"
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