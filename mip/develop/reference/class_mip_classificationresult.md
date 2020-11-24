---
title: ClassificationResult クラス
description: 'Microsoft Information Protection (MIP) SDK の classificationresult:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 4e64abc1cca11f11b19238282c9061dc26b29290
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569230"
---
# <a name="class-classificationresult"></a>ClassificationResult クラス 
実行状態での分類呼び出しの結果を含むクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  分類ポリシーの ID を取得します。
public std::string GetName() const  |  分類ポリシーの名前を取得します。
public int GetCount() const  |  インスタンス数を取得します。
public int GetConfidenceLevel() const  |  結果の信頼度を取得します。
public std:: string GetSensitiveInformationDetections () const  |  機密情報の検出を取得します。
public virtual std:: vector \<std::shared_ptr\<mip::DetailedClassificationResult\> \> GetDetailedClassificationAttributes () const  |  Enchanced 分類が有効になっている場合は、特定の検出バンドを取得します。
  
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

  
は、すべての機密情報の検出の Json 文字列 **を返し** ます。 空でない場合は、有効な json 形式である必要があります。
  
### <a name="getdetailedclassificationattributes-function"></a>GetDetailedClassificationAttributes 関数
Enchanced 分類が有効になっている場合は、特定の検出バンドを取得します。

  
**戻り** 値: 異なる信頼しきい値でのインスタンス数のベクター