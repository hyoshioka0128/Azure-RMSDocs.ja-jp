---
title: mip::ClassificationRequest をクラスします。
description: Mip::classificationrequest クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3fddd870b6aebb9f5209fc43160c32d87b1d7129
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573741"
---
# <a name="class-mipclassificationrequest"></a>mip::ClassificationRequest をクラスします。 
実行状態の分類の呼び出しの要求を含むクラスです。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::string GetClassificationId() const  |  分類ポリシーの ID を取得します。
public std::string GetRulePackageId() const  |  ルールのパッケージの ID を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getclassificationid-function"></a>GetClassificationId 関数
分類ポリシーの ID を取得します。

  
**返します**:分類ポリシーの ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 関数
ルールのパッケージの ID を取得します。

  
**返します**:ルールのパッケージの ID。 事前構築済みの分類は、空の guid に設定されます。