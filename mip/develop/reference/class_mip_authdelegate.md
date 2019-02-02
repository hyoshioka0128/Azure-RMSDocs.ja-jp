---
title: mip::AuthDelegate をクラスします。
description: Mip::authdelegate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: b6278d605dfbb9a9c4cf0cf1282a159c456c5561
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651998"
---
# <a name="class-mipauthdelegate"></a>mip::AuthDelegate をクラスします。 
認証用のデリゲートに関連する操作。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public bool AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token)  |  認証トークンが特定の id と指定したチャレンジを持つポリシー エンジンに必要な場合は、このメソッドが呼び出されます。 クライアントは、トークンの取得が成功したかどうかを返す必要があります。 成功した場合、特定のトークンのオブジェクトを初期化する必要があります。
  
## <a name="members"></a>メンバー
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 関数
認証トークンが特定の id と指定したチャレンジを持つポリシー エンジンに必要な場合は、このメソッドが呼び出されます。 クライアントは、トークンの取得が成功したかどうかを返す必要があります。 成功した場合、特定のトークンのオブジェクトを初期化する必要があります。

パラメーター:  
* **identity**: 


* **チャレンジ**: 


* **token**:

