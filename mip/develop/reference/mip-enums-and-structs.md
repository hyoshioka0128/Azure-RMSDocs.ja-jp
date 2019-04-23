---
title: MIP SDK for C リファレンス構造体と列挙型
description: MIP C++ SDK 構造体、列挙型のリファレンス ドキュメント。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: c9e634d436d02b147fc10a734c8c3d5b1fcdec71
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173358"
---
# <a name="enumerations-and-structures"></a>列挙体と構造体

## <a name="namespace-mip"></a>Namespace mip

 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
ActionSource 列挙型       |  SetLabel イベントが発生した原因を定義します。
enum ActionType       |  さまざまなアクション タイプ。
AssignmentMethod 列挙型       |  ドキュメント上のラベルの割り当て方法。 かどうか、ラベルの割り当てでは標準または特権操作 (管理者の操作に相当) として行うが自動的に。
enum Consent       |  サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。
名前列挙型       |  コンテンツの形式。
ContentMarkAlignment 列挙型       |  コンテンツの配置 (コンテンツ ヘッダーまたはフッターのコンテンツ) をマークします。
DataState 列挙型       |  データのアプリケーションを実行する対象の状態を定義します。
enum ErrorType       | _まだ文書化されていません。_
enum HttpRequestType       |  HTTP 要求の種類。
enum LogLevel       |  MIP SDK 全体で使用するさまざまなのログ レベル。
enum ProtectionHandlerCreationOptions       |  追加のポリシー作成の動作を支持するビット フラグ。
enum ProtectionType       |  保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。
watermarklayout: 列挙型       |  透かしのレイアウト。
struct ApplicationInfo  |  アプリケーション固有の情報を含む構造体。
PublishingLicenseContext 構造体  |  保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。
  
## <a name="enumerations-mip"></a>列挙型 (mip)

### <a name="actionsource"></a>ActionSource

SetLabel イベントが発生した原因を定義します。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
手動            | ユーザーが手動で選択
自動            | ポリシーの条件を設定します。
お勧めします            | ラベルがポリシーの条件で推奨された直後後にユーザーによって設定します。
DEFAULT            | 既定では、ポリシー設定します。
必須            | ポリシーのラベルの設定を適用した後、ユーザーが設定します。



### <a name="actiontype"></a>ActionType

さまざまなアクション タイプ。 CUSTOM は汎用的なアクション タイプです。 その他のアクション タイプは、すべて特定の意味を持つ特定のアクションです。

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


### <a name="assignmentmethod"></a>AssignmentMethod

ドキュメント上のラベルの割り当て方法。 かどうか、ラベルの割り当てでは標準または特権操作 (管理者の操作に相当) として行うが自動的に。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
STANDARD            | [ラベル](class_mip_label.md)割り当て方法は、標準
特権            | [ラベル](class_mip_label.md)特権が割り当て方法
AUTO            | [ラベル](class_mip_label.md)割り当て方法は自動


### <a name="consent"></a>同意

サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
AcceptAlways            | 同意し、この決定を記憶します
同意する            | 同意します (1 回限り)
[拒否]            | 同意しません


### <a name="contentformat"></a>名前

コンテンツの形式。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
DEFAULT            | コンテンツの形式は、標準のファイルの形式
電子メール            | コンテンツの形式は、電子メールの形式

### <a name="contentmarkalignment"></a>ContentMarkAlignment

コンテンツの配置 (コンテンツ ヘッダーまたはフッターのコンテンツ) をマークします。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
[LEFT]            | コンテンツ マーキングは、左に配置します。
[RIGHT]            | コンテンツ マーキングは、右側に配置されます。
センター            | コンテンツ マーキングが中央揃え

### <a name="datastate"></a>DataState
 値                         | [説明]                                
--------------------------------|---------------------------------------------
残りの部分            | データベース/ファイル/倉庫に物理的に格納されている非アクティブなデータ
モーション            | データをネットワーク上で転送または一時的に読み取りまたは更新するコンピューターのメモリ内に存在します。
USE            | データベース/ファイル/倉庫などに物理的に格納されている定数の変更のアクティブなデータ


### <a name="errortype"></a>ErrorType
 値                         | [説明]                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 呼び出し元が無効な入力を渡しました。
FILE_IO_ERROR            | 一般的なファイル IO エラー。
NETWORK_ERROR            | 一般的なネットワークの問題たとえば、サービスに到達できません。
TRANSIENT_NETWORK_ERROR            | ネットワークの一時的な問題です。たとえば、無効なゲートウェイです。
INTERNAL_ERROR            | 予期しない内部エラー。
JUSTIFICATION_REQUIRED            | ファイルのアクションを完了するには理由が提供される必要があります。
NOT_SUPPORTED_OPERATION            | 要求された操作はまだサポートされていません。
PRIVILEGED_REQUIRED            | 新しいラベルのメソッドが標準である場合、特権ラベルをオーバーライドできません。
ACCESS_DENIED            | ユーザーは、サービスへのアクセスを取得できませんでした。
CONSENT_DENIED            | ユーザーに同意を求めた操作で、同意が得られませんでした。
POLICY_SYNC_ERROR            | ポリシー データを同期しようとして失敗しました。
NO_PERMISSIONS            | ユーザーがコンテンツにアクセスできませんでした。 たとえば、権限、コンテンツを取り消すなし
NO_AUTH_TOKEN            | ユーザーは、空の認証トークンのためのコンテンツへのアクセスを取得できませんでした。
DISABLED_SERVICE            | ユーザーは、サービスを無効になっているため、コンテンツへのアクセスを取得できませんでした。
PROXY_AUTH_ERROR            | プロキシ認証に失敗しました。
NO_POLICY_ERROR            | ユーザーまたはテナントにポリシーが構成されていません
OPERATION_CANCELLED            | 操作は取り消されました
ADHOC_PROTECTION_REQUIRED            | アドホック保護をファイルにアクションを完了に設定する必要があります。
  
### <a name="httprequesttype"></a>HttpRequestType

HTTP 要求の種類。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
取得            | GET
Post            | POST

  
### <a name="loglevel"></a>ログ レベル

MIP SDK 全体で使用するさまざまなのログ レベル。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
警告            | 
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

追加のポリシー作成の動作を支持するビット フラグ。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
なし            | なし
OfflineOnly            | UI およびネットワークの操作を許可しません。
AllowAuditedExtraction            | 保護 SDK に対応していないアプリでコンテンツを開くことができます
PreferDeprecatedAlgorithms            | 下位互換性のために非推奨の暗号アルゴリズム (ECB) を使用します


### <a name="protectiontype"></a>ProtectionType

保護をテンプレートまたはアドホック (カスタム) に基づくかどうかについて説明します。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
TemplateBased            | ハンドルはテンプレートから作成されました
カスタム            | ハンドルはアドホックで作成されました

  
### <a name="watermarklayout"></a>Watermarklayout:

透かしのレイアウト。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
水平方向            | 透かしのレイアウトは横方向
対角線            | 透かしのレイアウトが斜め


## <a name="structures"></a>構造体 

### <a name="mipapplicationinfo"></a>mip::ApplicationInfo 
アプリケーション固有の情報を含む構造体。
  
#### <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  アプリケーション識別子としては、AAD ポータルの設定、(角かっこなし GUID である必要があります)。
public std::string applicationName  |  アプリケーションの名前 (有効な ASCII 文字を除くを含める必要がありますのみ ';')
public std::string applicationVersion  |  使用しているアプリケーションのバージョン (有効な ASCII 文字を除くを含める必要がありますのみ ';')
  
#### <a name="members"></a>メンバー
  
##### <a name="applicationid-struct-member"></a>applicationId 構造体のメンバー
アプリケーション識別子としては、AAD ポータルの設定、(角かっこなし GUID である必要があります)。
  
##### <a name="applicationname-struct-member"></a>applicationName 構造体のメンバー
アプリケーションの名前 (有効な ASCII 文字を除くを含める必要がありますのみ ';')
  
##### <a name="applicationversion-struct-member"></a>applicationVersion 構造体のメンバー
使用しているアプリケーションのバージョン (有効な ASCII 文字を除くを含める必要がありますのみ ';')  

### <a name="mippublishinglicensecontext"></a>mip::PublishingLicenseContext 
保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。
  
#### <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const std::vector\<uint8_t\> licenseInfo  | _まだ文書化されていません。_
public const std::vector\<uint8_t\> serializedPublishingLicense  | _まだ文書化されていません。_
public PublishingLicenseContext(const std::vector\<uint8_t\>& licenseInfo, const std::vector\<uint8_t\>& serializedPublishingLicense)  | _まだ文書化されていません。_
  
#### <a name="members"></a>メンバー
  
##### <a name="licenseinfo-struct-member"></a>licenseInfo 構造体のメンバー
_まだ文書化されていません。_

  
##### <a name="serializedpublishinglicense-struct-member"></a>serializedPublishingLicense 構造体のメンバー
_まだ文書化されていません。_

  
##### <a name="publishinglicensecontext-function"></a>PublishingLicenseContext 関数
_まだ文書化されていません。_
