---
title: クラス ProtectionEngine
description: 'Microsoft Information Protection (MIP) SDK の protectionengine:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 61311ec2ac7c622099e9e7f56f22191e0287278c
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763904"
---
# <a name="class-protectionengine"></a>クラス ProtectionEngine 
特定の ID に関連する、保護関連のアクションを管理します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を取得します。
public std:: shared_ptr\<asynccontrol\> gettemplates async (const std:: shared_ptr\<protectionengine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public std:: vector\<std:: shared_ptr\<templatedescriptor\> \> gettemplates (const std:: shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public bool IsFeatureSupported (FeatureId featureId)  |  チェックがサポートされています。
public std:: shared_ptr\<asynccontrol\> GetRightsForLabelIdAsync (const std:: string& documentId、const std:: String& lab/d、const std:: string& owneremail、const std:: string& delegatedUserEmail、const std:: shared_ptr\<protectionengine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。
public std:: vector\<std:: string\> GetRightsForLabelId (const std:: string& documentId、const std:: String& lab d、const std:: string& owneremail、const std:: string& delegatedUserEmail、const std:: shared_ptr\<void\>& context)  |  labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。
public std:: shared_ptr\<asynccontrol\> createprotectionhandler for発行 Async (const Protectionhandler::P ublishingsettings& settings、const std:: shared_ptr\<protectionhandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<protectionhandler\> createprotectionハンドラ Forpublishing (const Protectionhandler::P ublishingsettings& settings、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<asynccontrol\> CreateProtectionHandlerForConsumptionAsync (const Protectionhandler:: ConsumptionSettings& settings、const std:: shared_ptr\<protectionhandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<protectionhandler\> createprotectionハンドラ For従量課金 (const Protectionhandler:: ConsumptionSettings& settings, const std::\<shared_ptr\> void& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public bool LoadUserCert (const std:: shared_ptr\<void\>& context)  |  によっ事前 load ユーザーライセンサー証明書。 prelicense を使用している場合は、別のネットワーク呼び出しが incurr 可能性があります。
public std:: shared_ptr\<asynccontrol\> loadusercertasync (const std:: shared_ptr\<protectionengine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  によっ事前 load ユーザーライセンサー証明書。 prelicense を使用している場合は、別のネットワーク呼び出しが incurr 可能性があります。
public void RegisterContentForTrackingAndRevocation (const std:: vector\<Uint8_t\>& serializedPublishingLicense、const std:: string& Contentname、bool isOwnerNotificationEnabled、const std:: shared_ptr\<void\>& context)  |  ドキュメント追跡 & 失効のために発行ライセンス (PL) を登録します。
public std:: shared_ptr\<asynccontrol\> RegisterContentForTrackingAndRevocationAsync (const std:: vector\<uint8_t\>& SerializedPublishingLicense、const std:: string& contentname、bool isOwnerNotificationEnabled、const Std:: shared_ptr\<protectionengine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  ドキュメント追跡 & 失効のために発行ライセンス (PL) を登録します。
public void RevokeContent (const std:: vector\<Uint8_t\>& serializedPublishingLicense、const std:: shared_ptr\<void\>& context)  |  コンテンツの失効を実行します。
public std:: shared_ptr\<asynccontrol\> RevokeContentAsync (const std:: vector\<uint8_t\>& serializedPublishingLicense、const Std:: shared_ptr\<protectionengine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  コンテンツの失効を実行します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を取得します。

  
**戻り値**: エンジンの設定
  
### <a name="gettemplatesasync-function"></a>Gettemplates Async 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **observer**: [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) インターフェイスを実装するクラス 


* **context**: オブザーバーと省略可能な HttpDelegate に不透明に返されるクライアント コンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="gettemplates-function"></a>GetTemplates 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **context**: 省略可能な HttpDelegate に不透明に渡されるクライアント コンテキスト



  
**戻り値**: テンプレート ID の一覧
  
### <a name="isfeaturesupported-function"></a>IsFeatureSupported 関数
チェックがサポートされています。

パラメーター:  
* **featureid**: 確認する機能の id



  
**戻り**値: ブール型の結果
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync 関数
ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**: ドキュメント メタデータに関連付けられているドキュメント ID 


* **Lab/d**: ドキュメントが作成されたドキュメントメタデータに関連付けられているラベル ID 


* **Owneremail**: ドキュメントの所有者 


* **A**: 委任されたユーザーは、認証を行うユーザーまたはアプリケーションが別のユーザーの代理として動作しているときに指定され、none の場合は空になります。 


* **observer**: ProtectionEngine::Observer インターフェイスを実装するクラス 


* **context**: この同じコンテキストが ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess または ProtectionEngine::Observer::OnGetRightsForLabelIdFailure に転送されます



  
**戻り値**: Async control オブジェクト。
  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 関数
labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**: ドキュメント メタデータに関連付けられているドキュメント ID 


* **Lab/d**: ドキュメントが作成されたドキュメントメタデータに関連付けられているラベル ID 


* **ownerEmail**: ドキュメントの所有者 


* **A**: 委任されたユーザーは、認証を行うユーザーまたはアプリケーションが別のユーザーの代理として動作しているときに指定され、none の場合は空になります。 


* **context**: この同じコンテキストが省略可能な HttpDelegate に転送されます



  
**戻り値**: 権限の一覧
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>Createprotectionハンドラ For発行非同期関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**: 保護設定 


* **observer**: [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
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


* **observer**: ProtectionHandler::Observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="createprotectionhandlerforconsumption-function"></a>Createprotectionハンドラ For従量課金関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**: 保護設定 


* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト



  
**戻り値**: protectionhandler
  
### <a name="loadusercert-function"></a>LoadUserCert 関数
によっ事前 load ユーザーライセンサー証明書。 prelicense を使用している場合は、別のネットワーク呼び出しが incurr 可能性があります。

パラメーター:  
* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト



  
は、正常に読み込まれた場合は True、それ以外の場合は false**を返し**ます。
  
### <a name="loadusercertasync-function"></a>LoadUserCertAsync 関数
によっ事前 load ユーザーライセンサー証明書。 prelicense を使用している場合は、別のネットワーク呼び出しが incurr 可能性があります。

パラメーター:  
* **observer**: ProtectionHandler::Observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="registercontentfortrackingandrevocation-function"></a>RegisterContentForTrackingAndRevocation 関数
ドキュメント追跡 & 失効のために発行ライセンス (PL) を登録します。

パラメーター:  
* **Contentname**: serializedPublishingLicense によって指定されたコンテンツに関連付けられている名前。 SerializedPublishingLicense でコンテンツ名を指定すると、その値が優先されます。 


* **isOwnerNotificationEnabled**: ドキュメントの暗号化が解除されるたびに電子メールで所有者に通知する場合は true に設定し、通知を送信しない場合は false に設定します。 


* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト


  
### <a name="registercontentfortrackingandrevocationasync-function"></a>RegisterContentForTrackingAndRevocationAsync 関数
ドキュメント追跡 & 失効のために発行ライセンス (PL) を登録します。

パラメーター:  
* **serializedPublishingLicense**: 保護されたコンテンツからのシリアル化された公開ライセンス 


* **Contentname**: serializedPublishingLicense によって指定されたコンテンツに関連付けられている名前。 SerializedPublishingLicense でコンテンツ名を指定すると、その値が優先されます。 


* **isOwnerNotificationEnabled**: ドキュメントの暗号化が解除されるたびに電子メールで所有者に通知する場合は true に設定し、通知を送信しない場合は false に設定します。 


* **observer**: ProtectionHandler::Observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="revokecontent-function"></a>RevokeContent 関数
コンテンツの失効を実行します。

パラメーター:  
* **serializedPublishingLicense**: 保護されたコンテンツからのシリアル化された公開ライセンス 


* **コンテキスト**: オプションの httpdelegate に不透明転送されるクライアントコンテキスト


  
### <a name="revokecontentasync-function"></a>RevokeContentAsync 関数
コンテンツの失効を実行します。

パラメーター:  
* **serializedPublishingLicense**: 保護されたコンテンツからのシリアル化された公開ライセンス 


* **observer**: ProtectionHandler::Observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。