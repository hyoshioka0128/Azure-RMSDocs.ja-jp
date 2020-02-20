---
title: 'クラス mip:: HttpOperation'
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpoperation クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 4be7b54dd5df255c488043d84ebcfebbce7e6ac2
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489998"
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