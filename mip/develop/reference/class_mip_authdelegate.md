---
title: mip::AuthDelegate をクラスします。
description: Mip::authdelegate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bcc38bf4b55ca99cf926138279223a4140f7bbf4
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184843"
---
# <a name="class-mipauthdelegate"></a>mip::AuthDelegate をクラスします。 
認証用のデリゲートに関連する操作。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public bool AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token)  |  認証トークンが特定の id と指定したチャレンジを持つポリシー エンジンに必要な場合は、このメソッドが呼び出されます。 クライアントは、トークンの取得が成功したかどうかを返す必要があります。 成功した場合、特定のトークンのオブジェクトを初期化する必要があります。
  
## <a name="members"></a>メンバー
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 関数
認証トークンが特定の id と指定したチャレンジを持つポリシー エンジンに必要な場合は、このメソッドが呼び出されます。 クライアントは、トークンの取得が成功したかどうかを返す必要があります。 成功した場合、特定のトークンのオブジェクトを初期化する必要があります。

パラメーター:  
* **identity**: 


* **チャレンジ**: 


* **token**:

