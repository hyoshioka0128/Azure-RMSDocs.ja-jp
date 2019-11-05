---
title: class mip::HttpRequest
description: 'Microsoft Information Protection (MIP) SDK の mip:: httprequest クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: bfe55f09caaa20687750b055e10828f8cc6df2bd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560169"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  要求 ID を取得します。
public HttpRequestType GetRequestType() const  |  要求の種類を取得します。
public const std::string& GetUrl() const  |  要求 URL を取得します。
public const std:: vector\<uint8_t\>& GetBody () const  |  要求本文を取得します。
public const std:: map\<std:: string、std:: string、CaseInsensitiveComparator\>& GetHeaders () const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
要求 ID を取得します。

  
**戻り値**: 要求 id 対応する httpresponse.cache は同じ id を持つ
  
### <a name="getrequesttype-function"></a>GetRequestType 関数
要求の種類を取得します。

  
**戻り値**: 要求の種類
  
### <a name="geturl-function"></a>GetUrl 関数
要求 URL を取得します。

  
**返します**: 要求 URL
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
**戻り値**: 要求本文
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
**戻り値**: 要求ヘッダー