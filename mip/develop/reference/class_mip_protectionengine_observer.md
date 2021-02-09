---
title: 'クラス ProtectionEngine:: オブザーバー'
description: 'Microsoft Information Protection (MIP) SDK の protectionengine:: observer クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: b9243a1b7d9addaceaec907a368f7e651c99fbd5
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214628"
---
# <a name="class-protectionengineobserver"></a>クラス ProtectionEngine:: オブザーバー 
ProtectionEngine に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std:: vector \<std::shared_ptr\<TemplateDescriptor\> \>& templatedescriptors、const std:: shared_ptr \<void\>& context)  |  テンプレートが正しく取得されると呼び出されます。
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  テンプレートの取得でエラーが発生すると呼び出されます。
public virtual void OnGetRightsForLabelIdSuccess (const std:: shared_ptr \<std::vector\<std::string\> \>& 権限、const std:: shared_ptr \<void\>& context)  |  権限が正しく取得されると呼び出されます。
public virtual void OnGetRightsForLabelIdFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  ユーザーのラベル ID に対する権限を取得するときに呼び出されます。
public virtual void OnLoadUserCertSuccess (const std:: shared_ptr \<void\>& context)  |  ユーザー証明書が正常に読み込まれたときに呼び出されます。
パブリック仮想 void OnLoadUserCertFailure (const std:: exception_ptr& error、const std:: shared_ptr \<void\>& context)  |  ユーザー証明書の読み込みに失敗したときに呼び出されます。
public virtual void OnRegisterContentForTrackingAndRevocationSuccess (const std:: shared_ptr \<void\>& context)  |  & の失効を追跡するためのコンテンツの登録が成功したときに呼び出されます。
public virtual void OnRegisterContentForTrackingAndRevocationFailure (const std:: exception_ptr& error、const std:: shared_ptr \<void\>& context)  |  追跡 & の失効に向けたコンテンツの登録が失敗したときに呼び出されます。
public virtual void OnRevokeContentSuccess (const std:: shared_ptr \<void\>& context)  |  の失効が正常に終了したときに呼び出されます。
public virtual void OnRevokeContentFailure (const std:: exception_ptr& error、const std:: shared_ptr \<void\>& context)  |  コンテンツの失効が失敗したときに呼び出されます。
public virtual void OnCreateDelegatedLicensesSuccess (std:: vector \<std::shared_ptr\<DelegationLicense\> \> delegatedLicenses, const std:: shared_ptr \<void\>& context)  |  委任されたライセンスの作成が成功したときに呼び出されます。
public virtual void OnCreateDelegatedLicensesFailure (const std:: exception_ptr& error、const std:: shared_ptr \<void\>& context)  |  委任されたライセンスの作成に失敗したときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 関数
テンプレートが正しく取得されると呼び出されます。

パラメーター:  
* **templatedescriptors**: テンプレート記述子のリストへの参照 


* **context**: ProtectionEngine::GetTemplatesAsync に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を ProtectionEngine::GetTemplatesAsync に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnGetTemplatesSuccess または ProtectionEngine::Observer::OnGetTemplatesFailure に転送されます
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure 関数
テンプレートの取得でエラーが発生すると呼び出されます。

パラメーター:  
* **エラー**: テンプレートの取得中にエラーが発生しました 


* **context**: ProtectionEngine::GetTemplatesAsync に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を ProtectionEngine::GetTemplatesAsync に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnGetTemplatesSuccess または ProtectionEngine::Observer::OnGetTemplatesFailure に転送されます
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess 関数
権限が正しく取得されると呼び出されます。

パラメーター:  
* **rights**: 取得する権限の一覧への参照 


* **context**: ProtectionEngine::GetRightsForLabelIdAsync に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を ProtectionEngine::GetRightsForLabelIdAsync に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess または ProtectionEngine::Observer::OnGetRightsForLabelIdFailure に転送されます
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 関数
ユーザーのラベル ID に対する権限を取得するときに呼び出されます。

パラメーター:  
* **エラー**: 権限を取得中にエラーが発生しました 


* **context**: ProtectionEngine::GetRightsForLabelIdAsync に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function) を ProtectionEngine::GetRightsForLabelIdAsync に渡すことができ、その同じコンテキストがそのまま ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess または ProtectionEngine::Observer::OnGetRightsForLabelIdFailure に転送されます
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess 関数
ユーザー証明書が正常に読み込まれたときに呼び出されます。

パラメーター:  
* **コンテキスト**: protectionengine:: LoadUserCert に渡されたものと同じコンテキスト


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: LoadUserCertAsync に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnLoadUserCertSuccess または ProtectionEngine:: Observer:: Onloadusercertsuccess に対してそのまま転送されます。
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure 関数
ユーザー証明書の読み込みに失敗したときに呼び出されます。

パラメーター:  
* **エラー**: 権限を取得中にエラーが発生しました 


* **コンテキスト**: protectionengine:: LoadUserCert に渡されたものと同じコンテキスト


アプリケーションでは、任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: LoadUserCertAsync に渡すことができ、同じコンテキストは ProtectionEngine:: Observer:: OnLoadUserCertSuccess または ProtectionEngine:: Observer:: Onloadusercertsuccess に対してそのまま転送されます。
  
### <a name="onregistercontentfortrackingandrevocationsuccess-function"></a>OnRegisterContentForTrackingAndRevocationSuccess 関数
& の失効を追跡するためのコンテンツの登録が成功したときに呼び出されます。

パラメーター:  
* **コンテキスト**: protectionengine:: RegisterContentForTrackingAndRevocationAsync に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: RegisterContentForTrackingAndRevocationAsync に渡すことができます。また、同じコンテキストは、ProtectionEngine:: Observer:: OnRegisterContentForTrackingAndRevocationSuccess または ProtectionEngine:: Observer:: OnRegisterContentForTrackingAndRevocationFailure にそのまま転送されます。
  
### <a name="onregistercontentfortrackingandrevocationfailure-function"></a>OnRegisterContentForTrackingAndRevocationFailure 関数
追跡 & の失効に向けたコンテンツの登録が失敗したときに呼び出されます。

パラメーター:  
* **エラー**: コンテンツの登録中にエラーが発生しました 


* **コンテキスト**: protectionengine:: RegisterContentForTrackingAndRevocationAsync に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: RegisterContentForTrackingAndRevocationAsync に渡すことができます。また、同じコンテキストは、ProtectionEngine:: Observer:: OnRegisterContentForTrackingAndRevocationSuccess または ProtectionEngine:: Observer:: OnRegisterContentForTrackingAndRevocationFailure にそのまま転送されます。
  
### <a name="onrevokecontentsuccess-function"></a>OnRevokeContentSuccess 関数
の失効が正常に終了したときに呼び出されます。

パラメーター:  
* **コンテキスト**: protectionengine:: RevokeContentAsync に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: RevokeContentAsync に渡すことができます。また、同じコンテキストは、ProtectionEngine:: Observer:: OnRevokeContentSuccess または ProtectionEngine:: Observer:: OnRevokeContentFailure にそのまま転送されます。
  
### <a name="onrevokecontentfailure-function"></a>OnRevokeContentFailure 関数
コンテンツの失効が失敗したときに呼び出されます。

パラメーター:  
* **エラー**: コンテンツの取り消し中にエラーが発生しました 


* **コンテキスト**: protectionengine:: RevokeContentAsync に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: RevokeContentAsync に渡すことができます。また、同じコンテキストは、ProtectionEngine:: Observer:: OnRevokeContentSuccess または ProtectionEngine:: Observer:: OnRevokeContentFailure にそのまま転送されます。
  
### <a name="oncreatedelegatedlicensessuccess-function"></a>OnCreateDelegatedLicensesSuccess 関数
委任されたライセンスの作成が成功したときに呼び出されます。

パラメーター:  
* **コンテキスト**: protectionengine:: CreateDelegationLicensesAsync に渡されたのと同じコンテキスト。


アプリケーションは任意の種類のコンテキスト (たとえば、std::p romise、std:: function) を ProtectionEngine:: CreateDelegationLicensesAsync に渡すことができ、同じコンテキストは、ProtectionEngine:: Observer:: OnCreateDelegatedLicensesSuccess または ProtectionEngine:: Observer:: OnCreateDelegatedLicensesFailure にそのまま転送されます。
  
### <a name="oncreatedelegatedlicensesfailure-function"></a>OnCreateDelegatedLicensesFailure 関数
委任されたライセンスの作成に失敗したときに呼び出されます。

パラメーター:  
* **エラー**: 発生したエラー 


* **コンテキスト**: protectionengine:: CreateDelegationLicensesAsync に渡されたものと同じコンテキスト


アプリケーションは任意の種類のコンテキスト (std::p romise、std:: function など) を ProtectionEngine:: CreateDelegationLicensesAsync に渡すことができます。また、同じコンテキストは、ProtectionEngine:: Observer:: OnCreateDelegatedLicensesSuccess または ProtectionEngine:: Observer:: OnCreateDelegatedLicensesFailure にそのまま転送されます。