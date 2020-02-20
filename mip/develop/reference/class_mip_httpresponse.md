---
title: class mip::HttpResponse
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpresponse.cache クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e24eef471b11daffadb84235edbc93ff14696c25
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488060"
---
# <a name="class-miphttpresponse"></a>class mip::HttpResponse 
HttpDelegate をオーバーライドするときにクライアントアプリによって実装される、単一の HTTP 応答を記述するインターフェイス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  応答 ID を取得します。
public int32_t GetStatusCode() const  |  応答の状態コードを取得します。
public const std:: vector\<uint8_t\>& GetBody () const  |  要求本文を取得します。
public const std:: map\<std:: string、std:: string、CaseInsensitiveComparator\>& GetHeaders () const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId 関数
応答 ID を取得します。

  
**戻り値**: 対応する HTTPREQUEST の id が同じである応答 id
  
### <a name="getstatuscode-function"></a>GetStatusCode 関数
応答の状態コードを取得します。

  
**戻り値**: 状態コード
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
**戻り値**: 要求本文
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
**戻り値**: 要求ヘッダー