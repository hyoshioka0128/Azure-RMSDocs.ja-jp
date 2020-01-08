---
title: 参照構造体C++と列挙型用の MIP SDK
description: MIP C++ SDK の構造体と列挙型に関するリファレンスドキュメント。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2a641ace68d6999e3d452fa7f5c014ec1215556a
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556012"
---
# <a name="enumerations-and-structures"></a>列挙型と構造体

## <a name="namespace-mip"></a>名前空間 mip

[メンバー]                        | 説明                                
--------------------------------|---------------------------------------------
enum WatermarkLayout       |  透かしのレイアウト。
enum ContentMarkAlignment       |  コンテンツマーク (コンテンツヘッダーまたはコンテンツフッター) の配置。
列挙型のメソッド       |  ドキュメントのラベルの割り当て方法。 ラベルの割り当てが自動的に行われたか、標準または特権操作 (管理者操作と同等) であったか。
ActionSource の列挙       |  SetLabel イベントのトリガーを定義します。
enum DataState       |  アプリケーションが動作するデータの状態を定義します。
enum ContentFormat       |  コンテンツ形式。
enum LabelFilterType       |  ラベルフィルターの種類、オプションのプロパティセット。リストの秘密度ラベルを呼び出すときにラベルをフィルター処理するために使用できます。
enum Consent       |  サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。
列挙型の CacheStorageType       |  キャッシュのストレージの種類。
PFileExtensionBehavior の列挙       |  PFile の拡張機能の動作について説明します。
enum ErrorType       | まだ文書化されていません。
enum InspectorType       |  サポートされているファイルの種類に関連付けているインスペクターの種類。
列挙型 BodyType       |  ボディ型列挙子。
フライトの列挙機能       |  新しい機能を名前で定義します。
enum HttpRequestType       |  HTTP 要求の種類。
enum LogLevel       |  MIP SDK 全体で使用するさまざまなのログ レベル。
enum ProtectionType       |  保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。
enum ActionType       |  さまざまなアクション タイプ。
列挙型 LabelState       | まだ文書化されていません。
ActionDataType の列挙       | まだ文書化されていません。
列挙型 ConditionDataType       | まだ文書化されていません。
enum ContentMarkPlacement       | まだ文書化されていません。
enum LabelActionDataType       | まだ文書化されていません。
列挙型 ProtectionActionType       | まだ文書化されていません。
struct mip:: ApplicationInfo  |  アプリケーション固有の情報を含む構造体。
struct mip:: TelemetryConfiguration  |  カスタムテレメトリ設定 (一般的には使用されません)

### <a name="enumerations"></a>列挙

#### <a name="watermarklayout-enum"></a>WatermarkLayout 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
位置            | 透かしレイアウトは水平方向です
)            | 透かしのレイアウトが斜めです
透かしのレイアウト。
  
#### <a name="contentmarkalignment-enum"></a>ContentMarkAlignment 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
LEFT            | コンテンツのマークが左に揃えられます
RIGHT            | コンテンツのマークが右側に揃います
センター            | コンテンツのマークは中央に配置されます
コンテンツマーク (コンテンツヘッダーまたはコンテンツフッター) の配置。
  
#### <a name="assignmentmethod-enum"></a>メソッドの列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
STANDARD            | ラベルの割り当て方法は標準です
インストラクション            | ラベルの割り当て方法は特権です
AUTO            | ラベルの割り当て方法は自動です
ドキュメントのラベルの割り当て方法。 ラベルの割り当てが自動的に行われたか、標準または特権操作 (管理者操作と同等) であったか。
  
#### <a name="actionsource-enum"></a>ActionSource 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
MANUAL            | ユーザーによって手動で選択されました
AUTOMATIC            | ポリシー条件による設定
RECOMMENDED            | ポリシー条件によってラベルが推奨された後にユーザーが設定する
DEFAULT            | ポリシーに既定で設定する
SetLabel イベントのトリガーを定義します。
  
#### <a name="datastate-enum"></a>DataState 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
REST            | 物理的にデータベース/ファイル/ウェアハウスに格納されている非アクティブなデータ
動く            | ネットワークを通過するデータ、またはコンピューターのメモリ内で一時的に存在し、読み取りまたは更新されるデータ
USE            | データベース/ファイル/ウェアハウスなどに物理的に格納されている定数の変更によるアクティブなデータ
アプリケーションが動作するデータの状態を定義します。
  
#### <a name="contentformat-enum"></a>ContentFormat 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
DEFAULT            | コンテンツ形式は標準ファイル形式です
電子メール            | コンテンツ形式は電子メール形式です
コンテンツ形式。
  
#### <a name="labelfiltertype-enum"></a>LabelFilterType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
None            | 既定のラベル付けのフィルターを無効にする
カスタム            | カスタム保護が発生する可能性のあるラベルをフィルター処理する
TemplateProtection            | 転送不可になる可能性のあるラベルをフィルターする。
% Forwardprotection            | テンプレートの保護が発生する可能性のあるラベルをフィルター処理する
AdhocProtection            | アドホック保護が発生する可能性のあるラベルをフィルター処理する
HyokProtection            | Hyok 保護が発生する可能性のあるラベルをフィルター処理する
事前に宣言するテンプレート            | 定義済みのテンプレート保護が発生する可能性のあるラベルをフィルター処理する
ラベルフィルターの種類、オプションのプロパティセット。リストの秘密度ラベルを呼び出すときにラベルをフィルター処理するために使用できます。
  
#### <a name="consent-enum"></a>同意の列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
AcceptAlways            | 同意し、この決定を記憶します
同意する            | 同意します (1 回限り)
[拒否]            | 同意しません
サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。
  
#### <a name="cachestoragetype-enum"></a>CacheStorageType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
インメモリ            | メモリストレージ内
Ondisk です            | ディスク記憶域
OnDiskEncrypted            | 暗号化を使用するディスクストレージ (プラットフォームでサポートされている場合)
キャッシュのストレージの種類。
  
#### <a name="pfileextensionbehavior-enum"></a>PFileExtensionBehavior 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
既定            | 拡張機能は SDK の既定の動作となります
PFileSuffix            | 拡張機能が <EXT>になります。PFILE
PPrefix            | 拡張機能は P<EXT> になります
PFile の拡張機能の動作について説明します。
  
#### <a name="errortype-enum"></a>ErrorType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 呼び出し元が無効な入力を渡しました。
FILE_IO_ERROR            | 一般的なファイル IO エラー。
NETWORK_ERROR            | 一般的なネットワークの問題たとえば、到達できないサービスなどです。
TRANSIENT_NETWORK_ERROR            | 一時的なネットワークの問題たとえば、ゲートウェイが正しくありません。
INTERNAL_ERROR            | 予期しない内部エラー。
JUSTIFICATION_REQUIRED            | ファイルのアクションを完了するには理由が提供される必要があります。
NOT_SUPPORTED_OPERATION            | 要求された操作はまだサポートされていません。
PRIVILEGED_REQUIRED            | 新しいラベルのメソッドが標準である場合、特権ラベルをオーバーライドできません。
ACCESS_DENIED            | ユーザーはサービスにアクセスできませんでした。
CONSENT_DENIED            | ユーザーに同意を求めた操作で、同意が得られませんでした。
POLICY_SYNC_ERROR            | ポリシー データを同期しようとして失敗しました。
NO_PERMISSIONS            | ユーザーがコンテンツにアクセスできませんでした。 たとえば、アクセス許可はありません。コンテンツは失効します。
NO_AUTH_TOKEN            | 認証トークンが空であるため、ユーザーはコンテンツにアクセスできませんでした。
DISABLED_SERVICE            | サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした
PROXY_AUTH_ERROR            | プロキシ認証が失敗しました。
NO_POLICY            | ユーザー/テナントに対してポリシーが構成されていません
OPERATION_CANCELLED            | 操作が取り消されました。
ADHOC_PROTECTION_REQUIRED            | ファイルに対する操作を完了するには、アドホック保護を設定する必要があります
DEPRECATED_API            | 呼び出し元が非推奨の API を呼び出しました
TEMPLATE_NOT_FOUND            | テンプレート ID が認識されません
LABEL_NOT_FOUND            | ラベル ID が認識されません
LABEL_DISABLED            | ラベルが無効または非アクティブです
  
#### <a name="inspectortype-enum"></a>InspectorType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
不明            | 不明のファイルインスペクターです。
メッセージ            | Msg スタイルファイルインスペクター、rpq msg/msg ベース。
サポートされているファイルの種類に関連付けているインスペクターの種類。
  
#### <a name="bodytype-enum"></a>BodyType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
UNKNOWN            | 不明の本文の種類
TXT            | テキストスタイルの本文の種類、エンコードは utf8 として返されます
HTML            | HTML スタイルの本文型、エンコードは utf8 として返されます
RTF            | RTF スタイルの本文の種類、バイナリ形式
ボディ型列挙子。
  
#### <a name="flightingfeature-enum"></a>フライト機能列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
ServiceDiscovery            | 個別の HTTP 呼び出しに依存して RMS サービスエンドポイントを決定する
AuthInfoCache            | ドメイン/テナントごとに OAuth2 のチャレンジをキャッシュすることで、不要な401の応答を減らすことができます。 独自の HTTP 認証 (SPO、Edge など) を管理するアプリ/サービスに対して無効にする
LinuxEncryptedCache            | Linux プラットフォームの暗号化されたキャッシュを有効にします (この機能の前提条件をお読みください)
SingleDomainName            | Dns 参照に対して単一の会社名を有効にします。 例: [https://corprights](https://corprights)
PolicyAuth            | ポリシーサービスに送信される要求の自動 HTTP 認証を有効にします。 独自の HTTP 認証 (SPO、Edge など) を管理するアプリ/サービスに対して無効にする
新しい機能を名前で定義します。
  
#### <a name="httprequesttype-enum"></a>HttpRequestType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
取得            | GET
Post            | POST
HTTP 要求の種類。
  
#### <a name="loglevel-enum"></a>LogLevel 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
Trace            | 
［情報］            | 
警告            | 
Error            | 
MIP SDK 全体で使用するさまざまなのログ レベル。
  
#### <a name="protectiontype-enum"></a>ProtectionType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
TemplateBased            | ハンドルはテンプレートから作成されました
カスタム            | ハンドルはアドホックで作成されました
保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。
  
#### <a name="actiontype-enum"></a>ActionType 列挙型
 値                         | 説明                                
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
さまざまなアクション タイプ。
CUSTOM は汎用的なアクション タイプです。 その他のアクション タイプは、すべて特定の意味を持つ特定のアクションです。
  
#### <a name="labelstate-enum"></a>LabelState 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
NoChange            | 
Remove            | 
更新プログラム、更新            | 
  
#### <a name="actiondatatype-enum"></a>ActionDataType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
カスタム            | 
Protection            | 
ContentMarking            | 
AddWatermark            | 
ラベル            | 
  
#### <a name="conditiondatatype-enum"></a>ConditionDataType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
既定            | 
秘密度            | 
  
#### <a name="contentmarkplacement-enum"></a>ContentMarkPlacement 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
Header            | 
フッター            | 
  
#### <a name="labelactiondatatype-enum"></a>LabelActionDataType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
推奨            | 
[適用]            | 
  
#### <a name="protectionactiontype-enum"></a>ProtectionActionType 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
カスタム            | 
テンプレート            | 
前面へ移動            | 
Adhoc            | 
表示するプロンプト            | 
Hyok            | 
事前に宣言するテンプレート            | 
RemoveProtection            | 

### <a name="structures"></a>構造

#### <a name="struct-mipapplicationinfo"></a>struct mip:: ApplicationInfo 
アプリケーション固有の情報を含む構造体。
  
 [メンバー]                        | 説明                                
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
  
[メンバー]                        | 説明                                
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

## <a name="namespace-mipauditmetadatakeys"></a>名前空間 mip:: auditmetadatakeys
  
### <a name="summary"></a>要約
 [メンバー]                        | 説明                                
--------------------------------|---------------------------------------------
public std:: string Sender ()       |  文字列形式のメタデータキーを監査します。
public std:: string Recipients ()       | まだ文書化されていません。
public std:: string Lastsystem.string ()       | まだ文書化されていません。
public std:: string LastModifiedDate ()       | まだ文書化されていません。
  
### <a name="members"></a>[メンバー]
  
#### <a name="sender-function"></a>Sender 関数
文字列形式のメタデータキーを監査します。
  
#### <a name="recipients-function"></a>受信者関数
_まだ文書化されていません。_

  
#### <a name="lastmodifiedby-function"></a>Lastて関数
_まだ文書化されていません。_

  
#### <a name="lastmodifieddate-function"></a>LastModifiedDate 関数
_まだ文書化されていません。_

## <a name="namespace-miprights"></a>名前空間 mip:: rights
  
### <a name="summary"></a>要約
 
 [メンバー]                        | 説明                                
--------------------------------|---------------------------------------------
public std::string Owner()       |  '所有者' 権限の文字列識別子を取得します。
public std::string View()       |  '表示' 権限の文字列識別子を取得します。
public std::string AuditedExtract()       |  '監査済み抽出' 権限の文字列識別子を取得します。
public std::string Edit()       |  '編集' 権限の文字列識別子を取得します。
public std::string Export()       |  'エクスポート' 権限の文字列識別子を取得します。
public std::string Extract()       |  '抽出' 権限の文字列識別子を取得します。
public std::string Print()       |  '印刷' 権限の文字列識別子を取得します。
public std::string Comment()       |  'コメント' 権限の文字列識別子を取得します。
public std::string Reply()       |  '返信' 権限の文字列識別子を取得します。
public std::string ReplyAll()       |  '全員に返信' 権限の文字列識別子を取得します。
public std::string Forward()       |  '転送' 権限の文字列識別子を取得します。
public std:: vector\<std:: string\> EmailRights ()       |  電子メールに適用される権限の一覧を取得します。
public std:: vector\<std:: string\> EditableDocumentRights ()       |  ドキュメントに適用される権限の一覧を取得します。
public std:: vector\<std:: string\> CommonRights ()       |  すべてのシナリオで適用される権限の一覧を取得します。
  
### <a name="members"></a>[メンバー]
  
#### <a name="owner-function"></a>Owner 関数
'所有者' 権限の文字列識別子を取得します。

  
**戻り値**: '所有者' 権限の文字列識別子
  
#### <a name="view-function"></a>関数の表示
'表示' 権限の文字列識別子を取得します。

  
**戻り値**: '表示' 権限の文字列識別子
  
#### <a name="auditedextract-function"></a>AuditedExtract 関数
'監査済み抽出' 権限の文字列識別子を取得します。

  
**戻り値**: '監査済み抽出' 権限の文字列識別子
  
#### <a name="edit-function"></a>関数の編集
'編集' 権限の文字列識別子を取得します。

  
**戻り値**: '編集' 権限の文字列識別子
  
#### <a name="export-function"></a>Export 関数
'エクスポート' 権限の文字列識別子を取得します。

  
**戻り値**: 'エクスポート' 権限の文字列識別子
  
#### <a name="extract-function"></a>Extract 関数
'抽出' 権限の文字列識別子を取得します。

  
**戻り値**: '抽出' 権限の文字列識別子
  
#### <a name="print-function"></a>Print 関数
'印刷' 権限の文字列識別子を取得します。

  
**戻り値**: '印刷' 権限の文字列識別子
  
#### <a name="comment-function"></a>Comment 関数
'コメント' 権限の文字列識別子を取得します。

  
**戻り値**: 'コメント' 権限の文字列識別子
  
#### <a name="reply-function"></a>Reply 関数
'返信' 権限の文字列識別子を取得します。

  
**戻り値**: '返信' 権限の文字列識別子
  
#### <a name="replyall-function"></a>ReplyAll 関数
'全員に返信' 権限の文字列識別子を取得します。

  
**戻り値**: '全員に返信' 権限の文字列識別子
  
#### <a name="forward-function"></a>Forward 関数
'転送' 権限の文字列識別子を取得します。

  
**戻り値**: '転送' 権限の文字列識別子
  
#### <a name="emailrights-function"></a>EmailRights 関数
電子メールに適用される権限の一覧を取得します。

  
**戻り値**: 電子メールに適用される権限の一覧
  
#### <a name="editabledocumentrights-function"></a>EditableDocumentRights 関数
ドキュメントに適用される権限の一覧を取得します。

  
**戻り値**: ドキュメントに適用される権限の一覧
  
#### <a name="commonrights-function"></a>CommonRights 関数
すべてのシナリオで適用される権限の一覧を取得します。

  
**戻り値**: すべてのシナリオで適用される権限の一覧

## <a name="namespace-miproles"></a>名前空間 mip:: roles
  
### <a name="summary"></a>要約
 [メンバー]                        | 説明                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  'ビューアー' ロールの文字列識別子を取得します。
public std::string Reviewer()       |  'レビュー担当者' ロールの文字列識別子を取得します。
public std::string Author()       |  '作成者' ロールの文字列識別子を取得します。
public std::string CoOwner()       |  '共同所有者' ロールの文字列識別子を取得します。
  
### <a name="members"></a>[メンバー]
  
#### <a name="viewer-function"></a>ビューアー関数
'ビューアー' ロールの文字列識別子を取得します。

  
**戻り値**: 'ビューアー' ロールの文字列識別子。ビューアーが実行できるのはコンテンツの表示のみです。 編集、コピー、印刷は実行できません。
  
#### <a name="reviewer-function"></a>レビュー担当者関数
'レビュー担当者' ロールの文字列識別子を取得します。

  
**戻り値**: 'レビュー担当者' ロールの文字列識別子。レビュー担当者はコンテンツの表示と編集を実行できます。 コピーや印刷は実行できません。
  
#### <a name="author-function"></a>Author 関数
'作成者' ロールの文字列識別子を取得します。

  
**戻り値**: '作成者' ロールの文字列識別子。作成者はコンテンツの表示、編集、コピー、印刷を実行できます。
  
#### <a name="coowner-function"></a>CoOwner 関数
'共同所有者' ロールの文字列識別子を取得します。

  
**戻り値**: '共同所有者' ロールの文字列識別子。共同所有者はすべてのアクセス許可を持ちます。

