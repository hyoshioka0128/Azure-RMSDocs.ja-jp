---
title: Microsoft Information Protection (MIP) SDK バージョンリリース履歴とサポートポリシー
description: MIP SDK のバージョンリリース履歴と変更メモ。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/25/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: bd786925f22774c3e9173a69d88a08618da299fe
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760713"
---
# <a name="microsoft-information-protection-mip-software-development-kit-sdk-version-release-history-and-support-policy"></a>Microsoft Information Protection (MIP) ソフトウェア開発キット (SDK) バージョンリリース履歴とサポートポリシー

## <a name="servicing"></a>サービス 

各一般公開 (GA) バージョンは、次の GA バージョンがリリースされると6か月間サポートされます。 ドキュメントには、サポートされていないバージョンに関する情報が含まれない場合があります。 修正プログラムと新機能は、最新の GA バージョンにのみ適用されます。

プレビューバージョンを運用環境にデプロイすることはできません。 代わりに、最新のプレビューバージョンを使用して、次の GA バージョンに含まれる新しい機能や修正をテストします。 最新のプレビューバージョンのみがサポートされています。

## <a name="release-history"></a>リリース履歴

サポートされているリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。 

> [!NOTE]
> マイナー修正は記載されていないので、SDK に問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が解決されていない場合は、最新のプレビュー バージョンを確認します。
>  
> テクニカルサポートについては、 [Stack Overflow Microsoft Information Protection フォーラム](https://stackoverflow.com/questions/tagged/microsoft-information-protection)を参照してください。 

## <a name="version-16103"></a>バージョン1.6.103

**リリース日**: 2020 年4月16日

### <a name="general-sdk-changes"></a>一般的な SDK の変更

- TLS 1.2 は、ADRMS 以外のすべての HTTP 通信に適用されます。
- IOS/MacOS HTTP 実装を Nn 接続から Nの Lsession に移行した。
- Aria SDK から 1DS SDK に移行された iOS テレメトリコンポーネント。
- テレメトリコンポーネントでは、iOS、MacOs、Linux で MIP の HttpDelegate が使用されるようになりました。 (以前は win32 のみ)。
- C API のタイプセーフが改善されました。
- C++、C#、および Java Api で、プロファイルからの AuthDelegate をエンジンに移動しました。
- AuthDelegate がのコンストラクターから`Profile::Settings`に`Engine::Settings`移動しました。
- ポリシー同期に失敗した理由に関する詳細情報を提供するために、カテゴリを NoPolicyError に追加しました。
- メソッド`PolicyEngine::GetTenantId`を追加しました。
- 明示的なソブリン cloud のサポートが追加されました。
  - ターゲット`Engine::Settings::SetCloud`クラウド (GCC High、21 Vianet など) を設定する新しいメソッド。
  - 認識`Engine::Settings::SetCloudEndpointBaseUrl`されたクラウドでは、既存のメソッド呼び出しは不要になりました。
- IOS バイナリのビットコードを有効にしました。

### <a name="file-sdk"></a>ファイル SDK

- C# `IFileHandler::InspectAsync`および Java ラッパーに追加されました
- で`FileProfile::AcquirePolicyAuthToken`は、アプリケーションがトークンキャッシュをウォームアップできるようにするために、ポリシートークンの取得をトリガーするためのが新たにサポートされています。    
- `MsgInspector::GetAttachments`の`vector<shared_ptr<MsgAttachmentData>>`代わりにを返します。`vector<unique_ptr<MsgAttachmentData>>`
- `TelemetryConfiguration::isOptedOut`設定すると、テレメトリが完全に無効になります。 以前は、一連の最小のテレメトリが送信されていました。

### <a name="policy-sdk"></a>ポリシー SDK

- アプリケーションがを介し`PolicyProfile::AcquireAuthToken`てトークンキャッシュをウォームアップできるようにするための、トークン取得のトリガーの新しいサポート。
- 既定では、HYOK ラベルがフィルター処理されます。
- 削除されたラベルに関連付けられたメタデータが削除されます。
- キャッシュされたラベルポリシーと感度ポリシーが一致していない場合、ポリシーキャッシュはクリアされます。
- バージョン管理されたメタデータの新しいサポート:
  - ファイル形式は、ラベルメタデータの場所/形式を改訂する場合があります。 この場合、アプリケーションはすべてのメタデータを使用して MIP を提供する必要があり、mipmap はどのメタデータが "true" であるかを判断します。
  - `ContentLabel::GetExtendedProperties`では`vector<MetadataEntry>`なく、 `vector<pair<string, string>>`が返されるようになりました。
  - `MetadataAction::GetMetadataToAdd`では`vector<MetadataEntry>`なく、 `vector<pair<string, string>>`が返されるようになりました。
  - `ExecutionState::GetContentMetadata`ではなく`vector<MetadataEntry>`が返さ`vector<pair<string, string>>`れるようになりました。
  - `ExecutionState::GetContentMetadataVersion`は、現在のファイル形式 (通常は 0) に対してアプリケーションが認識するメタデータの最上位バージョンを返す必要があります。
  - `PolicyEngine::GetWxpMetadataVersion`テナント管理者によって構成された Office ドキュメントのメタデータバージョンを返します (0 = 既定、1 = coauth-有効形式)。
  - C API における同等の変更点:
    - `MIP_CC_ContentLabel_GetExtendedProperties`
    - `MIP_CC_MetadataAction_GetMetadataToAdd`
    - `mip_cc_metadata_callback`
    - `mip_cc_document_state`
    - `MIP_CC_PolicyEngine_GetWxpMetadataVersion`
- `TelemetryConfiguration::isOptedOut`設定すると、テレメトリが完全に無効になります。 以前は、一連の最小のテレメトリが送信されていました。 

### <a name="protection-sdk"></a>保護 SDK

- ドキュメント追跡の登録と取り消しの新しいサポート。
- 発行時に事前ライセンスを生成するための新しいサポート。
- 保護サービスによって使用される公開された Microsoft SSL 証明書を公開します。
   - `GetMsftCert` および `GetMsftCertPEM`
   - アプリケーションがインターフェイスを`HttpDelegate`オーバーライドする場合は、この CA によって発行されたサーバー証明書を信頼する必要があります。
   - この要件は、2020の後半で削除される予定です。    

## <a name="version-15124"></a>バージョン1.5.124

**リリース日**: 2020 年3月2日

### <a name="general-sdk-changes"></a>一般的な SDK の変更

- Java API (Windows のみ)
- 非同期 MIP タスクの取り消し
  - すべての非同期呼び出しは、Cancel () メソッドを使用して mip:: AsyncControl オブジェクトを返します
- 遅延読み込み依存バイナリ
- 必要に応じて特定のテレメトリ/監査プロパティをマスクする
   - Mip:: TelemetryConfiguration:: maskedProperties を使用して構成できます。
- 改善された例外:
  - すべてのエラーには、説明文字列に実行可能な相関 Id が含まれます
  - ネットワークエラーには ' Category '、' BaseUrl '、' RequestId '、および ' StatusCode ' フィールドがあります
- 改善された C API の結果/エラーの詳細

### <a name="file-sdk"></a>ファイル SDK

- ファイルがラベル付けまたは保護されているかどうかをネットワークで確認する
  - mip:: FileHandler:: IsLabeledOrProtected ()
  - 偽陽性の軽微なリスク (たとえば、ファイルにゾンビラベルのメタデータが含まれている場合)
- 特定の種類の保護に関連付けられているラベルをフィルター処理する
  - Mip:: FileEngine:: Settings:: SetLabelFilter () を使用して構成できます。
- ポリシーデータをファイル API に公開する
  - mip:: FileEngine:: GetPolicyDataXml ()

### <a name="policy-sdk"></a>ポリシー SDK

- 透かし/ヘッダー/フッターアクションの動的コンテンツマーク:
  - $ {Item. Label}、$ {Item.Name}、$ {User.Name}、$ {Event. DateTime} などのフィールドは、MIP によって自動的に設定されます
  - mip:: Id は、動的なコンテンツのマークによって使用されるわかりやすい "名前" フィールドを使用して作成できます。
  - Mip::P olicyEngine:: Settings:: Setバリエーション Abmarkextmarkingtype () を使用して構成できます。
- コンテンツにラベルが付けられているかどうかをネットワークで確認する
  - mip::P olicyHandler:: IsLabeled 付き ()
  - 偽陽性の軽微なリスク (たとえば、コンテンツにゾンビラベルのメタデータが含まれている場合)
- ラベルポリシーキャッシュ TTL
  - 既定値:30 日
  - Mip::P olicyProfile:: SetCustomSettings () を使用して構成可能
- **重大な変更**
  - 列挙型のリストから nullable ビットフィールドに更新されました。

### <a name="protection-sdk"></a>保護 SDK

- ライセンス前
  - 以前に取得したユーザー証明書と共に、暗号化されたコンテンツと共に事前ライセンスが存在する場合、コンテンツをオフラインで暗号化解除できます。
  - mip::P rotectionHandler:: ConsumptionSettings は、事前ライセンスを使用して作成できます。
  - mip::P rotectionEngine:: LoadUserCert |非同期 () は、mip::P rotectionProfile のキャッシュポリシーに従って格納されているユーザー証明書をフェッチします。
- サーバー固有の機能チェック
  - ユーザーのテナントが "暗号化のみ" 機能をサポートしているかどうかを確認します (Azure RMS でのみ利用可能)。
  - mip::P rotectionEngine:: IsFeatureSupported ()
- RMS テンプレートを取得するときの豊富な詳細情報
- **重大な変更**
  - `mip::ProtectionEngine::GetTemplates()``vector<shared_ptr<string>>`戻り値がに`vector<shared_ptr<mip::TemplateDescriptor>>`置き換えられました (C++)
  - `mip::ProtectionEngine::Observer::OnGetTemplatesSuccess()`コール`shared_ptr<vector<string>>`バックパラメーターが`vector<shared_ptr<mip::TemplateDescriptor>>`に置き換えられました (C++)
  - IProtectionEngine。 GetTemplates |Async () 戻り値`List<string>`がに`List<TemplateDescriptor>`置き換えられました。 (C#)
  - MIP_CC_ProtectionEngine_GetTemplates () mip_cc_guid * param mip_cc_template_descriptor * (C API) に置き換えられました

### <a name="c-api"></a>C API

- **重大な変更**: mip_cc_error * パラメーターを含むようにほとんどの関数が更新されました。 NULL にすることができます
  

### <a name="errorexception-updates"></a>エラー/例外の更新

- エラー処理の概要:
  - AccessDeniedError: ユーザーにコンテンツへのアクセス権が付与されていません
      - NoAuthTokenError: アプリは認証トークンを提供しませんでした
      - NoPermissionsError: ユーザーに特定のコンテンツへの権限が付与されていませんが、参照元または所有者が使用可能です
      - ServiceDisabledError: ユーザー/デバイス/プラットフォーム/テナントのサービスが無効になっています
  - AdhocProtectionRequiredError: ラベルを設定する前に、アドホック保護を設定する必要があります
  - BadInputError: ユーザー/アプリからの無効な入力
      - InsufficientBufferError: ユーザー/アプリからの無効なバッファー入力
      - LabelDisabledError: ラベル ID は認識されますが、使用することはできません
      - Labelnotfound エラー: ラベル ID が認識できません
      - Templatenotfound エラー: テンプレート ID が認識できません
  - ConsentDeniedError: ユーザー/アプリからの同意が必要な操作に同意が付与されていません
  - DeprecatedApiError: この API は非推奨とされました
  - FileIOError: ファイルの読み取り/書き込みに失敗しました
  - InternalError: 予期しない内部エラー
  - NetworkError
      - ProxyAuthenticationError: プロキシ認証が必要です
    - Category = BadResponse: サーバーが読み取り不可能な HTTP 応答を返しました (再試行が成功する可能性があります)
    - Category = canceled: 操作がユーザーまたはアプリによって取り消されたため、HTTP 接続を確立できませんでした (再試行は成功する場合があります)
    - Category = FailureResponseCode: サーバーが汎用エラー応答を返しました (再試行が成功する可能性があります)
    - Category = NoConnection: HTTP 接続を確立できませんでした (再試行が成功する可能性があります)
    - Category = Offline: アプリケーションがオフラインモードであるため、HTTP 接続を確立できませんでした (再試行は成功しません)
    - カテゴリ = プロキシ: プロキシの問題のため、HTTP 接続を確立できませんでした (再試行が成功しない可能性があります)
    - Category = SSL: SSL の問題のため、HTTP 接続を確立できませんでした (再試行が成功しない可能性があります)
    - カテゴリ = 調整済み: サーバーが "調整された" 応答を返しました (バックオフ/再試行が成功する場合があります)
    - Category = Timeout: タイムアウト後に HTTP 接続を確立できませんでした (再試行は成功する場合があります)
    - Category = UnexpectedResponse: サーバーから予期しないデータが返されました (再試行が成功する可能性があります)
  - NoPolicyError: テナントまたはユーザーがラベル用に構成されていません
  - NotSupportedError: 操作は現在の状態ではサポートされていません
  - Operationcancelのエラー: 操作が取り消されました
  - PrivilegedRequiredError: 割り当て方法が特権の場合を除き、ラベルを変更することはできません
- [変更点]
  - 未使用の PolicySyncError を削除しました。 NetworkError で置き換えられました
  - 使用されていないのを削除しました。 NetworkError カテゴリに置き換えられました

## <a name="version-140"></a>バージョン (バージョン) 

**リリース日**: 2019 年11月6日

このバージョンでは、.NET パッケージ (Microsoft. InformationProtection. File) の保護 SDK のサポートが導入されています。

### <a name="sdk-changes"></a>SDK の変更内容
- パフォーマンスの向上とバグの修正
- StorageType 列挙型を CacheStorageType に変更しました
- Gnustl ではなく、libc + + への Android リンク
- 廃止された、非推奨の Api を削除しました
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

### <a name="file-sdk"></a>ファイル SDK

- .RPMSG
  - 暗号化
  - String8 復号化のサポートを追加しました
- 構成可能な PFILE 拡張機能の<EXT>動作 (既定値、。PFILE または P<EXT>)
  - ProtectionSettings:: SetPFileExtensionBehavior

### <a name="policy-sdk"></a>ポリシー SDK

- 完全な C API
- 保護に関連付けられたラベルのフィルター処理を構成する
  - PolicyEngine:: 設定:: SetLabelFilter ()

### <a name="protection-sdk"></a>保護 SDK

- 廃止された、非推奨の Api を削除しました
  - ProtectionEngine:: Createprotectionハンドラ Fromdescriptor [Async] を削除しました (ProtectionEngine:: Createprotectionハンドラ Forpublishing [Async] を使用します)
  - ProtectionEngine:: Createprotectionハンドラ From発行ライセンス [Async] (ProtectionEngine:: Createprotectionハンドラ For従量課金の使用 [Async]) が削除されました
- 完全な C# API
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

- `mip::MipContext`は、新しい最上位レベルのオブジェクトです。
- 保護された MSG ファイルの暗号化解除がサポートされるようになりました。
- メッセージの検査。および`mip::FileInspector` `mip::FileHandler::InspectAsync()`でサポートされています。
- ディスク上のキャッシュが必要に応じて暗号化されるようになりました。
- 保護 SDK で中国ソブリン cloud がサポートされるようになりました。
- Android での Arm64 のサポート。
- IOS での Arm64e のサポート。
- エンドユーザーライセンス (使用可能) のキャッシュを無効にすることができるようになりました。
- . pfile 暗号化は、`mip::FileEngine::EnablePFile`
- HTTP 呼び出しの数を減らすことによる保護操作のパフォーマンスの向上
- から`mip::Identity`委任された id の詳細を`DelegatedUserEmail`削除`mip::FileEngine::Settings`し`mip::ProtectionSettings`、 `mip::PolicyEngine::Settings`代わりに、 `mip::ProtectionHandler`、 `PublishingSettings` 、 `ConsumptionSettings`、およびの各に追加しました。
- 以前に Labを返した関数は、オブジェクト`mip::Label`を返すようになりました。

### <a name="changes"></a>[変更点]

* 以前のバージョンでは、を呼び出す`mip::ReleaseAllResources`必要がありました。 バージョン1.3 は、これ`mip::MipContext::~MipContext`を`mip::MipContext::Shutdown`またはに置き換えます。
* および`ActionSource`から`mip::LabelingOptions`削除されました`mip::ExecutionState::GetNewLabelActionSource`
* で`mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` `mip::ProtectionEngine::CreateProtectionHandlerForPublishing`置き換えられます。
* で`mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` `mip::ProtectionEngine::CreateProtectionHandlerForConsumption`置き換えられます。
* 生`mip::PublishingLicenseContext`の`mip::PublishingLicenseInfo`シリアル化されたバイトではなく、リッチフィールドを含むように名前が変更され、更新されました。
* `mip::PublishingLicenseInfo`公開ライセンス (PL) を解析した後の MIP に関連するデータが含まれています。
* `mip::TemplateNotFoundError`また`mip::LabelNotFoundError` 、アプリケーションが、認識されないテンプレート id またはラベル id を渡すとスローされます。
* および`AcquireToken()` `mip::AuthDelegate::OAuth2Challenge()`の要求パラメーターを使用したラベルベースの条件付きアクセスのサポートが追加されました。 この機能は、セキュリティとコンプライアンスセンターのポータルを通じて公開されていません。


## <a name="version-120"></a>バージョン 1.2.0

**リリース日**: 2019 年4月15日

### <a name="new-features"></a>新機能

 - テレメトリコンポーネントでは、クライアントアプリケーションが HttpDelegate でオーバーライドした場合でも、MIP の残りの部分と同じ HTTP スタックが使用されるようになりました。
 - クライアントアプリケーションは、プロファイルで TaskDispatcherDelegate をオーバーライドすることにより、非同期タスクのスレッド動作を制御できます。
 - 現在、RPQ MSG encryption がプレビュー段階にあります。
 - ファイル/ポリシー SDK 例外処理動作を保護 SDK に配置する:
    - プロキシが認証を要求するように構成されている場合、すべての Sdk によって ProxyAuthError がスローされました。
    - アプリケーションの mip:: AuthDelegate:: AcquireOAuth2Token の実装によって空の認証トークンが指定されている場合、すべての Sdk によって NoAuthTokenError がスローされました。
 - ポリシー SDK の HTTP キャッシュ機能が改善され、必要な HTTP 呼び出しの数が半分に短縮されました。
 - エラーの検出とデバッグを改善するための、より豊富なログ/監査/テレメトリ。
 - AIP ラベルへの移行を容易にする外部/外部ラベルのサポート。
 - SCC から感度の種類をダウンロードするためのサードパーティ製アプリケーションのサポートを有効にしました。
 - より多くのテレメトリ設定が公開され、構成可能です (キャッシュ/スレッド動作など)。
 
### <a name="sdk-changes"></a>SDK の変更

 - mip_common .dll と mip_telemetry mip_core に分割されます。
 - Mip:: ContentState を mip::D ataState に名前変更し、アプリケーションが高レベルのデータと対話する方法を記述しました。
 - mip:: AdhocProtectionRequiredError exception は、ラベルを適用する前にアドホック保護を最初に適用する必要があることをアプリケーションに通知するために、FileHandler:: SetLabel によってスローされます。
 - mip:: Operationcancel/Error 例外は、操作がキャンセルされた場合にスローされます (シャットダウンや HTTP のキャンセルなどによって)。
 - 新しい Api:
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
    - mip:: HttpRequest:: GetBody は std:: string の代わりに std:: vector<uint8_t> を返します
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
 - (インターフェイス) mip:: Httpresponse.cache:: GetBody は std:: string の代わりに std:: vector<uint8_t> を返します
 - (インターフェイス) mip:: Httpresponse.cache インターフェイスには ' GetId ' メソッドの実装が必要です
 - mip:: ContentLabel:: Getchrono Time は std:: string の代わりに std:::: time_point を返します
 - mip:: FileEngine:: Createfileハンドラ Async は ' contentIdentifier ' パラメーターを受け入れなくなりました
 - mip::P olicyHandler:: NotifyCommitedActions から mip::P olicyHandler:: NotifyCommittedActions に名前変更されました


## <a name="version-110"></a>バージョン 1.1.0 

**リリース日**: 2019 年1月15日

このバージョンでは、次のプラットフォームのサポートが導入されています。

  - .NET
  - iOS SDK (ポリシー SDK)
  - Android SDK (ポリシー SDK および保護 SDK)

### <a name="new-features"></a>新機能

- ADRMS のサポート
- 保護 SDK の操作は (Win32 上で) 真の非同期であるため、非ブロッキングの暗号化/復号化操作を同時に行うことができます。
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
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - mip:: NoPolicyError が、テナントがラベルに対して構成されていない場合にスローされる
    - 次の作成に適用されます:
      - mip::FileEngine
      - mip::PolicyEngine
  - 特定のユーザー/デバイス/プラットフォーム/テナントに対して RMS サービスが無効になっている場合、mip:: ServiceDisabledError がスローされる
    - 次の作成に適用されます:
      - mip::FileHandler
      - mip::ProtectionHandler
  - mip:: NoPermissionsError は、ユーザーがドキュメントの暗号化を解除する権限を持っていないか、コンテンツの有効期限が切れている場合にスローされます。
    - 次の作成に適用されます:
      - mip::FileHandler
      - mip::ProtectionHandler

## <a name="next-steps"></a>次のステップ

- サポートされているプラットフォームなどの詳細については[、MIP SDK に関する faq と問題](faqs-known-issues.md)を参照してください。
- MIP SDK の使用を開始する方法については、「 [MIP sdk のセットアップと構成](setup-configure-mip.md)」を参照してください。
