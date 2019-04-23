---
title: class mip::ContentLabel
description: Mip::contentlabel クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 96f8cca48f385a21685e93eb5bc57abac571975c
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184775"
---
# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
特定の適用されたラベル インスタンスに対するプロパティも保持します。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::chrono::time_point\<std::chrono::system_clock\> GetCreationTime() const  |  ラベルの作成時間を取得します。
public AssignmentMethod GetAssignmentMethod() const  |  ラベルの割り当て方法を取得します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetExtendedProperties() const  |  拡張プロパティを取得します。
public bool IsProtectionAppliedFromLabel() const  |  保護がラベルによって適用されたかどうかを取得します。
public std::shared_ptr\<ラベル\>GetLabel() 定数  |  コンテンツに適用された実際のラベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getcreationtime-function"></a>GetCreationTime 関数
ラベルの作成時間を取得します。

  
**返します**:作成時間。
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod 関数
ラベルの割り当て方法を取得します。

  
**返します**:AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
**参照してください**: [:assignmentmethod](mip-enums-and-structs.md#assignmentmethod)
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties 関数
拡張プロパティを取得します。

  
**返します**:拡張プロパティ。
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel 関数
保護がラベルによって適用されたかどうかを取得します。

  
**返します**:True の場合、テンプレート保護があるし、してこのラベルは、それ以外の場合は false。
  
### <a name="getlabel-function"></a>GetLabel 関数
コンテンツに適用された実際のラベル オブジェクトを取得します。

  
**返します**:コンテンツに適用されたラベル オブジェクト。 
  
**関連項目**: [mip::Label](class_mip_label.md)