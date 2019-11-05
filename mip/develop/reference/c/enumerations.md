---
title: 列挙
description: 列挙
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: f1ad15819d10bcded670fe519db07667b7e7331e
ms.sourcegitcommit: 7a8eef5eb9d6440c6e2300cb3f264da31061b00d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73591615"
---
# <a name="enumerations"></a>列挙

## <a name="mip_cc_cache_storage_type"></a>mip_cc_cache_storage_type

キャッシュのストレージの種類

| フィールド | [説明] |
|---|---|
|  MIP_CACHE_STORAGE_TYPE_IN_MEMORY = 0         | インメモリストレージ  |
|  MIP_CACHE_STORAGE_TYPE_ON_DISK = 1           | ディスク上の記憶域  |
|  MIP_CACHE_STORAGE_TYPE_ON_DISK_ENCRYPTED = 2  | 暗号化を使用したディスク上のストレージ (プラットフォームでサポートされている場合)  |


```c
typedef enum {
  MIP_CACHE_STORAGE_TYPE_IN_MEMORY = 0,        
  MIP_CACHE_STORAGE_TYPE_ON_DISK = 1,          
  MIP_CACHE_STORAGE_TYPE_ON_DISK_ENCRYPTED = 2 
} mip_cc_cache_storage_type;

```

## <a name="mip_cc_content_format"></a>mip_cc_content_format

コンテンツ形式

| フィールド | [説明] |
|---|---|
|  MIP_CONTENT_FORMAT_DEFAULT = 0  | 標準ファイル形式  |
|  MIP_CONTENT_FORMAT_EMAIL = 1    | 電子メール  |


```c
typedef enum {
  MIP_CONTENT_FORMAT_DEFAULT = 0, 
  MIP_CONTENT_FORMAT_EMAIL = 1,   
} mip_cc_content_format;

```

## <a name="mip_cc_label_assignment_method"></a>mip_cc_label_assignment_method

新しいラベルの適用方法について説明します。

| フィールド | [説明] |
|---|---|
|  MIP_LABEL_ASSIGNMENT_METHOD_STANDARD = 0    | 標準ラベルの割り当てでは、以前の特権割り当てはオーバーライドされません。  |
|  MIP_LABEL_ASSIGNMENT_METHOD_PRIVILEGED = 1  | 特権ラベルの割り当ては、今後の標準割り当てによって上書きされることはありません。  |
|  MIP_LABEL_ASSIGNMENT_METHOD_AUTO = 2        | 予約済み。 使用しないでください。  |


```c
typedef enum {
  MIP_LABEL_ASSIGNMENT_METHOD_STANDARD = 0,   
  MIP_LABEL_ASSIGNMENT_METHOD_PRIVILEGED = 1, 
  MIP_LABEL_ASSIGNMENT_METHOD_AUTO = 2,       
} mip_cc_label_assignment_method;

```

## <a name="mip_cc_content_mark_alignment"></a>mip_cc_content_mark_alignment

コンテンツマークの配置 (コンテンツヘッダーまたはコンテンツフッター)

| フィールド | [説明] |
|---|---|
|  MIP_CONTENT_MARK_ALIGNMENT_LEFT = 0    | コンテンツのマークが左に揃えられます  |
|  MIP_CONTENT_MARK_ALIGNMENT_RIGHT = 1   | コンテンツのマークが右側に揃います  |
|  MIP_CONTENT_MARK_ALIGNMENT_CENTER = 2  | コンテンツのマークは中央に配置されます  |


```c
typedef enum {
  MIP_CONTENT_MARK_ALIGNMENT_LEFT = 0,   
  MIP_CONTENT_MARK_ALIGNMENT_RIGHT = 1,  
  MIP_CONTENT_MARK_ALIGNMENT_CENTER = 2, 
} mip_cc_content_mark_alignment;

```

## <a name="mip_cc_watermark_layout"></a>mip_cc_watermark_layout

透かしのレイアウト

| フィールド | [説明] |
|---|---|
|  MIP_WATERMARK_LAYOUT_HORIZONTAL = 0  | 透かしレイアウトは水平方向です  |
|  MIP_WATERMARK_LAYOUT_DIAGONAL = 1    | 透かしのレイアウトが斜めです  |


```c
typedef enum {
  MIP_WATERMARK_LAYOUT_HORIZONTAL = 0, 
  MIP_WATERMARK_LAYOUT_DIAGONAL = 1,   
} mip_cc_watermark_layout;

```

## <a name="mip_cc_consent"></a>mip_cc_consent

認識されないサービスエンドポイントへの接続が要求されたときのユーザーの応答

| フィールド | [説明] |
|---|---|
|  MIP_CONSENT_ACCEPT_ALWAYS = 0  | 同意し、この決定を記憶する  |
|  MIP_CONSENT_ACCEPT = 1         | 1回だけ同意する  |
|  MIP_CONSENT_REJECT = 2          | 同意しません  |


```c
typedef enum {
  MIP_CONSENT_ACCEPT_ALWAYS = 0, 
  MIP_CONSENT_ACCEPT = 1,        
  MIP_CONSENT_REJECT = 2         
} mip_cc_consent;

```

## <a name="mip_cc_flighting_feature"></a>mip_cc_flighting_feature

新しい特徴を名前で定義します

| フィールド | [説明] |
|---|---|
|  MIP_FLIGHTING_FEATURE_SERVICE_DISCOVERY = 0      | 個別の HTTP 呼び出しを使用して RMS サービスのエンドポイントを決定する (既定値は false) |
|  MIP_FLIGHTING_FEATURE_AUTH_INFO_CACHE = 1        | ドメイン/テナントごとに OAuth2 のチャレンジをキャッシュすることで、不要な401の応答を減らすことができます。 独自の HTTP 認証を管理するアプリ/サービス (既定値は true) に対して無効にする  |
|  MIP_FLIGHTING_FEATURE_LINUX_ENCRYPTED_CACHE = 2  | Linux プラットフォームの暗号化されたキャッシュを有効にします (既定値は false)  |
|  MIP_FLIGHTING_FEATURE_SINGLE_DOMAIN_NAME = 3     | Dns 参照に対して単一の会社名を有効にします。 例: https://corprights  |
|  MIP_FLIGHTING_FEATURE_POLICY_AUTH = 4            | ポリシーサービスに送信される要求の自動 HTTP 認証を有効にします。 独自の HTTP 認証を管理するアプリ/サービス (既定値は true) に対して無効にする  |


```c
typedef enum {
  MIP_FLIGHTING_FEATURE_SERVICE_DISCOVERY = 0,     
  MIP_FLIGHTING_FEATURE_AUTH_INFO_CACHE = 1,       
  MIP_FLIGHTING_FEATURE_LINUX_ENCRYPTED_CACHE = 2, 
  MIP_FLIGHTING_FEATURE_SINGLE_DOMAIN_NAME = 3,    
  MIP_FLIGHTING_FEATURE_POLICY_AUTH = 4,           
} mip_cc_flighting_feature;

```

## <a name="mip_cc_http_request_type"></a>mip_cc_http_request_type

HTTP 要求の種類

| フィールド | [説明] |
|---|---|
|  HTTP_REQUEST_TYPE_GET = 0   | HTTP GET  |
|  HTTP_REQUEST_TYPE_POST = 1  | HTTP POST  |


```c
typedef enum {
  HTTP_REQUEST_TYPE_GET = 0,  
  HTTP_REQUEST_TYPE_POST = 1, 
} mip_cc_http_request_type;

```

## <a name="mip_cc_http_result"></a>mip_cc_http_result

HTTP 操作の成功/失敗の状態

| フィールド | [説明] |
|---|---|
|  HTTP_RESULT_OK = 0       | HTTP 操作が正常に完了しました  |
|  HTTP_RESULT_FAILURE = 1  | HTTP 操作に失敗しました (例: タイムアウト、ネットワークエラーなど)  |


```c
typedef enum {
  HTTP_RESULT_OK = 0,      
  HTTP_RESULT_FAILURE = 1, 
} mip_cc_http_result;

```

## <a name="mip_cc_log_level"></a>mip_cc_log_level

ログレベル

| フィールド | [説明] |
|---|---|
|  MIP_LOG_LEVEL_TRACE = 0   | Trace  |
|  MIP_LOG_LEVEL_INFO        | ［情報］  |
|  MIP_LOG_LEVEL_WARNING     | 警告  |
|  MIP_LOG_LEVEL_ERROR       | Error  |


```c
typedef enum {
  MIP_LOG_LEVEL_TRACE = 0,  
  MIP_LOG_LEVEL_INFO,       
  MIP_LOG_LEVEL_WARNING,    
  MIP_LOG_LEVEL_ERROR,      
} mip_cc_log_level;

```

## <a name="mip_cc_protection_type"></a>mip_cc_protection_type

保護がテンプレートによって定義されているかアドホックであるかの説明

| フィールド | [説明] |
|---|---|
|  MIP_PROTECTION_TYPE_TEMPLATE_BASED = 0  | RMS テンプレートに基づく  |
|  MIP_PROTECTION_TYPE_CUSTOM = 1          | カスタム、アドホック保護  |


```c
typedef enum {
  MIP_PROTECTION_TYPE_TEMPLATE_BASED = 0, 
  MIP_PROTECTION_TYPE_CUSTOM = 1,         
} mip_cc_protection_type;

```

## <a name="mip_cc_result"></a>mip_cc_result

API の成功/失敗の結果

| フィールド | [説明] |
|---|---|
|  MIP_RESULT_ERROR_UNKNOWN                    | 不明なエラー  |
|  MIP_RESULT_ERROR_INSUFFICIENT_BUFFER        | アプリケーションによって指定されたバッファーが小さすぎます  |
|  MIP_RESULT_ERROR_BAD_INPUT                  | アプリケーションに無効な入力が渡されました  |
|  MIP_RESULT_ERROR_FILE_IO_ERROR              | 一般的なファイル i/o エラー  |
|  MIP_RESULT_ERROR_NETWORK                    | 一般的なネットワークエラー (たとえば、到達できないサービス)  |
|  MIP_RESULT_ERROR_TRANSIENT_NETWORK          | 一時的なネットワークエラー (例: 無効なゲートウェイ)  |
|  MIP_RESULT_ERROR_INTERNAL                   | 予期しない内部エラー  |
|  MIP_RESULT_ERROR_JUSTIFICATION_REQUIRED     | ファイルのアクションを完了するには理由が提供される必要があります。  |
|  MIP_RESULT_ERROR_NOT_SUPPORTED_OPERATION    | Opeation サポートされていません  |
|  MIP_RESULT_ERROR_PRIVILEGED_REQUIRED        | 標準メソッドでは特権ラベルをオーバーライドできません  |
|  MIP_RESULT_ERROR_ACCESS_DENIED              | ユーザーにはサービスにアクセスする権限がありません  |
|  MIP_RESULT_ERROR_CONSENT_DENIED             | ユーザーからの同意が必要な操作に同意が与えられていません  |
|  MIP_RESULT_ERROR_POLICY_SYNC                | ポリシーデータを同期しようとして失敗しました  |
|  MIP_RESULT_ERROR_NO_PERMISSIONS             | ユーザーがコンテンツにアクセスできませんでした (アクセス許可がない、コンテンツが失効しているなど)  |
|  MIP_RESULT_ERROR_NO_AUTH_TOKEN              | 認証トークンが空であるため、ユーザーはコンテンツにアクセスできませんでした  |
|  MIP_RESULT_ERROR_SERVICE_DISABLED           | サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした  |
|  MIP_RESULT_ERROR_PROXY_AUTH                 | プロキシ認証に失敗しました  |
|  MIP_RESULT_ERROR_NO_POLICY                  | ユーザー/テナントに対してポリシーが構成されていません  |
|  MIP_RESULT_ERROR_OPERATION_CANCELLED        | 操作が取り消されました  |
|  MIP_RESULT_ERROR_ADHOC_PROTECTION_REQUIRED  | ファイルに対する操作を完了するには、アドホック保護を設定する必要があります  |
|  MIP_RESULT_ERROR_DEPRECATED_API             | 呼び出し元が非推奨の API を呼び出しました  |
|  MIP_RESULT_ERROR_TEMPLATE_NOT_FOUND         | テンプレート ID が認識されません  |
|  MIP_RESULT_ERROR_LABEL_NOT_FOUND            | ラベル ID が認識されません  |
|  MIP_RESULT_ERROR_LABEL_DISABLED             | ラベルが無効または非アクティブです  |


```c
typedef enum {
  MIP_RESULT_SUCCESS = 0,

  // MIP C API errors
  MIP_RESULT_ERROR_UNKNOWN,                   
  MIP_RESULT_ERROR_INSUFFICIENT_BUFFER,       

  // MIP C++ exceptions
  MIP_RESULT_ERROR_BAD_INPUT,                 
  MIP_RESULT_ERROR_FILE_IO_ERROR,             
  MIP_RESULT_ERROR_NETWORK,                   
  MIP_RESULT_ERROR_TRANSIENT_NETWORK,         
  MIP_RESULT_ERROR_INTERNAL,                  
  MIP_RESULT_ERROR_JUSTIFICATION_REQUIRED,    
  MIP_RESULT_ERROR_NOT_SUPPORTED_OPERATION,   
  MIP_RESULT_ERROR_PRIVILEGED_REQUIRED,       
  MIP_RESULT_ERROR_ACCESS_DENIED,             
  MIP_RESULT_ERROR_CONSENT_DENIED,            
  MIP_RESULT_ERROR_POLICY_SYNC,               
  MIP_RESULT_ERROR_NO_PERMISSIONS,            
  MIP_RESULT_ERROR_NO_AUTH_TOKEN,             
  MIP_RESULT_ERROR_SERVICE_DISABLED,          
  MIP_RESULT_ERROR_PROXY_AUTH,                
  MIP_RESULT_ERROR_NO_POLICY,                 
  MIP_RESULT_ERROR_OPERATION_CANCELLED,       
  MIP_RESULT_ERROR_ADHOC_PROTECTION_REQUIRED, 
  MIP_RESULT_ERROR_DEPRECATED_API,            
  MIP_RESULT_ERROR_TEMPLATE_NOT_FOUND,        
  MIP_RESULT_ERROR_LABEL_NOT_FOUND,           
  MIP_RESULT_ERROR_LABEL_DISABLED,            
} mip_cc_result;

```

## <a name="mip_cc_action_type"></a>mip_cc_action_type

アクションの種類のビットマスク

| フィールド | [説明] |
|---|---|
|  MIP_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 < < 0      | ドキュメントのアクション タイプにコンテンツ フッターを追加します。 |
|  MIP_ACTION_TYPE_ADD_CONTENT_HEADER = 1 < < 1      | ドキュメントのアクション タイプにコンテンツ ヘッダーを追加します。 |
|  MIP_ACTION_TYPE_ADD_WATERMARK = 1 < < 2           | ドキュメントのアクション タイプ全体にウォーター マークを追加します。 |
|  MIP_ACTION_TYPE_CUSTOM = 1 < < 3                  | カスタム定義のアクション タイプ。 |
|  MIP_ACTION_TYPE_JUSTIFY = 1 < < 4                 | 正当化アクション タイプ。 |
|  MIP_ACTION_TYPE_METADATA = 1 < < 5                | メタ データ変更のアクション タイプ。 |
|  MIP_ACTION_TYPE_PROTECT_ADHOC = 1 < < 6           | アドホック ポリシーによる保護アクション タイプ。 |
|  MIP_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 < < 7     | テンプレートによる保護アクション タイプ。 |
|  MIP_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 < < 8  | 転送不可による保護アクション タイプ。 |
|  MIP_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 < < 9   | コンテンツ フッターの削除アクション タイプ。 |
|  MIP_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 < < 10  | コンテンツ ヘッダーの削除アクション タイプ。 |
|  MIP_ACTION_TYPE_REMOVE_PROTECTION = 1 < < 11      | 保護の削除アクション タイプ。 |
|  MIP_ACTION_TYPE_REMOVE_WATERMARK = 1 < < 12       | ウォーターマークの削除アクション タイプ。 |
|  MIP_ACTION_TYPE_APPLY_LABEL = 1 < < 13            | ラベルの適用アクション タイプ。 |
|  MIP_ACTION_TYPE_RECOMMEND_LABEL = 1 < < 14        | ラベルの推奨アクション タイプ。 |


```c
typedef enum {
  MIP_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 << 0,     
  MIP_ACTION_TYPE_ADD_CONTENT_HEADER = 1 << 1,     
  MIP_ACTION_TYPE_ADD_WATERMARK = 1 << 2,          
  MIP_ACTION_TYPE_CUSTOM = 1 << 3,                 
  MIP_ACTION_TYPE_JUSTIFY = 1 << 4,                
  MIP_ACTION_TYPE_METADATA = 1 << 5,               
  MIP_ACTION_TYPE_PROTECT_ADHOC = 1 << 6,          
  MIP_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 << 7,    
  MIP_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 << 8, 
  MIP_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 << 9,  
  MIP_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 << 10, 
  MIP_ACTION_TYPE_REMOVE_PROTECTION = 1 << 11,     
  MIP_ACTION_TYPE_REMOVE_WATERMARK = 1 << 12,      
  MIP_ACTION_TYPE_APPLY_LABEL = 1 << 13,           
  MIP_ACTION_TYPE_RECOMMEND_LABEL = 1 << 14,       
} mip_cc_action_type;

```

## <a name="mip_cc_label_action_state"></a>mip_cc_label_action_state

現在のラベルに関してアプリケーションが実行しようとしている内容について説明します。

| フィールド | [説明] |
|---|---|
|  MIP_LABEL_ACTION_STATE_NO_CHANGE = 0  | 現在のラベルは変更できません。  |
|  MIP_LABEL_ACTION_STATE_REMOVE = 1     | 現在のラベルは削除する必要があります。  |
|  MIP_LABEL_ACTION_STATE_UPDATE = 2     | 現在のラベルは変更する必要があります。  |


```c
typedef enum {
  MIP_LABEL_ACTION_STATE_NO_CHANGE = 0, 
  MIP_LABEL_ACTION_STATE_REMOVE = 1,    
  MIP_LABEL_ACTION_STATE_UPDATE = 2,    
} mip_cc_label_action_state;

```

## <a name="mip_cc_label_action_type"></a>mip_cc_label_action_type

アプリケーションが認識してサポートするラベル関連のアクション

| フィールド | [説明] |
|---|---|
|  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 < < 0      | ドキュメントのアクション タイプにコンテンツ フッターを追加します。  |
|  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_HEADER = 1 < < 1      | ドキュメントのアクション タイプにコンテンツ ヘッダーを追加します。  |
|  MIP_LABEL_ACTION_TYPE_ADD_WATERMARK = 1 < < 2           | ドキュメントのアクション タイプ全体にウォーター マークを追加します。  |
|  MIP_LABEL_ACTION_TYPE_CUSTOM = 1 < < 3                  | カスタム定義のアクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_JUSTIFY = 1 < < 4                 | 正当化アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_METADATA = 1 < < 5                | メタ データ変更のアクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_ADHOC = 1 < < 6           | アドホック ポリシーによる保護アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 < < 7     | テンプレートによる保護アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 < < 8  | 転送不可による保護アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 < < 9   | コンテンツ フッターの削除アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 < < 10  | コンテンツ ヘッダーの削除アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_PROTECTION = 1 < < 11      | 保護の削除アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_WATERMARK = 1 < < 12       | ウォーターマークの削除アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_APPLY_LABEL = 1 < < 13            | ラベルの適用アクション タイプ。  |
|  MIP_LABEL_ACTION_TYPE_RECOMMEND_LABEL = 1 < < 14        | ラベルの推奨アクション タイプ。  |


```c
typedef enum {
  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 << 0,     
  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_HEADER = 1 << 1,     
  MIP_LABEL_ACTION_TYPE_ADD_WATERMARK = 1 << 2,          
  MIP_LABEL_ACTION_TYPE_CUSTOM = 1 << 3,                 
  MIP_LABEL_ACTION_TYPE_JUSTIFY = 1 << 4,                
  MIP_LABEL_ACTION_TYPE_METADATA = 1 << 5,               
  MIP_LABEL_ACTION_TYPE_PROTECT_ADHOC = 1 << 6,          
  MIP_LABEL_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 << 7,    
  MIP_LABEL_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 << 8, 
  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 << 9,  
  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 << 10, 
  MIP_LABEL_ACTION_TYPE_REMOVE_PROTECTION = 1 << 11,     
  MIP_LABEL_ACTION_TYPE_REMOVE_WATERMARK = 1 << 12,      
  MIP_LABEL_ACTION_TYPE_APPLY_LABEL = 1 << 13,           
  MIP_LABEL_ACTION_TYPE_RECOMMEND_LABEL = 1 << 14,       
} mip_cc_label_action_type;

```

## <a name="mip_cc_data_state"></a>mip_cc_data_state

アプリケーションが動作しているときのデータの状態を定義します。

| フィールド | [説明] |
|---|---|
|  MIP_DATA_STATE_REST = 0    | 物理的にデータベース/ファイル/ウェアハウスに格納されている非アクティブなデータ  |
|  MIP_DATA_STATE_MOTION = 1  | ネットワークを通過するデータ、またはコンピューターのメモリ内で一時的に存在し、読み取りまたは更新されるデータ  |
|  MIP_DATA_STATE_USE = 2     | データベース/ファイル/ウェアハウスなどに物理的に格納されている定数の変更によるアクティブなデータ  |


```c
typedef enum {
  MIP_DATA_STATE_REST = 0,   
  MIP_DATA_STATE_MOTION = 1, 
  MIP_DATA_STATE_USE = 2,    
} mip_cc_data_state;

```

