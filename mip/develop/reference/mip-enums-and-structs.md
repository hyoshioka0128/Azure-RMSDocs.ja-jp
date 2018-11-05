---
title: '[概要]'
description: '[概要]'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5af209d5a627263399c8c60f474495dcadab24a0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446500"
---
# <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
**共通** |
enum Consent       |  サービス エンドポイントに接続するためにコンテンツが要求されるときのユーザーの応答。
struct ApplicationInfo  |  アプリケーション固有の情報を含む構造体。
**mip** |
enum ErrorType       | _まだ文書化されていません。_
enum HttpRequestType       |  HTTP 要求の種類。
enum LogLevel       |  MIP SDK 全体で使用するさまざまなのログ レベル。
enum ProtectionHandlerCreationOptions       |  追加のポリシー作成の動作を支持するビット フラグ。
enum ProtectionType       |  保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。
enum ActionType       |  さまざまなアクション タイプ。
struct mip::PublishingLicenseContext | 保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。

  
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

さまざまなアクション タイプ。

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

CUSTOM は汎用的なアクション タイプです。 その他のアクション タイプは、すべて特定の意味を持つ特定のアクションです。

ActionType 値は、次の演算子を使用して結合させることができます。

- [Action](class_mip_action.md) に対する AND (&) 演算子 (`operator &(ActionType a, ActionType b)`)
- [Action](class_mip_action.md) に対する OR (XOR) (^) 演算子  (`operator ^(ActionType a, ActionType b)`)


### <a name="errortype"></a>ErrorType
 値                         | 説明                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 呼び出し元が無効な入力を渡しました。
FILE_IO_ERROR            | 一般的なファイル IO エラー。
NETWORK_ERROR            | 一般的なネットワークの問題 (例: サービスのアクセス不可)。
TRANSIENT_NETWORK_ERROR            | 一時的なネットワークの問題 (例: 無効なゲートウェイ)。
INTERNAL_ERROR            | 予期しない内部エラー。 例: クライアント/サーバー プロトコル内部 (予期しない応答の受信)。
JUSTIFICATION_REQUIRED            | ファイルのアクションを完了するには理由が提供される必要があります。
NOT_SUPPORTED_OPERATION            | 要求された操作はまだサポートされていません。
PRIVILEGED_REQUIRED            | 新しいラベルのメソッドが標準である場合、特権ラベルをオーバーライドできません。
ACCESS_DENIED            | ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された、など。
CONSENT_DENIED            | ユーザーに同意を求めた操作で、同意が得られませんでした。
  
### <a name="httprequesttype"></a>HttpRequestType
HTTP 要求の種類。

 値                         | 説明                                
--------------------------------|---------------------------------------------
取得            | GET
Post            | POST
  
### <a name="loglevel"></a>ログ レベル

MIP SDK 全体で使用するさまざまなのログ レベル。

 値                         | 説明                                
--------------------------------|---------------------------------------------
Trace            | 
［情報］            | 
警告            | 
エラー            | 
Mip SDK 全体で使用するさまざまなのログ レベル。
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

追加のポリシー作成の動作を支持するビット フラグ。

 値                         | 説明                                
--------------------------------|---------------------------------------------
なし            | なし
OfflineOnly            | UI およびネットワークの操作を許可しません。
AllowAuditedExtraction            | 保護 SDK に対応していないアプリでコンテンツを開くことができます
PreferDeprecatedAlgorithms            | 下位互換性のために非推奨の暗号アルゴリズム (ECB) を使用します


### <a name="protectiontype"></a>ProtectionType
保護がテンプレートに基づくのか、アドホック (カスタム) かを説明します。

 値                         | 説明                                
--------------------------------|---------------------------------------------
TemplateBased            | ハンドルはテンプレートから作成されました
カスタム            | ハンドルはアドホックで作成されました

  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions
ProtectionHandlerCreationOptions ビットごとの OR 演算子。

パラメーター:  
* **a**: 左側の値 

* **b**: 右側の値

### <a name="releaseallresources"></a>ReleaseAllResources
シャットダウンの前にすべてのリソース (スレッドなど) を解放します。
MIP 動的ライブラリがアプリケーションによって遅延読み込みされる場合、デッドロックを回避するため、それらの MIP ライブラリをアプリケーションで明示的にアンロードする前に、この関数は呼び出される必要があります。 たとえば、Win32 で、この関数は、FreeLibrary または \__FUnloadDelayLoadedDLL2 によって MIP DLL を明示的にアンロードするための任意の呼び出しの前に呼び出される必要があります。 アプリケーションでは、この関数を呼び出す前に、すべての MIP オブジェクト (例: プロファイル、エンジン、ハンドラー) への参照を解放する必要があります。
  
**戻り値**: パラメーターのビットごとの OR
  
## <a name="structures"></a>構造体

### <a name="applicationinfo"></a>ApplicationInfo 
アプリケーション固有の情報を含む構造体。

 フィールド                        | 説明                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  Azure AD ポータルで設定されているアプリケーション ID。
 public std::string applicationName  |  アプリケーション名
 public std::string applicationVersion  |  使用されているアプリケーションのバージョン
  
### <a name="mippublishinglicensecontext"></a>mip::PublishingLicenseContext 
保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。
  
 フィールド                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector<uint8_t> licenseInfo  | _まだ文書化されていません。_
public const std::vector<uint8_t> serializedPublishingLicense  | _まだ文書化されていません。_
public PublishingLicenseContext(const std::vector<uint8_t>& licenseInfo, const std::vector<uint8_t>& serializedPublishingLicense)  | _まだ文書化されていません。_
  
