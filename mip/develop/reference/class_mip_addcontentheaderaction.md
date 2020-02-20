---
title: class mip::AddContentHeaderAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: addcontentheaderaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f58fe47de4ee1f79f64415013fc1949ef53b2adf
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490729"
---
# <a name="class-mipaddcontentheaderaction"></a>class mip::AddContentHeaderAction 
コンテンツ ヘッダーの追加を指定するアクション クラス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  コンテンツ ヘッダー要素をマークするために使用する API。
public const std::string& GetText() const  |  コンテンツ ヘッダーに移動されるテキストを取得します。
public const std::string& GetFontName() const  |  コンテンツ ヘッダーの表示に使用されるフォント名を取得します。
public int GetFontSize() const  |  コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。
public const std::string& GetFontColor() const  |  コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。
public ContentMarkAlignment GetAlignment() const  |  ヘッダーの配置を取得します。
public int GetMargin() const  |  一番下からのヘッダーの余白を取得します。
  
## <a name="members"></a>Members
  
### <a name="getuielementname-function"></a>GetUIElementName 関数
コンテンツ ヘッダー要素をマークするために使用する API。

  
**戻り値**: コンテンツ ヘッダーを保持する UI 要素に使用する必要のある名前。 コンテンツヘッダーを削除する必要がある場合、RemoveContentHeaderAction でも同じ名前が返されます。
  
### <a name="gettext-function"></a>GetText 関数
コンテンツ ヘッダーに移動されるテキストを取得します。

  
**戻り値**: コンテンツ ヘッダーのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
コンテンツ ヘッダーの表示に使用されるフォント名を取得します。

  
**戻り値**: フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。

  
**戻り値**: 整数値としてのフォント サイズ。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。

  
**戻り値**: 文字列としてのフォントの色 (例: #000000")。
  
### <a name="getalignment-function"></a>GetAlignment 関数
ヘッダーの配置を取得します。

  
**戻り値**: ContentMarkAlignment 列挙子: LEFT|RIGHT|CENTER。 
  
**関連**項目: [contentmarkalignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin 関数
一番下からのヘッダーの余白を取得します。

  
**戻り値**: ドキュメントの一番下からの余白 (例: 10 mm)。