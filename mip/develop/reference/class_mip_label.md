---
title: class mip::Label
description: Mip::label クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: aa2d5106f8da03b4cf6a9dbd99c440989dc7ff6d
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650665"
---
# <a name="class-miplabel"></a>class mip::Label 
単一の Microsoft Information Protection ラベルの抽象化。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  ラベル ID を取得します。
public const std::string& GetName() const  |  ラベル名を取得します。
public const std::string& GetDescription() const  |  ラベルの説明を取得します。
public const std::string& GetColor() const  |  ラベルの表示色を取得します。
public int GetSensitivity() const  |  ラベルの秘密度を取得します。
public const std::string& GetTooltip() const  |  ラベルのヒントの説明を取得します。
public bool IsActive() const  |  ラベルがアクティブかどうかを示すブール値を取得します。
public std::weak_ptr\<Label\> GetParent() const  |  親ラベルを取得します。
public const std::vector\<std::shared_ptr\<ラベル\>\>& GetChildren() 定数  |  現在のラベルの子ラベルを取得します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  カスタム ラベルの設定を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
ラベル ID を取得します。

  
**返します**:ラベル ID
  
### <a name="getname-function"></a>GetName 関数
ラベル名を取得します。

  
**返します**:ラベル名。
  
### <a name="getdescription-function"></a>GetDescription 関数
ラベルの説明を取得します。

  
**返します**:ラベルの説明。
  
### <a name="getcolor-function"></a>GetColor 関数
ラベルの表示色を取得します。

  
**返します**:色の値の文字列形式。 "#RRGGBB" で、RR、GG、BB は 16 進数の 0 ～ f です。
  
### <a name="getsensitivity-function"></a>GetSensitivity 関数
ラベルの秘密度を取得します。

  
**返します**:数値。 大きい値は高い秘密度を意味します。
  
### <a name="gettooltip-function"></a>GetTooltip 関数
ラベルのヒントの説明を取得します。

  
**返します**:ヒントの文字列。
  
### <a name="isactive-function"></a>IsActive 関数
ラベルがアクティブかどうかを示すブール値を取得します。
アクティブなラベルのみを適用できます。 非アクティブなラベルは適用できず、表示目的でのみ使用されます。 

  
**返します**:True の場合、ラベルがアクティブで、それ以外の場合は false。
  
### <a name="getparent-function"></a>GetParent 関数
親ラベルを取得します。

  
**返します**:親への弱いポインターにラベルを付ける場合はそれ以外の場合、空のポインターが存在します。
  
### <a name="getchildren-function"></a>GetChildren 関数
現在のラベルの子ラベルを取得します。

  
**返します**:ラベルへの共有ポインターのベクター。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
カスタム ラベルの設定を取得します。

  
**返します**:カスタム設定を表すキー値のペアのベクター。