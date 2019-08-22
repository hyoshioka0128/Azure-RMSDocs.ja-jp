---
title: class mip::HttpResponse
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpresponse.cache クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 4d7711f755f4ffde923eb7d913abdb5bd2a905db
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884126"
---
# <a name="class-miphttpresponse"></a>class mip::HttpResponse 
[HttpDelegate](class_mip_httpdelegate.md) をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  応答 ID を取得します。
public int32_t GetStatusCode() const  |  応答の状態コードを取得します。
public const std:: vector\<uint8_t\>& getbody () const  |  要求本文を取得します。
public const std:: map\<std:: string、std:: string、CaseInsensitiveComparator\>& GetHeaders () const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
応答 ID を取得します。

  
次の**値を返し**ます。対応する HttpRequest が同じ ID を持つ応答 ID
  
### <a name="getstatuscode-function"></a>GetStatusCode 関数
応答の状態コードを取得します。

  
次の**値を返し**ます。状態コード
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
次の**値を返し**ます。要求本文
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
次の**値を返し**ます。要求ヘッダー