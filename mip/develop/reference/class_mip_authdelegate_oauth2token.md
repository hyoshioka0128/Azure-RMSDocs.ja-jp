---
title: クラスの mip::AuthDelegate::OAuth2Token
description: Mip::authdelegate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: bef28489d16b040ff910103d9e0bf5a4719c66ff
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255973"
---
# <a name="class-mipauthdelegateoauth2token"></a>クラスの mip::AuthDelegate::OAuth2Token 
MIP SDK で oauth2 トークンを SDK に渡す必要がある方法を定義するクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public OAuth2Token()  |  新しい[OAuth2Token](class_mip_authdelegate_oauth2token.md)オブジェクト。
public OAuth2Token(const std::string& accessToken)  |  新しい[OAuth2Token](class_mip_authdelegate_oauth2token.md) accessToken からのオブジェクト。
public const std::string& GetAccessToken() const  |  アクセス トークンの文字列を取得します。
public void SetAccessToken(const std::string& accessToken)  |  アクセス トークンの文字列を設定します。
  
## <a name="members"></a>メンバー
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
新しい[OAuth2Token](class_mip_authdelegate_oauth2token.md)オブジェクト。
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
新しい[OAuth2Token](class_mip_authdelegate_oauth2token.md) accessToken からのオブジェクト。

パラメーター:  
* **accessToken**:実際のアクセス トークンは、SDK に渡されます。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 関数
アクセス トークンの文字列を取得します。

  
**返します**:アクセス トークンの文字列。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 関数
アクセス トークンの文字列を設定します。

パラメーター:  
* **accessToken**: アクセス トークン文字列。

