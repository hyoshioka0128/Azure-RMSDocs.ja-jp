---
title: class mip AddContentFooterAction
description: class mip AddContentFooterAction のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 73f641d965c3cf0236919557128af2ed07705672
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445837"
---
# <a name="class-mipaddcontentfooteraction"></a>class mip::AddContentFooterAction 
コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  コンテンツ フッター要素をマークするために使用する API。
 public const std::string& GetText() const  |  コンテンツ フッターに移動されるテキストを取得します。
 public const std::string& GetFontName() const  |  コンテンツ フッターの表示に使用されるフォント名を取得します。
 public int GetFontSize() const  |  コンテンツ フッターの表示に使用されるフォント サイズを取得します。
 public const std::string& GetFontColor() const  |  コンテンツ フッターの表示に使用されるフォントの色を取得します。
 public ContentMarkAlignment GetAlignment() const  |  フッターの配置を取得します。
 public int GetMargin() const  |  一番下からのフッターの余白を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname"></a>GetUIElementName
コンテンツ フッター要素をマークするために使用する API。

  
**戻り値**: コンテンツ フッターを保持する UI 要素に使用する必要のある名前。 コンテンツ フッターを削除する必要がある場合は、[RemoveContentFooterAction](class_mip_removecontentfooteraction.md) でも同じ名前が返されます。
  
### <a name="gettext"></a>GetText
コンテンツ フッターに移動されるテキストを取得します。

  
**戻り値**: コンテンツ フッターのテキスト。
  
### <a name="getfontname"></a>GetFontName
コンテンツ フッターの表示に使用されるフォント名を取得します。

  
**戻り値**: フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize"></a>GetFontSize
コンテンツ フッターの表示に使用されるフォント サイズを取得します。

  
**戻り値**: 整数値としてのフォント サイズ。
  
### <a name="getfontcolor"></a>GetFontColor
コンテンツ フッターの表示に使用されるフォントの色を取得します。

  
**戻り値**: 文字列としてのフォントの色 (例: "#000000")。
  
### <a name="getalignment"></a>GetAlignment
フッターの配置を取得します。

  
**戻り値**: ContentMarkAlignment 列挙子: LEFT|RIGHT|CENTER。 
  
**関連項目**: ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
一番下からのフッターの余白を取得します。

  
**戻り値**: ドキュメントの一番下からの余白 (例: 10 mm)。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。