---
title: class mip::ProtectionEngine
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionengine クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 0bf87713b209e17d2728232f97f68946ca5d847f
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057646"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
特定の ID に関連する、保護関連のアクションを管理します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を取得します。
public void gettemplates async (const std:: shared_ptr\<protectionengine:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public std:: vector\<std:: string\> gettemplates (const std:: shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public void GetRightsForLabelIdAsync (const std:: string & documentId、const std:: string & lab d、const std:: string & owneremail、const std:: string & delegatedUserEmail、const std:: shared_ptr\<protectionengine:: Observer\>& オブザーバー、const std:: shared_ptr\<void\>& コンテキスト)  |  ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。
public std:: vector\<std:: string\> GetRightsForLabelId (const std:: string & documentId、const std:: string & lab d、const std:: string & owneremail、const std:: string & delegatedUserEmail、const std:: shared\<ptr\>& コンテキスト) (_s)  |  labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。
public void createprotectionハンドラ fromdescriptor async (const std:: shared_ptr\<protectiondescriptor\>& 記述子、const protectionハンドラのオプション & オプション、const std:: shared_ptr\<Protectionhandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<protectionhandler\> createprotectionhandler fromdescriptor (const std:: shared_ptr\<protectionhandler\>& descriptor、const protectionhandler/オプション& オプション、const std:: shared_ptr\<void\>& コンテキスト)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public void createprotectionハンドラ from発行 licenseasync (const std:: vector\<uint8_t\>& serializedPublishingLicense、const protectionハンドラ options & options、const std:: shared_ptr\<Protectionhandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& context)  |  シリアル化された発行ライセンスから保護ハンドラーを作成します。
public std:: shared_ptr\<protectionhandler\> createprotectionハンドラ from発行ライセンス (const std:: vector\<uint8_t\>& serializedPublishingLicense、constProtectionハンドラのオプション & オプション、const std:: shared_ptr\<void\>& context)  |  シリアル化された発行ライセンスから保護ハンドラーを作成します。
public void createprotectionhandler for発行非同期 (const protectionhandler::P ublishingsettings & 設定、const std:: shared_ptr\<protectionhandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& コンテキスト)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<protectionhandler\> createprotectionハンドラ forpublishing (const protectionhandler::P ublishingsettings & settings、const std:: shared_ptr\<void\>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public void CreateProtectionHandlerForConsumptionAsync (const protectionhandler:: ConsumptionSettings & settings、const std:: shared_ptr\<protectionhandler:: オブザーバー\>& オブザーバー、const std:: shared_ptr\<void\>& コンテキスト)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std:: shared_ptr\<protectionhandler\> createprotectionハンドラ for従量課金 (const protectionhandler:: ConsumptionSettings & settings, const std::\<shared_ptr\>void & context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を取得します。

  
次の**値を返し**ます。エンジンの設定
  
### <a name="gettemplatesasync-function"></a>Gettemplates Async 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **オブザーバー**:[Protectionengine:: Observer](class_mip_protectionengine_observer.md)インターフェイスを実装するクラス 


* **コンテキスト**:オブザーバーとオプションの[Httpdelegate](class_mip_httpdelegate.md)に不透明に渡されるクライアントコンテキスト


  
### <a name="gettemplates-function"></a>GetTemplates 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **コンテキスト**:省略可能な[Httpdelegate](class_mip_httpdelegate.md)に渡されるクライアントコンテキスト不透明



  
次の**値を返し**ます。テンプレート Id の一覧
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync 関数
ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**:ドキュメントメタデータに関連付けられているドキュメント ID 


* **labの登録 d**:[ラベル](class_mip_label.md)ドキュメントが作成されたドキュメントメタデータに関連付けられている ID 


* **ownerEmail**: ドキュメントの所有者 


* **A**: 委任されたユーザーは、認証を行うユーザーまたはアプリケーションが別のユーザーの代理として動作しているときに指定され、none の場合は空になります。 


* **オブザーバー**:[Protectionengine:: Observer](class_mip_protectionengine_observer.md)インターフェイスを実装するクラス 


* **コンテキスト**:この同じコンテキストは、 [Protectionengine:: observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function)または[Protectionengine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)に転送されます。


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 関数
labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**:ドキュメントメタデータに関連付けられているドキュメント ID 


* **labの登録 d**:[ラベル](class_mip_label.md)ドキュメントが作成されたドキュメントメタデータに関連付けられている ID 


* **Owneremail**:ドキュメントの所有者 


* **A**: 委任されたユーザーは、認証を行うユーザーまたはアプリケーションが別のユーザーの代理として動作しているときに指定され、none の場合は空になります。 


* **コンテキスト**:この同じコンテキストがオプションの[Httpdelegate](class_mip_httpdelegate.md)に転送されます



  
次の**値を返し**ます。権限の一覧
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>Createprotectionハンドラ From記述子 Async 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **記述子**:保護構成を記述する[Protectiondescriptor](class_mip_protectiondescriptor.md) 


* **オプション**:作成オプション 


* **オブザーバー**:[Protectionhandler:: Observer](class_mip_protectionhandler_observer.md)インターフェイスを実装するクラス 


* **コンテキスト**:オブザーバーとオプションの[Httpdelegate](class_mip_httpdelegate.md)に不透明に渡されるクライアントコンテキスト


> れこのメソッドは、Createprotectionハンドラ For発行非同期を優先するため、まもなく非推奨となります。
  
### <a name="createprotectionhandlerfromdescriptor-function"></a>Createprotectionハンドラ Fromdescriptor 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **記述子**:保護構成を記述する[Protectiondescriptor](class_mip_protectiondescriptor.md) 


* **オプション**:作成オプション 


* **コンテキスト**:省略可能な[Httpdelegate](class_mip_httpdelegate.md)に不透明に渡されるクライアントコンテキスト



  
次の**値を返し**ます。[ProtectionHandler](class_mip_protectionhandler.md)
> れこのメソッドは、Createprotectionハンドラ For発行非同期を優先するため、まもなく非推奨となります。
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>Createprotectionハンドラ From発行 Licenseasync 関数
シリアル化された発行ライセンスから保護ハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**:シリアル化された発行ライセンス 


* **オプション**:作成オプション 


* **オブザーバー**:[Protectionhandler:: Observer](class_mip_protectionhandler_observer.md)インターフェイスを実装するクラス 


* **コンテキスト**:オブザーバーとオプションの[Httpdelegate](class_mip_httpdelegate.md)に不透明に渡されるクライアントコンテキスト


> れこのメソッドは、CreateProtectionHandlerForConsumptionAsync を優先するとすぐに非推奨となります。
  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>Createprotectionハンドラ From発行ライセンス関数
シリアル化された発行ライセンスから保護ハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**:シリアル化された発行ライセンス 


* **オプション**:作成オプション 


* **オブザーバー**:[Protectionhandler:: Observer](class_mip_protectionhandler_observer.md)インターフェイスを実装するクラス 


* **コンテキスト**:省略可能な[Httpdelegate](class_mip_httpdelegate.md)に不透明に渡されるクライアントコンテキスト



  
次の**値を返し**ます。[ProtectionHandler](class_mip_protectionhandler.md)
> れこのメソッドは、Createprotectionハンドラ For従量課金を優先するため、間もなく非推奨となる予定です。
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>Createprotectionハンドラ For発行非同期関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**:保護設定 


* **オブザーバー**:[Protectionhandler:: Observer](class_mip_protectionhandler_observer.md)インターフェイスを実装するクラス 


* **コンテキスト**:オブザーバーとオプションの[Httpdelegate](class_mip_httpdelegate.md)に不透明に転送されるクライアントコンテキスト


  
### <a name="createprotectionhandlerforpublishing-function"></a>Createprotectionハンドラ Forpublishing 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**:保護設定 


* **コンテキスト**:省略可能な[Httpdelegate](class_mip_httpdelegate.md)に不透明転送されるクライアントコンテキスト



  
次の**値を返し**ます。[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**:保護設定 


* **オブザーバー**:[Protectionhandler:: Observer](class_mip_protectionhandler_observer.md)インターフェイスを実装するクラス 


* **コンテキスト**:オブザーバーとオプションの[Httpdelegate](class_mip_httpdelegate.md)に不透明に転送されるクライアントコンテキスト


  
### <a name="createprotectionhandlerforconsumption-function"></a>Createprotectionハンドラ For従量課金関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **設定**:保護設定 


* **コンテキスト**:省略可能な[Httpdelegate](class_mip_httpdelegate.md)に不透明転送されるクライアントコンテキスト



  
次の**値を返し**ます。[ProtectionHandler](class_mip_protectionhandler.md)