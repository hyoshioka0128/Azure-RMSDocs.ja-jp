---
title: class mip::AddWatermarkAction
description: Mip::addwatermarkaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: f3a8d50d55dc615a7aa81e8686b356bfc2d41654
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173526"
---
# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
ウォーターマークの追加を指定するアクション クラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  ウォーターマーク要素を示すために使用される API。
public WatermarkLayout GetLayout() const  |  ウォーターマーク レイアウトを取得するために使用される API。
public const std::string& GetText() const  |  ウォーターマークに移動されるテキストを取得します。
public const std::string& GetFontName() const  |  ウォーターマークの表示に使用されるフォント名を取得します。
public int GetFontSize() const  |  ウォーターマークの表示に使用されるフォント サイズを取得します。
public const std::string& GetFontColor() const  |  ウォーターマークの表示に使用されるフォントの色を取得します。
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。

## <a name="members"></a>メンバー
  
### <a name="getuielementname-function"></a>GetUIElementName 関数
ウォーターマーク要素を示すために使用される API。

  
**返します**:この名前は、レベルのウォーターマークを保持する UI 要素に使用する必要があります。 ウォーターマークを削除する必要がある場合は、RemoveWatermarkingAction でも同じ名前が返されます。
  
### <a name="getlayout-function"></a>GetLayout 関数
ウォーターマーク レイアウトを取得するために使用される API。

  
**返します**:WatermarkLayout: 列挙型 HORIZONTAL|DIAGONAL の形式のウォーターマーク レイアウト。 、
  
### <a name="gettext-function"></a>GetText 関数
ウォーターマークに移動されるテキストを取得します。

  
**返します**:コンテンツ ヘッダーのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
ウォーターマークの表示に使用されるフォント名を取得します。

  
**返します**:フォントの名前。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
ウォーターマークの表示に使用されるフォント サイズを取得します。

  
**返します**:整数としてのフォント サイズです。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
ウォーターマークの表示に使用されるフォントの色を取得します。

  
**返します**:文字列 (たとえば、「#000000」) としてのフォントの色。

### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。