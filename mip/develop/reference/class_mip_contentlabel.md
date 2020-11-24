---
title: クラス ContentLabel
description: 'Microsoft Information Protection (MIP) SDK の contentlabel:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a60244b9db9b3087dde71cbdbcf63ba170cb06c3
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569183"
---
# <a name="class-contentlabel"></a>クラス ContentLabel 
コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
特定の適用されたラベル インスタンスに対するプロパティも保持します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: chrono:: time_point \<std::chrono::system_clock\> get time () const  |  ラベルの作成時間を取得します。
public AssignmentMethod GetAssignmentMethod() const  |  ラベルの割り当て方法を取得します。
public const std:: vector \<MetadataEntry\>& getextendedproperties () const  |  拡張プロパティを取得します。
public bool IsProtectionAppliedFromLabel() const  |  保護がラベルによって適用されたかどうかを取得します。
public std::shared_ptr\<Label\> GetLabel() const  |  コンテンツに適用された実際のラベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getcreationtime-function"></a>Getて Time 関数
ラベルの作成時間を取得します。

  
は、作成時刻 **を返し** ます。
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod 関数
ラベルの割り当て方法を取得します。

  
**戻り値**: AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
**関連項目**: mip::AssignmentMethod
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties 関数
拡張プロパティを取得します。

  
**戻り値**: 拡張プロパティ。
  
### <a name="isprotectionappliedfromlabel-function"></a>Isprotection/Edfromlabel 関数
保護がラベルによって適用されたかどうかを取得します。

  
**戻り値**: テンプレートの保護があり、このラベルによるものの場合は true、それ以外の場合は false。
  
### <a name="getlabel-function"></a>GetLabel 関数
コンテンツに適用された実際のラベル オブジェクトを取得します。

  
**戻り値**: コンテンツに適用されたラベル オブジェクト。 
  
**関連** 項目: mip:: Label