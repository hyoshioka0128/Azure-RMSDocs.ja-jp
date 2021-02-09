---
title: ClassificationResult クラス
description: 'Microsoft Information Protection (MIP) SDK の classificationresult:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: c1f4154bbc12613726aac8f56a322cb6cd4d5a53
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211874"
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