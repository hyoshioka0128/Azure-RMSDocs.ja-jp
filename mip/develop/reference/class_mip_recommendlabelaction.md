---
title: class mip::RecommendLabelAction
description: Mip::recommendlabelaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: eeab9022b257ff327e2c83b1d8860662355180e5
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173244"
---
# <a name="class-miprecommendlabelaction"></a>class mip::RecommendLabelAction 
このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  提案されたラベル ID を取得します。
public const std::vector\<std::string\>& GetClassificationIds() const  |  一致し、このラベルを表示するが発生した分類 Id を取得します。
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。

## <a name="members"></a>メンバー
  
### <a name="getlabelid-function"></a>GetLabelId 関数
提案されたラベル ID を取得します。

  
**返します**:ラベル ID
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルを表示するが発生した分類 Id を取得します。

  
**返します**:Const std::vector < std::string > & 分類ラベルを表示するを原因となった Id の一覧。

### <a name="gettype-function"></a>GetType 関数    
[アクション](class_mip_action.md)の種類を取得します。  

**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。