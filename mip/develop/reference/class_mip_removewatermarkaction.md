---
title: RemoveWatermarkAction クラス
description: 'Microsoft Information Protection (MIP) SDK の removewatermarkaction:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: eee2617a7f3c1225d789a5d1f6124caa3d3deec0
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569495"
---
# <a name="class-removewatermarkaction"></a>RemoveWatermarkAction クラス 
ドキュメントからのウォーターマークの削除を指定するアクション クラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector \<std::string\>& GetUIElementNames ()  |  削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。
public ActionType GetType() const  |  アクションの種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementnames-function"></a>GetUIElementNames 関数
削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。

  
**戻り値**: UI 要素名の一覧。
  
### <a name="gettype-function"></a>GetType 関数
アクションの種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。