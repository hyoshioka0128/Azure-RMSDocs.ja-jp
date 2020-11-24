---
title: 'クラス AuthDelegate:: OAuth2Token'
description: 'Microsoft Information Protection (MIP) SDK の authdelegate:: oauth2token クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a8532e1950977e421fa25b426fa4e4061e610d8d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569271"
---
# <a name="class-authdelegateoauth2token"></a>クラス AuthDelegate:: OAuth2Token 
アプリケーションによって提供されるアクセストークン情報を格納しているクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック OAuth2Token ()  |  新しい OAuth2Token オブジェクトを構築します。
public OAuth2Token (const std:: string& accessToken)  |  JWT アクセストークンから新しい OAuth2Token オブジェクトを構築します。
public const std:: string& GetAccessToken () const  |  アクセストークン文字列を取得します。
public void SetAccessToken (const std:: string& accessToken)  |  アクセストークン文字列を設定します。
public const std:: string& GetErrorMessage () const  |  エラーメッセージがある場合は、それを取得します。
public void SetErrorMessage (const std:: string& errorMessage)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
新しい OAuth2Token オブジェクトを構築します。
  
### <a name="oauth2token-function"></a>OAuth2Token 関数
JWT アクセストークンから新しい OAuth2Token オブジェクトを構築します。

パラメーター:  
* **accessToken**: JWT アクセストークン。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 関数
アクセストークン文字列を取得します。

  
**戻り値**: アクセストークン文字列。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 関数
アクセストークン文字列を設定します。

パラメーター:  
* **accessToken**: アクセストークン文字列。


  
### <a name="geterrormessage-function"></a>GetErrorMessage 関数
エラーメッセージがある場合は、それを取得します。

  
は、エラーメッセージ **を返し** ます。
  
### <a name="seterrormessage-function"></a>SetErrorMessage 関数
エラー メッセージを設定します。

パラメーター:  
* **errorMessage**: エラーメッセージ。

