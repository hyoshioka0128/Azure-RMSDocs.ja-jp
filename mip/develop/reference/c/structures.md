---
title: 構造体
description: 構成.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 9/22/2020
ms.openlocfilehash: 2939a4c64ab3e1a47704811875c6a7e941bcfe3c
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569382"
---
# <a name="structures"></a>構造体

## <a name="mip_cc_application_info"></a>mip_cc_application_info

アプリケーション固有の情報を含む構造体 

| フィールド | 説明 |
|---|---|
| applicationId | AAD ポータルで設定されたアプリケーション id (角かっこなしの GUID である必要があります)。  |
| applicationName | アプリケーション名 ('; ' を除く有効な ASCII 文字のみを含める必要があります)  |
| applicationVersion | 使用されているアプリケーションのバージョン ('; ' を除く有効な ASCII 文字のみを含める必要があります)   |


```c
typedef struct {
  const char* applicationId;      
  const char* applicationName;    
  const char* applicationVersion; 
} mip_cc_application_info;

```

## <a name="mip_cc_oauth2_challenge"></a>mip_cc_oauth2_challenge

OAuth2 トークンを生成するためにサーバーによって提供される情報

| フィールド | 説明 |
|---|---|
| authority | OAuth2 機関  |
| resource | OAuth2 リソース  |
| scope | OAuth2 スコープ  |


```c
typedef struct {
  const char* authority; 
  const char* resource;  
  const char* scope;     
} mip_cc_oauth2_challenge;

```

## <a name="mip_cc_handle"></a>mip_cc_handle

MIP オブジェクトへの非透過ハンドル

| フィールド | 説明 |
|---|---|
| typeId | 特定のハンドルの種類を一意に識別するマジック番号  |
| [データ] | 未処理のハンドルデータ  |


```c
typedef struct {
  uint32_t typeId; 
  void* data;      
} mip_cc_handle;

```

## <a name="mip_cc_guid"></a>mip_cc_guid

GUID

```c
typedef struct {
  char guid[37];
} mip_cc_guid;

```

## <a name="mip_cc_kv_pair"></a>mip_cc_kv_pair

キーと値のペア

| フィールド | 説明 |
|---|---|
| key | キー  |
| value | 値  |


```c
typedef struct {
  const char* key;   
  const char* value; 
} mip_cc_kv_pair;

```

## <a name="mip_cc_error"></a>mip_cc_error

エラー情報

```c
typedef struct {
  mip_cc_result result;
  char description[ERROR_STRING_BUFFER_SIZE];

  // MIP_RESULT_ERROR_NETWORK details
  mip_cc_network_error_category networkError_Category;
  int32_t networkError_ResponseCode;

  // MIP_RESULT_ERROR_NO_PERMISSIONS details
  char noPermissionsError_Owner[ERROR_STRING_BUFFER_SIZE];
  char noPermissionsError_Referrer[ERROR_STRING_BUFFER_SIZE];

  // MIP_RESULT_ERROR_SERVICE_DISABLED details
  mip_cc_service_disabled_error_extent serviceDisabledError_Extent;
} mip_cc_error;

```

## <a name="mip_cc_http_header"></a>mip_cc_http_header

HTTP 要求/応答ヘッダー

| フィールド | 説明 |
|---|---|
| name | ヘッダー名/キー  |
| value | ヘッダー値  |


```c
typedef struct {
  const char* name;  
  const char* value; 
} mip_cc_http_header;

```

## <a name="mip_cc_http_request"></a>mip_cc_http_request

HTTP 要求

| フィールド | 説明 |
|---|---|
| id | 一意の要求 ID--mip_cc_http_response の同じプロパティと相関しています  |
| 型 | HTTP 要求の種類 (GET、POST など)  |
| url | HTTP 要求 URL  |
| bodySize | HTTP 要求本文のサイズ (バイト単位)  |
| body | Buffer 格納 HTTP 要求本文  |
| headersCount | HTTP 要求ヘッダーの数  |
| headers | HTTP 要求ヘッダーを格納しているバッファー  |


```c
typedef struct {
  const char* id;                    
  mip_cc_http_request_type type;     
  const char* url;                   
  int64_t bodySize;                  
  const uint8_t* body;               
  int64_t headersCount;              
  const mip_cc_http_header* headers; 
} mip_cc_http_request;

```

## <a name="mip_cc_http_response"></a>mip_cc_http_response

HTTP 応答

| フィールド | 説明 |
|---|---|
| id | 一意の要求 ID--mip_cc_http_request の同じプロパティと相関しています  |
| statusCode | HTTP 応答の状態コード  |
| bodySize | HTTP 応答本文のサイズ (バイト単位)  |
| body | Buffer 格納 HTTP 応答本文  |
| headersCount | HTTP 応答ヘッダーの数  |
| headers | HTTP 応答ヘッダーを含むバッファー  |


```c
typedef struct {
  const char* id;                    
  int32_t statusCode;                
  int64_t bodySize;                  
  const uint8_t* body;               
  int64_t headersCount;              
  const mip_cc_http_header* headers; 
} mip_cc_http_response;

```

## <a name="mip_cc_identity"></a>mip_cc_identity

ユーザー識別情報を格納する構造体。

| フィールド | 説明 |
|---|---|
| email | ユーザーの電子メール アドレス  |
| name | コンテンツのマーキングに使用されるユーザーフレンドリ名。  |


```c
typedef struct {
  const char* email;          
  const char* name;           
} mip_cc_identity;

```

## <a name="mip_cc_feature_override"></a>mip_cc_feature_override

1つの機能の有効/無効の状態を定義します。

| フィールド | 説明 |
|---|---|
| の機能 | 機能名  |
| value | 有効/無効の状態  |


```c
typedef struct {
  mip_cc_flighting_feature feature; 
  bool value;                       
} mip_cc_feature_override;

```

## <a name="mip_cc_user_rights"></a>mip_cc_user_rights

ユーザーのグループとそれに関連付けられている権限

| フィールド | 説明 |
|---|---|
| users | ユーザーの一覧  |
| ユーザ数 | ユーザー数  |
| 権限 | 権限の一覧  |
| rightsCount | 権限の数  |


```c
typedef struct {
  const char** users;  
  int64_t usersCount;  
  const char** rights; 
  int64_t rightsCount; 
} mip_cc_user_rights;

```

## <a name="mip_cc_user_roles"></a>mip_cc_user_roles

ユーザーのグループとそれに関連付けられているロール

| フィールド | 説明 |
|---|---|
| users | ユーザーの一覧  |
| ユーザ数 | ユーザー数  |
| roles | ロールの一覧  |
| ロール数 | ロール数  |


```c
typedef struct {
  const char** users;  
  int64_t usersCount;  
  const char** roles; 
  int64_t rolesCount; 
} mip_cc_user_roles;

```

## <a name="mip_cc_async_task"></a>mip_cc_async_task

単一の非同期タスクのディスパッチ要求を定義します

| フィールド | 説明 |
|---|---|
| id | タスク ID  |
| delayMs | タスクの実行までの遅延時間 (ミリ秒)  |
| executeOnIndependentThread | このタスクを完全に独立したスレッドで実行するか、共有スレッドを再利用できるかを指定します。  |


```c
typedef struct {
  const char* id;                   
  int64_t delayMs;                  
  bool executeOnIndependentThread;  
} mip_cc_async_task;

```

## <a name="mip_cc_application_action_state"></a>mip_cc_application_action_state

ラベル関連の操作を実行するときのアプリケーションの現在の状態を表します。

| フィールド | 説明 |
|---|---|
| actionState | アプリケーションがラベルの状態を変更しようとしているかどうかを示します。  |
| newLabel | ' ActionType ' が ' UPDATE ' の場合: 新しいラベル。  |
| newLabelExtendedProperties | ' ActionType ' が ' UPDATE ' の場合は、メタデータに書き込む追加のプロパティ。  |
| Newlabelのメソッド | ' ActionType ' が ' UPDATE ' の場合は、新しいラベルの割り当て方法。  |
| isDowngradeJustified | ' ActionType ' が ' UPDATE ' の場合: ラベルダウングレードがユーザーによって正当化されているかどうか。  |
| downgradeJustification | ' ActionType ' が ' UPDATE ' の場合: ユーザーが指定したダウングレードの理由テキスト。  |
| supportedActions | アプリケーションが実行できるラベル関連のアクションを記述する列挙マスク。  |


```c
typedef struct {
  mip_cc_label_action_state actionState;                    
  mip_cc_label newLabel;                                    
  mip_cc_dictionary newLabelExtendedProperties;             
  mip_cc_label_assignment_method newLabelAssignmentMethod;  
  bool isDowngradeJustified;                                
  const char* downgradeJustification;                       
  mip_cc_label_action_type supportedActions;                
} mip_cc_application_action_state;

```

## <a name="mip_cc_document_state"></a>mip_cc_document_state

名前/プレフィックスでフィルター処理されたドキュメント metatdata を取得するためのコールバック関数定義。

| フィールド | 説明 |
|---|---|
| dataState | アプリケーションと対話するときのドキュメントデータの状態。 |
| contentMetadataCallback | ドキュメントメタデータのコールバック。 |
| protectionDescriptor | ドキュメントが現在保護されている場合は保護記述子、それ以外の場合は null。  |
| contentFormat | ドキュメントの形式 (ファイルと電子メール)。  |
| auditMetadata | 監査レポートを送信するときに使用される、アプリケーション固有のオプションのメタデータ。 認識される値: "送信者": 送信者の電子メールアドレス。' 受信者 ': 電子メールの受信者の JSON 配列です。' Lastmodified ': ドキュメントを最後に変更したユーザーの電子メールアドレス。' LastModifiedDate ': ドキュメントが最後に変更された日付  |
| contentMetadataVersion | ドキュメントメタデータのバージョン。既定値は0です。  |
| contentMetadataVersionFormat | メタデータのバージョン管理の処理方法について説明します。  |

```c
typedef struct {

  const char* contentId;


  mip_cc_data_state dataState;

  mip_cc_metadata_callback contentMetadataCallback;

  mip_cc_protection_descriptor protectionDescriptor;

  mip_cc_content_format contentFormat;

  mip_cc_dictionary auditMetadata;

  uint32_t contentMetadataVersion;

  mip_cc_metadata_version_format contentMetadataVersionFormat;

} mip_cc_document_state;

```

## <a name="mip_cc_metadata_entry"></a>mip_cc_metadata_entry

メタデータエントリ

| フィールド | 説明 |
|---|---|
| key | キーの入力 |
| value | 値の入力  |
| version | バージョンエントリは、特にわからない限り0に初期化する必要があります。 |


```c
typedef struct {
  const char* key;        
  const char* value;      
  uint32_t version;       
} mip_cc_metadata_entry;

```

