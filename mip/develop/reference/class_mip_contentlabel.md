---
title: class mip::ContentLabel
description: 'Microsoft Information Protection (MIP) SDK の mip:: contentlabel クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 27f8adba3e65647a3804256e0b429e1457003085
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884400"
---
# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
特定の適用されたラベル インスタンスに対するプロパティも保持します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: chrono:: time_point\<std:: chrono:: system_clock\> get time () const  |  ラベルの作成時間を取得します。
public AssignmentMethod GetAssignmentMethod() const  |  ラベルの割り当て方法を取得します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetExtendedProperties() const  |  拡張プロパティを取得します。
public bool IsProtectionAppliedFromLabel() const  |  保護がラベルによって適用されたかどうかを取得します。
public std:: shared_ptr\<ラベル\> getlabel () const  |  コンテンツに適用された実際のラベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getcreationtime-function"></a>Getて Time 関数
ラベルの作成時間を取得します。

  
次の**値を返し**ます。作成時刻。
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod 関数
ラベルの割り当て方法を取得します。

  
次の**値を返し**ます。AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
**関連**項目: [mip::](mip-enums-and-structs.md#assignmentmethod-enum)を実行するメソッド
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties 関数
拡張プロパティを取得します。

  
次の**値を返し**ます。拡張プロパティ。
  
### <a name="isprotectionappliedfromlabel-function"></a>Isprotection/Edfromlabel 関数
保護がラベルによって適用されたかどうかを取得します。

  
次の**値を返し**ます。テンプレート保護がある場合は True、それ以外の場合は false。
  
### <a name="getlabel-function"></a>GetLabel 関数
コンテンツに適用された実際のラベル オブジェクトを取得します。

  
次の**値を返し**ます。コンテンツに適用されるラベルオブジェクト。 
  
**関連項目**: [mip::Label](class_mip_label.md)