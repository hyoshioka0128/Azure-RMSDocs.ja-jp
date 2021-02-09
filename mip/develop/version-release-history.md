---
title: Microsoft Information Protection (MIP) SDK バージョンリリース履歴とサポートポリシー
description: MIP SDK のバージョンリリース履歴と変更メモ。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/25/2019
ms.author: mbaldwin
ms.openlocfilehash: 3e3d32dd5e66ee6948567bc43ebd5ecfa16154b6
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215512"
---
# <a name="microsoft-information-protection-mip-software-development-kit-sdk-version-release-history-and-support-policy"></a>Microsoft Information Protection (MIP) ソフトウェア開発キット (SDK) バージョンリリース履歴とサポートポリシー

## <a name="servicing"></a>サービス

各一般公開 (GA) バージョンは、次の GA バージョンがリリースされると1年間サポートされます。 ドキュメントには、サポートされていないバージョンに関する情報が含まれない場合があります。 修正プログラムと新機能は、最新の GA バージョンにのみ適用されます。

プレビューバージョンを運用環境にデプロイすることはできません。 代わりに、最新のプレビューバージョンを使用して、次の GA バージョンに含まれる新しい機能や修正をテストします。 最新のプレビューバージョンのみがサポートされています。

## <a name="release-history"></a>リリース履歴

サポートされているリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。

> [!NOTE]
> 軽微な修正プログラムは記載されていません。 SDK で問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が解決されていない場合は、最新のプレビュー バージョンを確認します。
>  
> テクニカルサポートについては、 [Stack Overflow Microsoft Information Protection フォーラム](https://stackoverflow.com/questions/tagged/microsoft-information-protection)を参照してください。

## <a name="version-1886"></a>バージョン1.8.86

**リリース日:** 2021年1月13日

### <a name="general-changes"></a>一般的な変更

- ARM での Mac のサポートが追加されました。
- Mac 用のすべての .dylib ファイルが署名されています。
- すべてのクラウドは、3つの Sdk すべてで完全にサポートされています。
- `TelemetryConfiguration` の名前を `DiagnosticConfiguration` に変更します。
- で `MipContext` はなくを受け入れるように更新されました `DiagnosticConfiguration` `TelemetryConfiguration` 。
- 新しいとが公開さ `TelemetryDelegate` `AuditDelegate` れています。
- いくつかのカスタム設定の名前が変更され、バージョン1.9 で削除される予定です。 これらは、バージョン1.8 の更新プログラムの名前と同時に機能します。 

| 新しい名前          | 古い名前                   |
| ----------------- | -------------------------- |
| is_debug_audit    | is_debug_telemetry         |
| is_audit_disabled | is_built_in_audit_disabled |

### <a name="file-sdk"></a>ファイル SDK

- 2つのキー暗号化を使用したユーザー定義ラベルのサポートが追加されました。
- `MsgInspector.BodyType`メッセージファイルの本文エンコードの種類を公開する API を追加しました。
- User-Defined のアクセス許可を持つ二重キー暗号化をサポートするための Api を追加しました。
- のフラグが追加されました。これにより `mip::FileHandler` 、呼び出し元は監査検出イベントの送信を無効にできます。 これにより、API を使用すると重複する検出イベントが発生するシナリオが修正さ `ClassifyAsync()` れます。
- 次のようなバグを修正します。 
  - XPS ファイルの保護の設定に失敗しました。
  - SharePoint Online からアップロード/ダウンロードした後、またはカスタムのアクセス許可を削除した後に、ファイルを開くことはできません。
  - `RemoveProtection()` 関数は、メッセージを受信します。 "rpq msg" と入力します。 では、メッセージファイルのみが受け入れられるようになりました。
  - 保護されていないファイルを追跡または失効しようとしたときに発生したクラッシュ。

### <a name="policy-sdk"></a>ポリシー SDK

- `ActionId`Microsoft Office と SharePoint Online のラベル付きドキュメントの一貫性を確保するために、既定のメタデータプロパティから削除されました。
- Azure 管理範囲固有のラベルのサポートが追加されました。
- 各のデリゲートを使用してテレメトリと監査の両方をオーバーライドする機能が追加されました。
  - Audit delegate は、AIP 監査イベントを AIP Analytics 以外の宛先または AIP Analytics に送信する機能を提供します。
- `mip::PolicyHandler`呼び出し元が監査検出イベントの送信を検出できるようにするフラグをに追加しました。 これにより、API を使用すると重複する検出イベントが発生するシナリオが修正さ `ClassifyAsync()` れます。
- 特定のシナリオで暗号化されたポリシーデータベースを開くことができなかったバグを修正しました。
- `AuditDelegate`開発者が既定の MIPMAP SDK 監査パイプラインをオーバーライドし、独自のインフラストラクチャにイベントを送信できるようにする新しい機能が追加されています。 
- `mip::ClassifierUniqueIdsAndContentFormats` で `GetContentFormat()` はなくが返されるようになりました `std::string` `mip::ContentFormat` 。 この変更は、.NET ラッパーと Java ラッパーでレプリケートされます。 
- `ContentFormat.Default` がになりました `ContentFormat.File` 。

### <a name="protection-sdk"></a>保護 SDK

- True の `ProtectionEngineSettings.SetAllowCloudServiceOnly` 場合に Active Directory Rights Management サービスクラスターへの接続を禁止するプロパティが追加されました。 クラウド環境のみが使用されます。
- 委任ライセンスを取得するためのサポートを追加しました。
  - 委任ライセンスを使用すると、サービスはユーザーに代わってコンテンツのライセンスを取得できます。
  - これにより、サービスに対して追加の呼び出しを行わずに、サービスが権限のデータを表示し、ユーザーの代わりに復号化できるようになります。  

### <a name="java-wrapper-public-preview"></a>Java ラッパー (パブリックプレビュー)

- Java ラッパーの追跡と取り消しのサポートを追加しました。
- Java ラッパーにストリームサポートを追加しました

### <a name="c-api"></a>C API

- C API から **MIP_FLIGHTING_FEATURE_KEEP_PDF_LINEARIZATION** フラグが削除されました。

## <a name="version-17147"></a>バージョン1.7.147

### <a name="file-sdk"></a>ファイル SDK

- .PBIX ファイル形式のマイナーバグ修正。 

## <a name="version-17145"></a>バージョン1.7.145

**リリース日:** 2020年11月13日

### <a name="general-changes"></a>一般的な変更

- NuGet パッケージを更新して、常にではなく更新時にのみ依存関係をコピーするようにしました。
- .NET でのデバッグ構成では、ネイティブライブラリのリリースバージョンが使用されます。 リモートサーバーにデバッグモードで .NET ソリューションを展開するお客様は、VC + + デバッグランタイムをインストールする必要がありましたが、これは簡単ではありませんでした。 ネイティブライブラリにデバッグする必要がある場合は、SDK の再頒布可能パッケージからプロジェクトフォルダーに Dll をコピーしてください (https://ala.ms/mipsdkbins)
- .NET Core プロジェクトの警告を生成したバグを修正しました。

## <a name="version-17133"></a>バージョン1.7.133

**リリース日**: 2020 年9月23日

### <a name="general-sdk-changes"></a>一般的な SDK の変更

- パブリックプレビューは、Windows および Ubuntu 18.04 の Java で使用できます。
- .NET Core が Windows でサポートされるようになりました。
- Ubuntu 18.04 での .NET Core のパブリックプレビューのサポート。
- ストレージキャッシュの種類がに設定されている場合に、キーストアのローカルログ記録が向上しました。 `OnDiskEncrypted.`
- .Net ラッパーで機能フライトを有効にしました
- SDK テレメトリ動作を1.6 に戻しました。 最小テレメトリに対してのみオプトインを選択したときに、使用状況イベントの最小セットが送信されるようになりました。

### <a name="file-sdk"></a>ファイル SDK

- での UTF-16/UTF-8 本文変換を修正 `MSGInspector` します。
- File SDK によって保護されるファイルの最大ファイルサイズの既定値を 6 GB に設定します。
  - 使用可能なメモリ内のファイルサイズ *以上* を必要とする大きなファイルの暗号化解除によって行われた変更。
  - カスタム設定でオーバーライドでき `max_file_size_for_protection` ます。
- 線形補間 Pdf のサポートが追加されました。
- 変更イベントで LastModifiedDate が更新されなかったバグを修正しました。
- 保護された PDF の作成でのメモリリークを修正した。
- ファイル SDK は、追跡ファイルの失効をサポートしています。
- `FileEngine::Settings::SetLabelFilter` は非推奨です `ConfigureFunctionality` 。代わりにを使用してください。

### <a name="policy-sdk"></a>ポリシー SDK

- ポリシー SDK で、暗号化のみのラベル付け操作がサポートされるようになりました。
- キャッシュされた `mip::Identity` エンジンから正常に読み込まれなかったバグを修正しました。
- 分類 API で分類の GUID の比較で大文字と小文字が区別されるバグを修正しました。
- 新しいフィールドを追加して監査イベントを強化します。

### <a name="protection-sdk"></a>保護 SDK

- キャッシュされた `mip::Identity` エンジンから正常に読み込まれなかったバグを修正しました。
- 新しく作成された発行ライセンスの暗黙的な登録が追加されました。
- Office ファイルでの DKE のサポートに使用される暗号化アルゴリズムのサポートが追加されました。
- 作成 `documentId` さ `owner` れたパラメーターとパラメーター (省略可能)。

### <a name="c-apis"></a>C Api

- 不足している id と DKE Api が追加されました。
- `AuthDelegate`すべての sdk でプロファイルからエンジンに移動されました。
- C 用ポリシーの発行の SDK サンプル
- `MIP_CC_CreateProtectionEngineSettingsWithIdentity` は非推奨とされ `MIP_CC_CreateProtectionEngineSettingsWithIdentityAndAuthCallback` ます。代わりにを使用してください。
- `MIP_CC_CreateProtectionEngineSettingsWithEngineId` は非推奨とされ `MIP_CC_CreateProtectionEngineSettingsWithEngineIdAndAuthCallback` ます。代わりにを使用してください。
- `MIP_CC_CreateProtectionProfileSettings` 署名が変更されました。
- `MIP_CC_CreatePolicyEngineSettingsWithIdentity` は非推奨とされました。を使用 `MIP_CC_CreatePolicyEngineSettingsWithIdentityAndAuthCallback` してください。
- `MIP_CC_CreatePolicyEngineSettingsWithEngineId` は非推奨とされました。を使用 `MIP_CC_CreatePolicyEngineSettingsWithEngineIdAndAuthCallback` してください。
- `MIP_CC_PolicyEngineSettings_SetLabelFilter` は非推奨とされました。を使用 `MIP_CC_PolicyEngineSettings_ConfigureFunctionality` してください。
- `MIP_CC_CreatePolicyProfileSettings` 署名が変更されました。

### <a name="breaking-changes"></a>重大な変更

#### <a name="common"></a>共通

- `TelemetryConfiguration::isTelemetryOptedOut` が `isMinimalTelemetryEnabled` に変更されました。 

#### <a name="c-api"></a>C API

- `mip_cc_document_state`新しい値 contentmetadataversionformat で更新されました `mip_cc_metadata_version_format`

## <a name="version-16103"></a>バージョン1.6.103

**リリース日**: 2020 年4月16日

### <a name="general-sdk-changes"></a>一般的な SDK の変更

- TLS 1.2 は、ADRMS 以外のすべての HTTP 通信に適用されます。
- IOS/macOS HTTP 実装を Nn 接続から Nの Lsession に移行した。
- Aria SDK から 1DS SDK に移行された iOS テレメトリコンポーネント。
- テレメトリコンポーネントでは、iOS、macOs、Linux で MIP の HttpDelegate が使用されるようになりました。 (以前は win32 のみ)。
- C API のタイプセーフが改善されました。
- C++、C#、および Java Api で、プロファイルからの AuthDelegate をエンジンに移動しました。
- AuthDelegate がのコンストラクターから `Profile::Settings` に移動しました `Engine::Settings` 。
- ポリシー同期に失敗した理由に関する詳細情報を提供するために、カテゴリを NoPolicyError に追加しました。
- `PolicyEngine::GetTenantId`メソッドを追加しました。
- すべてのクラウドの明示的なサポートが追加されました。
  - `Engine::Settings::SetCloud`ターゲットクラウド (GCC High、21 Vianet など) を設定する新しいメソッド。
  - `Engine::Settings::SetCloudEndpointBaseUrl`認識されたクラウドでは、既存のメソッド呼び出しは不要になりました。
- IOS バイナリのビットコードを有効にしました。

### <a name="file-sdk"></a>ファイル SDK

- `IFileHandler::InspectAsync`C# および Java ラッパーに追加されました
- では、 `FileProfile::AcquirePolicyAuthToken` アプリケーションがトークンキャッシュをウォームアップできるようにするために、ポリシートークンの取得をトリガーするためのが新たにサポートされています。    
- `MsgInspector::GetAttachments`の代わりにを返します。 `vector<shared_ptr<MsgAttachmentData>>``vector<unique_ptr<MsgAttachmentData>>`
- `TelemetryConfiguration::isOptedOut` 設定すると、テレメトリが完全に無効になります。 以前は、一連の最小のテレメトリが送信されていました。

### <a name="policy-sdk"></a>ポリシー SDK

- アプリケーションがを介してトークンキャッシュをウォームアップできるようにするための、トークン取得のトリガーの新しいサポート `PolicyProfile::AcquireAuthToken` 。
- 既定では、HYOK ラベルがフィルター処理されます。
- 削除されたラベルに関連付けられたメタデータが削除されます。
- キャッシュされたラベルポリシーと感度ポリシーが一致していない場合、ポリシーキャッシュはクリアされます。
- バージョン管理されたメタデータの新しいサポート:
  - ファイル形式は、ラベルメタデータの場所/形式を改訂する場合があります。 この場合、アプリケーションはすべてのメタデータを使用して MIP を提供する必要があり、mipmap はどのメタデータが "true" であるかを判断します。
  - `ContentLabel::GetExtendedProperties` で `vector<MetadataEntry>` はなく、が返されるようになりました `vector<pair<string, string>>` 。
  - `MetadataAction::GetMetadataToAdd` で `vector<MetadataEntry>` はなく、が返されるようになりました `vector<pair<string, string>>` 。
  - `ExecutionState::GetContentMetadata` ではなくが返されるようになりました `vector<MetadataEntry>` `vector<pair<string, string>>` 。
  - `ExecutionState::GetContentMetadataVersion` は、現在のファイル形式 (通常は 0) に対してアプリケーションが認識するメタデータの最上位バージョンを返す必要があります。
  - `PolicyEngine::GetWxpMetadataVersion` テナント管理者によって構成された Office ドキュメントのメタデータバージョンを返します (0 = 既定、1 = coauth-有効形式)。
  - C API における同等の変更点:
    - `MIP_CC_ContentLabel_GetExtendedProperties`
    - `MIP_CC_MetadataAction_GetMetadataToAdd`
    - `mip_cc_metadata_callback`
    - `mip_cc_document_state`
    - `MIP_CC_PolicyEngine_GetWxpMetadataVersion`
- `TelemetryConfiguration::isOptedOut` 設定すると、テレメトリが完全に無効になります。 以前は、一連の最小のテレメトリが送信されていました。 

### <a name="protection-sdk"></a>保護 SDK

- ドキュメント追跡の登録と取り消しの新しいサポート。
- 発行時に事前ライセンスを生成するための新しいサポート。
- 保護サービスによって使用される公開済みの Microsoft TLS 証明書。
   - `GetMsftCert` および `GetMsftCertPEM`
   - アプリケーションが `HttpDelegate` インターフェイスをオーバーライドする場合は、この CA によって発行されたサーバー証明書を信頼する必要があります。
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
  - 既定:30 日
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
  - `mip::ProtectionEngine::GetTemplates()``vector<shared_ptr<string>>`戻り値がに置き換えられました `vector<shared_ptr<mip::TemplateDescriptor>>` (C++)
  - `mip::ProtectionEngine::Observer::OnGetTemplatesSuccess()` コールバック `shared_ptr<vector<string>>` パラメーターがに置き換えられました `vector<shared_ptr<mip::TemplateDescriptor>>` (C++)
  - IProtectionEngine。 GetTemplates |Async () 戻り値 `List<string>` がに置き換えられました `List<TemplateDescriptor>` 。 (C#)
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
- 以前に非推奨とされた Api の削除
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
- 削除された mip_telemetry.dll (mip_core.dll にマージ)

### <a name="file-sdk"></a>ファイル SDK

- .RPMSG
  - 暗号化
  - String8 復号化のサポートを追加しました
- 構成可能な PFILE 拡張機能の動作 (既定値、 <EXT> 。PFILE または P <EXT> )
  - ProtectionSettings:: SetPFileExtensionBehavior

### <a name="policy-sdk"></a>ポリシー SDK

- 完全な C API
- 保護に関連付けられたラベルのフィルター処理を構成する
  - PolicyEngine:: 設定:: SetLabelFilter ()

### <a name="protection-sdk"></a>保護 SDK

- 以前に非推奨とされた Api の削除
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

- `mip::MipContext` は、新しい最上位レベルのオブジェクトです。
- 保護された MSG ファイルの暗号化解除がサポートされるようになりました。
- メッセージの検査。およびでサポートされて `mip::FileInspector` い `mip::FileHandler::InspectAsync()` ます。
- ディスク上のキャッシュが必要に応じて暗号化されるようになりました。
- 保護 SDK が中国語のクラウドのお客様をサポートするようになりました。
- Android での Arm64 のサポート。
- IOS での Arm64e のサポート。
- エンドユーザーライセンス (使用可能) のキャッシュを無効にすることができるようになりました。
- . pfile 暗号化は、 `mip::FileEngine::EnablePFile`
- HTTP 呼び出しの数を減らすことによる保護操作のパフォーマンスの向上
- から委任された id の詳細を削除 `mip::Identity` し、代わりに、、、 `DelegatedUserEmail` `mip::FileEngine::Settings` `mip::ProtectionSettings` `mip::PolicyEngine::Settings` 、および `mip::ProtectionHandler` の各 `PublishingSettings` に追加しました `ConsumptionSettings` 。
- 以前に Labを返した関数は、オブジェクトを返すようになりました `mip::Label` 。

### <a name="changes"></a>[変更点]

* 以前のバージョンでは、を呼び出す必要がありました `mip::ReleaseAllResources` 。 バージョン 1.3 `mip::MipContext::~MipContext` は、これをまたはに置き換え `mip::MipContext::Shutdown` ます。
* `ActionSource`およびから削除されました `mip::LabelingOptions``mip::ExecutionState::GetNewLabelActionSource`
* で置き換えら `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` `mip::ProtectionEngine::CreateProtectionHandlerForPublishing` れます。
* で置き換えら `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` `mip::ProtectionEngine::CreateProtectionHandlerForConsumption` れます。
* `mip::PublishingLicenseContext` `mip::PublishingLicenseInfo` 生のシリアル化されたバイトではなく、リッチフィールドを含むように名前が変更され、更新されました。
* `mip::PublishingLicenseInfo` 公開ライセンス (PL) を解析した後の MIP に関連するデータが含まれています。
* `mip::TemplateNotFoundError` また、 `mip::LabelNotFoundError` アプリケーションが、認識されないテンプレート id またはラベル id を渡すとスローされます。
* およびの要求パラメーターを使用したラベルベースの条件付きアクセスのサポートが追加されました `AcquireToken()` `mip::AuthDelegate::OAuth2Challenge()` 。 この機能は、セキュリティとコンプライアンスセンターのポータルを通じて公開されていません。


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

 - mip_common.dll mip_core.dll と mip_telemetry.dll に分割されます。
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

## <a name="next-steps"></a>次の手順

- サポートされているプラットフォームなどの詳細については [、MIP SDK に関する faq と問題](faqs-known-issues.md) を参照してください。
- MIP SDK の使用を開始する方法については、「 [MIP sdk のセットアップと構成](setup-configure-mip.md) 」を参照してください。
