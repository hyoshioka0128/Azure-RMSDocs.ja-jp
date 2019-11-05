---
title: class mip::Action
description: 'Microsoft Information Protection (MIP) SDK の mip:: action クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d3cc1aecfb5ca8bf2d78dd9d6c8c280b5541389d
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560407"
---
# <a name="class-mipaction"></a>class mip::Action 
アクションのインターフェイス。 各アクションは、(ポリシーで定義されているように) アプリケーションがラベルを適用するために実行する必要がある手順に対応します
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public ActionType GetType() const  |  アクションの種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="gettype-function"></a>GetType 関数
アクションの種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。