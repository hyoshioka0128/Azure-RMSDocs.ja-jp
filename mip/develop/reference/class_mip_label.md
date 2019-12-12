---
title: class mip::Label
description: 'Microsoft Information Protection (MIP) SDK の mip:: label クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 5bdc88746a8921f306d9d52dbe75f3c2b826a5b6
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560138"
---
# <a name="class-miplabel"></a>class mip::Label 
単一の Microsoft Information Protection ラベルの抽象化。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  ラベル ID を取得します。
public const std::string& GetName() const  |  ラベル名を取得します。
public const std::string& GetDescription() const  |  ラベルの説明を取得します。
public const std::string& GetColor() const  |  ラベルの表示色を取得します。
public int GetSensitivity() const  |  ラベルの秘密度を取得します。
public const std::string& GetTooltip() const  |  ラベルのヒントの説明を取得します。
public const std:: string & GetAutoTooltip () const  |  このラベルが適用される分類のツールヒントの説明を取得します。
public bool IsActive() const  |  ラベルがアクティブかどうかを示すブール値を取得します。
public std:: weak_ptr\<Label\> GetParent () const  |  親ラベルを取得します。
public const std:: vector\<std:: shared_ptr\<Label\>\>& GetChildren () const  |  現在のラベルの子ラベルを取得します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  ラベルのカスタム設定を取得します。
public ActionSource GetActionSource() const  |  ラベルのアクションソースを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
ラベル ID を取得します。

  
**戻り値**: ラベル ID。
  
### <a name="getname-function"></a>GetName 関数
ラベル名を取得します。

  
**戻り値**: ラベル名。
  
### <a name="getdescription-function"></a>GetDescription 関数
ラベルの説明を取得します。

  
**戻り値**: ラベルの説明。
  
### <a name="getcolor-function"></a>GetColor 関数
ラベルの表示色を取得します。

  
**戻り値**: 文字列形式での色の値。 "#RRGGBB" で、RR、GG、BB は 16 進数の 0 ～ f です。
  
### <a name="getsensitivity-function"></a>GetSensitivity 関数
ラベルの秘密度を取得します。

  
**戻り値**: 数値。 大きい値は高い秘密度を意味します。
  
### <a name="gettooltip-function"></a>GetTooltip 関数
ラベルのヒントの説明を取得します。

  
**戻り値**: ヒントの文字列。
  
### <a name="getautotooltip-function"></a>GetAutoTooltip 関数
このラベルが適用される分類のツールヒントの説明を取得します。

  
**戻り値**: ヒントの文字列。
  
### <a name="isactive-function"></a>IsActive 関数
ラベルがアクティブかどうかを示すブール値を取得します。
アクティブなラベルのみを適用できます。 非アクティブなラベルは適用できず、表示目的でのみ使用されます。 

  
**戻り値**: ラベルがアクティブな場合は true、それ以外の場合は false。
  
### <a name="getparent-function"></a>GetParent 関数
親ラベルを取得します。

  
**戻り値**: 親ラベルが存在する場合は親ラベルへの弱いポインター、存在しない場合は空のポインターです。
  
### <a name="getchildren-function"></a>GetChildren 関数
現在のラベルの子ラベルを取得します。

  
**戻り値**: ラベルへの共有ポインターのベクター。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
ラベルのカスタム設定を取得します。

  
**戻り**値: カスタム設定を表すキーと値のペアのベクター。
  
### <a name="getactionsource-function"></a>GetActionSource 関数
ラベルのアクションソースを取得します。

  
**戻り値**: アクションソース