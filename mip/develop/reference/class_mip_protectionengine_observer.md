---
title: class mip::ProtectionEngine::Observer
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionengine クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 688bc59b992e885b2b9724111c19f69f860badd9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489675"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
ProtectionEngine に関連する通知を受信するインターフェイスです。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std:: vector\<std:: shared_ptr\<TemplateDescriptor\>\>& Templatedescriptor、const std:: shared_ptr\<void\>& context)  |  テンプレートが正しく取得されると呼び出されます。
public virtual void OnGetTemplatesFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  テンプレートの取得でエラーが発生すると呼び出されます。
public virtual void OnGetRightsForLabelIdSuccess (const std:: shared_ptr\<std:: vector\<std:: string\>\>& 権限、const std:: shared_ptr\<void\>& context)  |  権限が正しく取得されると呼び出されます。
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  ユーザーのラベル ID に対する権限を取得するときに呼び出されます。
public virtual void OnLoadUserCertSuccess (const std:: shared_ptr\<void\>& context)  |  ユーザー証明書が正常に読み込まれたときに呼び出されます。
パブリック仮想 void OnLoadUserCertFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  ユーザー証明書の読み込みに失敗したときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 関数
テンプレートが正しく取得されると呼び出されます。

パラメータ:  
* **templatedescriptors**: テンプレート記述子のリストへの参照 


* **コンテキスト**: protectionengine:: Gettemplates async に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: Gettemplates Async に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnGetTemplatesSuccess または ProtectionEngine:: O にそのまま転送されます。bserver:: OnGetTemplatesFailure
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure 関数
テンプレートの取得でエラーが発生すると呼び出されます。

パラメータ:  
* **エラー**: テンプレートの取得中にエラーが発生しました 


* **コンテキスト**: protectionengine:: Gettemplates async に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: Gettemplates Async に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnGetTemplatesSuccess または ProtectionEngine:: O にそのまま転送されます。bserver:: OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess 関数
権限が正しく取得されると呼び出されます。

パラメータ:  
* **rights**: 取得する権限の一覧への参照 


* **コンテキスト**: protectionengine:: GetRightsForLabelIdAsync に渡されたものと同じコンテキスト


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: GetRightsForLabelIdAsync に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess に対してそのまま転送されます。ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 関数
ユーザーのラベル ID に対する権限を取得するときに呼び出されます。

パラメータ:  
* **エラー**: 権限を取得中にエラーが発生しました 


* **コンテキスト**: protectionengine:: GetRightsForLabelIdAsync に渡されたものと同じコンテキスト


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: GetRightsForLabelIdAsync に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess に対してそのまま転送されます。ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess 関数
ユーザー証明書が正常に読み込まれたときに呼び出されます。

パラメータ:  
* **コンテキスト**: protectionengine:: LoadUserCert に渡されたものと同じコンテキスト


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: LoadUserCertAsync に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnLoadUserCertSuccess または ProtectionEngine:: O にそのまま転送されます。bserver:: OnLoadUserCertFailure
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure 関数
ユーザー証明書の読み込みに失敗したときに呼び出されます。

パラメータ:  
* **エラー**: 権限を取得中にエラーが発生しました 


* **コンテキスト**: protectionengine:: LoadUserCert に渡されたものと同じコンテキスト


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: LoadUserCertAsync に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnLoadUserCertSuccess または ProtectionEngine:: O にそのまま転送されます。bserver:: OnLoadUserCertFailure