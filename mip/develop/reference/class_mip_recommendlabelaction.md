---
title: class mip::RecommendLabelAction
description: Mip::recommendlabelaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 665a244a858ba9924f27df96ca3b6471cb5fc829
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56260121"
---
# <a name="class-miprecommendlabelaction"></a>class mip::RecommendLabelAction 
このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
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
