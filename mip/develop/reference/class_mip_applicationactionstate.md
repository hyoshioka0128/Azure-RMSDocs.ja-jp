---
title: 'クラス mip:: ApplicationActionState'
description: 'Microsoft Information Protection (MIP) SDK の mip:: applicationactionstate クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: a75ade6fcbb87e24b778b4368eb65080e767c130
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055515"
---
# <a name="class-mipapplicationactionstate"></a>クラス mip:: ApplicationActionState 
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック LabelState GetNewLabelState () const  |  新しいラベルの状態を取得します。
public std:: shared_ptr\<ラベル\> getnewlabel () const  |  ドキュメントに適用される必要のある機密ラベル ID を取得します。
public std::p air\<bool, std:: string\> IsDowngradeJustified () const  |  実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  新しいラベルの割り当て方法を取得します。
public virtual std::vector\<std::pair\<std::string, std::string\>\> GetNewLabelExtendedProperties() const  |  新しいラベルの拡張プロパティを返します。
public ActionType GetSupportedActions() const  |  サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。
public bool IsRecommendationEnabled () const  |  推奨アクションを表すブール値を取得します。 既定では、ユーザーが else を指定しない限り、true になります。
  
## <a name="members"></a>メンバー
  
### <a name="getnewlabelstate-function"></a>GetNewLabelState 関数
新しいラベルの状態を取得します。

  
次の**値を返し**ます。新しいラベルの状態。 
  
**関連**項目: mip:: labelstate
  
### <a name="getnewlabel-function"></a>GetNewLabel 関数
ドキュメントに適用される必要のある機密ラベル ID を取得します。

  
次の**値を返し**ます。コンテンツに適用される機密ラベル ID が存在する場合は、それ以外の場合は空。ラベルを削除する場合は空。
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified 関数
実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。

  
次の**値を返し**ます。Justifiedalong を使用してダウングレードを行う場合は True、それ以外の場合は false 
  
**関連項目**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>Getnewlabelのメソッド関数
新しいラベルの割り当て方法を取得します。

  
次の**値を返し**ます。割り当て方法標準、PRIVILEGED、AUTO。 
  
**関連**項目: [mip::](mip-enums-and-structs.md#assignmentmethod-enum)を実行するメソッド
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties 関数
新しいラベルの拡張プロパティを返します。

  
次の**値を返し**ます。コンテンツに適用される拡張プロパティ。
  
### <a name="getsupportedactions-function"></a>GetSupportedActions 関数
サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。

  
次の**値を返し**ます。サポートされているすべてのアクションの種類を記述するマスクされた列挙型。
ActionType::Justify must be supported. ポリシーとラベルの変更に理由が必要な場合、常に理由アクションが返されます。
  
### <a name="isrecommendationenabled-function"></a>IsRecommendationEnabled 関数
推奨アクションを表すブール値を取得します。 既定では、ユーザーが else を指定しない限り、true になります。

  
次の**値を返し**ます。推奨アクションを表すブール値が返されます。
このフィールドが影響を受けるには、ActionType:: RecommendLabel を有効にする必要があります。