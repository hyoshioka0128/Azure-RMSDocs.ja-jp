---
title: class mip AddContentHeaderAction
description: class mip AddContentHeaderAction のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: bc60fe32005a0c6bc8088ab7687a3f711ae7a99a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445650"
---
# <a name="class-mipaddcontentheaderaction"></a>class mip::AddContentHeaderAction 
コンテンツ ヘッダーの追加を指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  コンテンツ ヘッダー要素をマークするために使用する API。
 public const std::string& GetText() const  |  コンテンツ ヘッダーに移動されるテキストを取得します。
 public const std::string& GetFontName() const  |  コンテンツ ヘッダーの表示に使用されるフォント名を取得します。
 public int GetFontSize() const  |  コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。
 public const std::string& GetFontColor() const  |  コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。
 public ContentMarkAlignment GetAlignment() const  |  ヘッダーの配置を取得します。
 public int GetMargin() const  |  一番下からのヘッダーの余白を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname"></a>GetUIElementName
コンテンツ ヘッダー要素をマークするために使用する API。

  
**戻り値**: コンテンツ ヘッダーを保持する UI 要素に使用する必要のある名前。 コンテンツ ヘッダーを削除する必要がある場合は、[RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) に同じ名前が返されます。
  
### <a name="gettext"></a>GetText
コンテンツ ヘッダーに移動されるテキストを取得します。

  
**戻り値**: コンテンツ ヘッダーのテキスト。
  
### <a name="getfontname"></a>GetFontName
コンテンツ ヘッダーの表示に使用されるフォント名を取得します。

  
**戻り値**: フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize"></a>GetFontSize
コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。

  
**戻り値**: 整数値としてのフォント サイズ。
  
### <a name="getfontcolor"></a>GetFontColor
コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。

  
**戻り値**: 文字列としてのフォントの色 (例: #000000")。
  
### <a name="getalignment"></a>GetAlignment
ヘッダーの配置を取得します。

  
**戻り値**: ContentMarkAlignment 列挙子: LEFT|RIGHT|CENTER。 
  
**関連項目**: ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
一番下からのヘッダーの余白を取得します。

  
**戻り値**: ドキュメントの一番下からの余白 (例: 10 mm)。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。