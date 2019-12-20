---
title: 構造
description: 構成.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: aa544dfbd046ae8c3137cbc115d9af6ea219bc07
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73591597"
---
# <a name="structures"></a>構造

## <a name="mip_cc_application_info"></a>mip_cc_application_info

アプリケーション固有の情報を含む構造体 

| フィールド | [説明] |
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

| フィールド | [説明] |
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

## <a name="mip_cc_guid"></a>mip_cc_guid

GUID

```c
typedef struct {
  char guid[37];
} mip_cc_guid;

```

## <a name="mip_cc_kv_pair"></a>mip_cc_kv_pair

キー/値ペア

| フィールド | [説明] |
|---|---|
| key | キー  |
| value | 値  |


```c
typedef struct {
  const char* key;   
  const char* value; 
} mip_cc_kv_pair;

```

## <a name="mip_cc_http_header"></a>mip_cc_http_header

HTTP 要求/応答ヘッダー

| フィールド | [説明] |
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

| フィールド | [説明] |
|---|---|
| id | 一意の要求 ID--mip_cc_http_response の同じプロパティと相関しています  |
| type | HTTP 要求の種類 (GET、POST など)  |
| url | HTTP 要求 URL  |
| bodySize | HTTP 要求本文のサイズ (バイト単位)  |
| body | Buffer 格納 HTTP 要求本文  |
| headersCount | HTTP 要求ヘッダーの数  |
| ヘッダー | HTTP 要求ヘッダーを格納しているバッファー  |


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

| フィールド | [説明] |
|---|---|
| id | 一意の要求 ID--mip_cc_http_request の同じプロパティと相関しています  |
| StatusCode | HTTP 応答の状態コード  |
| bodySize | HTTP 応答本文のサイズ (バイト単位)  |
| body | Buffer 格納 HTTP 応答本文  |
| headersCount | HTTP 応答ヘッダーの数  |
| ヘッダー | HTTP 応答ヘッダーを含むバッファー  |


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

アプリケーション固有の情報を含む構造体 

| フィールド | [説明] |
|---|---|
| 電子メール | ユーザーの電子メール アドレス  |


```c
typedef struct {
  const char* email;          
} mip_cc_identity;

```

## <a name="mip_cc_feature_override"></a>mip_cc_feature_override

1つの機能の有効/無効の状態を定義します。

| フィールド | [説明] |
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

| フィールド | [説明] |
|---|---|
| ユーザー | ユーザーの一覧  |
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

| フィールド | [説明] |
|---|---|
| ユーザー | ユーザーの一覧  |
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

| フィールド | [説明] |
|---|---|
| id | [タスク ID]  |
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

| フィールド | [説明] |
|---|---|
| actionState | アプリケーションがラベルの状態を変更しようとしているかどうかを示します。  |
| newLabel | ' ActionType ' が ' UPDATE ' の場合: 新しいラベル。  |
| newLabelExtendedProperties | ' ActionType ' が ' UPDATE ' の場合は、メタデータに書き込む追加のプロパティ。  |
| Newlabel割り当て Ementmethod | ' ActionType ' が ' UPDATE ' の場合は、新しいラベルの割り当て方法。  |
| isDowngradeJustified | ' ActionType ' が ' UPDATE ' の場合: ラベルダウングレードがユーザーによって正当化されているかどうか。  |
| downgradeJustification | ' ActionType ' が ' UPDATE ' の場合: ユーザーが指定したダウングレードの理由テキスト。  |
| supportedActions | アプリケーションが実行できるラベル関連のアクションを記述する列挙マスク。  |


```c
typedef struct {
  mip_cc_label_action_state actionState;                    
  mip_cc_label newLabel;                                    
  mip_cc_dictionary newLabelExtendedProperties;             
  mip_cc_label_assignment_method newLabelAssignementMethod; 
  bool isDowngradeJustified;                                
  const char* downgradeJustification;                       
  mip_cc_label_action_type supportedActions;                
} mip_cc_application_action_state;

```

## <a name="mip_cc_document_state"></a>mip_cc_document_state

ラベル認識ドキュメントの現在の状態を表します。

| フィールド | [説明] |
|---|---|
| contentId | ユーザーが判読できるドキュメントの説明がテナント監査ポータルに表示されます。 ファイルの例: [表し];電子メールの例: [件名: 送信者]。 |
| dataState | アプリケーションと対話するときのドキュメントデータの状態  |
| contentMetadataCallback | ドキュメントメタデータのコールバック  |
| protectionDescriptor | ドキュメントが現在保護されている場合は保護記述子、それ以外の場合は null  |
| contentFormat | ドキュメントの形式 (ファイルと電子メール)  |
| auditMetadata | 監査レポートを送信するときに使用される、アプリケーション固有のオプションのメタデータ。 認識される値: "送信者": 送信者の電子メールアドレス。' 受信者 ': 電子メールの受信者の JSON 配列です。' Lastmodified ': ドキュメントを最後に変更したユーザーの電子メールアドレス。' LastModifiedDate ': ドキュメントが最後に変更された日付。 |

```c
typedef struct {
  const char* contentId;
  mip_cc_data_state dataState;
  mip_cc_metadata_callback contentMetadataCallback;
  mip_cc_protection_descriptor protectionDescriptor;
  mip_cc_content_format contentFormat;
  mip_cc_dictionary auditMetadata;
} mip_cc_document_state;