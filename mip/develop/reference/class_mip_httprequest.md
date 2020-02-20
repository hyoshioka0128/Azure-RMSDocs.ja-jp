---
title: class mip::HttpRequest
description: 'Microsoft Information Protection (MIP) SDK の mip:: httprequest クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f3b26ad07b8b3bfc556646cfd96a71aa9188bbb0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488094"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  要求 ID を取得します。
public HttpRequestType GetRequestType() const  |  要求の種類を取得します。
public const std::string& GetUrl() const  |  要求 URL を取得します。
public const std:: vector\<uint8_t\>& GetBody () const  |  要求本文を取得します。
public const std:: map\<std:: string、std:: string、CaseInsensitiveComparator\>& GetHeaders () const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>Members
  
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