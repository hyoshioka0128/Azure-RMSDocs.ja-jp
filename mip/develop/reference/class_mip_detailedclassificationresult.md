---
title: DetailedClassificationResult クラス
description: 'Microsoft Information Protection (MIP) SDK の detailedclassificationresult:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d43b75c232d6bfe60f1b7124c66c007d021dd2ee
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567025"
---
# <a name="class-detailedclassificationresult"></a>DetailedClassificationResult クラス 
実行状態での分類呼び出しの結果を含むクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public int GetConfidenceLevel() const  |  結果の信頼度を取得します。
public int GetCount() const  |  インスタンス数を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel 関数
結果の信頼度を取得します。

  
**戻り値**: 0-100 から数えた数値の信頼度。
  
### <a name="getcount-function"></a>GetCount 関数
インスタンス数を取得します。

  
**戻り値**: インスタンス数。