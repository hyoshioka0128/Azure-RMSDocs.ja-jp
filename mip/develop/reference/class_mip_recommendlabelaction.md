---
title: class mip::RecommendLabelAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: recommendlabelaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 2038c8eb1a6baa52dc696be998853ca6774edccf
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489539"
---
# <a name="class-miprecommendlabelaction"></a>class mip::RecommendLabelAction 
このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<Label\>& GetLabel () const  |  推奨されるラベルを取得します。
public const std:: vector\<std:: string\>& GetClassificationIds () const  |  一致し、このラベルが表示される原因となった分類 Id を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
推奨されるラベルを取得します。

  
は、ラベルを**返し**ます。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルが表示される原因となった分類 Id を取得します。

  
は、Const std:: vector < std:: string > &、このラベルが表示される原因となった分類 Id の一覧を**返し**ます。