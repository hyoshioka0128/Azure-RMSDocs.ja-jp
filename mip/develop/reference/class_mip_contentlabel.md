---
title: class mip::ContentLabel
description: 'Microsoft Information Protection (MIP) SDK の mip:: contentlabel クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a29ea5be05d928f25b9a4255416d93acedcb1c0b
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558924"
---
# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
特定の適用されたラベル インスタンスに対するプロパティも保持します。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: chrono:: time_point\<std:: chrono:: system_clock\> Get Time () const  |  ラベルの作成時間を取得します。
public AssignmentMethod GetAssignmentMethod() const  |  ラベルの割り当て方法を取得します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetExtendedProperties () const  |  拡張プロパティを取得します。
public bool IsProtectionAppliedFromLabel() const  |  保護がラベルによって適用されたかどうかを取得します。
public std:: shared_ptr\<Label\> GetLabel () const  |  コンテンツに適用された実際のラベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getcreationtime-function"></a>Getて Time 関数
ラベルの作成時間を取得します。

  
は、作成時刻**を返し**ます。
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod 関数
ラベルの割り当て方法を取得します。

  
**戻り値**: AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
**関連**項目: [mip::](mip-enums-and-structs.md#assignmentmethod-enum)を実行するメソッド
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties 関数
拡張プロパティを取得します。

  
**戻り値**: 拡張プロパティ。
  
### <a name="isprotectionappliedfromlabel-function"></a>Isprotection/Edfromlabel 関数
保護がラベルによって適用されたかどうかを取得します。

  
**戻り値**: テンプレートの保護があり、このラベルによるものの場合は true、それ以外の場合は false。
  
### <a name="getlabel-function"></a>GetLabel 関数
コンテンツに適用された実際のラベル オブジェクトを取得します。

  
**戻り値**: コンテンツに適用されたラベル オブジェクト。 
  
**関連**項目: mip:: Label