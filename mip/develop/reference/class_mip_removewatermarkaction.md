---
title: RemoveWatermarkAction クラス
description: 'Microsoft Information Protection (MIP) SDK の removewatermarkaction:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 2c140461d0cf8b01b25893900191563b1fe3c8b0
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213166"
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