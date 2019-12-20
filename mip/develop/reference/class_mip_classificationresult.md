---
title: class mip::ClassificationResult
description: 'Microsoft Information Protection (MIP) SDK の mip:: classificationresult クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6f4b1147ef6831ca622d095c0cada67b9f0cf023
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73559392"
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

  
は、すべての機密情報の検出の Json 文字列**を返し**ます。