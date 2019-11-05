---
title: 'クラス mip:: Identity'
description: 'Microsoft Information Protection (MIP) SDK の mip:: identity クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 633a0ac8536f7bbd285eee67934f27d65b399bf4
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560156"
---
# <a name="class-mipidentity"></a>クラス mip:: Identity 
Id の抽象化。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック Id ()  |  ユーザーの電子メールアドレスが不明な場合に使用される既定の Id コンストラクター。
パブリック Id (const Identity & その他)  |  Id コピーコンストラクター。
パブリック明示的な Id (const std:: string & email)  |  ユーザーの電子メールアドレスがわかっている場合に使用される id コンストラクター。
public const std:: string & GetEmail () const  |  電子メールを取得します。
  
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
* **email**: ユーザーの電子メールアドレス。


  
### <a name="getemail-function"></a>GetEmail 関数
電子メールを取得します。

  
は、電子メールを**返し**ます。