---
title: 'クラス mip:: AuthDelegate:: OAuth2Token'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d8bce56e02778d48e6e3c0cfdb02f1c3f1f4054a
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560348"
---
# <a name="class-mipauthdelegateoauth2token"></a>クラス mip:: AuthDelegate:: OAuth2Token 
Mipmap SDK が oauth2 トークンを SDK に渡すことを要求する方法を定義するクラス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック OAuth2Token ()  |  新しい OAuth2Token オブジェクトを構築します。
public OAuth2Token(const std::string& accessToken)  |  AccessToken から新しい OAuth2Token オブジェクトを構築します。
public const std::string& GetAccessToken() const  |  アクセストークン文字列を取得します。
public void SetAccessToken (const std:: string & accessToken)  |  アクセストークン文字列を設定します。
  
## <a name="members"></a>メンバー
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
新しい OAuth2Token オブジェクトを構築します。
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
AccessToken から新しい OAuth2Token オブジェクトを構築します。

パラメーター:  
* **accessToken**: SDK に渡される実際のアクセストークン。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 関数
アクセストークン文字列を取得します。

  
は、アクセストークンの文字列を**返し**ます。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 関数
アクセストークン文字列を設定します。

パラメーター:  
* **accessToken**: アクセストークン文字列。

