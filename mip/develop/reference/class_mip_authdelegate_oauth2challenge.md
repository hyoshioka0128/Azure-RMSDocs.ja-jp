---
title: 'クラス AuthDelegate:: OAuth2Challenge'
description: 'Microsoft Information Protection (MIP) SDK の authdelegate:: oauth2challenge クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: f422b99674213904316eab622bfc915f128228ec
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569286"
---
# <a name="class-authdelegateoauth2challenge"></a>クラス AuthDelegate:: OAuth2Challenge 
oauth2 トークンを生成するために、呼び出し元アプリケーションから必要なすべての情報を含むクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック OAuth2Challenge (const std:: string& authority、const std:: string& resource、const std:: string& scope、const std:: string& claim)  |  新しい OAuth2Challenge オブジェクトを構築します。
public const std:: string& GetAuthority () const  |  権限文字列を取得します。
public const std:: string& GetResource () const  |  リソース文字列を取得します。
public const std:: string& GetScope () const  |  スコープ文字列を取得します。
public const std:: string& GetClaims () const  |  クレーム文字列を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge 関数
新しい OAuth2Challenge オブジェクトを構築します。

パラメーター:  
* **authority**: トークンを生成する必要がある機関。 


* **リソース**: トークンが設定されているリソース。 


* **スコープ**: トークンが設定されているスコープ。


  
### <a name="getauthority-function"></a>GetAuthority 関数
権限文字列を取得します。

  
は、authority 文字列を **返し** ます。
  
### <a name="getresource-function"></a>GetResource 関数
リソース文字列を取得します。

  
は、リソース文字列を **返し** ます。
  
### <a name="getscope-function"></a>GetScope 関数
スコープ文字列を取得します。

  
は、スコープ文字列を **返し** ます。
  
### <a name="getclaims-function"></a>GetClaims 関数
クレーム文字列を取得します。

  
は、要求文字列を **返し** ます。