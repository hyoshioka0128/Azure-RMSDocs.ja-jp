---
title: ClassificationRequest クラス
description: 'Microsoft Information Protection (MIP) SDK の classificationrequest:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 0d4b8d3ed5e12698c0044975516b017d1c9376b0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763545"
---
# <a name="class-classificationrequest"></a>ClassificationRequest クラス 
実行状態に対する分類呼び出しの要求を含むクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: string GetClassificationId () const  |  分類ポリシーの ID を取得します。
public std:: string GetRulePackageId () const  |  ルールパッケージの ID を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getclassificationid-function"></a>GetClassificationId 関数
分類ポリシーの ID を取得します。

  
**戻り値**: 分類ポリシーの ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 関数
ルールパッケージの ID を取得します。

  
**戻り値**: 規則パッケージの ID。 事前構築済みの分類は空の guid に設定されます。