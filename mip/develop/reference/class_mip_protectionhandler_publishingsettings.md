---
title: クラス mip::P rotectionHandler::P ublishingSettings
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionhandler クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 83489b41811cdaaf46b7336b21eeccb8289eb9f1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893125"
---
# <a name="class-mipprotectionhandlerpublishingsettings"></a>クラス mip::P rotectionHandler::P ublishingSettings 
新しいコンテンツを保護する[Protectionhandler](class_mip_protectionhandler.md)を作成するために使用される設定。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
公開発行設定 (const std:: shared_ptr\<protectiondescriptor\>& protectiondescriptor)  |  新しいエンジンを作成するための ProtectionHandler:: Settings コンストラクター。
public std:: shared_ptr\<protectiondescriptor\> getprotectiondescriptor () const  | _まだ文書化されていません。_
public bool GetIsAuditedExtractionAllowed () const  |  非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されているかどうかを取得します。
public void SetIsAuditedExtractionAllowed (bool isAuditedExtractionAllowed)  |  非 MIP 対応アプリケーションで保護されたコンテンツを開くことを許可するかどうかを設定します。
public bool GetIsDeprecatedAlgorithmPreferred () const  |  非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを取得します。
public void SetIsDeprecatedAlgorithmPreferred (bool isDeprecatedAlgorithmPreferred)  |  非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを設定します。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  委任されたユーザーを設定します。
public const std:: string & GetDelegatedUserEmail () const  |  委任されたユーザーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="publishingsettings-function"></a>発行設定関数
新しいエンジンを作成するための ProtectionHandler:: Settings コンストラクター。

パラメーター:  
* **Protectiondescriptor**:保護の詳細


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
_まだ文書化されていません。_

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed 関数
非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されているかどうかを取得します。

  
次の**値を返し**ます。非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されている場合
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed 関数
非 MIP 対応アプリケーションで保護されたコンテンツを開くことを許可するかどうかを設定します。

パラメーター:  
* **Isauditedextractionallowed**:非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されている場合


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred 関数
非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを取得します。

  
次の**値を返し**ます。Deprectated crypto アルゴリズムが推奨される場合
  
### <a name="setisdeprecatedalgorithmpreferred-function"></a>SetIsDeprecatedAlgorithmPreferred 関数
非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを設定します。

パラメーター:  
* : Deprectated crypto アルゴリズムが推奨される**場合**


  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 関数
委任されたユーザーを設定します。

パラメーター:  
* **delegatedUserEmail**: 委任の電子メール。


委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作するときに指定します。
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 関数
委任されたユーザーを取得します。

  
次の**値を返し**ます。委任されたユーザー認証を行っているユーザーまたはアプリケーションが別のユーザーの代理で動作しているときに、委任されたユーザーを指定します。