---
title: class mip::ClassificationResult
description: 'Microsoft Information Protection (MIP) SDK の mip:: classificationresult クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a245cd4d9505de8adbf3cc1a2de6d2fa20369ce7
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490406"
---
# <a name="class-mipclassificationresult"></a>class mip::ClassificationResult 
実行状態での分類呼び出しの結果を含むクラス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  分類ポリシーの ID を取得します。
public std::string GetName() const  |  分類ポリシーの名前を取得します。
public int GetCount() const  |  インスタンス数を取得します。
public int GetConfidenceLevel() const  |  結果の信頼度を取得します。
public std:: string GetSensitiveInformationDetections () const  |  機密情報の検出を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
分類ポリシーの ID を取得します。

  
**戻り値**: 分類ポリシーの ID。
  
### <a name="getname-function"></a>GetName 関数
分類ポリシーの名前を取得します。

  
**戻り値**: 分類ポリシーの名前。
  
### <a name="getcount-function"></a>GetCount 関数
インスタンス数を取得します。

  
**戻り値**: インスタンス数。
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel 関数
結果の信頼度を取得します。
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections 関数
機密情報の検出を取得します。

  
は、すべての機密情報の検出の Json 文字列**を返し**ます。 空でない場合は、有効な json 形式である必要があります。