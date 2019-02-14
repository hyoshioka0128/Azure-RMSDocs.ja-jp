---
title: class mip::ProtectByTemplateAction
description: Mip::protectbytemplateaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 9c7114bcceceef537675ca04499cdb1710456b82
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252369"
---
# <a name="class-mipprotectbytemplateaction"></a>class mip::ProtectByTemplateAction 
テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetTemplateId() const  |  アクションに関連付けられている保護テンプレート ID を取得します。
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="gettemplateid-function"></a>GetTemplateId 関数
アクションに関連付けられている保護テンプレート ID を取得します。

  
**返します**:保護テンプレート ID
  
### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。
