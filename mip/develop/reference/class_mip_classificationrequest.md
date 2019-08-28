---
title: 'クラス mip:: ClassificationRequest'
description: 'Microsoft Information Protection (MIP) SDK の mip:: classificationrequest クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 39fde4fa5fb0fe6f91545c9cffa36ed976a4b8b1
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055318"
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