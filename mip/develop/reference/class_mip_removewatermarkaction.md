---
title: class mip::RemoveWatermarkAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: removewatermarkaction クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: c456c48e4f41500422c0350dbffca7492abca451
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057131"
---
# <a name="class-mipremovewatermarkaction"></a>class mip::RemoveWatermarkAction 
ドキュメントからのウォーターマークの削除を指定するアクション クラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: string\>& GetUIElementNames ()  |  削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementnames-function"></a>GetUIElementNames 関数
削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。

  
次の**値を返し**ます。Ui 要素名の一覧。
  
### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
次の**値を返し**ます。ActionType: この基底クラスをキャストできる派生アクションの種類。