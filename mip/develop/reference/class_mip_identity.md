---
title: クラス Id
description: 'Microsoft Information Protection (MIP) SDK の identity:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: ae89ed32a48deae7132bc65adabf86f7fb63ffe1
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566873"
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

  
は、電子メールを **返し** ます。
  
### <a name="getname-function"></a>GetName 関数
ユーザーのフレンドリ名を取得します。 テキストマークに使用されます。

  
**戻り値**: フレンドリ名。