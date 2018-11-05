---
title: class mip JustifyAction
description: class mip JustifyAction のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: db61b9c718ae7ddbe1441d379e5a4b6b95d69951
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445293"
---
# <a name="class-mipjustifyaction"></a>class mip::JustifyAction 
正当化[アクション](class_mip_action.md)は、ラベルをダウングレードする理由の提供と実行状態での応答の設定を要求します。
  
**関連項目**: [mip::ExecutionState::IsDowngradeJustified](class_mip_executionstate.md#isdowngradejustified)
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。