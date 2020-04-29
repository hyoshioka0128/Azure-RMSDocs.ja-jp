---
title: クラス Id
description: 'Microsoft Information Protection (MIP) SDK の identity:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 1b1dbbe146832773613124917c1ea6d43f5cf13a
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762367"
---
# <a name="class-identity"></a>クラス Id 
Id の抽象化。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック Id ()  |  ユーザーの電子メールアドレスが不明な場合に使用される既定の Id コンストラクター。
パブリック Id (const Identity& その他)  |  Id コピーコンストラクター。
パブリック明示的な Id (const std:: string& email)  |  ユーザーの電子メールアドレスがわかっている場合に使用される id コンストラクター。
パブリック明示的な Id (const std:: string& email、const std:: string& name)  |  ユーザーの電子メールアドレスとユーザー名がわかっている場合に使用される id コンストラクターです。
public const std:: string& GetEmail () const  |  電子メールを取得します。
public const std::string& GetName() const  |  ユーザーのフレンドリ名を取得します。 テキストマークに使用されます。
  
## <a name="members"></a>メンバー
  
### <a name="identity-function"></a>Identity 関数
ユーザーの電子メールアドレスが不明な場合に使用される既定の Id コンストラクター。
  
### <a name="identity-function"></a>Identity 関数
Id コピーコンストラクター。

パラメーター:  
* **Id**: コピーの作成に使用されます。


  
### <a name="identity-function"></a>Identity 関数
ユーザーの電子メールアドレスがわかっている場合に使用される id コンストラクター。

パラメーター:  
* **email**: 有効な電子メールアドレスである必要があります。


  
### <a name="identity-function"></a>Identity 関数
ユーザーの電子メールアドレスとユーザー名がわかっている場合に使用される id コンストラクターです。

パラメーター:  
* **email**: 有効な電子メールアドレスである必要があります。 


* **名前**: ユーザー名。


  
### <a name="getemail-function"></a>GetEmail 関数
電子メールを取得します。

  
は、電子メールを**返し**ます。
  
### <a name="getname-function"></a>GetName 関数
ユーザーのフレンドリ名を取得します。 テキストマークに使用されます。

  
**戻り値**: フレンドリ名。