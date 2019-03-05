---
title: class mip::RemoveWatermarkAction
description: Mip::removewatermarkaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 99993007fb80fdc0cb714f2769c36bd1cef63059
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332876"
---
# <a name="class-mipremovewatermarkaction"></a>class mip::RemoveWatermarkAction 
ドキュメントからのウォーターマークの削除を指定するアクション クラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
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
