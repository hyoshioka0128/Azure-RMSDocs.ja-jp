---
title: class mip ProtectionEngine
description: class mip ProtectionEngine のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ddc8cfd58acb2a80d024978084b625f3d3728c87
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446738"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
特定の ID に関連する、保護関連のアクションを管理します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  エンジンの設定を取得します。
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public std::vector<std::string> GetTemplates(const std::shared_ptr<void>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public void GetRightsForLabelIdAsync(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。
public std::vector<std::string> GetRightsForLabelId(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<void>& context)  |  labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。
public void GetGrantingLabelIdsAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  ユーザーが利用できるラベル ID のコレクションを取得します。
public std::vector<std::string> GetGrantingLabelIds(const std::shared_ptr<void>& context)  |  ユーザーが利用できるラベル ID のコレクションを取得します。
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromDescriptor(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  シリアル化された発行ライセンスから保護ハンドラーを作成します。
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicense(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  シリアル化された発行ライセンスから保護ハンドラーを作成します。
public void CreateProtectionHandlerFromPublishingLicenseContextAsync(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  発行ライセンス コンテキストから保護ハンドラーを作成します。
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicenseContext(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  発行ライセンス コンテキストから保護ハンドラーを作成します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
エンジンの設定を取得します。

  
**戻り値**: エンジンの設定
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **observer**: [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) インターフェイスを実装するクラス 


* **context**: オブザーバーと省略可能な [HttpDelegate](class_mip_httpdelegate.md) に不透明に返されるクライアント コンテキスト


  
### <a name="gettemplates"></a>GetTemplates
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **context**: 省略可能な [HttpDelegate](class_mip_httpdelegate.md) に不透明に渡されるクライアント コンテキスト



  
**戻り値**: テンプレート ID の一覧
  
### <a name="getrightsforlabelidasync"></a>GetRightsForLabelIdAsync
ラベル ID に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**: ドキュメント メタデータに関連付けられているドキュメント ID 


* **labelId**: ドキュメントの作成時に使用されたドキュメント メタデータに関連付けられている[ラベル](class_mip_label.md) ID 


* **ownerEmail**: ドキュメントの所有者 


* **observer**: [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) インターフェイスを実装するクラス 


* **context**: この同じコンテキストが [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) または [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure) に転送されます


  
### <a name="getrightsforlabelid"></a>GetRightsForLabelId
labelId に関する、ユーザーが利用可能な権限のコレクションを取得します。

パラメーター:  
* **documentId**: ドキュメント メタデータに関連付けられているドキュメント ID 


* **labelId**: ドキュメントの作成時に使用されたドキュメント メタデータに関連付けられている[ラベル](class_mip_label.md) ID 


* **ownerEmail**: ドキュメントの所有者 


* **context**: この同じコンテキストが省略可能な [HttpDelegate](class_mip_httpdelegate.md) に転送されます



  
**戻り値**: 権限の一覧
  
### <a name="getgrantinglabelidsasync"></a>GetGrantingLabelIdsAsync
ユーザーが利用できるラベル ID のコレクションを取得します。

パラメーター:  
* **observer**: [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) インターフェイスを実装するクラス 


* **context**: この同じコンテキストが [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) または ProtectionEngine::Observer::OnGrantingLabelIdsFailure に転送されます


  
### <a name="getgrantinglabelids"></a>GetGrantingLabelIds
ユーザーが利用できるラベル ID のコレクションを取得します。

パラメーター:  
* **context**: この同じコンテキストが省略可能な [HttpDelegate](class_mip_httpdelegate.md) に転送されます



  
**戻り値**: ラベル ID の一覧
  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **descriptor**: 保護構成を記述する [ProtectionDescriptor](class_mip_protectiondescriptor.md) 


* **options**: 作成オプション 


* **observer**: [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) インターフェイスを実装するクラス 


* **context**: オブザーバーと省略可能な [HttpDelegate](class_mip_httpdelegate.md) に不透明に返されるクライアント コンテキスト


  
### <a name="protectionhandler"></a>ProtectionHandler
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **descriptor**: 保護構成を記述する [ProtectionDescriptor](class_mip_protectiondescriptor.md) 


* **options**: 作成オプション 


* **context**: 省略可能な [HttpDelegate](class_mip_httpdelegate.md) に不透明に返されるクライアント コンテキスト



  
**戻り値**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
シリアル化された発行ライセンスから保護ハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**: シリアル化された発行ライセンス 


* **options**: 作成オプション 


* **observer**: [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) インターフェイスを実装するクラス 


* **context**: オブザーバーと省略可能な [HttpDelegate](class_mip_httpdelegate.md) に不透明に返されるクライアント コンテキスト


  
### <a name="protectionhandler"></a>ProtectionHandler
シリアル化された発行ライセンスから保護ハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**: シリアル化された発行ライセンス 


* **options**: 作成オプション 


* **observer**: [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) インターフェイスを実装するクラス 


* **context**: 省略可能な [HttpDelegate](class_mip_httpdelegate.md) に不透明に返されるクライアント コンテキスト



  
**戻り値**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync
発行ライセンス コンテキストから保護ハンドラーを作成します。

パラメーター:  
* **publishingLicenseContext**: シリアル化された発行ライセンスの前処理されたフォーム 


* **options**: 作成オプション 


* **observer**: [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) インターフェイスを実装するクラス 


* **context**: オブザーバーと省略可能な [HttpDelegate](class_mip_httpdelegate.md) に不透明に返されるクライアント コンテキスト


  
### <a name="protectionhandler"></a>ProtectionHandler
発行ライセンス コンテキストから保護ハンドラーを作成します。

パラメーター:  
* **publishingLicenseContext**: シリアル化された発行ライセンスの前処理されたフォーム 


* **options**: 作成オプション 


* **observer**: [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) インターフェイスを実装するクラス 


* **context**: 省略可能な [HttpDelegate](class_mip_httpdelegate.md) に不透明に返されるクライアント コンテキスト



  
**戻り値**: [ProtectionHandler](class_mip_protectionhandler.md)