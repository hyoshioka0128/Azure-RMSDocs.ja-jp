---
title: class mip::RecommendLabelAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: recommendlabelaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: dd3d2d0ecf7b549105e1a6373a998e77d4e77de8
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883208"
---
# <a name="class-miprecommendlabelaction"></a>class mip::RecommendLabelAction 
このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<ラベル\>& getlabel () const  |  推奨されるラベルを取得します。
public const std:: vector\<std:: string\>& GetClassificationIds () const  |  一致し、このラベルが表示される原因となった分類 Id を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
推奨されるラベルを取得します。

  
次の**値を返し**ます。ラベル。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルが表示される原因となった分類 Id を取得します。

  
次の**値を返し**ます。Const std:: vector < std:: string >、このラベルが表示される原因となった分類 Id の一覧を & します。