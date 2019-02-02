---
title: class mip::HttpResponse
description: Mip::httpresponse クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 9cbd899548be15833456a7c1e1fe34c3b5629717
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650294"
---
# <a name="class-miphttpresponse"></a>class mip::HttpResponse 
[HttpDelegate](class_mip_httpdelegate.md) をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public int32_t GetStatusCode() const  |  応答の状態コードを取得します。
public const std::string& GetBody() const  |  要求本文を取得します。
public const std::map\<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders() const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getstatuscode-function"></a>GetStatusCode 関数
応答の状態コードを取得します。

  
**返します**:状態コード
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
**返します**:要求本文
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
**返します**:要求ヘッダー