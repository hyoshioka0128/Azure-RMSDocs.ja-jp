---
title: class mip::AddContentHeaderAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: addcontentheaderaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: e9de81595ead9a629c3266962a08f1b13fdb9675
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885930"
---
# <a name="class-mipaddcontentheaderaction"></a>class mip::AddContentHeaderAction 
コンテンツ ヘッダーの追加を指定するアクション クラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  コンテンツ ヘッダー要素をマークするために使用する API。
public const std::string& GetText() const  |  コンテンツ ヘッダーに移動されるテキストを取得します。
public const std::string& GetFontName() const  |  コンテンツ ヘッダーの表示に使用されるフォント名を取得します。
public int GetFontSize() const  |  コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。
public const std::string& GetFontColor() const  |  コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。
public ContentMarkAlignment GetAlignment() const  |  ヘッダーの配置を取得します。
public int GetMargin() const  |  一番下からのヘッダーの余白を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname-function"></a>GetUIElementName 関数
コンテンツ ヘッダー要素をマークするために使用する API。

  
次の**値を返し**ます。コンテンツヘッダーを保持する UI 要素に使用する名前。 コンテンツ ヘッダーを削除する必要がある場合は、[RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) に同じ名前が返されます。
  
### <a name="gettext-function"></a>GetText 関数
コンテンツ ヘッダーに移動されるテキストを取得します。

  
次の**値を返し**ます。コンテンツヘッダーのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
コンテンツ ヘッダーの表示に使用されるフォント名を取得します。

  
次の**値を返し**ます。フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。

  
次の**値を返し**ます。整数としてのフォントサイズ。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。

  
次の**値を返し**ます。文字列としてのフォントの色 (たとえば、#000000 ")。
  
### <a name="getalignment-function"></a>GetAlignment 関数
ヘッダーの配置を取得します。

  
次の**値を返し**ます。ContentMarkAlignment 列挙子:左 |RIGHT |点. 
  
**関連**項目:[ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin 関数
一番下からのヘッダーの余白を取得します。

  
次の**値を返し**ます。ドキュメントの下部にある余白 (10 mm など)。