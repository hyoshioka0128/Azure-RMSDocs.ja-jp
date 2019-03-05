---
title: class mip::ApplyLabelAction
description: Mip::applylabelaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ad1367480497ede6c8efd33d6ebc60c4c6ca34c5
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332230"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  必要なラベル ID を取得します。
public const std::vector\<std::string\>& GetClassificationIds() const  |  一致し、このラベルを表示するが発生した分類 Id を取得します。
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabelid-function"></a>GetLabelId 関数
必要なラベル ID を取得します。

  
**返します**:ラベル ID
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルを表示するが発生した分類 Id を取得します。

  
**返します**:Const std::vector < std::string > & 分類ラベルを表示するを原因となった Id の一覧。
  
### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。
