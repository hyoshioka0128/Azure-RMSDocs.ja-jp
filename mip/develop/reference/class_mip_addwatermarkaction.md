---
title: class mip::AddWatermarkAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: addwatermarkaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 80ae66e54fe00ad96652b3568d49e256211dffc4
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490712"
---
# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
ウォーターマークの追加を指定するアクション クラス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  ウォーターマーク要素を示すために使用される API。
public WatermarkLayout GetLayout() const  |  ウォーターマーク レイアウトを取得するために使用される API。
public const std::string& GetText() const  |  ウォーターマークに移動されるテキストを取得します。
public const std::string& GetFontName() const  |  ウォーターマークの表示に使用されるフォント名を取得します。
public int GetFontSize() const  |  ウォーターマークの表示に使用されるフォント サイズを取得します。
public const std::string& GetFontColor() const  |  ウォーターマークの表示に使用されるフォントの色を取得します。
  
## <a name="members"></a>Members
  
### <a name="getuielementname-function"></a>GetUIElementName 関数
ウォーターマーク要素を示すために使用される API。

  
**戻り値**: ウォーターマークを保持する UI 要素に使用する必要のある名前。 ウォーターマークを削除する必要がある場合は、RemoveWatermarkingAction でも同じ名前が返されます。
  
### <a name="getlayout-function"></a>GetLayout 関数
ウォーターマーク レイアウトを取得するために使用される API。

  
**戻り値**: WatermarkLayout: 列挙型 HORIZONTAL|DIAGONAL の形式のウォーターマーク レイアウト。 ,
  
### <a name="gettext-function"></a>GetText 関数
ウォーターマークに移動されるテキストを取得します。

  
**戻り値**: コンテンツ ヘッダーのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
ウォーターマークの表示に使用されるフォント名を取得します。

  
**戻り値**: フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
ウォーターマークの表示に使用されるフォント サイズを取得します。

  
**戻り値**: 整数値としてのフォント サイズ。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
ウォーターマークの表示に使用されるフォントの色を取得します。

  
**戻り値**: 文字列としてのフォントの色 (例: "#000000")。