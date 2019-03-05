---
title: class mip::ProtectionEngine
description: Mip::protectionengine クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ad364a0aff564fe50341f4f44b9cb4ab69c5aa60
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333655"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
特定の ID に関連する、保護関連のアクションを管理します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を取得します。
public void GetTemplatesAsync (const std::shared_ptr\<ProtectionEngine::Observer\>& observer、const std::shared_ptr\<void\>& コンテキスト)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public std::vector\<std::string\> GetTemplates(const std::shared_ptr\<void\>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public void GetRightsForLabelIdAsync (const std::string & documentId、const std::string & labelId、const std::string & ownerEmail、const std::shared_ptr\<ProtectionEngine::Observer\>& observer、const std:: shared_ptr\<void\>& コンテキスト)  |  ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。
public std::vector\<std::string\> GetRightsForLabelId (const std::string & documentId、const std::string & labelId、const std::string & ownerEmail、const std::shared_ptr\<void\>(& a) コンテキスト)  |  labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。
public void CreateProtectionHandlerFromDescriptorAsync (const std::shared_ptr\<ProtectionDescriptor\>& 記述子、const ProtectionHandlerCreationOptions & オプション、const std::shared_ptr\<ProtectionHandler::Observer\>& observer、const std::shared_ptr\<void\>& コンテキスト)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std::shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromDescriptor (const std::shared_ptr\<ProtectionDescriptor\>& 記述子、const ProtectionHandlerCreationOptions(& a) オプション, const std::shared_ptr\<void\>& コンテキスト)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public void CreateProtectionHandlerFromPublishingLicenseAsync (const std::vector\<uint8_t\>& serializedPublishingLicense、const ProtectionHandlerCreationOptions & オプション、const std::shared_ptr\<ProtectionHandler::Observer\>& observer、const std::shared_ptr\<void\>& コンテキスト)  |  シリアル化された発行ライセンスから保護ハンドラーを作成します。
public std::shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicense (const std::vector\<uint8_t\>& serializedPublishingLicense、constProtectionHandlerCreationOptions & オプション、const std::shared_ptr\<void\>& コンテキスト)  |  シリアル化された発行ライセンスから保護ハンドラーを作成します。
public void CreateProtectionHandlerFromProtectionInfoAsync (const std::vector\<uint8_t\>& serializedPublishingLicense、const std::vector\<uint8_t\>& serializedProtectionInfo、const std::shared_ptr\<ProtectionHandler::Observer\>& observer、const std::shared_ptr\<void\>& コンテキスト)  |  シリアル化された発行ライセンスと、情報をシリアル化された保護から、保護のハンドラーを作成します。
public std::shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromProtectionInfo (const std::vector\<uint8_t\>& serializedPublishingLicense、const std::vector\<uint8_t\>& serializedProtectionInfo、const std::shared_ptr\<void\>& コンテキスト)  |  シリアル化された発行ライセンスと、情報をシリアル化された保護から、保護のハンドラーを作成します。
public void CreateProtectionHandlerFromPublishingLicenseContextAsync (const PublishingLicenseContext & publishingLicenseContext、const ProtectionHandlerCreationOptions & オプション、const std::shared_ptr\<ProtectionHandler::Observer\>& observer、const std::shared_ptr\<void\>& コンテキスト)  |  発行ライセンス コンテキストから保護ハンドラーを作成します。
public std::shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicenseContext (const PublishingLicenseContext & publishingLicenseContext、const ProtectionHandlerCreationOptions (& a)オプション、const std::shared_ptr\<void\>& コンテキスト)  |  発行ライセンス コンテキストから保護ハンドラーを作成します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を取得します。

  
**返します**:エンジンの設定
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **オブザーバー**:実装するクラス、 [ProtectionEngine::Observer](class_mip_protectionengine_observer.md)インターフェイス 


* **コンテキスト**:不透明オブザーバーに渡されたと省略可能となるクライアント コンテキスト[HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="gettemplates-function"></a>GetTemplates 関数
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **コンテキスト**:クライアント コンテキスト不透明に渡される省略可能に[HttpDelegate](class_mip_httpdelegate.md)



  
**返します**:テンプレート Id の一覧
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync 関数
ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**:ドキュメント メタデータに関連付けられたドキュメント ID 


* **labelId**:[ラベル](class_mip_label.md)ドキュメントを作成するドキュメントのメタデータに関連付けられている ID 


* **ownerEmail**: ドキュメントの所有者 


* **オブザーバー**:実装するクラス、 [ProtectionEngine::Observer](class_mip_protectionengine_observer.md)インターフェイス 


* **コンテキスト**:この同じコンテキストに転送される[ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function)または[ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 関数
labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**:ドキュメント メタデータに関連付けられたドキュメント ID 


* **labelId**:[ラベル](class_mip_label.md)ドキュメントを作成するドキュメントのメタデータに関連付けられている ID 


* **ownerEmail**:ドキュメントの所有者 


* **コンテキスト**:このコンテキストは、省略可能に転送される[HttpDelegate](class_mip_httpdelegate.md)



  
**返します**:権限の一覧
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>CreateProtectionHandlerFromDescriptorAsync 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **記述子**:A [ProtectionDescriptor](class_mip_protectiondescriptor.md)保護構成を記述します。 


* **オプション**:作成オプション 


* **オブザーバー**:実装するクラス、 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)インターフェイス 


* **コンテキスト**:不透明オブザーバーに渡されたと省略可能となるクライアント コンテキスト[HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfromdescriptor-function"></a>CreateProtectionHandlerFromDescriptor 関数
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **記述子**:A [ProtectionDescriptor](class_mip_protectiondescriptor.md)保護構成を記述します。 


* **オプション**:作成オプション 


* **コンテキスト**:不透明オプションに渡されるクライアント コンテキスト[HttpDelegate](class_mip_httpdelegate.md)



  
**返します**:[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>CreateProtectionHandlerFromPublishingLicenseAsync 関数
シリアル化された発行ライセンスから保護ハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**:シリアル化された発行ライセンス 


* **オプション**:作成オプション 


* **オブザーバー**:実装するクラス、 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)インターフェイス 


* **コンテキスト**:不透明オブザーバーに渡されたと省略可能となるクライアント コンテキスト[HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>CreateProtectionHandlerFromPublishingLicense 関数
シリアル化された発行ライセンスから保護ハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**:シリアル化された発行ライセンス 


* **オプション**:作成オプション 


* **オブザーバー**:実装するクラス、 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)インターフェイス 


* **コンテキスト**:不透明オプションに渡されるクライアント コンテキスト[HttpDelegate](class_mip_httpdelegate.md)



  
**返します**:[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfromprotectioninfoasync-function"></a>CreateProtectionHandlerFromProtectionInfoAsync 関数
シリアル化された発行ライセンスと、情報をシリアル化された保護から、保護のハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**:シリアル化された発行ライセンス 


* **serializedProtectionInfo**:シリアル化された保護情報 


* **オブザーバー**:実装するクラス、 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)インターフェイス 


* **コンテキスト**:オブザーバーに不透明渡されるクライアント コンテキスト


  
### <a name="createprotectionhandlerfromprotectioninfo-function"></a>CreateProtectionHandlerFromProtectionInfo 関数
シリアル化された発行ライセンスと、情報をシリアル化された保護から、保護のハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**:シリアル化された発行ライセンス 


* **serializedProtectionInfo**:シリアル化された保護情報 


* **コンテキスト**:オブザーバーに不透明渡されるクライアント コンテキスト



  
**返します**:[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync-function"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync 関数
発行ライセンス コンテキストから保護ハンドラーを作成します。

パラメーター:  
* **publishingLicenseContext**:シリアル化された公開ライセンスの前処理されたフォーム 


* **オプション**:作成オプション 


* **オブザーバー**:実装するクラス、 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)インターフェイス 


* **コンテキスト**:不透明オブザーバーに渡されたと省略可能となるクライアント コンテキスト[HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicensecontext-function"></a>CreateProtectionHandlerFromPublishingLicenseContext 関数
発行ライセンス コンテキストから保護ハンドラーを作成します。

パラメーター:  
* **publishingLicenseContext**:シリアル化された公開ライセンスの前処理されたフォーム 


* **オプション**:作成オプション 


* **オブザーバー**:実装するクラス、 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)インターフェイス 


* **コンテキスト**:不透明オプションに渡されるクライアント コンテキスト[HttpDelegate](class_mip_httpdelegate.md)



  
**返します**:[ProtectionHandler](class_mip_protectionhandler.md)
