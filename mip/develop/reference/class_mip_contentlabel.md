---
title: class mip ContentLabel
description: class mip ContentLabel のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c105f620ed2cd3d6f1427f2543784ea66ce2c4d7
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446024"
---
# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
特定の適用されたラベル インスタンスに対するプロパティも保持します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetCreationTime() const  |  ラベルの作成時間を取得します。
 public AssignmentMethod GetAssignmentMethod() const  |  ラベルの割り当て方法を取得します。
public const std::vector<std::pair<std::string, std::string>>& GetExtendedProperties() const  |  拡張プロパティを取得します。
 public bool IsProtectionAppliedFromLabel() const  |  保護がラベルによって適用されたかどうかを取得します。
public std::shared_ptr<Label> GetLabel() const  |  コンテンツに適用された実際のラベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getcreationtime"></a>GetCreationTime
ラベルの作成時間を取得します。

  
**戻り値**: GMT 文字列としての作成時間。
  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
ラベルの割り当て方法を取得します。

  
**戻り値**: AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
**関連項目**: mip::AssignmentMethod
  
### <a name="getextendedproperties"></a>GetExtendedProperties
拡張プロパティを取得します。

  
**戻り値**: 拡張プロパティ。
  
### <a name="isprotectionappliedfromlabel"></a>IsProtectionAppliedFromLabel
保護がラベルによって適用されたかどうかを取得します。

  
**戻り値**: テンプレートの保護があり、このラベルによるものの場合は true、それ以外の場合は false。
  
### <a name="label"></a>Label
コンテンツに適用された実際のラベル オブジェクトを取得します。

  
**戻り値**: コンテンツに適用されたラベル オブジェクト。 
  
**関連項目**: [mip::Label](class_mip_label.md)