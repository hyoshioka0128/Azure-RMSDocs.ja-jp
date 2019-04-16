---
title: mip::HttpOperation をクラスします。
description: Mip::httpoperation クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: e3eaedbf508f116b19521286b686bc955d108efe
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574484"
---
# <a name="class-miphttpoperation"></a>mip::HttpOperation をクラスします。 
オーバーライドする場合、クライアント アプリケーションによって実装される単一の HTTP 操作を表すインターフェイスを[HttpDelegate](class_mip_httpdelegate.md)します。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  操作 ID を取得します
public std::shared_ptr\<HttpResponse\> GetResponse()  |  存在する場合は、応答を取得します。
public bool IsCancelled()  |  操作のキャンセル状態を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
操作 ID を取得します

  
**返します**:操作 ID が、対応する[HttpRequest](class_mip_httprequest.md)と[HttpResponse](class_mip_httpresponse.md)同じ ID を持つ
  
### <a name="getresponse-function"></a>GetResponse 関数
存在する場合は、応答を取得します。

  
**返します**:応答
  
### <a name="iscancelled-function"></a>IsCancelled 関数
操作のキャンセル状態を取得します。

  
**返します**:取り消しの状態