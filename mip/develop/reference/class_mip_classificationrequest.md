---
title: ClassificationRequest クラス
description: 'Microsoft Information Protection (MIP) SDK の classificationrequest:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2e509950bad2d219843c2d45ebd3922a19bef7f4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569238"
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