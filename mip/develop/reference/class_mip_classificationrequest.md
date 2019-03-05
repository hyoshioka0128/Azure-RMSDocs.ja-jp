---
title: mip::ClassificationRequest をクラスします。
description: Mip::classificationrequest クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 61846ef3b8273169e9cf38eaa173eac3ba18dae6
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330522"
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
