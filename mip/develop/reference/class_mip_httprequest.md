---
title: クラス HttpRequest
description: 'Microsoft Information Protection (MIP) SDK の httprequest:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: af302a760ee6b8f24b077b2c45bfe86ab0a80dac
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762712"
---
# <a name="class-httprequest"></a>クラス HttpRequest 
1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  要求 ID を取得します。
public HttpRequestType GetRequestType() const  |  要求の種類を取得します。
public const std::string& GetUrl() const  |  要求 URL を取得します。
public const std:: vector\<Uint8_t\>& getbody () const  |  要求本文を取得します。
public const std:: map\<std:: string、std:: String、CaseInsensitiveComparator\>& GetHeaders () const  |  要求ヘッダーを取得します。
  
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