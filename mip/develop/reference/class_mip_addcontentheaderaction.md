---
title: AddContentHeaderAction クラス
description: 'Microsoft Information Protection (MIP) SDK の addcontentheaderaction:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: e5a2993af705855dde94f5be37e22f1e9ab87c99
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212453"
---
# <a name="class-addcontentheaderaction"></a>AddContentHeaderAction クラス 
コンテンツ ヘッダーの追加を指定するアクション クラス。
  
## <a name="summary"></a>まとめ
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

  
**戻り値**: コンテンツ ヘッダーを保持する UI 要素に使用する必要のある名前。 コンテンツ ヘッダーを削除する必要がある場合は、RemoveContentHeaderAction に同じ名前が返されます。
  
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

  
は、文字列としてのフォントの色 (たとえば、#000000 ") を **返し** ます。
  
### <a name="getalignment-function"></a>GetAlignment 関数
ヘッダーの配置を取得します。

  
**戻り値**: ContentMarkAlignment 列挙子: LEFT|RIGHT|CENTER。 
  
**関連項目**: ContentMarkAlignment
  
### <a name="getmargin-function"></a>GetMargin 関数
一番下からのヘッダーの余白を取得します。

  
**戻り値**: ドキュメントの一番下からの余白 (例: 10 mm)。