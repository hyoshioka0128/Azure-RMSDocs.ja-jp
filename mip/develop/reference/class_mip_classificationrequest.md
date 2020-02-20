---
title: 'クラス mip:: ClassificationRequest'
description: 'Microsoft Information Protection (MIP) SDK の mip:: classificationrequest クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 27c6e01eea2dae3735ce5cc3e5cd618b6223d2eb
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489029"
---
# <a name="class-mipclassificationrequest"></a>クラス mip:: ClassificationRequest 
実行状態に対する分類呼び出しの要求を含むクラス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public std::string GetClassificationId() const  |  分類ポリシーの ID を取得します。
public std::string GetRulePackageId() const  |  ルールパッケージの ID を取得します。
  
## <a name="members"></a>Members
  
### <a name="getclassificationid-function"></a>GetClassificationId 関数
分類ポリシーの ID を取得します。

  
**戻り値**: 分類ポリシーの ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 関数
ルールパッケージの ID を取得します。

  
**戻り値**: 規則パッケージの ID。 事前構築済みの分類は空の guid に設定されます。