---
title: class mip::ProtectByTemplateAction
description: Mip::protectbytemplateaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7ce74109d555761dde5710c4628faed3b3a2523e
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333468"
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
