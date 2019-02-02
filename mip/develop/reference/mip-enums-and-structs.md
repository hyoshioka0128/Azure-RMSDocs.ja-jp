---
title: MIP SDK for C リファレンス構造体と列挙型
description: MIP C++ SDK 構造体、列挙型のリファレンス ドキュメント。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d3ca101d3141f2a1e36fcfec11e805907c125b8e
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651770"
---
# <a name="summary"></a>まとめ

 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
**Namespace `mip` :** |
ActionSource 列挙型       |  SetLabel イベントが発生した原因を定義します。
enum ActionType       |  さまざまなアクション タイプ。
AssignmentMethod 列挙型       |  ドキュメント上のラベルの割り当て方法。 かどうか、ラベルの割り当てでは標準または特権操作 (管理者の操作に相当) として行うが自動的に。
enum Consent       |  サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。
名前列挙型       |  コンテンツの形式。
ContentMarkAlignment 列挙型       |  コンテンツの配置 (コンテンツ ヘッダーまたはフッターのコンテンツ) をマークします。
ContentState 列挙型       |  データのアプリケーションを実行する対象の状態を定義します。
enum ErrorType       | _まだ文書化されていません。_
enum HttpRequestType       |  HTTP 要求の種類。
enum LogLevel       |  MIP SDK 全体で使用するさまざまなのログ レベル。
enum ProtectionHandlerCreationOptions       |  追加のポリシー作成の動作を支持するビット フラグ。
enum ProtectionType       |  保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。
watermarklayout: 列挙型       |  透かしのレイアウト。
struct ApplicationInfo  |  アプリケーション固有の情報を含む構造体。
PublishingLicenseContext 構造体 | 保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。
  
## <a name="enumerations-mip"></a>列挙型 (`mip`)

### <a name="actionsource-enum"></a>ActionSource 列挙型

SetLabel イベントが発生した原因を定義します。

 値                         | 説明                                
--------------------------------|---------------------------------------------
手動            | ユーザーが手動で選択
自動            | ポリシーの条件を設定します。
お勧めします            | ラベルがポリシーの条件で推奨された直後後にユーザーによって設定します。
既定値            | 既定では、ポリシー設定します。
必須            | ポリシーのラベルの設定を適用した後、ユーザーが設定します。


### <a name="actiontype-enum"></a>ActionType 列挙型

さまざまなアクション タイプ。 CUSTOM は汎用的なアクション タイプです。 その他のアクション タイプは、すべて特定の意味を持つ特定のアクションです。

 値                         | 説明                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | ドキュメントのアクション タイプにコンテンツ フッターを追加します。
ADD_CONTENT_HEADER            | ドキュメントのアクション タイプにコンテンツ ヘッダーを追加します。
ADD_WATERMARK            | ドキュメントのアクション タイプ全体にウォーター マークを追加します。
カスタム            | カスタム定義のアクション タイプ。
JUSTIFY            | 正当化アクション タイプ。
メタデータ            | メタ データ変更のアクション タイプ。
PROTECT_ADHOC            | アドホック ポリシーによる保護アクション タイプ。
PROTECT_BY_TEMPLATE            | テンプレートによる保護アクション タイプ。
PROTECT_DO_NOT_FORWARD            | 転送不可による保護アクション タイプ。
REMOVE_CONTENT_FOOTER            | コンテンツ フッターの削除アクション タイプ。
REMOVE_CONTENT_HEADER            | コンテンツ ヘッダーの削除アクション タイプ。
REMOVE_PROTECTION            | 保護の削除アクション タイプ。
REMOVE_WATERMARK            | ウォーターマークの削除アクション タイプ。
APPLY_LABEL            | ラベルの適用アクション タイプ。
RECOMMEND_LABEL            | ラベルの推奨アクション タイプ。

### <a name="assignmentmethod-enum"></a>AssignmentMethod 列挙型

ドキュメント上のラベルの割り当て方法。 かどうか、ラベルの割り当てでは標準または特権操作 (管理者の操作に相当) として行うが自動的に。

 値                         | 説明                                
--------------------------------|---------------------------------------------
標準            | [ラベル](class_mip_label.md)割り当て方法は、標準
特権            | [ラベル](class_mip_label.md)特権が割り当て方法
自動            | [ラベル](class_mip_label.md)割り当て方法は自動


### <a name="consent-enum"></a>同意の列挙型

サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。

 値                         | 説明                                
--------------------------------|---------------------------------------------
AcceptAlways            | 同意し、この決定を記憶します
そのまま使用します。            | 同意します (1 回限り)
元に戻す            | 同意しません


### <a name="contentformat-enum"></a>名前列挙型

コンテンツの形式。

 値                         | 説明                                
--------------------------------|---------------------------------------------
既定値            | コンテンツの形式は、標準のファイルの形式
電子メール            | コンテンツの形式は、電子メールの形式

### <a name="contentmarkalignment-enum"></a>ContentMarkAlignment 列挙型

コンテンツの配置 (コンテンツ ヘッダーまたはフッターのコンテンツ) をマークします。

 値                         | 説明                                
--------------------------------|---------------------------------------------
左            | コンテンツ マーキングは、左に配置します。
そうです            | コンテンツ マーキングは、右側に配置されます。
CENTER            | コンテンツ マーキングが中央揃え

### <a name="contentstate-enum"></a>ContentState 列挙型

データのアプリケーションを実行する対象の状態を定義します。

 値                         | 説明                                
--------------------------------|---------------------------------------------
残りの部分            | データベース/ファイル/倉庫に物理的に格納されている非アクティブなデータ
モーション            | データをネットワーク上で転送または一時的に読み取りまたは更新するコンピューターのメモリ内に存在します。
USE            | データベース/ファイル/倉庫などに物理的に格納されている定数の変更のアクティブなデータ

### <a name="errortype-enum"></a>ErrorType 列挙型

 値                         | 説明                                
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
  
### <a name="httprequesttype-enum"></a>HttpRequestType 列挙型

HTTP 要求の種類。

 値                         | 説明                                
--------------------------------|---------------------------------------------
取得            | GET
Post            | POST

  
### <a name="loglevel-enum"></a>LogLevel 列挙型

MIP SDK 全体で使用するさまざまなのログ レベル。

 値                         | 説明                                
--------------------------------|---------------------------------------------
トレース            | 
Info            | 
警告            | 
[エラー]            | 

  
### <a name="protectionhandlercreationoptions-enum"></a>ProtectionHandlerCreationOptions 列挙型

追加のポリシー作成の動作を支持するビット フラグ。

 値                         | 説明                                
--------------------------------|---------------------------------------------
なし            | なし
OfflineOnly            | UI およびネットワークの操作を許可しません。
AllowAuditedExtraction            | 保護 SDK に対応していないアプリでコンテンツを開くことができます
PreferDeprecatedAlgorithms            | 下位互換性のために非推奨の暗号アルゴリズム (ECB) を使用します
  
### <a name="protectiontype-enum"></a>ProtectionType 列挙型

保護をテンプレートまたはアドホック (カスタム) に基づくかどうかについて説明します。

 値                         | 説明                                
--------------------------------|---------------------------------------------
TemplateBased            | ハンドルはテンプレートから作成されました
カスタム            | ハンドルはアドホックで作成されました
  
### <a name="watermarklayout-enum"></a>Watermarklayout: 列挙型

透かしのレイアウト。

 値                         | 説明                                
--------------------------------|---------------------------------------------
水平方向            | 透かしのレイアウトは横方向
対角線            | 透かしのレイアウトが斜め


## <a name="structures"></a>構造体 

### `mip::ApplicationInfo` 

アプリケーション固有の情報を含む構造体。
  
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  アプリケーション識別子としては、AAD ポータルの設定、(角かっこなし GUID である必要があります)。
 public std::string applicationName  |  アプリケーションの名前 (有効な ASCII 文字を除くを含める必要がありますのみ ';')
 public std::string applicationVersion  |  使用しているアプリケーションのバージョン (有効な ASCII 文字を除くを含める必要がありますのみ ';')
  
### `mip::PublishingLicenseContext` 

保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。
  
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector\<uint8_t\> licenseInfo  | _まだ文書化されていません。_
public const std::vector\<uint8_t\> serializedPublishingLicense  | _まだ文書化されていません。_
public PublishingLicenseContext(const std::vector\<uint8_t\>& licenseInfo, const std::vector\<uint8_t\>& serializedPublishingLicense)  | _まだ文書化されていません。_
  
