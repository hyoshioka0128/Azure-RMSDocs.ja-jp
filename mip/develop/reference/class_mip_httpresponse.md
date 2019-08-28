---
title: class mip::HttpResponse
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpresponse.cache クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 3fe574665d6a51c03135cf863fcec9d2106e549d
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056024"
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