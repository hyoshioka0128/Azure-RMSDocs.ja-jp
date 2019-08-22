---
title: class mip::ClassificationResult
description: 'Microsoft Information Protection (MIP) SDK の mip:: classificationresult クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 83856362e0d0a347f660cb60a64a82e24062c247
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885855"
---
# <a name="class-mipclassificationresult"></a>class mip::ClassificationResult 
実行状態での分類呼び出しの結果を含むクラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  分類ポリシーの ID を取得します。
public int GetCount() const  |  インスタンス数を取得します。
public int GetConfidenceLevel() const  |  結果の信頼度を取得します。
public std:: string GetSensitiveInformationDetections () const  |  機密情報の検出を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
分類ポリシーの ID を取得します。

  
次の**値を返し**ます。分類ポリシーの ID。
  
### <a name="getcount-function"></a>GetCount 関数
インスタンス数を取得します。

  
次の**値を返し**ます。インスタンス数。
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel 関数
結果の信頼度を取得します。
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections 関数
機密情報の検出を取得します。

  
次の**値を返し**ます。すべての機密情報の検出の Json 文字列。