---
title: 'クラス mip:: AuthDelegate:: OAuth2Token'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: b7b9b73d9f1f3952af1d6a9bdea94c75a8032fb7
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885901"
---
# <a name="class-mipauthdelegateoauth2token"></a>クラス mip:: AuthDelegate:: OAuth2Token 
Mipmap SDK が oauth2 トークンを SDK に渡すことを要求する方法を定義するクラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック OAuth2Token ()  |  新しい[OAuth2Token](class_mip_authdelegate_oauth2token.md)オブジェクトを構築します。
public OAuth2Token(const std::string& accessToken)  |  AccessToken から新しい[OAuth2Token](class_mip_authdelegate_oauth2token.md)オブジェクトを構築します。
public const std::string& GetAccessToken() const  |  アクセストークン文字列を取得します。
public void SetAccessToken (const std:: string & accessToken)  |  アクセストークン文字列を設定します。
  
## <a name="members"></a>メンバー
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
新しい[OAuth2Token](class_mip_authdelegate_oauth2token.md)オブジェクトを構築します。
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
AccessToken から新しい[OAuth2Token](class_mip_authdelegate_oauth2token.md)オブジェクトを構築します。

パラメーター:  
* **accessToken**:SDK に渡される実際のアクセストークン。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 関数
アクセストークン文字列を取得します。

  
次の**値を返し**ます。アクセストークン文字列。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 関数
アクセストークン文字列を設定します。

パラメーター:  
* **accessToken**: アクセストークン文字列。

