---
title: クラス ApplicationActionState
description: 'Microsoft Information Protection (MIP) SDK の applicationactionstate:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 936f64f24211f000dc26153f17bd094f4d7d3c8d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569310"
---
# <a name="class-applicationactionstate"></a>クラス ApplicationActionState 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック LabelState GetNewLabelState () const  |  新しいラベルの状態を取得します。
public std:: shared_ptr \<Label\> getnewlabel () const  |  ドキュメントに適用される必要のある機密ラベル ID を取得します。
public std::p air \<bool, std::string\> IsDowngradeJustified () const  |  実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  新しいラベルの割り当て方法を取得します。
パブリック仮想 std:: vector \<std::pair\<std::string, std::string\> \> getnewlabelextendedproperties () const  |  新しいラベルの拡張プロパティを返します。
public ActionType GetSupportedActions() const  |  サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。
public bool IsRecommendationEnabled () const  |  推奨アクションを表すブール値を取得します。 既定では、ユーザーが else を指定しない限り、true になります。
  
## <a name="members"></a>メンバー
  
### <a name="getnewlabelstate-function"></a>GetNewLabelState 関数
新しいラベルの状態を取得します。

  
**戻り値**: 新しいラベルの状態。 
  
**関連** 項目: mip:: labelstate
  
### <a name="getnewlabel-function"></a>GetNewLabel 関数
ドキュメントに適用される必要のある機密ラベル ID を取得します。

  
**戻り値**: コンテンツに適用される機密ラベル ID が存在する場合はその ID、それ以外でラベルを削除する場合は空。
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified 関数
実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。

  
**戻り値**: ダウングレードの正当性が理由メッセージと共に示される場合は true、それ以外の場合は false。 
  
**関連** 項目: mip:: ジャスト Ifyaction
  
### <a name="getnewlabelassignmentmethod-function"></a>Getnewlabelのメソッド関数
新しいラベルの割り当て方法を取得します。

  
**戻り値**: 割り当て方法: STANDARD、PRIVILEGED、AUTO。 
  
**関連項目**: mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties 関数
新しいラベルの拡張プロパティを返します。

  
**戻り値**: コンテンツに適用される拡張プロパティ。
  
### <a name="getsupportedactions-function"></a>GetSupportedActions 関数
サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。

  
**戻り値**: サポートされているすべてのアクションの種類を表すマスクされた列挙型。
ActionType::Justify must be supported. ポリシーとラベルの変更に理由が必要な場合、常に理由アクションが返されます。
  
### <a name="isrecommendationenabled-function"></a>IsRecommendationEnabled 関数
推奨アクションを表すブール値を取得します。 既定では、ユーザーが else を指定しない限り、true になります。

  
**戻り値: 推奨** されるアクションを表すブール値を返します。
このフィールドが影響を受けるには、ActionType:: RecommendLabel を有効にする必要があります。