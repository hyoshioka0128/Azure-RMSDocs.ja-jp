---
title: Microsoft Information Protection (MIP) SDK バージョンリリース履歴とサポートポリシー
description: MIP SDK のリリース履歴と変更メモをバージョンします。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/25/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: a678765835785dcb40aaf65e7f92e78fba67c73a
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74479112"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Microsoft Information Protection (MIP) SDK バージョンリリース履歴とサポートポリシー

## <a name="servicing"></a>サービス 

各一般公開 (GA) バージョンは、次の GA バージョンがリリースされると6か月間サポートされます。 ドキュメントには、サポートされていないバージョンに関する情報が含まれない場合があります。 修正プログラムと新機能は、最新の GA バージョンにのみ適用されます。

プレビューバージョンを運用環境にデプロイすることはできません。 代わりに、最新のプレビューバージョンを使用して、次の GA バージョンに含まれる新しい機能や修正をテストします。 最新のプレビューバージョンのみがサポートされています。

## <a name="release-history"></a>リリース履歴

サポートされているリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。 

> [!NOTE]
> マイナー修正は記載されていないので、SDK に問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が解決されていない場合は、最新のプレビュー バージョンを確認します。
>  
> テクニカルサポートについては、 [Stack Overflow Microsoft Information Protection フォーラム](https://stackoverflow.com/questions/tagged/microsoft-information-protection)を参照してください。 

## <a name="version-140"></a>バージョン (バージョン) 

**リリース日**: 2019 年11月6日

このバージョンでは、.NET パッケージ (Microsoft. InformationProtection. File) の保護 API のサポートが導入されています。

### <a name="sdk-changes"></a>SDK の変更内容
- パフォーマンスの向上とバグの修正
- StorageType 列挙型を CacheStorageType に変更しました
- Gnustl ではなく、libc + + への Android リンク
- 以前に非推奨とされた Api を削除しました
  - ファイル/ポリシー/プロファイル:: 設定は MipContext を使用して初期化する必要があります
  - ファイル/ポリシー/プロファイル:: 設定パス、アプリケーション情報、ロガーデリゲート、テレメトリ、およびログレベルの getter/setter が削除されました。 これらのプロパティは MipContext によって管理されます。
- Apple プラットフォームでのスタティックライブラリのサポートの強化
  - モノリシックスタティックライブラリ
    - libmip_file_sdk_static。
    - libmip_upe_sdk_static。
    - libmip_protection_sdk_static。
    - libmip_upe_and_protection_sdk_static。
  - 別のライブラリに抽出されたサードパーティの依存関係
    - libsqlite3
    - libssl. a
- Mip_telemetry .dll (mip_core にマージ) が削除されました。

### <a name="file-api"></a>ファイル API

- .RPMSG
  - 暗号化
  - String8 復号化のサポートを追加しました
- 構成可能な PFILE 拡張動作 (既定、<EXT>)。PFILE、または P<EXT>)
  - ProtectionSettings:: SetPFileExtensionBehavior

### <a name="policy-api"></a>ポリシー API

- 完全な C API
- 保護に関連付けられたラベルのフィルター処理を構成する
  - PolicyEngine:: 設定:: SetLabelFilter ()

### <a name="protection-api"></a>保護 API

- 以前に非推奨とされた Api を削除しました
  - ProtectionEngine:: Createprotectionハンドラ Fromdescriptor [Async] を削除しました (ProtectionEngine:: Createprotectionハンドラ Forpublishing [Async] を使用します)
  - ProtectionEngine:: Createprotectionハンドラ From発行ライセンス [Async] (ProtectionEngine:: Createprotectionハンドラ For従量課金の使用 [Async]) が削除されました
- 完全C#な API
- 完全な C API
  - V 1.3 C API preview からの c API 正規化の変更:
    - Mip_cc_storage_type 名前が mip_cc_cache_storage_type に変更されました
    - MIP_CC_AddProtectionProfileEngine 名前が MIP_CC_ProtectionProfile_AddEngine に変更されました
    - MIP_CC_CreateProtectionEngineSettingsForExistingEngine 名前が MIP_CC_CreateProtectionEngineSettingsWithEng に変更されました
    - MIP_CC_CreateProtectionEngineSettingsForNewEngine 名前が MIP_CC_CreateProtectionEngineSettingsWithIdentity に変更されました
    - MIP_CC_SetProtectionProfileSettingsHttpDelegate 名前が MIP_CC_ProtectionProfileSettings_SetHttpDelegate に変更されました
    - MIP_CC_CreateProtectionHandlerForConsumption 名前が MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption に変更されました
    - MIP_CC_CreateProtectionHandlerForPublishing 名前が MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing に変更されました
    - MIP_CC_GetProtectionEngineId 名前が MIP_CC_ProtectionEngine_GetEngineId に変更されました
    - MIP_CC_GetProtectionEngineTemplates 名前が MIP_CC_ProtectionEngine_GetTemplates に変更されました
    - MIP_CC_GetProtectionEngineTemplatesSize 名前が MIP_CC_ProtectionEngine_GetTemplatesSize に変更されました
    - MIP_CC_SetTelemetryConfigurationHttpDelegate 名前が MIP_CC_TelemetryConfiguration_SetHttpDelegate に変更されました
    - MIP_CC_SetTelemetryConfigurationHostName 名前が MIP_CC_TelemetryConfiguration_SetHostName に変更されました
    - MIP_CC_SetTelemetryConfigurationIsLocalCachingEnabled 名前が MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled に変更されました
    - MIP_CC_SetTelemetryConfigurationIsNetworkDetectionEnabled 名前が MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled に変更されました
    - MIP_CC_SetTelemetryConfigurationIsTelemetryOptedOut 名前が MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut に変更されました
    - MIP_CC_SetTelemetryConfigurationLibraryName 名前が MIP_CC_TelemetryConfiguration_SetLibraryName に変更されました
    - コンマ区切りの文字列バッファーではなく mip_cc_string_list に設定するために、MIP_CC_ProtectionEngine_GetRightsForLabelIdSize および更新された MIP_CC_ProtectionEngine_GetRightsForLabelId を削除しました
    - コンマ区切りの文字列バッファーではなく mip_cc_string_list に設定するために、MIP_CC_ProtectionHandler_GetRightsSize および更新された MIP_CC_ProtectionHandler_GetRights を削除しました
    - Mip_cc_guid ではなく文字列バッファーにデータを設定するために MIP_CC_ProtectionEngine_GetEngineIdSize および更新された MIP_CC_ProtectionEngine_GetEngineId を追加しました
    - MIP_CC_CreateProtectionDescriptorFromUserRights は ' mip_cc_dictionary ' ではなく ' mip_cc_dictionary ' パラメーターを受け取るようになりました
    - MIP_CC_ProtectionEngineSettings_SetCustomSettings は ' mip_cc_dictionary ' ではなく ' mip_cc_dictionary ' パラメーターを受け取るようになりました
    - MIP_CC_ProtectionProfileSettings_SetCustomSettings は ' mip_cc_dictionary ' ではなく ' mip_cc_dictionary ' パラメーターを受け取るようになりました
    - MIP_CC_TelemetryConfiguration_SetCustomSettings は ' mip_cc_dictionary ' ではなく ' mip_cc_dictionary ' パラメーターを受け取るようになりました
    - MIP_CC_CreateMipContext は ' isOfflineOnly ' および ' loggerDelegateOverride ' パラメーターを受け取ります


## <a name="version-130"></a>バージョン 1.3.0

**リリース日**: 2019 年8月22日

### <a name="new-features"></a>新機能

- `mip::MipContext` は、新しい最上位レベルのオブジェクトです。
- 保護された MSG ファイルの暗号化解除がサポートされるようになりました。
- メッセージの検査。 `mip::FileInspector` および `mip::FileHandler::InspectAsync()`経由でサポートされています。
- ディスク上のキャッシュが必要に応じて暗号化されるようになりました。
- 保護 API で中国ソブリン cloud がサポートされるようになりました。
- Android での Arm64 のサポート。
- IOS での Arm64e のサポート。
- エンドユーザーライセンス (使用可能) のキャッシュを無効にすることができるようになりました。
- pfile 暗号化が無効になっている可能性があり `mip::FileEngine::EnablePFile`
- HTTP 呼び出しの数を減らすことによる保護操作のパフォーマンスの向上
- 委任された id の詳細を `mip::Identity` から削除し、代わりに `mip::FileEngine::Settings`、`mip::ProtectionSettings`、`mip::PolicyEngine::Settings`、`mip::ProtectionHandler`の `PublishingSettings` と `ConsumptionSettings`に `DelegatedUserEmail` を追加しました。
- 以前に Lab/d を返した関数は、`mip::Label` オブジェクトを返すようになりました。

### <a name="changes"></a>変更点

* 以前のバージョンでは、`mip::ReleaseAllResources`を呼び出す必要がありました。 バージョン1.3 では、これが `mip::MipContext::~MipContext` または `mip::MipContext::Shutdown`で置き換えられます。
* `mip::LabelingOptions` から削除された `ActionSource` `mip::ExecutionState::GetNewLabelActionSource`
* `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` を `mip::ProtectionEngine::CreateProtectionHandlerForPublishing`に置き換えました。
* `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` を `mip::ProtectionEngine::CreateProtectionHandlerForConsumption`に置き換えました。
* `mip::PublishingLicenseContext` 名前を `mip::PublishingLicenseInfo` に変更して更新し、生のシリアル化されたバイトではなく、リッチフィールドを含むようにしました。
* `mip::PublishingLicenseInfo` には、公開ライセンス (PL) を解析した後の MIP に関連するデータが含まれています。
* `mip::TemplateNotFoundError` および `mip::LabelNotFoundError`、アプリケーションが、認識されないテンプレート ID またはラベル ID を渡したときにスローされます。
* `AcquireToken()` および `mip::AuthDelegate::OAuth2Challenge()`の要求パラメーターを使用したラベルベースの条件付きアクセスのサポートが追加されました。 この機能は、セキュリティとコンプライアンスセンターのポータルを通じて公開されていません。


## <a name="version-120"></a>バージョン 1.2.0

**リリース日**: 2019 年4月15日

### <a name="new-features"></a>新機能

 - テレメトリコンポーネントでは、クライアントアプリケーションが HttpDelegate でオーバーライドした場合でも、MIP の残りの部分と同じ HTTP スタックが使用されるようになりました。
 - クライアントアプリケーションは、プロファイルで TaskDispatcherDelegate をオーバーライドすることにより、非同期タスクのスレッド動作を制御できます。
 - 現在、RPQ MSG encryption がプレビュー段階にあります。
 - ファイル/ポリシー SDK 例外処理動作を保護 SDK に配置する:
    - プロキシが認証を要求するように構成されている場合、すべての Sdk によって ProxyAuthError がスローされました。
    - アプリケーションの mip:: AuthDelegate:: AcquireOAuth2Token の実装によって空の認証トークンが指定されている場合、すべての Sdk によって NoAuthTokenError がスローされました。
 - ポリシー SDK の HTTP キャッシュ機能が向上したため、必要な HTTP 呼び出しの数が半分に減りました。
 - エラーの検出とデバッグを改善するための、より豊富なログ/監査/テレメトリ。
 - AIP ラベルへの移行を容易にする外部/外部ラベルのサポート。
 - SCC から感度の種類をダウンロードするためのサードパーティ製アプリケーションのサポートを有効にしました。
 - より多くのテレメトリ設定が公開され、構成可能です (キャッシュ/スレッド動作など)。
 
### <a name="sdk-changes"></a>SDK の変更

 - mip_common .dll と mip_telemetry mip_core に分割されます。
 - Mip:: ContentState を mip::D ataState に名前変更し、アプリケーションが高レベルのデータと対話する方法を記述しました。
 - mip:: AdhocProtectionRequiredError exception は、ラベルを適用する前にアドホック保護を最初に適用する必要があることをアプリケーションに通知するために、FileHandler:: SetLabel によってスローされます。
 - mip:: Operationcancel/Error 例外は、操作がキャンセルされた場合にスローされます (シャットダウンや HTTP のキャンセルなどによって)。
 - 新しい API:
    - mip:: ClassificationResult:: GetSensitiveInformationDetections
    - mip:: FileEngine:: GetLastPolicyFetchTime
    - mip:: FileEngine:: GetDefaultSensitivityLabel
    - mip:: FileEngine:: GetPolicyId
    - mip:: FileEngine:: HasClassificationRules
    - mip:: FileEngine:: Settings:: SetPolicyCloudEndpointBaseUrl
    - mip:: FileHandler:: GetDecryptedTemporaryFileAsync
    - mip:: FileHandler:: Observer:: OnGetDecryptedTemporaryFileFailure
    - mip:: FileHandler:: Observer:: OnGetDecryptedTemporaryFileSuccess
    - mip:: File/Policy/ProtectionProfile:: SetTaskDispatcherDelegate
    - mip:: File/Policy/ProtectionProfile:: SetTelemetryConfiguration
    - mip:: HttpRequest:: GetBody は std:: string の代わりに std:: vector < uint8_t > を返します
    - mip:: HttpRequest:: GetId
    - mip::P olicyEngine:: GetLastPolicyFetchTime
    - mip::P olicyEngine:: GetPolicyId
    - mip::P olicyEngine:: HasClassificationRules
    - mip::P olicyEngine:: Settings:: SetCloudEndpointBaseUrl
    - mip::P rotectionDescriptor:: GetContentId
    - (インターフェイス) mip:: TaskDispatcherDelegate
 
### <a name="new-requirements"></a>新しい要件
 - プロセスを終了する前に mip:: ReleaseAllResources を呼び出す必要があります (すべてのプロファイル、エンジン、およびハンドラーへの参照をクリアした後)
 - (インターフェイス) mip:: ExecutionState:: GetClassificationResults の戻り値の型と "classificationIds" パラメーターが変更されました
 - (インターフェイス) mip:: FileExecutionState:: GetAuditMetadata をアプリケーションで実装すると、テナント管理者の監査ダッシュボードに公開する詳細情報を指定できます (送信者、受信者、最終更新など)。
 - (インターフェイス) mip:: FileExecutionState:: GetClassificationResults 戻り値の型が変更され、FileHandler パラメーターが必要になりました
 - (インターフェイス) mip:: FileExecutionState:: GetDataState は、アプリケーションが contentIdentifier と対話する方法を指定するために、アプリケーションによって実装される必要があります。
 - (インターフェイス) mip:: HttpDelegate インターフェイスには、' CancelOperation ' および ' CancelAllOperations ' メソッドが必要です
 - (インターフェイス) mip:: HttpDelegate インターフェイス ' Send ' と ' SendAsync ' は mip:: Httpresponse.cache の代わりに mip:: HttpOperation を返します
 - (インターフェイス) mip:: Httpresponse.cache:: GetBody は std:: string の代わりに std:: vector < uint8_t > を返します
 - (インターフェイス) mip:: Httpresponse.cache インターフェイスには ' GetId ' メソッドの実装が必要です
 - mip:: ContentLabel:: Getchrono Time は std:: string の代わりに std:::: time_point を返します
 - mip:: FileEngine:: Createfileハンドラ Async は ' contentIdentifier ' パラメーターを受け入れなくなりました
 - mip::P olicyHandler:: NotifyCommitedActions から mip::P olicyHandler:: NotifyCommittedActions に名前変更されました


## <a name="version-110"></a>バージョン 1.1.0

**リリース日**: 2019 年1月15日

このバージョンでは、次のプラットフォームのサポートが導入されています。

  - .NET
  - iOS SDK (ポリシー API)
  - Android SDK (ポリシー API と保護 API)

### <a name="new-features"></a>新機能

- ADRMS のサポート
- 保護 API の操作は (Win32 上で) 真の非同期であり、非ブロッキングの暗号化/復号化操作を同時に行うことができます。
  - アプリケーションコールバック (AuthDelegate、HTTPDelegate など) をバックグラウンドスレッドで呼び出すことができるようになりました
- IT 管理者によって設定されたカスタムラベルのプロパティを mip:: Label:: GetCustomSettings を使用して読み取ることができるようになりました。
- シリアル化された発行ライセンスをファイルから直接取得できるようになりました。 mip:: FileHandler:: GetSerializedPublishingLicense を使用して HTTP 操作を行う必要はありません。
- Mip:: Fileengine:: Observer:: OnAddPolicyEngineStarting/mip::P Olicyengine:: Observer:: OnAddEngineStarting を使用して mip:: FileEngine/mip::P olicyEngine の作成を完了するために HTTP 操作が必要かどうかがアプリケーションに通知されます。
- 保護されたコンテンツの有効期限が切れているかどうかを検出します。また、便宜的な方法 mip::P rotectionDescriptor::D oesContentExpire 切れ
- 分類:
  - 秘密度の種類 (CC # の、passport # などの正規表現式) は、SCC サービスから取得できます。
    - Mip:: FileEngine:: Settings/mip::P olicyEngine:: Settings フラグを設定して機能を有効にします
    - Mip:: FileEngine:: ListSensitivityTypes/mip::P olicyEngine:: ListSensitivityTypes を使用した型の読み取り
  - 外部ドキュメントスキャナーユーティリティからの分類の結果を MIP に渡すことで、ドキュメントの内容に基づいて推奨されるラベルや必要なラベルを作成できます。
    - Mip:: FileExecutionState:: GetClassificationResults/mip:: ExecutionState:: GetClassificationResults を使用して結果を MIP に渡します
    - mip:: ApplyLabelAction および mip:: RecommendLabelAction は mip::P olicyEngine:: ComputeActions によって返されます。分類の結果が、必須ラベルまたは推奨ラベルを示すポリシールールと一致する場合に使用します。

### <a name="new-requirements"></a>新しい要件 

  - Mip:: FileProfile、mip::P olicyProfile、mip::P rotectionProfile を作成するときに、ID/名前/バージョンフィールド mip:: ApplicationInfo を強制的に作成します
  - Mip:: Fileハンドラを作成するときは、アプリケーションで新しい mip:: FileExecutionState インターフェイスを実装する必要があります
  
### <a name="new-exceptions"></a>新しい例外 

  - mip:: NoAuthTokenError がスローされました (キャンセルにより、アプリケーションの AuthDelegate から空のトークンが返された場合)
    - 次の作成に適用されます:
      - mip:: FileEngine
      - mip:: FileHandler
      - mip::P olicyEngine
      - mip::P rotectionHandler
  - mip:: NoPolicyError が、テナントがラベルに対して構成されていない場合にスローされる
    - 次の作成に適用されます:
      - mip:: FileEngine
      - mip::P olicyEngine
  - 特定のユーザー/デバイス/プラットフォーム/テナントに対して RMS サービスが無効になっている場合、mip:: ServiceDisabledError がスローされる
    - 次の作成に適用されます:
      - mip:: FileHandler
      - mip::P rotectionHandler
  - mip:: NoPermissionsError は、ユーザーがドキュメントの暗号化を解除する権限を持っていないか、コンテンツの有効期限が切れている場合にスローされます。
    - 次の作成に適用されます:
      - mip:: FileHandler
      - mip::P rotectionHandler

## <a name="next-steps"></a>次のステップ

- サポートされているプラットフォームなどの詳細については[、MIP SDK に関する faq と問題](faqs-known-issues.md)を参照してください。
- MIP SDK の使用を開始する方法については、「 [MIP sdk のセットアップと構成](setup-configure-mip.md)」を参照してください。
