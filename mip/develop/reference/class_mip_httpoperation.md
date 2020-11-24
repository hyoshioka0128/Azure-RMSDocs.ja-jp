---
title: HttpOperation クラス
description: 'Microsoft Information Protection (MIP) SDK の httpoperation:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: ece0d76577747170e4328bc1d9bdabb0678e65a5
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566881"
---
# <a name="class-httpoperation"></a>HttpOperation クラス 
HttpDelegate をオーバーライドするときにクライアントアプリによって実装される、単一の HTTP 操作を記述するインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  操作 ID を取得します。
public std:: shared_ptr \<HttpResponse\> GetResponse ()  |  応答を取得します (存在する場合)。
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