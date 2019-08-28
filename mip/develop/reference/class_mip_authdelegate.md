---
title: 'クラス mip:: AuthDelegate'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f1f2a9f1f1f61d381cbf0da58cfdef9cad6044e2
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056293"
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

