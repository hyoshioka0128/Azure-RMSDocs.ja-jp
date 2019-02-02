---
title: mip::ClassificationRequest をクラスします。
description: Mip::classificationrequest クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: a7350961af4c2e5d63211840382ee7a0b701f1c4
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652032"
---
# <a name="class-mipclassificationrequest"></a>mip::ClassificationRequest をクラスします。 
実行状態の分類の呼び出しの要求を含むクラスです。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
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