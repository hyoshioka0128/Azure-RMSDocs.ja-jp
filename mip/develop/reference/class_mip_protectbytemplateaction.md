---
title: class mip ProtectByTemplateAction
description: class mip ProtectByTemplateAction のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: cb5f42b25e6f499bc09f3f460ec4a253627b45a5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445463"
---
# <a name="class-mipprotectbytemplateaction"></a>class mip::ProtectByTemplateAction 
テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetTemplateId() const  |  アクションに関連付けられている保護テンプレート ID を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="gettemplateid"></a>GetTemplateId
アクションに関連付けられている保護テンプレート ID を取得します。

  
**戻り値**: 保護テンプレート ID。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。