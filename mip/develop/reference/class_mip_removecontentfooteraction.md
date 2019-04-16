---
title: class mip::RemoveContentFooterAction
description: Mip::removecontentfooteraction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 14afd4688c13f419ab3019e9c268ba7d355121c8
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574263"
---
# <a name="class-mipremovecontentfooteraction"></a>class mip::RemoveContentFooterAction 
ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::vector\<std::string\>& GetUIElementNames()  |  削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。

## <a name="members"></a>メンバー
  
### <a name="getuielementnames-function"></a>GetUIElementNames 関数
削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。

  
**返します**:Ui 要素名の一覧。

### <a name="gettype-function"></a>GetType 関数    
[アクション](class_mip_action.md)の種類を取得します。  

**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。