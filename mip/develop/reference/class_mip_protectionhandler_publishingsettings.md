---
title: クラス mip::P rotectionHandler::P ublishingSettings
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionhandler クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e61eb300cbc787ecbb7fd14ec5dcb060d4f47d0a
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490763"
---
# <a name="class-mipprotectionhandlerpublishingsettings"></a>クラス mip::P rotectionHandler::P ublishingSettings 
新しいコンテンツを保護する ProtectionHandler を作成するために使用される設定。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
公開発行設定 (const std:: shared_ptr\<ProtectionDescriptor\>& protectionDescriptor)  |  新しいエンジンを作成するための ProtectionHandler:: Settings コンストラクター。
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  | _まだ文書化されていません。_
public bool GetIsAuditedExtractionAllowed () const  |  非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されているかどうかを取得します。
public void SetIsAuditedExtractionAllowed (bool isAuditedExtractionAllowed)  |  非 MIP 対応アプリケーションで保護されたコンテンツを開くことを許可するかどうかを設定します。
public bool GetIsDeprecatedAlgorithmPreferred () const  |  非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを取得します。
public void SetIsDeprecatedAlgorithmPreferred (bool isDeprecatedAlgorithmPreferred)  |  非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを設定します。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  委任されたユーザーを設定します。
public const std:: string & GetDelegatedUserEmail () const  |  委任されたユーザーを取得します。
public bool IsPublishingFormatJson () const  |  返された pl が json 形式であるかどうかを取得します (xml 形式は広く受け入れられており、既定値です)。
public void Set発行 Formatjson (bool isPublishingFormatJson)  |  返された pl が json 形式であるかどうかを示します (xml 形式は広く受け入れられており、既定値です)。
  
## <a name="members"></a>Members
  
### <a name="publishingsettings-function"></a>発行設定関数
新しいエンジンを作成するための ProtectionHandler:: Settings コンストラクター。

パラメータ:  
* **Protectiondescriptor**: 保護の詳細


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
_まだ文書化されていません。_

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed 関数
非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されているかどうかを取得します。

  
**を返し**ます。非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されている場合
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed 関数
非 MIP 対応アプリケーションで保護されたコンテンツを開くことを許可するかどうかを設定します。

パラメータ:  
* **Isauditedextractionallowed**: 非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されている場合


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred 関数
非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを取得します。

  
は、deprectated crypto アルゴリズムが推奨される場合は**を返し**ます。
  
### <a name="setisdeprecatedalgorithmpreferred-function"></a>SetIsDeprecatedAlgorithmPreferred 関数
非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを設定します。

パラメータ:  
* : Deprectated crypto アルゴリズムが推奨される**場合**


  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 関数
委任されたユーザーを設定します。

パラメータ:  
* **delegatedUserEmail**: 委任の電子メール。


委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作するときに指定します。
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 関数
委任されたユーザーを取得します。

  
**戻り値**: 委任されたユーザー: 認証を行っているユーザーまたはアプリケーションが別のユーザーの代理で動作しているときに、委任されたユーザーを指定します。
  
### <a name="ispublishingformatjson-function"></a>IsPublishingFormatJson 関数
返された pl が json 形式であるかどうかを取得します (xml 形式は広く受け入れられており、既定値です)。

  
は、が json 形式の出力に設定されている場合に True**を返し**ます。
  
### <a name="setpublishingformatjson-function"></a>Set発行 Formatjson 関数
返された pl が json 形式であるかどうかを示します (xml 形式は広く受け入れられており、既定値です)。

パラメータ:  
* **isPublishingFormatJson**: json 形式が有効になっている場合。

