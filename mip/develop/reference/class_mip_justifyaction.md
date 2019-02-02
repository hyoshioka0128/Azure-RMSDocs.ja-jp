---
title: class mip::JustifyAction
description: Mip::justifyaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: e52a38f8ca25ecb8cc8ae470cb77164abb2b6ec8
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650688"
---
# <a name="class-mipjustifyaction"></a>class mip::JustifyAction 
正当化[アクション](class_mip_action.md)は、ラベルをダウングレードする理由の提供と実行状態での応答の設定を要求します。
  
**関連項目**: [mip::ExecutionState::IsDowngradeJustified](class_mip_executionstate.md#isdowngradejustified-function)
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。