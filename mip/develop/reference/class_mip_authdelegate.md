---
title: クラス AuthDelegate
description: 'Microsoft Information Protection (MIP) SDK の authdelegate:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 9a971a7d0e8cf78baa5231225da620c9e1c8fa47
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569279"
---
# <a name="class-authdelegate"></a>クラス AuthDelegate 
認証関連の操作のデリゲート。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token (const Identity& Identity, const OAuth2Challenge& チャレンジ, OAuth2Token& token)  |  このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。
パブリック仮想 bool AcquireOAuth2Token (const Identity& Identity、const OAuth2Challenge& チャレンジ、const std:: shared_ptr \<void\>& context、OAuth2Token& token)  |  このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。
  
## <a name="members"></a>メンバー
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 関数
このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。

パラメーター:  
* **id**: トークンが要求されたユーザー 


* **課題**: OAuth2 チャレンジ 


* **トークン**: [出力] Base64 でエンコードされた OAuth2 トークン



  
が **返さ** れます: トークンが正常に取得された場合は True、失敗した場合は false。トークンの出力パラメーターにエラーメッセージが含まれている場合は、後でアプリケーションに発生する NoAuthTokenError 例外に含まれます。
> 非推奨: コンテキストパラメーターを受け入れるものを優先するため、このメソッドはまもなく非推奨とされます。 新しいバージョンが実装されている場合は、このバージョンを実装する必要はありません。
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 関数
このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。

パラメーター:  
* **id**: トークンが要求されたユーザー 


* **課題**: OAuth2 チャレンジ 


* **コンテキスト**: ホストアプリケーションによって MIP API に渡された不透明なコンテキスト 


* **トークン**: [出力] Base64 でエンコードされた OAuth2 トークン



  
が **返さ** れます: トークンが正常に取得された場合は True、失敗した場合は false。トークンの出力パラメーターにエラーメッセージが含まれている場合は、後でアプリケーションに発生する NoAuthTokenError 例外に含まれます。