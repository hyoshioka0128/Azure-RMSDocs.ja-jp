---
title: class mip::ApplyLabelAction
description: Mip::applylabelaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 70f226cc112062582b5441f6c3ae7fc3dc7de118
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59572937"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
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