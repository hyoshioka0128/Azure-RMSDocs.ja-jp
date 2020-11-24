---
title: クラス Addcontentフッターアクション
description: 'Microsoft Information Protection (MIP) SDK の addcontentフッター action:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 58f4e72361f9dfbe1e13b1d636f5cb6acd287784
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569359"
---
# <a name="class-addcontentfooteraction"></a>クラス Addcontentフッターアクション 
コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
  
## <a name="summary"></a>まとめ
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

  
**戻り値**: コンテンツ フッターを保持する UI 要素に使用する必要のある名前。 コンテンツ フッターを削除する必要がある場合は、RemoveContentFooterAction でも同じ名前が返されます。
  
### <a name="gettext-function"></a>GetText 関数
コンテンツ フッターに移動されるテキストを取得します。

  
**戻り値**: コンテンツ フッターのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
コンテンツ フッターの表示に使用されるフォント名を取得します。

  
**戻り値**: フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
コンテンツ フッターの表示に使用されるフォント サイズを取得します。

  
**戻り値**: 整数値としてのフォント サイズ。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
コンテンツ フッターの表示に使用されるフォントの色を取得します。

  
**戻り値**: 文字列としてのフォントの色 (例: "#000000")。
  
### <a name="getalignment-function"></a>GetAlignment 関数
フッターの配置を取得します。

  
**戻り値**: ContentMarkAlignment 列挙子: LEFT|RIGHT|CENTER。 
  
**関連項目**: ContentMarkAlignment
  
### <a name="getmargin-function"></a>GetMargin 関数
一番下からのフッターの余白を取得します。

  
**戻り値**: ドキュメントの一番下からの余白 (例: 10 mm)。