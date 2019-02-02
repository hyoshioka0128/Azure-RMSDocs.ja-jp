---
title: class mip::AddContentFooterAction
description: Mip::addcontentfooteraction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 064581d2b3a3c0ab9b926f0defe161dba46dfe49
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650852"
---
# <a name="class-mipaddcontentfooteraction"></a>class mip::AddContentFooterAction 
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
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname-function"></a>GetUIElementName 関数
コンテンツ フッター要素をマークするために使用する API。

  
**返します**:コンテンツ フッターを保持する名前の UI 要素のために使用する必要があります。 コンテンツ フッターを削除する必要がある場合は、[RemoveContentFooterAction](class_mip_removecontentfooteraction.md) でも同じ名前が返されます。
  
### <a name="gettext-function"></a>GetText 関数
コンテンツ フッターに移動されるテキストを取得します。

  
**返します**:コンテンツ フッターのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
コンテンツ フッターの表示に使用されるフォント名を取得します。

  
**返します**:フォントの名前。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
コンテンツ フッターの表示に使用されるフォント サイズを取得します。

  
**返します**:整数としてのフォント サイズです。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
コンテンツ フッターの表示に使用されるフォントの色を取得します。

  
**返します**:文字列 (たとえば、「#000000」) としてのフォントの色。
  
### <a name="getalignment-function"></a>GetAlignment 関数
フッターの配置を取得します。

  
**返します**:ContentMarkAlignment 列挙子。左 |右 |CENTER。 
  
**参照してください**:[ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin 関数
一番下からのフッターの余白を取得します。

  
**返します**:ドキュメント (たとえば、10 mm) の下の余白。
  
### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。