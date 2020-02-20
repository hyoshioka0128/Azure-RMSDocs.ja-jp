---
title: class mip::RemoveWatermarkAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: removewatermarkaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c2e6eb141d213a9ca19a345a4dac68120200abf8
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489488"
---
# <a name="class-mipremovewatermarkaction"></a>class mip::RemoveWatermarkAction 
ドキュメントからのウォーターマークの削除を指定するアクション クラス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: string\>& GetUIElementNames ()  |  削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。
public ActionType GetType() const  |  アクションの種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementnames-function"></a>GetUIElementNames 関数
削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。

  
**戻り値**: UI 要素名の一覧。
  
### <a name="gettype-function"></a>GetType 関数
アクションの種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。