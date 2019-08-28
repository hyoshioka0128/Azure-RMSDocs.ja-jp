---
title: class mip::AddWatermarkAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: addwatermarkaction クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2b6a50385e5d891b8893949a8761e7f38f591f17
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056343"
---
# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
ウォーターマークの追加を指定するアクション クラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  ウォーターマーク要素を示すために使用される API。
public WatermarkLayout GetLayout() const  |  ウォーターマーク レイアウトを取得するために使用される API。
public const std::string& GetText() const  |  ウォーターマークに移動されるテキストを取得します。
public const std::string& GetFontName() const  |  ウォーターマークの表示に使用されるフォント名を取得します。
public int GetFontSize() const  |  ウォーターマークの表示に使用されるフォント サイズを取得します。
public const std::string& GetFontColor() const  |  ウォーターマークの表示に使用されるフォントの色を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname-function"></a>GetUIElementName 関数
ウォーターマーク要素を示すために使用される API。

  
次の**値を返し**ます。ウォーターマークを保持する UI 要素に使用する名前。 ウォーターマークを削除する必要がある場合は、RemoveWatermarkingAction でも同じ名前が返されます。
  
### <a name="getlayout-function"></a>GetLayout 関数
ウォーターマーク レイアウトを取得するために使用される API。

  
次の**値を返し**ます。WatermarkLayout: 列挙型 HORIZONTAL|DIAGONAL の形式のウォーターマーク レイアウト。 ,
  
### <a name="gettext-function"></a>GetText 関数
ウォーターマークに移動されるテキストを取得します。

  
次の**値を返し**ます。コンテンツヘッダーのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
ウォーターマークの表示に使用されるフォント名を取得します。

  
次の**値を返し**ます。フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
ウォーターマークの表示に使用されるフォント サイズを取得します。

  
次の**値を返し**ます。整数としてのフォントサイズ。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
ウォーターマークの表示に使用されるフォントの色を取得します。

  
次の**値を返し**ます。文字列としてのフォントの色 (たとえば、"#000000")。