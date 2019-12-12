---
title: 'クラス mip:: HttpOperation'
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpoperation クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6f0c3cc726d72d89a8682907ebc350270db5daee
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558786"
---
# <a name="class-miphttpoperation"></a>クラス mip:: HttpOperation 
HttpDelegate をオーバーライドするときにクライアントアプリによって実装される、単一の HTTP 操作を記述するインターフェイス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  操作 ID を取得します。
public std:: shared_ptr\<Httpresponse.cache\> GetResponse ()  |  応答を取得します (存在する場合)。
public bool IsCancelled ()  |  操作のキャンセルステータスを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
操作 ID を取得します。

  
**戻り値**: 操作 id 対応する HttpRequest と HTTPRESPONSE.CACHE の id は同じになります
  
### <a name="getresponse-function"></a>GetResponse 関数
応答を取得します (存在する場合)。

  
**戻り値**: Response
  
### <a name="iscancelled-function"></a>IsCancelled 関数
操作のキャンセルステータスを取得します。

  
**戻り値**: キャンセル状態