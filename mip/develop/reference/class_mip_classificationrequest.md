---
title: 'クラス mip:: ClassificationRequest'
description: 'Microsoft Information Protection (MIP) SDK の mip:: classificationrequest クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 62b600a377d195c693c94dff7a0472305b53b3f2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74840311"
---
# <a name="class-mipclassificationrequest"></a>クラス mip:: ClassificationRequest 
実行状態に対する分類呼び出しの要求を含むクラス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetClassificationId() const  |  分類ポリシーの ID を取得します。
public std::string GetRulePackageId() const  |  ルールパッケージの ID を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getclassificationid-function"></a>GetClassificationId 関数
分類ポリシーの ID を取得します。

  
**戻り値**: 分類ポリシーの ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 関数
ルールパッケージの ID を取得します。

  
**戻り値**: 規則パッケージの ID。 事前構築済みの分類は空の guid に設定されます。