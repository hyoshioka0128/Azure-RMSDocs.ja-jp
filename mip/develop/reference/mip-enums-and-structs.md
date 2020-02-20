---
title: 参照構造体C++と列挙型用の MIP SDK
description: MIP C++ SDK の構造体と列挙型に関するリファレンスドキュメント。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2ee3c660a14df74f432870d364002cee86a5ce27
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489267"
---
# <a name="enumerations-and-structures"></a>列挙型と構造体

## <a name="namespace-mip"></a>名前空間 mip

Members                        | [説明]                                
--------------------------------|---------------------------------------------
enum WatermarkLayout       |  透かしのレイアウト。
enum ContentMarkAlignment       |  コンテンツマーク (コンテンツヘッダーまたはコンテンツフッター) の配置。
列挙型のメソッド       |  ドキュメントのラベルの割り当て方法。 ラベルの割り当てが自動的に行われたか、標準または特権操作 (管理者操作と同等) であったか。
ActionSource の列挙       |  SetLabel イベントのトリガーを定義します。
enum DataState       |  アプリケーションが動作するデータの状態を定義します。
enum ContentFormat       |  コンテンツ形式。
enum LabelFilterType       |  ラベルフィルターの種類、オプションのプロパティセット。リストの秘密度ラベルを呼び出すときにラベルをフィルター処理するために使用できます。
列挙型の FeatureId       |  新しい機能を名前で定義します。
列挙型の可変 Abmarkextmarkingtype       |  さまざまな動的フィールドは、既知のアプリケーションのテキストメッセージに設定できます。 $ {Item. Label} $ {Item.Name} $ {Item. Location} $ {User.Name} $ {PrincipalName} $ {} $ {} $ {DateTime} その他のものはまだ定義されていません。 sdk によってそれらが適切に置き換えられますこれらのコントロールフラグを使用する値。
enum Consent       |  サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。
列挙型の CacheStorageType       |  キャッシュのストレージの種類。
PFileExtensionBehavior の列挙       |  PFile の拡張機能の動作について説明します。
enum ErrorType       | _まだ文書化されていません。_
enum InspectorType       |  サポートされているファイルの種類に関連付けているインスペクターの種類。
列挙型 BodyType       |  ボディ型列挙子。
フライトの列挙機能       |  新しい機能を名前で定義します。
enum HttpRequestType       |  HTTP 要求の種類。
enum LogLevel       |  MIP SDK 全体で使用するさまざまなのログ レベル。
enum ProtectionType       |  保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。
enum ActionType       |  さまざまなアクション タイプ。
列挙型 LabelState       | _まだ文書化されていません。_
ActionDataType の列挙       | _まだ文書化されていません。_
列挙型 ConditionDataType       | _まだ文書化されていません。_
enum ContentMarkPlacement       | _まだ文書化されていません。_
enum LabelActionDataType       | _まだ文書化されていません。_
列挙型 ProtectionActionType       | _まだ文書化されていません。_
struct mip:: ApplicationInfo  |  アプリケーション固有の情報を含む構造体。
struct mip:: TelemetryConfiguration  |  カスタムテレメトリ設定 (一般的には使用されません)

### <a name="enumerations"></a>列挙体

#### <a name="watermarklayout-enum"></a>WatermarkLayout 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
位置            | 透かしレイアウトは水平方向です
)            | 透かしのレイアウトが斜めです

透かしのレイアウト。
  
#### <a name="contentmarkalignment-enum"></a>ContentMarkAlignment 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
LEFT            | コンテンツのマークが左に揃えられます
[RIGHT]            | コンテンツのマークが右側に揃います
CENTER            | コンテンツのマークは中央に配置されます

コンテンツマーク (コンテンツヘッダーまたはコンテンツフッター) の配置。
  
#### <a name="assignmentmethod-enum"></a>メソッドの列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
STANDARD            | ラベルの割り当て方法は標準です
インストラクション            | ラベルの割り当て方法は特権です
AUTO            | ラベルの割り当て方法は自動です

ドキュメントのラベルの割り当て方法。 ラベルの割り当てが自動的に行われたか、標準または特権操作 (管理者操作と同等) であったか。
  
#### <a name="actionsource-enum"></a>ActionSource 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
手動            | ユーザーによって手動で選択されました
自動            | ポリシー条件による設定
RECOMMENDED            | ポリシー条件によってラベルが推奨された後にユーザーが設定する
DEFAULT            | ポリシーに既定で設定する

SetLabel イベントのトリガーを定義します。
  
#### <a name="datastate-enum"></a>DataState 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
REST            | 物理的にデータベース/ファイル/ウェアハウスに格納されている非アクティブなデータ
動く            | ネットワークを通過するデータ、またはコンピューターのメモリ内で一時的に存在し、読み取りまたは更新されるデータ
USE            | データベース/ファイル/ウェアハウスなどに物理的に格納されている定数の変更によるアクティブなデータ

アプリケーションが動作するデータの状態を定義します。
  
#### <a name="contentformat-enum"></a>ContentFormat 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
DEFAULT            | コンテンツ形式は標準ファイル形式です
電子メール            | コンテンツ形式は電子メール形式です

コンテンツ形式。
  
#### <a name="labelfiltertype-enum"></a>LabelFilterType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
なし            | 既定のラベル付けのフィルターを無効にする
CustomProtection            | カスタム保護が発生する可能性のあるラベルをフィルター処理する
TemplateProtection            | 転送不可になる可能性のあるラベルをフィルターする。
% Forwardprotection            | テンプレートの保護が発生する可能性のあるラベルをフィルター処理する
AdhocProtection            | アドホック保護が発生する可能性のあるラベルをフィルター処理する
HyokProtection            | Hyok 保護が発生する可能性のあるラベルをフィルター処理する
PredefinedTemplateProtection            | 定義済みのテンプレート保護が発生する可能性のあるラベルをフィルター処理する
DoubleKeyProtection            | 2つのキーが必要な保護が発生する可能性のあるラベルをフィルターする (テンプレート、アドホック、dnf)

ラベルフィルターの種類、オプションのプロパティセット。リストの秘密度ラベルを呼び出すときにラベルをフィルター処理するために使用できます。
  
#### <a name="featureid-enum"></a>FeatureId 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
EncryptOnly            | サーバーで EncryptOnly 機能がサポートされているかどうかを確認する

新しい機能を名前で定義します。
  
#### <a name="variabletextmarkingtype-enum"></a>可変 Abingextmarkingtype 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
既定値            | 既知のマーキングが変換されました不明なマークが削除されました
PassThrough            | 既知のマーキングが変換されました不明なマークが渡されました
なし            | すべてのマーキングが渡されます。

さまざまな動的フィールドは、既知のアプリケーションのテキストメッセージに設定できます。 $ {Item. Label} $ {Item.Name} $ {Item. Location} $ {User.Name} $ {PrincipalName} $ {} $ {} $ {DateTime} その他のものはまだ定義されていません。 sdk によってそれらが適切に置き換えられますこれらのコントロールフラグを使用する値。
  
#### <a name="consent-enum"></a>同意の列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
AcceptAlways            | 同意し、この決定を記憶します
同意する            | 同意します (1 回限り)
却下            | 同意しません

サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。
  
#### <a name="cachestoragetype-enum"></a>CacheStorageType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
インメモリ            | メモリストレージ内
Ondisk です            | ディスク記憶域
OnDiskEncrypted            | 暗号化を使用するディスクストレージ (プラットフォームでサポートされている場合)

キャッシュのストレージの種類。
  
#### <a name="pfileextensionbehavior-enum"></a>PFileExtensionBehavior 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
既定値            | 拡張機能は SDK の既定の動作となります
PFileSuffix            | 拡張機能が <EXT>になります。PFILE
PPrefix            | 拡張機能は P<EXT> になります

PFile の拡張機能の動作について説明します。
  
#### <a name="errortype-enum"></a>ErrorType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 呼び出し元が無効な入力を渡しました。
INSUFFICIENT_BUFFER_ERROR            | 呼び出し元が小さすぎるバッファーを渡しました。
FILE_IO_ERROR            | 一般的なファイル IO エラー。
NETWORK_ERROR            | 一般的なネットワークの問題たとえば、到達できないサービスなどです。
INTERNAL_ERROR            | 予期しない内部エラー。
JUSTIFICATION_REQUIRED            | ファイルのアクションを完了するには理由が提供される必要があります。
NOT_SUPPORTED_OPERATION            | 要求された操作はまだサポートされていません。
PRIVILEGED_REQUIRED            | 新しいラベルのメソッドが標準である場合、特権ラベルをオーバーライドできません。
ACCESS_DENIED            | ユーザーはサービスにアクセスできませんでした。
CONSENT_DENIED            | ユーザーに同意を求めた操作で、同意が得られませんでした。
NO_PERMISSIONS            | ユーザーがコンテンツにアクセスできませんでした。 たとえば、アクセス許可はありません。コンテンツは失効します。
NO_AUTH_TOKEN            | 認証トークンが空であるため、ユーザーはコンテンツにアクセスできませんでした。
DISABLED_SERVICE            | サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした
PROXY_AUTH_ERROR            | プロキシ認証に失敗しました。
NO_POLICY            | ユーザー/テナントに対してポリシーが構成されていません
OPERATION_CANCELLED            | 操作が取り消されました。
ADHOC_PROTECTION_REQUIRED            | ファイルに対する操作を完了するには、アドホック保護を設定する必要があります
DEPRECATED_API            | 呼び出し元が非推奨の API を呼び出しました
TEMPLATE_NOT_FOUND            | テンプレート ID が認識されません
LABEL_NOT_FOUND            | ラベル ID が認識されません
LABEL_DISABLED            | ラベルが無効または非アクティブです
  
#### <a name="inspectortype-enum"></a>InspectorType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
不明            | 不明のファイルインスペクターです。
Msg (英語の可能性あり)            | Msg スタイルファイルインスペクター、rpq msg/msg ベース。

サポートされているファイルの種類に関連付けているインスペクターの種類。
  
#### <a name="bodytype-enum"></a>BodyType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
UNKNOWN            | 不明の本文の種類
拡張子            | テキストスタイルの本文の種類、エンコードは utf8 として返されます
HTML (HTML)            | HTML スタイルの本文型、エンコードは utf8 として返されます
RTF            | RTF スタイルの本文の種類、バイナリ形式

ボディ型列挙子。
  
#### <a name="flightingfeature-enum"></a>フライト機能列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
ServiceDiscovery            | 個別の HTTP 呼び出しに依存して RMS サービスエンドポイントを決定する
AuthInfoCache            | ドメイン/テナントごとに OAuth2 のチャレンジをキャッシュすることで、不要な401の応答を減らすことができます。 独自の HTTP 認証 (SPO、Edge など) を管理するアプリ/サービスに対して無効にする
LinuxEncryptedCache            | Linux プラットフォームの暗号化されたキャッシュを有効にします (この機能の前提条件をお読みください)
SingleDomainName            | Dns 参照に対して単一の会社名を有効にします。 例: [https://corprights](https://corprights)
PolicyAuth            | ポリシーサービスに送信される要求の自動 HTTP 認証を有効にします。 独自の HTTP 認証 (SPO、Edge など) を管理するアプリ/サービスに対して無効にする
UrlRedirectCache            | HTTP 操作の数を減らすためのキャッシュ URL のリダイレクト
PreLicensing            | ライセンス認証前の api チェックを有効にする
DoubleKey            | 2つのキー保護機能を有効にして、顧客キーを使用してで暗号化する
変数 Policyttl            | 変数ポリシーの有効期間を有効にし、無限ポリシーに戻す機能を無効にする
バリエーションのマーク            | 変数テキストのマークを有効にする

新しい機能を名前で定義します。
  
#### <a name="httprequesttype-enum"></a>HttpRequestType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
取得            | GET
Post            | POST

HTTP 要求の種類。
  
#### <a name="loglevel-enum"></a>LogLevel 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
トレース            | 
[情報]            | 
［警告］            | 
エラー            | 

MIP SDK 全体で使用するさまざまなのログ レベル。
  
#### <a name="protectiontype-enum"></a>ProtectionType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
TemplateBased            | ハンドルはテンプレートから作成されました
カスタム            | ハンドルはアドホックで作成されました

保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。
  
#### <a name="actiontype-enum"></a>ActionType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | ドキュメントのアクション タイプにコンテンツ フッターを追加します。
ADD_CONTENT_HEADER            | ドキュメントのアクション タイプにコンテンツ ヘッダーを追加します。
ADD_WATERMARK            | ドキュメントのアクション タイプ全体にウォーター マークを追加します。
カスタム            | カスタム定義のアクション タイプ。
JUSTIFY            | 正当化アクション タイプ。
METADATA            | メタ データ変更のアクション タイプ。
PROTECT_ADHOC            | アドホック ポリシーによる保護アクション タイプ。
PROTECT_BY_TEMPLATE            | テンプレートによる保護アクション タイプ。
PROTECT_DO_NOT_FORWARD            | 転送不可による保護アクション タイプ。
REMOVE_CONTENT_FOOTER            | コンテンツ フッターの削除アクション タイプ。
REMOVE_CONTENT_HEADER            | コンテンツ ヘッダーの削除アクション タイプ。
REMOVE_PROTECTION            | 保護の削除アクション タイプ。
REMOVE_WATERMARK            | ウォーターマークの削除アクション タイプ。
APPLY_LABEL            | ラベルの適用アクション タイプ。
RECOMMEND_LABEL            | ラベルの推奨アクション タイプ。
PROTECT_ADHOC_DK            | アドホック ポリシーによる保護アクション タイプ。
PROTECT_BY_TEMPLATE_DK            | テンプレートによる保護アクション タイプ。
PROTECT_DO_NOT_FORWARD_DK            | 転送不可による保護アクション タイプ。

さまざまなアクション タイプ。 CUSTOM は汎用的なアクション タイプです。 その他のアクション タイプは、すべて特定の意味を持つ特定のアクションです。
  
#### <a name="labelstate-enum"></a>LabelState 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
NoChange            | 
削除            | 
更新            | 
  
#### <a name="actiondatatype-enum"></a>ActionDataType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
カスタム            | 
保護            | 
ContentMarking            | 
AddWatermark            | 
[ラベル]            | 
  
#### <a name="conditiondatatype-enum"></a>ConditionDataType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
既定値            | 
検出感度            | 
  
#### <a name="contentmarkplacement-enum"></a>ContentMarkPlacement 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
ヘッダー            | 
フッター            | 
  
#### <a name="labelactiondatatype-enum"></a>LabelActionDataType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
おすすめ            | 
適用            | 
  
#### <a name="protectionactiontype-enum"></a>ProtectionActionType 列挙型
値                         | [説明]                                
--------------------------------|---------------------------------------------
カスタム            | 
テンプレート            | 
前面へ移動            | 
Adhoc            | 
表示するプロンプト            | 
Hyok            | 
事前に宣言するテンプレート            | 
RemoveProtection            | 
 

### <a name="structures"></a>構造体

#### <a name="struct-mipapplicationinfo"></a>struct mip:: ApplicationInfo 
アプリケーション固有の情報を含む構造体。
  
Members                        | [説明]                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  AAD ポータルで設定されたアプリケーション id (角かっこなしの GUID である必要があります)。
public std::string applicationName  |  アプリケーション名 ('; ' を除く有効な ASCII 文字のみを含める必要があります)
public std::string applicationVersion  |  使用されているアプリケーションのバージョン ('; ' を除く有効な ASCII 文字のみを含める必要があります)
  

##### <a name="applicationid-struct-member"></a>applicationId 構造体メンバー
AAD ポータルで設定されたアプリケーション id (角かっこなしの GUID である必要があります)。
  
##### <a name="applicationname-struct-member"></a>applicationName 構造体メンバー
アプリケーション名 ('; ' を除く有効な ASCII 文字のみを含める必要があります)
  
##### <a name="applicationversion-struct-member"></a>applicationVersion 構造体メンバー
使用されているアプリケーションのバージョン ('; ' を除く有効な ASCII 文字のみを含める必要があります)

#### <a name="struct-miptelemetryconfiguration"></a>struct mip:: TelemetryConfiguration 
カスタムテレメトリ設定 (一般的には使用されません)
  
Members                        | [説明]                                
--------------------------------|---------------------------------------------
public std:: string hostNameOverride  |  ホストテレメトリのインスタンス名。 設定されていない場合、MIP は独自のホストとして機能します。
public std:: string libraryNameOverride  |  代替テレメトリライブラリ (DLL) ファイル名。
public std:: shared_ptr\<HttpDelegate\> httpDelegateOverride  |  設定すると、このインスタンスによって HTTP 処理が管理されます
public std:: shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  設定した場合、非同期タスクの処理はこのインスタンスによって管理されます。テレメトリオブジェクトを保持できるため、taskDispatcherDelegateOverides を共有することはできません。また、taskDispatcher が解放されるまで、リリースを防ぐ必要があります。
public bool isNetworkDetectionEnabled  |  設定すると、テレメトリコンポーネントによってバックグラウンドスレッドでネットワークの状態が ping されます。
public bool isLocalCachingEnabled  |  設定すると、テレメトリコンポーネントはディスク上のキャッシュを使用します。
public bool isTraceLoggingEnabled  |  設定すると、テレメトリコンポーネントによって警告/エラーログがディスクに書き込まれます
public bool isTelemetryOptedOut  |  設定すると、必要なサービスデータテレメトリのみが送信されます
public bool isFastShutdownEnabled  |  設定した場合、シャットダウン時にイベントはアップロードされません。監査イベントはログ記録時に直ちにアップロードされます
public std:: map\<std:: string、std:: string\> customSettings  |  カスタムテレメトリ設定 >
  

##### <a name="hostnameoverride-struct-member"></a>hostNameOverride struct メンバー
ホストテレメトリのインスタンス名。 設定されていない場合、MIP は独自のホストとして機能します。
  
##### <a name="librarynameoverride-struct-member"></a>libraryNameOverride 構造体メンバー
代替テレメトリライブラリ (DLL) ファイル名。
  
##### <a name="httpdelegate"></a>HttpDelegate
設定すると、このインスタンスによって HTTP 処理が管理されます
  
##### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
設定した場合、非同期タスクの処理はこのインスタンスによって管理されます。テレメトリオブジェクトを保持できるため、taskDispatcherDelegateOverides を共有することはできません。また、taskDispatcher が解放されるまで、リリースを防ぐ必要があります。
  
##### <a name="isnetworkdetectionenabled-struct-member"></a>isNetworkDetectionEnabled struct メンバー
設定すると、テレメトリコンポーネントによってバックグラウンドスレッドでネットワークの状態が ping されます。
  
##### <a name="islocalcachingenabled-struct-member"></a>isLocalCachingEnabled 構造体メンバー
設定すると、テレメトリコンポーネントはディスク上のキャッシュを使用します。
  
##### <a name="istraceloggingenabled-struct-member"></a>isTraceLoggingEnabled struct メンバー
設定すると、テレメトリコンポーネントによって警告/エラーログがディスクに書き込まれます
  
##### <a name="istelemetryoptedout-struct-member"></a>isTelemetryOptedOut struct メンバー
設定すると、必要なサービスデータテレメトリのみが送信されます
  
##### <a name="isfastshutdownenabled-struct-member"></a>isFastShutdownEnabled 構造体メンバー
設定した場合、シャットダウン時にイベントはアップロードされません。監査イベントはログ記録時に直ちにアップロードされます
  
##### <a name="customsettings-struct-member"></a>customSettings 構造体メンバー
カスタムテレメトリ設定 >
