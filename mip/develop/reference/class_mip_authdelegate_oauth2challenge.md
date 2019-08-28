---
title: 'クラス mip:: AuthDelegate:: OAuth2Challenge'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2e96fb769a1b917715daa872736c6d2b81e2626e
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055416"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>クラス mip:: AuthDelegate:: OAuth2Challenge 
oauth2 トークンを生成するために、呼び出し元アプリケーションから必要なすべての情報を含むクラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック OAuth2Challenge (const std:: string & authority、const std:: string & resource、const std:: string & scope、const std:: string & claim)  |  新しい[OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)オブジェクトを構築します。
public const std::string& GetAuthority() const  |  権限文字列を取得します。
public const std::string& GetResource() const  |  リソース文字列を取得します。
public const std::string& GetScope() const  |  スコープ文字列を取得します。
public const std:: string & GetClaims () const  |  クレーム文字列を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge 関数
新しい[OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)オブジェクトを構築します。

パラメーター:  
* **authority**: トークンを生成する必要がある機関。 


* **リソース**: トークンが設定されているリソース。 


* **スコープ**: トークンが設定されているスコープ。


  
### <a name="getauthority-function"></a>GetAuthority 関数
権限文字列を取得します。

  
次の**値を返し**ます。機関文字列。
  
### <a name="getresource-function"></a>GetResource 関数
リソース文字列を取得します。

  
次の**値を返し**ます。リソース文字列。
  
### <a name="getscope-function"></a>GetScope 関数
スコープ文字列を取得します。

  
次の**値を返し**ます。スコープ文字列。
  
### <a name="getclaims-function"></a>GetClaims 関数
クレーム文字列を取得します。

  
次の**値を返し**ます。クレーム文字列。