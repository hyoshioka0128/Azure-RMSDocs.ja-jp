---
title: クラスラベル
description: 'Microsoft Information Protection (MIP) SDK の label:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 726c61d1b73389bfdc10afb961177659e5a137d4
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213897"
---
# <a name="class-label"></a>クラスラベル 
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
public const std:: string& GetAutoTooltip () const  |  このラベルが適用される分類のツールヒントの説明を取得します。
public bool IsActive() const  |  ラベルがアクティブかどうかを示すブール値を取得します。
public std::weak_ptr\<Label\> GetParent() const  |  親ラベルを取得します。
public const std:: vector \<std::shared_ptr\<Label\> \>& getchildren () const  |  現在のラベルの子ラベルを取得します。
public const std:: vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  ラベルのカスタム設定を取得します。
public ActionSource GetActionSource() const  |  ラベルのアクションソースを取得します。
public const std:: vector \<std::string\>& getcontentformats () const  |  コンテンツタイプを取得します。
  
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

  
**戻り** 値: カスタム設定を表すキーと値のペアのベクター。
  
### <a name="getactionsource-function"></a>GetActionSource 関数
ラベルのアクションソースを取得します。

  
**戻り値**: アクションソース
  
### <a name="getcontentformats-function"></a>GetContentFormats 関数
コンテンツタイプを取得します。

  
<Returns>