---
title: 'クラス mip:: ClassificationRequest'
description: 'Microsoft Information Protection (MIP) SDK の mip:: classificationrequest クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 1966123c8a0975ea42aa119883cabd47db594bc4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884487"
---
# <a name="class-mipclassificationrequest"></a>クラス mip:: ClassificationRequest 
実行状態に対する分類呼び出しの要求を含むクラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetClassificationId() const  |  分類ポリシーの ID を取得します。
public std::string GetRulePackageId() const  |  ルールパッケージの ID を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getclassificationid-function"></a>GetClassificationId 関数
分類ポリシーの ID を取得します。

  
次の**値を返し**ます。分類ポリシーの ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 関数
ルールパッケージの ID を取得します。

  
次の**値を返し**ます。規則パッケージの ID。 事前構築済みの分類は空の guid に設定されます。