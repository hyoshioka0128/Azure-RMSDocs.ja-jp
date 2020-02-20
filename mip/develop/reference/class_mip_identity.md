---
title: 'クラス mip:: Identity'
description: 'Microsoft Information Protection (MIP) SDK の mip:: identity クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d50092be5277d5e88e6ec408280ca76bbc333a4c
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488026"
---
# <a name="class-mipidentity"></a>クラス mip:: Identity 
Id の抽象化。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック Id ()  |  ユーザーの電子メールアドレスが不明な場合に使用される既定の Id コンストラクター。
パブリック Id (const Identity & その他)  |  Id コピーコンストラクター。
パブリック明示的な Id (const std:: string & email)  |  ユーザーの電子メールアドレスがわかっている場合に使用される id コンストラクター。
パブリック明示的な Id (const std:: string & email、const std:: string & name)  |  ユーザーの電子メールアドレスとユーザー名がわかっている場合に使用される id コンストラクターです。
public const std::string& GetEmail() const  |  電子メールを取得します。
public const std::string& GetName() const  |  ユーザーのフレンドリ名を取得します。 テキストマークに使用されます。
  
## <a name="members"></a>Members
  
### <a name="identity-function"></a>Identity 関数
ユーザーの電子メールアドレスが不明な場合に使用される既定の Id コンストラクター。
  
### <a name="identity-function"></a>Identity 関数
Id コピーコンストラクター。

パラメータ:  
* **Id**: コピーの作成に使用されます。


  
### <a name="identity-function"></a>Identity 関数
ユーザーの電子メールアドレスがわかっている場合に使用される id コンストラクター。

パラメータ:  
* **email**: 有効な電子メールアドレスである必要があります。


  
### <a name="identity-function"></a>Identity 関数
ユーザーの電子メールアドレスとユーザー名がわかっている場合に使用される id コンストラクターです。

パラメータ:  
* **email**: 有効な電子メールアドレスである必要があります。 


* **名前**: ユーザー名。


  
### <a name="getemail-function"></a>GetEmail 関数
電子メールを取得します。

  
は、電子メールを**返し**ます。
  
### <a name="getname-function"></a>GetName 関数
ユーザーのフレンドリ名を取得します。 テキストマークに使用されます。

  
**戻り値**: フレンドリ名。