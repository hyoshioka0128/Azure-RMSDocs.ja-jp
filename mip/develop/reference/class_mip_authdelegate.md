---
title: 'クラス mip:: AuthDelegate'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: b865a26b9cfd96cf4beafa2eb712917405f1dd5c
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884495"
---
# <a name="class-mipauthdelegate"></a>クラス mip:: AuthDelegate 
認証関連の操作のデリゲート。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token (const mip:: Identity & identity, const OAuth2Challenge & チャレンジ, OAuth2Token & token)  |  このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。
パブリック仮想 bool AcquireOAuth2Token (const mip:: identity & identity、const OAuth2Challenge & チャレンジ、const std:: shared_ptr\<void\>& context、OAuth2Token & token)  |  このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。
  
## <a name="members"></a>メンバー
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 関数
このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。

パラメーター:  
* **id**: 


* **課題**: 


* **トークン**: 


> れこのメソッドは、コンテキストパラメーターを受け入れるものを優先することで、すぐに非推奨となります。 新しいバージョンが実装されている場合は、このバージョンを実装する必要はありません。
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 関数
このメソッドは、指定された id とチャレンジを持つポリシーエンジンに認証トークンが必要な場合に呼び出されます。 クライアントは、トークンの取得に成功したかどうかを返す必要があります。 成功した場合は、指定されたトークンオブジェクトを初期化する必要があります。

パラメーター:  
* **id**:トークンが要求されたユーザー 


* **課題**:OAuth2 チャレンジ 


* **コンテキスト**:ホストアプリケーションによって MIP API に渡された不透明なコンテキスト 


* **トークン**: [出力] Base64 でエンコードされた OAuth2 トークン

