---
title: 'クラス mip:: AuthDelegate'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 30907f3bf4a08f72305a59290c8cbd891def44c9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490610"
---
# <a name="class-mipauthdelegate"></a>クラス mip:: AuthDelegate 
認証関連の操作のデリゲート。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token (const mip:: Identity & identity, const OAuth2Challenge & チャレンジ, OAuth2Token & token)  |  このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。
パブリック仮想 bool AcquireOAuth2Token (const mip:: Identity & identity、const OAuth2Challenge & チャレンジ、const std:: shared_ptr\<void\>& context、OAuth2Token & token)  |  このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。
  
## <a name="members"></a>Members
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 関数
このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。

パラメータ:  
* **id**: トークンが要求されたユーザー 


* **課題**: OAuth2 チャレンジ 


* **トークン**: [出力] Base64 でエンコードされた OAuth2 トークン



  
が**返さ**れます: トークンが正常に取得された場合は True、失敗した場合は false。トークンの出力パラメーターにエラーメッセージが含まれている場合は、後でアプリケーションに発生する NoAuthTokenError 例外に含まれます。
> 非推奨: コンテキストパラメーターを受け入れるものを優先するため、このメソッドはまもなく非推奨とされます。 新しいバージョンが実装されている場合は、このバージョンを実装する必要はありません。
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 関数
このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。

パラメータ:  
* **id**: トークンが要求されたユーザー 


* **課題**: OAuth2 チャレンジ 


* **コンテキスト**: ホストアプリケーションによって MIP API に渡された不透明なコンテキスト 


* **トークン**: [出力] Base64 でエンコードされた OAuth2 トークン



  
が**返さ**れます: トークンが正常に取得された場合は True、失敗した場合は false。トークンの出力パラメーターにエラーメッセージが含まれている場合は、後でアプリケーションに発生する NoAuthTokenError 例外に含まれます。