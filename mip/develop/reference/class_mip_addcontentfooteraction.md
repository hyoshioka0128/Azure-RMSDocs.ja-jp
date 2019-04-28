---
title: class mip::AddContentFooterAction
description: Mip::addcontentfooteraction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 625406d1b2207e4b1f74c77c6813ee3d852f0d37
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173500"
---
# <a name="class-mipaddcontentfooteraction"></a>class mip::AddContentFooterAction 
コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
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
  
**参照してください**:[ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment)
  
### <a name="getmargin-function"></a>GetMargin 関数
一番下からのフッターの余白を取得します。

  
**返します**:ドキュメント (たとえば、10 mm) の下の余白。

### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。