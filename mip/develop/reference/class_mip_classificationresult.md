---
title: class mip::ClassificationResult
description: Mip::classificationresult クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 28b174fe65de5980fb1922cfb4c3e5cee7cab1d8
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650750"
---
# <a name="class-mipclassificationresult"></a>class mip::ClassificationResult 
実行状態での分類呼び出しの結果を含むクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  分類ポリシーの ID を取得します。
public int GetCount() const  |  インスタンス数を取得します。
public int GetConfidenceLevel() const  |  結果の信頼度を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
分類ポリシーの ID を取得します。

  
**返します**:分類ポリシーの ID。
  
### <a name="getcount-function"></a>GetCount 関数
インスタンス数を取得します。

  
**返します**:インスタンスの数。
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel 関数
結果の信頼度を取得します。