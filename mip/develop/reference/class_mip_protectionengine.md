---
title: class mip::ProtectionEngine
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionengine クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 9eb44a39f32c2997729e6d77ddace96c580328cd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73557738"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
特定の ID に関連する、保護関連のアクションを管理します。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を取得します。
public void Gettemplates Async (const std:: shared_ptr\<ProtectionEngine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public std:: vector\<std:: string\> GetTemplates (const std:: shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public void GetRightsForLabelIdAsync (const std:: string & documentId、const std:: string & Lab d、const std:: string & ownerEmail、const std:: string & delegatedUserEmail、const std:: shared_ptr\<ProtectionEngine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。
public std:: vector\<std:: string\> GetRightsForLabelId (const std:: string & documentId、const std:: string & Lab d、const std:: string & ownerEmail、const std:: string & delegatedUserEmail、const std:: shared_ptr @no__t& コンテキスト\>) void (_s)  |  labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。
public void Createprotectionhandler For発行非同期 (const ProtectionHandler::P ublishingSettings & 設定、const std:: shared_ptr\<ProtectionHandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& コンテキスト)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<ProtectionHandler\> Createprotectionハンドラ Forpublishing (const ProtectionHandler::P ublishingSettings & settings、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public void CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler:: ConsumptionSettings & settings、const std:: shared_ptr\<ProtectionHandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void @no__ & コンテキスト) (_s)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<ProtectionHandler\> Createprotectionハンドラ For従量課金 (const ProtectionHandler:: ConsumptionSettings & settings、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を取得します。

  
**戻り値**: エンジンの設定
  
### <a name="gettemplatesasync-function"></a>Gettemplates Async 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **オブザーバー**: protectionengine:: observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーとオプションの httpdelegate に不透明に戻されるクライアントコンテキスト


  
### <a name="gettemplates-function"></a>GetTemplates 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **コンテキスト**: オプションの httpdelegate に不透明渡されるクライアントコンテキスト



  
**戻り値**: テンプレート ID の一覧
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync 関数
ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**: ドキュメント メタデータに関連付けられているドキュメント ID 


* **Lab/d**: ドキュメントが作成されたドキュメントメタデータに関連付けられているラベル ID 


* **ownerEmail**: ドキュメントの所有者 


* **A**: 委任されたユーザーは、認証を行うユーザーまたはアプリケーションが別のユーザーの代理として動作しているときに指定され、none の場合は空になります。 


* **オブザーバー**: protectionengine:: observer インターフェイスを実装するクラス 


* **コンテキスト**: この同じコンテキストは protectionengine:: observer:: OnGetRightsForLabelIdSuccess または protectionengine:: observer:: OnGetRightsForLabelIdFailure に転送されます。


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 関数
labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**: ドキュメント メタデータに関連付けられているドキュメント ID 


* **Lab/d**: ドキュメントが作成されたドキュメントメタデータに関連付けられているラベル ID 


* **ownerEmail**: ドキュメントの所有者 


* **A**: 委任されたユーザーは、認証を行うユーザーまたはアプリケーションが別のユーザーの代理として動作しているときに指定され、none の場合は空になります。 


* **コンテキスト**: この同じコンテキストは、オプションの httpdelegate に転送されます



  
**戻り値**: 権限の一覧
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>Createprotectionハンドラ For発行非同期関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**: 保護設定 


* **オブザーバー**: protectionhandler:: observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト


  
### <a name="createprotectionhandlerforpublishing-function"></a>Createprotectionハンドラ Forpublishing 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**: 保護設定 


* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト



  
**戻り値**: protectionhandler
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**: 保護設定 


* **オブザーバー**: protectionhandler:: observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト


  
### <a name="createprotectionhandlerforconsumption-function"></a>Createprotectionハンドラ For従量課金関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**: 保護設定 


* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト



  
**戻り値**: protectionhandler