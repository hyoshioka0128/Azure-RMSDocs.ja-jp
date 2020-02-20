---
title: class mip::ProtectionEngine
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionengine クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 23f9f54a3f9701d0c9321b7ba643ed7dd3f47be1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486836"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
特定の ID に関連する、保護関連のアクションを管理します。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を取得します。
パブリック std:: shared_ptr\<AsyncControl\> Gettemplates Async (const std:: shared_ptr\<ProtectionEngine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public std:: vector\<std:: shared_ptr\<TemplateDescriptor\>\> GetTemplates (const std:: shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public bool IsFeatureSupported (FeatureId featureId)  |  チェックがサポートされています。
public std:: shared_ptr\<AsyncControl\> GetRightsForLabelIdAsync (const std:: string & documentId、const std:: string & Lab d、const std:: string & ownerEmail、const std:: string & delegatedUserEmail、const std:: shared_ptr\<ProtectionEngine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。
public std:: vector\<std:: string\> GetRightsForLabelId (const std:: string & documentId、const std:: string & Lab d、const std:: string & ownerEmail、const std:: string & delegatedUserEmail、const std:: shared_ptr\<void\>& context)  |  labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。
public std:: shared_ptr\<AsyncControl\> Createprotectionハンドラ For発行非同期 (const ProtectionHandler::P ublishingSettings & settings、const std:: shared_ptr\<ProtectionHandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<ProtectionHandler\> Createprotectionハンドラ Forpublishing (const ProtectionHandler::P ublishingSettings & settings、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<AsyncControl\> CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler:: ConsumptionSettings & settings、const std:: shared_ptr\<ProtectionHandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<ProtectionHandler\> Createprotectionハンドラ For従量課金 (const ProtectionHandler:: ConsumptionSettings & settings, const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public bool LoadUserCert (const std:: shared_ptr\<void\>& context)  |  によっ事前 load ユーザーライセンサー証明書。 prelicense を使用している場合は、別のネットワーク呼び出しが incurr 可能性があります。
public std:: shared_ptr\<AsyncControl\> LoadUserCertAsync (const std:: shared_ptr\<ProtectionEngine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  によっ事前 load ユーザーライセンサー証明書。 prelicense を使用している場合は、別のネットワーク呼び出しが incurr 可能性があります。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を取得します。

  
**戻り値**: エンジンの設定
  
### <a name="gettemplatesasync-function"></a>Gettemplates Async 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメータ:  
* **オブザーバー**: protectionengine:: observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーとオプションの httpdelegate に不透明に戻されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="gettemplates-function"></a>GetTemplates 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメータ:  
* **コンテキスト**: オプションの httpdelegate に不透明渡されるクライアントコンテキスト



  
**戻り値**: テンプレート ID の一覧
  
### <a name="isfeaturesupported-function"></a>IsFeatureSupported 関数
チェックがサポートされています。

パラメータ:  
* **featureid**: 確認する機能の id



  
**戻り**値: ブール型の結果
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync 関数
ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメータ:  
* **documentId**: ドキュメント メタデータに関連付けられているドキュメント ID 


* **Lab/d**: ドキュメントが作成されたドキュメントメタデータに関連付けられているラベル ID 


* **ownerEmail**: ドキュメントの所有者 


* **A**: 委任されたユーザーは、認証を行うユーザーまたはアプリケーションが別のユーザーの代理として動作しているときに指定され、none の場合は空になります。 


* **オブザーバー**: protectionengine:: observer インターフェイスを実装するクラス 


* **コンテキスト**: この同じコンテキストは protectionengine:: observer:: OnGetRightsForLabelIdSuccess または protectionengine:: observer:: OnGetRightsForLabelIdFailure に転送されます。



  
**戻り値**: Async control オブジェクト。
  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 関数
labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメータ:  
* **documentId**: ドキュメント メタデータに関連付けられているドキュメント ID 


* **Lab/d**: ドキュメントが作成されたドキュメントメタデータに関連付けられているラベル ID 


* **ownerEmail**: ドキュメントの所有者 


* **A**: 委任されたユーザーは、認証を行うユーザーまたはアプリケーションが別のユーザーの代理として動作しているときに指定され、none の場合は空になります。 


* **コンテキスト**: この同じコンテキストは、オプションの httpdelegate に転送されます



  
**戻り値**: 権限の一覧
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>Createprotectionハンドラ For発行非同期関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメータ:  
* **設定**: 保護設定 


* **オブザーバー**: protectionhandler:: observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="createprotectionhandlerforpublishing-function"></a>Createprotectionハンドラ Forpublishing 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメータ:  
* **設定**: 保護設定 


* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト



  
**戻り値**: protectionhandler
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメータ:  
* **設定**: 保護設定 


* **オブザーバー**: protectionhandler:: observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="createprotectionhandlerforconsumption-function"></a>Createprotectionハンドラ For従量課金関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメータ:  
* **設定**: 保護設定 


* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト



  
**戻り値**: protectionhandler
  
### <a name="loadusercert-function"></a>LoadUserCert 関数
によっ事前 load ユーザーライセンサー証明書。 prelicense を使用している場合は、別のネットワーク呼び出しが incurr 可能性があります。

パラメータ:  
* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト



  
は、正常に読み込まれた場合は True、それ以外の場合は false**を返し**ます。
  
### <a name="loadusercertasync-function"></a>LoadUserCertAsync 関数
によっ事前 load ユーザーライセンサー証明書。 prelicense を使用している場合は、別のネットワーク呼び出しが incurr 可能性があります。

パラメータ:  
* **オブザーバー**: protectionhandler:: observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。