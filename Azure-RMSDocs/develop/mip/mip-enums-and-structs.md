# <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 enum Consent       |  サービス エンドポイントへの接続に同意するユーザーの決定を表します。
 struct ApplicationInfo  |  Azure AD ポータルで設定されているアプリケーション ID。
**mip** |
 enum ActionType       |  さまざまなアクション タイプ。
 enum ErrorType       | _まだ文書化されていません。_
 enum LogLevel       |  Mip SDK 全体で使用するさまざまなのログ レベル。
 enum ProtectionHandlerCreationOptions       |  追加のポリシー作成の動作を支持するビット フラグ。
 enum ProtectionType       |  保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。

  
## <a name="enumerations-common"></a>列挙型 (共通)
  
### <a name="consent"></a>同意
サービス エンドポイントへの接続に同意するユーザーの決定を表します。

 値                         | 説明                                
--------------------------------|---------------------------------------------
AcceptAlways            | 同意し、この決定を記憶します
同意する            | 同意します (1 回限り)
[拒否]            | 同意しません
  
## <a name="enumerations-mip"></a>列挙型 (mip)

### <a name="actiontype"></a>ActionType

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
  
**ActionType** の値は次の演算子をサポートします。

* [Action](class_mip_action.md) タイプの列挙型に対する Or (|) 演算子。  
* [Action](class_mip_action.md) タイプの列挙型に対する And (&) 演算子。  
* [Action](class_mip_action.md) タイプの列挙型に対する Xor (^) 演算子。  

### <a name="errortype"></a>ErrorType

 値                         | 説明                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 呼び出し元が無効な入力を渡しました。
FILE_IO_ERROR            | 一般的なファイル IO エラー。
NETWORK_ERROR            | 一般的なネットワークの問題 (例: サービスのアクセス不可)。
INTERNAL_ERROR            | 予期しない内部エラー。 例: クライアント/サーバー プロトコル内部 (予期しない応答の受信)。
JUSTIFICATION_REQUIRED            | ファイルのアクションを完了するには理由が提供される必要があります。
NOT_SUPPORTED_OPERATION            | 要求された操作はまだサポートされていません。
PRIVILEGED_REQUIRED            | 新しいラベルのメソッドが標準である場合、特権ラベルをオーバーライドできません。
ACCESS_DENIED            | ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された、など。
  
### <a name="loglevel"></a>ログ レベル

 値                         | 説明                                
--------------------------------|---------------------------------------------
Trace            | 
［情報］            | 
警告            | 
エラー            | 
Mip SDK 全体で使用するさまざまなのログ レベル。
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

 値                         | 説明                                
--------------------------------|---------------------------------------------
なし            | なし
OfflineOnly            | UI およびネットワークの操作を許可しません。
AllowAuditedExtraction            | 保護 SDK に対応していないアプリでコンテンツを開くことができます
PreferDeprecatedAlgorithms            | 下位互換性のために非推奨の暗号アルゴリズム (ECB) を使用します
追加のポリシー作成の動作を支持するビット フラグ。
  
### <a name="protectiontype"></a>ProtectionType

 値                         | 説明                                
--------------------------------|---------------------------------------------
TemplateBased            | ハンドルはテンプレートから作成されました
カスタム            | ハンドルはアドホックで作成されました
保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

ProtectionHandlerCreationOptions ビットごとの OR 演算子。

パラメーター: 
 
* **a**: 左側の値 

* **b**: 右側の値
  
**戻り値**: パラメーターのビットごとの OR
  


## <a name="structures"></a>構造体

### <a name="applicationinfo"></a>ApplicationInfo 
Azure AD ポータルで設定されているアプリケーション ID。
  
 フィールド                        | 説明                                
--------------------------------|---------------------------------------------
 public std::string applicationId  | Azure AD ポータル内のアプリケーション ID。
 public std::string friendlyName  | ポータルで指定されている、アプリのフレンドリ名。
  
