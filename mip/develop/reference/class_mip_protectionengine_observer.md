---
title: class mip::ProtectionEngine::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionengine クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e5196535dc474d2649c084b55c55a80c3af349b9
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560753"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
ProtectionEngine に関連する通知を受信するインターフェイスです。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std:: shared_ptr\<std:: vector\<std:: string\>\>& templateIds const std:: shared_ptr\<void\>& context)  |  テンプレートが正しく取得されると呼び出されます。
public virtual void OnGetTemplatesFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  テンプレートの取得でエラーが発生すると呼び出されます。
public virtual void OnGetRightsForLabelIdSuccess (const std:: shared_ptr\<std:: vector\<std:: string\>\>& 権限、const std:: shared_ptr\<void\>& context)  |  権限が正しく取得されると呼び出されます。
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  ユーザーのラベル ID に対する権限を取得するときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 関数
テンプレートが正しく取得されると呼び出されます。

パラメーター:  
* **templateIds**: 取得したテンプレートのリストへの参照 


* **コンテキスト**: protectionengine:: Gettemplates async に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: Gettemplates Async に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnGetTemplatesSuccess または ProtectionEngine:: O にそのまま転送されます。bserver:: OnGetTemplatesFailure
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure 関数
テンプレートの取得でエラーが発生すると呼び出されます。

パラメーター:  
* **エラー**: テンプレートの取得中にエラーが発生しました 


* **コンテキスト**: protectionengine:: Gettemplates async に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: Gettemplates Async に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnGetTemplatesSuccess または ProtectionEngine:: O にそのまま転送されます。bserver:: OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess 関数
権限が正しく取得されると呼び出されます。

パラメーター:  
* **rights**: 取得する権限の一覧への参照 


* **コンテキスト**: protectionengine:: GetRightsForLabelIdAsync に渡されたものと同じコンテキスト


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: GetRightsForLabelIdAsync に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess に対してそのまま転送されます。ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 関数
ユーザーのラベル ID に対する権限を取得するときに呼び出されます。

パラメーター:  
* **エラー**: 権限を取得中にエラーが発生しました 


* **コンテキスト**: protectionengine:: GetRightsForLabelIdAsync に渡されたものと同じコンテキスト


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: GetRightsForLabelIdAsync に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess に対してそのまま転送されます。ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure