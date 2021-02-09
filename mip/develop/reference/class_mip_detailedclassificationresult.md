---
title: DetailedClassificationResult クラス
description: 'Microsoft Information Protection (MIP) SDK の detailedclassificationresult:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 9b1921c046867207d6b1d9a67df46f442fb95977
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211637"
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