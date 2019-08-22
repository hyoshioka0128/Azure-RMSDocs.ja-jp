---
title: 'クラス mip:: AuthDelegate:: OAuth2Challenge'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 836704d51d1afa55bc296681c863ee10a072ea79
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885913"
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