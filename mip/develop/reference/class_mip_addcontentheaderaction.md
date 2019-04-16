---
title: class mip::AddContentHeaderAction
description: Mip::addcontentheaderaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 367626955ba1652b20b372efd309d15304e5336f
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573447"
---
# <a name="class-mipaddcontentheaderaction"></a>class mip::AddContentHeaderAction 
コンテンツ ヘッダーの追加を指定するアクション クラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
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
  
### <a name="getuielementname-function"></a>GetUIElementName 関数
コンテンツ ヘッダー要素をマークするために使用する API。

  
**返します**:この名前は、コンテンツ ヘッダーを保持する UI 要素に使用する必要があります。 コンテンツ ヘッダーを削除する必要がある場合は、[RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) に同じ名前が返されます。
  
### <a name="gettext-function"></a>GetText 関数
コンテンツ ヘッダーに移動されるテキストを取得します。

  
**返します**:コンテンツ ヘッダーのテキスト。
  
### <a name="getfontname-function"></a>GetFontName 関数
コンテンツ ヘッダーの表示に使用されるフォント名を取得します。

  
**返します**:フォントの名前。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize-function"></a>GetFontSize 関数
コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。

  
**返します**:整数としてのフォント サイズです。
  
### <a name="getfontcolor-function"></a>GetFontColor 関数
コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。

  
**返します**:文字列としてのフォントの色 (たとえば、#000000")。
  
### <a name="getalignment-function"></a>GetAlignment 関数
ヘッダーの配置を取得します。

  
**返します**:ContentMarkAlignment 列挙子。左 |右 |CENTER。 
  
**参照してください**:[ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment)
  
### <a name="getmargin-function"></a>GetMargin 関数
一番下からのヘッダーの余白を取得します。

  
**返します**:ドキュメント (たとえば、10 mm) の下の余白。

### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。