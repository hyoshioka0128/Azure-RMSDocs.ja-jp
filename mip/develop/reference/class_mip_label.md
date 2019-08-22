---
title: class mip::Label
description: 'Microsoft Information Protection (MIP) SDK の mip:: label クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 3d746c1f271d75c160ca721ebe6f0fef0f15bd5e
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884048"
---
# <a name="class-miplabel"></a>class mip::Label 
単一の Microsoft Information Protection ラベルの抽象化。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  ラベル ID を取得します。
public const std::string& GetName() const  |  ラベル名を取得します。
public const std::string& GetDescription() const  |  ラベルの説明を取得します。
public const std::string& GetColor() const  |  ラベルの表示色を取得します。
public int GetSensitivity() const  |  ラベルの秘密度を取得します。
public const std::string& GetTooltip() const  |  ラベルのヒントの説明を取得します。
public bool IsActive() const  |  ラベルがアクティブかどうかを示すブール値を取得します。
public std:: weak_ptr\<Label\> GetParent () const  |  親ラベルを取得します。
public const std:: vector\<std:: shared_ptr\<ラベル\>\>& getchildren () const  |  現在のラベルの子ラベルを取得します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  ラベルのカスタム設定を取得します。
public ActionSource GetActionSource() const  |  ラベルのアクションソースを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
ラベル ID を取得します。

  
次の**値を返し**ます。ラベル ID。
  
### <a name="getname-function"></a>GetName 関数
ラベル名を取得します。

  
次の**値を返し**ます。ラベル名。
  
### <a name="getdescription-function"></a>GetDescription 関数
ラベルの説明を取得します。

  
次の**値を返し**ます。ラベルの説明。
  
### <a name="getcolor-function"></a>GetColor 関数
ラベルの表示色を取得します。

  
次の**値を返し**ます。色の値文字列の形式。 "#RRGGBB" で、RR、GG、BB は 16 進数の 0 ～ f です。
  
### <a name="getsensitivity-function"></a>GetSensitivity 関数
ラベルの秘密度を取得します。

  
次の**値を返し**ます。数値。 大きい値は高い秘密度を意味します。
  
### <a name="gettooltip-function"></a>GetTooltip 関数
ラベルのヒントの説明を取得します。

  
次の**値を返し**ます。ツールヒント文字列。
  
### <a name="isactive-function"></a>IsActive 関数
ラベルがアクティブかどうかを示すブール値を取得します。
アクティブなラベルのみを適用できます。 非アクティブなラベルは適用できず、表示目的でのみ使用されます。 

  
次の**値を返し**ます。ラベルがアクティブである場合は True、それ以外の場合は false。
  
### <a name="getparent-function"></a>GetParent 関数
親ラベルを取得します。

  
次の**値を返し**ます。親ラベルへの弱いポインターが存在する場合はそれを指す、それ以外の場合は空のポインター。
  
### <a name="getchildren-function"></a>GetChildren 関数
現在のラベルの子ラベルを取得します。

  
次の**値を返し**ます。ラベルへの共有ポインターのベクター。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
ラベルのカスタム設定を取得します。

  
次の**値を返し**ます。カスタム設定を表すキーと値のペアのベクター。
  
### <a name="getactionsource-function"></a>GetActionSource 関数
ラベルのアクションソースを取得します。

  
次の**値を返し**ます。[アクション](class_mip_action.md)のソース