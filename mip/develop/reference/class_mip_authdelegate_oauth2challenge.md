---
title: 'クラス mip:: AuthDelegate:: OAuth2Challenge'
description: 'Microsoft Information Protection (MIP) SDK の mip:: authdelegate クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 8e3119e18d465c9ad66dd1cbbece003b96d1a3b7
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489063"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>クラス mip:: AuthDelegate:: OAuth2Challenge 
oauth2 トークンを生成するために、呼び出し元アプリケーションから必要なすべての情報を含むクラス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック OAuth2Challenge (const std:: string & authority、const std:: string & resource、const std:: string & scope、const std:: string & claim)  |  新しい OAuth2Challenge オブジェクトを構築します。
public const std::string& GetAuthority() const  |  権限文字列を取得します。
public const std::string& GetResource() const  |  リソース文字列を取得します。
public const std::string& GetScope() const  |  スコープ文字列を取得します。
public const std:: string & GetClaims () const  |  クレーム文字列を取得します。
  
## <a name="members"></a>Members
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge 関数
新しい OAuth2Challenge オブジェクトを構築します。

パラメータ:  
* **authority**: トークンを生成する必要がある機関。 


* **リソース**: トークンが設定されているリソース。 


* **スコープ**: トークンが設定されているスコープ。


  
### <a name="getauthority-function"></a>GetAuthority 関数
権限文字列を取得します。

  
は、authority 文字列を**返し**ます。
  
### <a name="getresource-function"></a>GetResource 関数
リソース文字列を取得します。

  
は、リソース文字列を**返し**ます。
  
### <a name="getscope-function"></a>GetScope 関数
スコープ文字列を取得します。

  
は、スコープ文字列を**返し**ます。
  
### <a name="getclaims-function"></a>GetClaims 関数
クレーム文字列を取得します。

  
は、要求文字列を**返し**ます。