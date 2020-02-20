---
title: 'クラス mip:: AuthDelegate:: OAuth2Token'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 6053a282d162dc2b0f316b265fe6878a4c535a7f
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490440"
---
# <a name="class-mipauthdelegateoauth2token"></a>クラス mip:: AuthDelegate:: OAuth2Token 
アプリケーションによって提供されるアクセストークン情報を格納しているクラス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック OAuth2Token ()  |  新しい OAuth2Token オブジェクトを構築します。
public OAuth2Token(const std::string& accessToken)  |  JWT アクセストークンから新しい OAuth2Token オブジェクトを構築します。
public const std::string& GetAccessToken() const  |  アクセストークン文字列を取得します。
public void SetAccessToken (const std:: string & accessToken)  |  アクセストークン文字列を設定します。
public const std:: string & GetErrorMessage () const  |  エラーメッセージがある場合は、それを取得します。
public void SetErrorMessage (const std:: string & errorMessage)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
新しい OAuth2Token オブジェクトを構築します。
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
JWT アクセストークンから新しい OAuth2Token オブジェクトを構築します。

パラメータ:  
* **accessToken**: JWT アクセストークン。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 関数
アクセストークン文字列を取得します。

  
**戻り値**: アクセストークン文字列。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 関数
アクセストークン文字列を設定します。

パラメータ:  
* **accessToken**: アクセストークン文字列。


  
### <a name="geterrormessage-function"></a>GetErrorMessage 関数
エラーメッセージがある場合は、それを取得します。

  
は、エラーメッセージ**を返し**ます。
  
### <a name="seterrormessage-function"></a>SetErrorMessage 関数
エラー メッセージを設定します。

パラメータ:  
* **errorMessage**: エラーメッセージ。

