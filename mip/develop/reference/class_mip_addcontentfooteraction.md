---
title: class mip::AddContentFooterAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: addcontentフッターアクションクラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: a9dc9b68dbe2a4ca1a670f608f2ae3e0010affe6
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056381"
---
# <a name="class-mipaddcontentfooteraction"></a>class mip::AddContentFooterAction 
コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  コンテンツ フッター要素をマークするために使用する API。
public const std::string& GetText() const  |  コンテンツ フッターに移動されるテキストを取得します。
public const std::string& GetFontName() const  |  コンテンツ フッターの表示に使用されるフォント名を取得します。
public int GetFontSize() const  |  コンテンツ フッターの表示に使用されるフォント サイズを取得します。
public const std::string& GetFontColor() const  |  コンテンツ フッターの表示に使用されるフォントの色を取得します。
public ContentMarkAlignment GetAlignment() const  |  フッターの配置を取得します。
public int GetMargin() const  |  一番下からのフッターの余白を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname-function"></a>GetUIElementName 関数
コンテンツ フッター要素をマークするために使用する API。

  
次の**値を返し**ます。コンテンツフッターを保持する UI 要素に使用する名前。 コンテンツ フッターを削除する必要がある場合は、[RemoveContentFooterAction](class_mip_removecontentfooteraction.md) でも同じ名前が返されます。
  
### <a name="gettext-function"></a>GetText 関数
コンテンツ フッターに移動されるテキストを取得します。

  
次の**値を返し**ます。コンテンツフッターのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
コンテンツ フッターの表示に使用されるフォント名を取得します。

  
次の**値を返し**ます。フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
コンテンツ フッターの表示に使用されるフォント サイズを取得します。

  
次の**値を返し**ます。整数としてのフォントサイズ。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
コンテンツ フッターの表示に使用されるフォントの色を取得します。

  
次の**値を返し**ます。文字列としてのフォントの色 (たとえば、"#000000")。
  
### <a name="getalignment-function"></a>GetAlignment 関数
フッターの配置を取得します。

  
次の**値を返し**ます。ContentMarkAlignment 列挙子:左 |RIGHT |点. 
  
**関連**項目:[ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin 関数
一番下からのフッターの余白を取得します。

  
次の**値を返し**ます。ドキュメントの下部にある余白 (10 mm など)。