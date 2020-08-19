---
title: 関数
description: 関数
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 4/16/2020
ms.openlocfilehash: 12aa46260b9c1ed2bac5f1e02c1e358292e86835
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564383"
---
# <a name="functions-c"></a>関数 (C)

## <a name="mip_cc_auth_callback"></a>mip_cc_auth_callback

OAuth2 トークンを取得するためのコールバック関数の定義

**パラメーター**

パラメーター | 説明
|---|---|
| ID | トークンを取得する対象の電子メールアドレス |
| challenge | OAuth2 チャレンジ |
| context | この認証コールバックの原因となった MIP API に渡された非透過アプリケーションコンテキスト |
| tokenBuffer | Outputトークンがコピーされるバッファー。 Null の場合、' actualTokenSize ' が設定されますが、 |
| tokenBufferSize | 出力バッファーのサイズ (バイト単位) |
| actualTokenSize | Outputトークンの実際のサイズ (バイト単位) |

**Return**: True がトークンを取得した場合は、それ以外の場合は false

```c
MIP_CC_CALLBACK(mip_cc_auth_callback,
    bool,
    const mip_cc_identity*,
    const mip_cc_oauth2_challenge*,
    const void*,
    uint8_t*,
    const int64_t,
    int64_t*);
```

## <a name="mip_cc_consent_callback"></a>mip_cc_consent_callback

ユーザーから外部サービスエンドポイントへのアクセスに同意するためのコールバック関数定義

**パラメーター**

パラメーター | 説明
|---|---|
| url | SDK がユーザーの同意を必要とする URL |

**戻り値**: ユーザーの同意応答

```c
MIP_CC_CALLBACK(mip_cc_consent_callback,
    mip_cc_consent,
    const char*);
```

## <a name="mip_cc_createdictionary"></a>MIP_CC_CreateDictionary

文字列のキー/値の辞書を作成する

**パラメーター**

パラメーター | 説明
|---|---|
| entries | キー/値ペアの配列 |
| count | キー/値ペアの数 |
| ディクショナリ | Output新しく作成されたディクショナリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: mip_cc_dictionary は、を呼び出して解放する必要があり MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CreateDictionary(
    const mip_cc_kv_pair* entries,
    const int64_t count,
    mip_cc_dictionary* dictionary,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_dictionary_getentries"></a>MIP_CC_Dictionary_GetEntries

ディクショナリを構成するキーと値のペアを取得する

**パラメーター**

パラメーター | 説明
|---|---|
| ディクショナリ | ソースディクショナリ |
| entries | Outputキー/値ペアの配列、mip_cc_dictionary オブジェクトによって所有されているメモリ |
| count | Outputキー/値ペアの数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' entries ' のメモリは mip_cc_dictionary オブジェクトによって所有されているため、個別に解放しないでください。 

```c
mip_cc_result MIP_CC_Dictionary_GetEntries(
    const mip_cc_dictionary dictionary,
    mip_cc_kv_pair** entries,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasedictionary"></a>MIP_CC_ReleaseDictionary

ディクショナリに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| ディクショナリ | リリースされるディクショナリ |

```c
void MIP_CC_ReleaseDictionary(mip_cc_dictionary dictionary);
```

## <a name="mip_cc_http_send_callback_fn"></a>mip_cc_http_send_callback_fn

HTTP 要求を発行するためのコールバック関数の定義

**パラメーター**

パラメーター | 説明
|---|---|
| request | アプリケーションによって実行される HTTP 要求 |
| context | この HTTP 要求の原因となった MIP API 呼び出しに渡された、同じ不透明なコンテキスト。 |

```c
MIP_CC_CALLBACK(mip_cc_http_send_callback_fn,
    void,
    const mip_cc_http_request*,
    const void*);
```

## <a name="mip_cc_http_cancel_callback_fn"></a>mip_cc_http_cancel_callback_fn

HTTP 要求をキャンセルするためのコールバック関数の定義

**パラメーター**

パラメーター | 説明
|---|---|
| requestId | キャンセルされる HTTP 要求の ID |

```c
MIP_CC_CALLBACK(mip_cc_http_cancel_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_createhttpdelegate"></a>MIP_CC_CreateHttpDelegate

MIP の既定の HTTP スタックをオーバーライドするために使用できる HTTP デリゲートを作成します。

**パラメーター**

パラメーター | 説明
|---|---|
| sendCallback | HTTP 要求を発行するための関数ポインター |
| cancelCallback | HTTP 要求をキャンセルするための関数ポインター |
| httpDelegate | OutputHTTP delegate オブジェクトへのハンドル |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateHttpDelegate(
    const mip_cc_http_send_callback_fn sendCallback,
    const mip_cc_http_cancel_callback_fn cancelCallback,
    mip_cc_http_delegate* httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_notifyhttpdelegateresponse"></a>MIP_CC_NotifyHttpDelegateResponse

Http 応答の準備ができていることを HTTP デリゲートに通知します

**パラメーター**

パラメーター | 説明
|---|---|
| httpDelegate | HTTP delegate オブジェクトへのハンドル |
| requestId | この操作に関連付けられている HTTP 要求の ID |
| 結果 | 操作の成功/失敗の状態 |
| 応答 | 操作が成功した場合は HTTP 応答、それ以外の場合は nullptr |

**メモ**: この関数は、HTTP 操作が完了したときにアプリケーションによって呼び出される必要があります。 HTTP 応答の ID が HTTP 要求の ID と一致し、MIP が応答とその要求を関連付けることができるようにする必要があります。 

```c
void MIP_CC_NotifyHttpDelegateResponse(
    const mip_cc_http_delegate httpDelegate,
    const char* requestId,
    const mip_cc_http_result result,
    const mip_cc_http_response* response);
```

## <a name="mip_cc_releasehttpdelegate"></a>MIP_CC_ReleaseHttpDelegate

HTTP デリゲートハンドルに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| httpDelegate | 解放される HTTP デリゲート |

```c
void MIP_CC_ReleaseHttpDelegate(mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_logger_init_callback_fn"></a>mip_cc_logger_init_callback_fn

Logger を初期化するためのコールバック関数の定義

**パラメーター**

パラメーター | 説明
|---|---|
| storagePath | ログが格納されるファイルパス |

```c
MIP_CC_CALLBACK(mip_cc_logger_init_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_logger_write_callback_fn"></a>mip_cc_logger_write_callback_fn

Log ステートメントを記述するためのコールバック関数の定義

**パラメーター**

パラメーター | 説明
|---|---|
| レベル | log ステートメントのログレベルです。 |
| message | log ステートメントのメッセージ。 |
| 関数 (function) | log ステートメントの関数名。 |
| file | log ステートメントが生成されたファイルの名前。 |
| line | log ステートメントが生成された行番号。 |

```c
MIP_CC_CALLBACK(mip_cc_logger_write_callback_fn,
    void,
    const mip_cc_log_level,
    const char*,
    const char*,
    const char*,
    const int32_t);
```

## <a name="mip_cc_createloggerdelegate"></a>MIP_CC_CreateLoggerDelegate

Mipmap の既定のロガーをオーバーライドするために使用できる logger デリゲートを作成します。

**パラメーター**

パラメーター | 説明
|---|---|
| initCallback | 初期化のための関数ポインター |
| flushCallback | ログをフラッシュするための関数ポインター |
| writeCallback | Log ステートメントを記述するための関数ポインター |
| loggerDelegate | OutputLogger デリゲートオブジェクトを処理するハンドル |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateLoggerDelegate(
    const mip_cc_logger_init_callback_fn initCallback,
    const mip_cc_logger_flush_callback_fn flushCallback,
    const mip_cc_logger_write_callback_fn writeCallback,
    mip_cc_logger_delegate* loggerDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseloggerdelegate"></a>MIP_CC_ReleaseLoggerDelegate

Logger デリゲートハンドルに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| loggerDelegate | 解放される logger デリゲート |

```c
void MIP_CC_ReleaseLoggerDelegate(mip_cc_logger_delegate loggerDelegate);
```

## <a name="mip_cc_createmipcontext"></a>MIP_CC_CreateMipContext

すべてのプロファイルインスタンス間で共有される状態を管理する MIP コンテキストを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| applicationInfo | 保護 SDK を使用しているアプリケーションに関する情報 |
| path | ログ記録、テレメトリ、その他の保護関連資料が格納されるファイルパス |
| logLevel | Miplog の最小ログレベル |
| isOfflineOnly | ネットワーク操作を有効または無効にします (オフライン時にサポートされるすべての操作ではありません) |
| loggerDelegateOverride | OptionalLogger オーバーライドの実装 |
| telemetryOverride | Optionalオーバーライドされたテレメトリ設定。 NULL の場合、既定の設定が使用されます |
| mipContext | Output新しく作成された mipmap コンテキストインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateMipContext(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    mip_cc_mip_context* mipContext,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmipcontextwithcustomfeaturesettings"></a>MIP_CC_CreateMipContextWithCustomFeatureSettings

すべてのプロファイルインスタンス間で共有される状態を管理する MIP コンテキストを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| applicationInfo | 保護 SDK を使用しているアプリケーションに関する情報 |
| path | ログ記録、テレメトリ、その他の保護関連資料が格納されるファイルパス |
| logLevel | Miplog の最小ログレベル |
| isOfflineOnly | ネットワーク操作を有効または無効にします (オフライン時にサポートされるすべての操作ではありません) |
| loggerDelegateOverride | OptionalLogger オーバーライドの実装 |
| telemetryOverride | Optionalオーバーライドされたテレメトリ設定。 NULL の場合、既定の設定が使用されます |
| featureSettings | Optionalカスタム機能のオーバーライドの配列 |
| featureSettingsSize | カスタム機能のオーバーライドのサイズ (上書き数) |
| mipContext | Output新しく作成された mipmap コンテキストインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateMipContextWithCustomFeatureSettings(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    const mip_cc_feature_override* featureSettings,
    const int64_t featureSettingsSize,
    mip_cc_mip_context* mipContext,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasemipcontext"></a>MIP_CC_ReleaseMipContext

Mipmap コンテキストに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| mipContext | 解放される MIP コンテキスト |

```c
void MIP_CC_ReleaseMipContext(mip_cc_mip_context mipContext);
```

## <a name="mip_cc_protectiondescriptor_getprotectiontype"></a>MIP_CC_ProtectionDescriptor_GetProtectionType

RMS テンプレートによって定義されているかどうかにかかわらず、保護の種類を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| protectionType | Output保護の種類 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetProtectionType(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_protection_type* protectionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getownersize"></a>MIP_CC_ProtectionDescriptor_GetOwnerSize

所有者を格納するために必要なバッファーのサイズを取得します

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| ownerSize | Output所有者を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwnerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getowner"></a>MIP_CC_ProtectionDescriptor_GetOwner

保護所有者を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| ownerBuffer | Output所有者がコピーされるバッファー。 |
| ownerBufferSize | OwnerBuffer のサイズ (文字数)。 |
| actualOwnerSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ownerbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualOwnerSize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwner(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getnamesize"></a>MIP_CC_ProtectionDescriptor_GetNameSize

名前を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| nameSize | Output名前を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetNameSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getname"></a>MIP_CC_ProtectionDescriptor_GetName

保護名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| nameBuffer | Output名前がコピーされるバッファー。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetName(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescriptionsize"></a>MIP_CC_ProtectionDescriptor_GetDescriptionSize

説明を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| 説明のサイズ | Output説明を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescriptionSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescription"></a>MIP_CC_ProtectionDescriptor_GetDescription

保護の説明を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| descriptionBuffer | Output説明のコピー先となるバッファー。 |
| descriptionBufferSize | DescriptionBuffer のサイズ (文字数)。 |
| actualDescriptionSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: descriptionbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualdescriptionsize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescription(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_gettemplateid"></a>MIP_CC_ProtectionDescriptor_GetTemplateId

テンプレート ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| templateId | Output保護に関連付けられているテンプレート ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetTemplateId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getlabelid"></a>MIP_CC_ProtectionDescriptor_GetLabelId

ラベル ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| labelId | Output保護に関連付けられているラベル ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetLabelId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentid"></a>MIP_CC_ProtectionDescriptor_GetContentId

コンテンツ ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| contentId | Output保護に関連付けられたコンテンツ ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doescontentexpire"></a>MIP_CC_ProtectionDescriptor_DoesContentExpire

コンテンツの有効期限が切れているかどうかを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| 有効期限が切れます | Outputコンテンツの有効期限が切れるかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesContentExpire(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesContentExpire,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentvaliduntil"></a>MIP_CC_ProtectionDescriptor_GetContentValidUntil

保護の有効期限 (エポックからの秒数) を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| contentValidUntil | Outputコンテンツの有効期限 (エポックからの秒数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentValidUntil(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* contentValidUntil,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doesallowofflineaccess"></a>MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess

オフラインアクセスが許可されているかどうかを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| アクセスの許可 | Outputオフラインアクセスが許可されているかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesAllowOfflineAccess,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrersize"></a>MIP_CC_ProtectionDescriptor_GetReferrerSize

参照元を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| referrerSize | Output参照元を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* referrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrer"></a>MIP_CC_ProtectionDescriptor_GetReferrer

保護参照元を取得します

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| referrerBuffer | Output参照元がコピーされるバッファー。 |
| referrerBufferSize | ReferrerBuffer のサイズ (文字数)。 |
| actualReferrerSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: referrerBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualReferrerSize は必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrer(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* referrerBuffer,
    const int64_t referrerBufferSize,
    int64_t* actualReferrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurlsize"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize

2つのキーの URL を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| url | Output2つのキーの URL を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurl"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl

2つのキーの URL を取得します

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| urlBuffer | OutputUrl がコピーされるバッファー。 |
| urlBufferSize | UrlBuffer のサイズ (文字数)。 |
| actualUrlSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: urlbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualurlsize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectiondescriptor"></a>MIP_CC_ReleaseProtectionDescriptor

保護記述子に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 解放される保護記述子 |

```c
void MIP_CC_ReleaseProtectionDescriptor(mip_cc_protection_descriptor protectionDescriptor);
```

## <a name="mip_cc_createstringlist"></a>MIP_CC_CreateStringList

文字列リストの作成

**パラメーター**

パラメーター | 説明
|---|---|
| 文字列 | 文字列の配列 |
| count | 文字列の数 |
| stringList | Output新しく作成された文字列リスト |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: mip_cc_string_list は、を呼び出して解放する必要があり MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_CreateStringList(
    const char** strings,
    const int64_t count,
    mip_cc_string_list* stringList,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_stringlist_getstrings"></a>MIP_CC_StringList_GetStrings

文字列リストを構成する文字列を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| stringList | ソース文字列リスト |
| 文字列 | Output文字列の配列、mip_cc_string_list オブジェクトによって所有されているメモリ |
| count | Output文字列の数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' strings ' のメモリは mip_cc_string_list オブジェクトによって所有されているため、個別に解放しないでください。 

```c
mip_cc_result MIP_CC_StringList_GetStrings(
    const mip_cc_string_list stringList,
    const char*** strings,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasestringlist"></a>MIP_CC_ReleaseStringList

文字列リストに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| stringList | 解放される文字列リスト |

```c
void MIP_CC_ReleaseStringList(mip_cc_string_list stringList);
```

## <a name="mip_cc_dispatch_task_callback_fn"></a>mip_cc_dispatch_task_callback_fn

非同期タスクをディスパッチするためのコールバック関数の定義

**パラメーター**

パラメーター | 説明
|---|---|
| taskId | 一意のタスク識別子 |

```c
MIP_CC_CALLBACK(mip_cc_dispatch_task_callback_fn,
    void,
    const mip_cc_async_task*);
```

## <a name="mip_cc_cancel_task_callback_fn"></a>mip_cc_cancel_task_callback_fn

バックグラウンドタスクをキャンセルするためのコールバック関数

**パラメーター**

パラメーター | 説明
|---|---|
| taskId | 一意のタスク識別子 |

**Return**: タスクが正常にキャンセルされた場合は True、それ以外の場合は false

```c
MIP_CC_CALLBACK(mip_cc_cancel_task_callback_fn,
    bool,
    const char*);
```

## <a name="mip_cc_createtaskdispatcherdelegate"></a>MIP_CC_CreateTaskDispatcherDelegate

MIP の既定の非同期タスク処理をオーバーライドするために使用できるタスクディスパッチャーデリゲートを作成します。

**パラメーター**

パラメーター | 説明
|---|---|
| dispatchTaskCallback | 非同期タスクをディスパッチするための関数ポインター |
| cancelTaskCallback | バックグラウンドタスクを取り消すための関数ポインター |
| cancelAllTasksCallback | すべてのバックグラウンドタスクをキャンセルするための関数ポインター |
| taskDispatcher | Outputタスクディスパッチャーデリゲートオブジェクトのハンドル |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateTaskDispatcherDelegate(
    const mip_cc_dispatch_task_callback_fn dispatchTaskCallback,
    const mip_cc_cancel_task_callback_fn cancelTaskCallback,
    const mip_cc_cancel_all_tasks_callback_fn cancelAllTasksCallback,
    mip_cc_task_dispatcher_delegate* taskDispatcher,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_executedispatchedtask"></a>MIP_CC_ExecuteDispatchedTask

タスクが現在のスレッドで実行するようにスケジュールされていることを TaskDispatcher デリゲートに通知します

**パラメーター**

パラメーター | 説明
|---|---|
| taskDispatcher | タスクディスパッチャーデリゲートオブジェクトのハンドル |
| taskId | この操作に関連付けられている非同期タスクの ID |

**メモ**: この関数は、タスクの実行がスケジュールされている場合に、アプリケーションによって呼び出される必要があります。 これにより、現在のスレッドでタスクが即時に実行されます。 この ID は、以前にディスパッチされ、取り消されていないタスクの ID と一致している必要があります。 

```c
void MIP_CC_ExecuteDispatchedTask(const mip_cc_task_dispatcher_delegate taskDispatcher, const char* taskId);
```

## <a name="mip_cc_releasetaskdispatcherdelegate"></a>MIP_CC_ReleaseTaskDispatcherDelegate

タスクディスパッチャーデリゲートハンドルに関連付けられているリソースの解放

**パラメーター**

パラメーター | 説明
|---|---|
| taskDispatcher | 解放されるタスクディスパッチャーデリゲート |

```c
void MIP_CC_ReleaseTaskDispatcherDelegate(mip_cc_task_dispatcher_delegate taskDispatcher);
```

## <a name="mip_cc_createtelemetryconfiguration"></a>MIP_CC_CreateTelemetryConfiguration

保護プロファイルの作成に使用する設定オブジェクトを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | Output既定の設定を含む新しく作成されたテレメトリ構成インスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateTelemetryConfiguration(
    mip_cc_telemetry_configuration* telemetryConfig,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethostname"></a>MIP_CC_TelemetryConfiguration_SetHostName

内部テレメトリ設定を上書きするテレメトリホスト名を設定する

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| hostName | ホスト名 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: このプロパティは、クライアントアプリケーションで同じ ARIA/1ds テレメトリコンポーネントが使用されており、その内部テレメトリ設定 (キャッシュ、ログ、優先順位など) を MIP の既定の設定の代わりに使用する場合に設定されます。 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHostName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* hostName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setlibraryname"></a>MIP_CC_TelemetryConfiguration_SetLibraryName

テレメトリ共有ライブラリオーバーライドの設定

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| libraryName | Aria/1DS SDK の C API を実装する DLL の名前 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: このプロパティは、の代わりに使用する必要がある ARIA/1DS SDK の C API を実装する既存のテレメトリ DLL がクライアントにある場合に設定され mip_ClientTelemetry.dll 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetLibraryName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* libraryName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethttpdelegate"></a>MIP_CC_TelemetryConfiguration_SetHttpDelegate

既定のテレメトリ HTTP スタックをクライアント独自にオーバーライドする

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| httpDelegate | クライアントアプリケーションによって実装される HTTP コールバックインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: このプロパティが設定されていない場合、テレメトリコンポーネントは MIP の既定の HTTP スタックを使用します 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHttpDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_settaskdispatcherdelegate"></a>MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate

既定の非同期タスクディスパッチャーをクライアント独自にオーバーライドする

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| taskDispatcherDelegate | クライアントアプリケーションによって実装されたタスクディスパッチャーコールバックインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setisnetworkdetectionenabled"></a>MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled

バックグラウンドスレッドでテレメトリコンポーネントがネットワークステータスに ping を実行できるかどうかを設定します。

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| isCachingEnabled | テレメトリコンポーネントが許可されているかどうか。バックグラウンドスレッドでネットワークステータスに ping を実行します。 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 既定値は ' true ' です 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isNetworkDetectionEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setislocalcachingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled

テレメトリコンポーネントでディスクへのキャッシュの書き込みが許可されているかどうかを設定します。

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| isCachingEnabled | テレメトリコンポーネントでディスクへのキャッシュの書き込みが許可されているかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 既定値は ' true ' です 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isCachingEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setistraceloggingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled

テレメトリコンポーネントでディスクへのログの書き込みが許可されているかどうかを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| isTraceLoggingEnabled | テレメトリコンポーネントでディスクへのログの書き込みが許可されているかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 既定値は ' true ' です 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTraceLoggingEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setistelemetryoptedout"></a>MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut

アプリケーション/ユーザーがオプションのテレメトリをオプトアウトしたかどうかを設定します。

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| isTelemetryOptedOut | アプリケーション/ユーザーがオプションのテレメトリをオプトアウトしたかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 既定値は ' false ' です 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTelemetryOptedOut,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setcustomsettings"></a>MIP_CC_TelemetryConfiguration_SetCustomSettings

カスタムテレメトリ設定を設定します

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| Customsettings.ini | カスタムテレメトリ設定 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetCustomSettings(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_addmaskedproperty"></a>MIP_CC_TelemetryConfiguration_AddMaskedProperty

テレメトリプロパティを mask に設定します

**パラメーター**

パラメーター | 説明
|---|---|
| telemetryConfig | テレメトリの構成 |
| eventName | イベント名 |
| propertyName | プロパティ名 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_TelemetryConfiguration_AddMaskedProperty(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* eventName,
    const char* propertyName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasetelemetryconfiguration"></a>MIP_CC_ReleaseTelemetryConfiguration

保護プロファイル設定に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| profileSettings | リリースされる保護プロファイルの設定 |

```c
void MIP_CC_ReleaseTelemetryConfiguration(mip_cc_telemetry_configuration telemetryConfig);
```

## <a name="mip_cc_releaseprotectionengine"></a>MIP_CC_ReleaseProtectionEngine

保護エンジンに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | 保護エンジンを解放する |

```c
void MIP_CC_ReleaseProtectionEngine(mip_cc_protection_engine engine);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforpublishing"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing

新しいコンテンツを公開するための保護ハンドラーを作成します

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ハンドラーが作成されるエンジン |
| settings | 保護ハンドラーの設定 |
| context | HttpDelegate と AuthDelegate に渡されるクライアントコンテキスト不透明 |
| handler | Output新しく作成された保護ハンドラーのインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing(
    const mip_cc_protection_engine engine,
    const mip_cc_protection_handler_publishing_settings settings,
    const void* context,
    mip_cc_protection_handler* handler,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforconsumption"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption

既存のコンテンツを使用するための保護ハンドラーを作成します

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ハンドラーが作成されるエンジン |
| settings | 保護ハンドラーの設定 |
| context | HttpDelegate と AuthDelegate に渡されるクライアントコンテキスト不透明 |
| handler | Output新しく作成された保護ハンドラーのインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption(
  const mip_cc_protection_engine engine,
  const mip_cc_protection_handler_consumption_settings settings,
  const void* context,
  mip_cc_protection_handler* handler,
  mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getengineidsize"></a>MIP_CC_ProtectionEngine_GetEngineIdSize

エンジン ID に必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | 保護エンジン |
| idSize | Outputエンジン ID を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineIdSize(
    const mip_cc_protection_engine engine,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getengineid"></a>MIP_CC_ProtectionEngine_GetEngineId

エンジン ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | 保護エンジン |
| idBuffer | OutputId がコピーされるバッファー。 |
| idBufferSize | IdBuffer のサイズ (文字数)。 |
| actualIdSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: idbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualIdSize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineId(
    const mip_cc_protection_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_gettemplatessize"></a>MIP_CC_ProtectionEngine_GetTemplatesSize

保護エンジンに関連付けられている RMS テンプレートの数を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | 保護エンジン |
| context | HttpDelegate と AuthDelegate に渡されるクライアントコンテキスト不透明 |
| テンプレートのサイズ | Outputテンプレートの数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**メモ**: この API は、独立した HTTP 操作になる可能性があります。 不要な余分な HTTP 操作を回避するには、事前に定義されたバッファーで ' MIP_CC_ProtectionEngine_GetTemplates ' を直接使用することを検討してください。 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplatesSize(
    const mip_cc_protection_engine engine,
    const void* context,
    int64_t* templatesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_gettemplates"></a>MIP_CC_ProtectionEngine_GetTemplates

ユーザーが使用できるテンプレートのコレクションを取得する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | 保護エンジン |
| context | HttpDelegate と AuthDelegate に渡されるクライアントコンテキスト不透明 |
| mip_cc_template_descriptor | [出力] テンプレートハンドラーを作成するためのバッファー。 |
| templateBufferSize | TemplateBuffer のサイズ (項目数)。 |
| Actualtemplates のサイズ | Outputバッファーに書き込まれたテンプレート Id の数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: templatebuffer が null または不十分な場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualTemplateSize は必要最小限のバッファーサイズに設定されます。 各 mip_cc_template_descriptor は MIP_CC_ReleaseTemplateDescriptor () を呼び出すことによって、呼び出し元によって解放される必要があります。 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplates(
    const mip_cc_protection_engine engine,
    const void* context,
    mip_cc_template_descriptor* templateDescriptors,
    const int64_t templateBufferSize,
    int64_t* actualTemplatesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getrightsforlabelid"></a>MIP_CC_ProtectionEngine_GetRightsForLabelId

ラベル ID に対してユーザーに付与された権限の一覧を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | 保護エンジン |
| context | HttpDelegate と AuthDelegate に渡されるクライアントコンテキスト不透明 |
| documentId | ドキュメントに割り当てられているドキュメント ID |
| labelId | ドキュメントに適用されたラベル ID |
| ownerEmail | ドキュメントの所有者 |
| delagedUserEmail | 認証を行っているユーザーまたはアプリケーションが別のユーザーの代理で動作している場合は、ユーザーの電子メール、何も指定しない場合は空 |
| 権限 | Outputユーザーに付与された権限の一覧、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' rights ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetRightsForLabelId(
    const mip_cc_protection_engine engine,
    const void* context,
    const char* documentId,
    const char* labelId,
    const char* ownerEmail,
    const char* delegatedUserEmail,
    mip_cc_string_list* rights,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getclientdatasize"></a>MIP_CC_ProtectionEngine_GetClientDataSize

保護エンジンに関連付けられているクライアントデータのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | 保護エンジン |
| clientDataSize | Outputクライアントデータのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientDataSize(
    const mip_cc_protection_engine engine,
    int64_t* clientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getclientdata"></a>MIP_CC_ProtectionEngine_GetClientData

保護エンジンに関連付けられているクライアントデータを取得する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | 保護エンジン |
| clientDataBuffer | Outputクライアントデータがコピーされるバッファー |
| clientDataBufferSize | ClientDataBuffer のサイズ (文字数)。 |
| actualClientDataSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: clientDataBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualClientDataSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientData(
    const mip_cc_protection_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionenginesettingswithidentity"></a>MIP_CC_CreateProtectionEngineSettingsWithIdentity

新しい保護エンジンを作成するために使用される設定オブジェクトを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| ID | ProtectionEngine に関連付けられる id |
| clientData | エンジンと共に保存されるカスタマイズ可能なクライアントデータ |
| locale | テキスト結果が出力されるロケール |
| engineSettings | Output新しく作成された設定インスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateProtectionEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    mip_cc_protection_engine_settings* engineSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setclientdata"></a>MIP_CC_ProtectionEngineSettings_SetClientData

このエンジンと共に不透明に格納され、セッション間で保持されるクライアントデータを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| clientData | クライアントデータ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetClientData(
    const mip_cc_protection_engine_settings engineSettings,
    const char* clientData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcustomsettings"></a>MIP_CC_ProtectionEngineSettings_SetCustomSettings

機能のゲートとテストに使用されるカスタム設定を構成します。

**パラメーター**

パラメーター | 説明
|---|---|
| engineSettings | エンジンの設定 |
| Customsettings.ini | カスタム設定のキーと値のペア |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCustomSettings(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setsessionid"></a>MIP_CC_ProtectionEngineSettings_SetSessionId

ログとテレメトリを関連付けるために使用できるセッション ID を設定します。

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| sessionID | 保護エンジンの有効期間を表すセッション ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetSessionId(
    const mip_cc_protection_engine_settings engineSettings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcloud"></a>MIP_CC_ProtectionEngineSettings_SetCloud

すべてのサービス要求のエンドポイント Url に影響するクラウドを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| cloud | クラウド識別子 (既定 = 不明) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: cloud が指定されていない場合は、可能であれば、エンジンの id ドメインの DNS 参照によって決定されます。それ以外の場合は、グローバルクラウドにフォールバックします。 

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloud(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_cloud cloud,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcloudendpointbaseurl"></a>MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl

すべてのサービス要求のベース URL を設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| cloudEndpointBaseUrl | ベース URL (例: ' https://api.aadrm.com ') |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: この値は読み取り専用であり、Cloud = MIP_CLOUD_CUSTOM に設定する必要があります 

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_protection_engine_settings engineSettings,
    const char* cloudEndpointBaseUrl,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionenginesettings"></a>MIP_CC_ReleaseProtectionEngineSettings

保護エンジンの設定に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| engineSettings | リリースされる保護エンジンの設定 |

```c
void MIP_CC_ReleaseProtectionEngineSettings(mip_cc_protection_engine_settings engineSettings);
```

## <a name="mip_cc_createprotectionhandlerpublishingsettings"></a>MIP_CC_CreateProtectionHandlerPublishingSettings

新しいコンテンツを公開するための保護ハンドラーの作成に使用される設定オブジェクトを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| ディスクリプタ | 保護の詳細 |
| settings | Output新しく作成された設定インスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateProtectionHandlerPublishingSettings(
    const mip_cc_protection_descriptor descriptor,
    mip_cc_protection_handler_publishing_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisdeprecatedalgorithmpreferred"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred

非推奨の暗号アルゴリズム (ECB) が下位互換性のために推奨されるかどうかを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 保護ハンドラーの設定 |
| isDeprecatedAlgorithmPreferred | 非推奨のアルゴリズムが推奨されるかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isDeprecatedAlgorithmPreferred,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisauditedextractionallowed"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed

非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されるかどうかを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 保護ハンドラーの設定 |
| isAuditedExtractionAllowed | 非 MIP 対応アプリケーションで保護されたコンテンツを開くことが許可されているかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isAuditedExtractionAllowed,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setispublishingformatjson"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson

PL が JSON 形式であるかどうかを設定します (既定は XML)

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 保護ハンドラーの設定 |
| isPublishingFormatJson | 結果として得られる PL が JSON 形式であるかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isPublishingFormatJson,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail

委任されたユーザーを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 保護ハンドラーの設定 |
| delegatedUserEmail | 委任されたユーザーの電子メールアドレス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作しているときに指定します。 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setprelicenseuseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail

ライセンス前のユーザーを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 保護ハンドラーの設定 |
| preLicenseUserEmail | ライセンス前のユーザーの電子メールアドレス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ライセンスを発行するときに事前ライセンスを取得する必要がある場合は、ライセンスを使用するユーザーを指定します。 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* preLicenseUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettings"></a>MIP_CC_CreateProtectionHandlerConsumptionSettings

既存のコンテンツを使用するための保護ハンドラーの作成に使用される設定オブジェクトを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| Licensebuffer の発行 | 未加工の公開ライセンスを含むバッファー |
| Licensebuffersize の発行 | 発行ライセンスバッファーのサイズ |
| settings | Output新しく作成された設定インスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettings(
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettingswithprelicense"></a>MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense

既存のコンテンツを使用するための保護ハンドラーの作成に使用される設定オブジェクトを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| preLicenseBuffer | 未処理のライセンスバッファーを含むバッファー |
| preLicenseBufferSize | ライセンスの前のバッファーのサイズ |
| Licensebuffer の発行 | 未加工の公開ライセンスを含むバッファー |
| Licensebuffersize の発行 | 発行ライセンスバッファーのサイズ |
| settings | Output新しく作成された設定インスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense(
    const uint8_t* preLicenseBuffer,
    const int64_t preLicenseBufferSize,
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setisofflineonly"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly

保護ハンドラーの作成でオンライン HTTP 操作が許可されるかどうかを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 保護ハンドラーの設定 |
| isOfflineOnly | HTTP 操作が禁止されている場合は True、それ以外の場合は false。 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: これが true に設定されている場合、コンテンツが既に暗号化解除されていて、その unexpired ライセンスがキャッシュされている場合にのみ、保護ハンドラーの作成が成功します。 キャッシュされたコンテンツが見つからない場合、MIP_RESULT_ERROR_NETWORK 結果が返されます。 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly(
    const mip_cc_protection_handler_consumption_settings settings,
    const bool isOfflineOnly,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail

委任されたユーザーを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 保護ハンドラーの設定 |
| delegatedUserEmail | 委任されたユーザーの電子メールアドレス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作しているときに指定します。 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_consumption_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize

発行ライセンスのサイズを取得します (バイト単位)

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| Licensebuffersize の発行 | Output発行ライセンスのサイズ (バイト単位) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize(
    const mip_cc_protection_handler handler,
    int64_t* publishingLicenseBufferSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicense"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicense

発行ライセンスを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| Licensebuffer の発行 | Output発行ライセンスが書き込まれるバッファー |
| Licensebuffersize の発行 | 発行ライセンスバッファーのサイズ |
| Actual発行 Licensesize | Output発行ライセンスの実際のサイズ (バイト単位) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 発行 licensebuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、Actual発行 licensesize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicense(
    const mip_cc_protection_handler handler,
    uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    int64_t* actualPublishingLicenseSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedprelicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize

プレライセンスのサイズを取得します (バイト単位)

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| format | ライセンス前の形式 |
| preLicenseBufferSize | Outputプレライセンスのサイズ (バイト単位) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize(
    const mip_cc_protection_handler handler,
    mip_cc_pre_license_format format,
    int64_t* preLicenseBufferSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedprelicense"></a>MIP_CC_ProtectionHandler_GetSerializedPreLicense

ライセンスの取得

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| format | ライセンス前の形式 |
| preLicenseBuffer | Output事前ライセンスが書き込まれるバッファー |
| preLicenseBufferSize | ライセンス前のバッファーのサイズ |
| actualPreLicenseSize | Output事前ライセンスの実際のサイズ (バイト単位) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: preLicenseBuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualPreLicenseSize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPreLicense(
    const mip_cc_protection_handler handler,
    mip_cc_pre_license_format format,
    uint8_t* preLicenseBuffer,
    const int64_t preLicenseBufferSize,
    int64_t* actualPreLicenseSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getprotectiondescriptor"></a>MIP_CC_ProtectionHandler_GetProtectionDescriptor

保護記述子を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| ディスクリプタ | Output保護記述子 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectionDescriptor(
    const mip_cc_protection_handler handler,
    mip_cc_protection_descriptor* descriptor,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getrights"></a>MIP_CC_ProtectionHandler_GetRights

ユーザーに付与されている権限の一覧を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| 権限 | Outputユーザーに付与された権限の一覧、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' rights ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetRights(
    const mip_cc_protection_handler handler,
    mip_cc_string_list* rights,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getprotectedcontentsize"></a>MIP_CC_ProtectionHandler_GetProtectedContentSize

保護されたコンテンツのサイズ、埋め込みのファクタリングなどを計算します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| unprotectedSize | 保護されていない/クリアテキストコンテンツのサイズ (バイト単位) |
| ある Finalfinalblock | 対象の保護されていないコンテンツに最後のブロックが含まれているかどうかを示します。 |
| protectedSize | Output保護されたコンテンツのサイズ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectedContentSize(
    const mip_cc_protection_handler handler,
    const int64_t unprotectedSize,
    const bool includesFinalBlock,
    int64_t* protectedSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getblocksize"></a>MIP_CC_ProtectionHandler_GetBlockSize

保護ハンドラーによって使用される暗号モードのブロックサイズ (バイト単位) を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| blockSize | Outputブロックサイズ (バイト単位) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_GetBlockSize(
    const mip_cc_protection_handler handler,
    int64_t* blockSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getissuedusersize"></a>MIP_CC_ProtectionHandler_GetIssuedUserSize

保護されたコンテンツへのアクセスが許可されているユーザーを格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| issuedUserSize | Output発行されたユーザーを保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUserSize(
    const mip_cc_protection_handler handler,
    int64_t* issuedUserSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getissueduser"></a>MIP_CC_ProtectionHandler_GetIssuedUser

保護されたコンテンツへのアクセスが許可されているユーザーを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| issuedUserBuffer | Output発行されたユーザーがコピーされるバッファー。 |
| issuedUserBufferSize | IssuedUserBuffer のサイズ (文字数)。 |
| actualIssuedUserSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: issuedUserBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualIssuedUserSize は必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUser(
    const mip_cc_protection_handler handler,
    char* issuedUserBuffer,
    const int64_t issuedUserBufferSize,
    int64_t* actualIssuedUserSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getownersize"></a>MIP_CC_ProtectionHandler_GetOwnerSize

保護されたコンテンツの所有者を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| ownerSize | Output発行されたユーザーを保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwnerSize(
    const mip_cc_protection_handler handler,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getowner"></a>MIP_CC_ProtectionHandler_GetOwner

保護されたコンテンツの所有者を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| ownerBuffer | Output発行されたユーザーがコピーされるバッファー。 |
| ownerBufferSize | OwnerBuffer のサイズ (文字数)。 |
| actualOwnerSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ownerbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualOwnerSize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwner(
    const mip_cc_protection_handler handler,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getcontentid"></a>MIP_CC_ProtectionHandler_GetContentId

保護されたコンテンツのコンテンツ IE を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| contentId | Outputコンテンツ ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_GetContentId(
    const mip_cc_protection_handler handler,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_doesusedeprecatedalgorithm"></a>MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm

保護ハンドラーが旧バージョンとの互換性のために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 保護されたコンテンツを表すハンドラー |
| doesUseDeprecatedAlgorithm | Output保護ハンドラーが非推奨の暗号アルゴリズムを使用するかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm(
    const mip_cc_protection_handler handler,
    bool* doesUseDeprecatedAlgorithm,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_decryptbuffer"></a>MIP_CC_ProtectionHandler_DecryptBuffer

バッファーの復号化

**パラメーター**

パラメーター | 説明
|---|---|
| offsetFromStart | 暗号化されたコンテンツの先頭からの inputBuffer の相対位置 |
| inputBuffer | 復号化される暗号化されたコンテンツのバッファー |
| inputBufferSize | 入力バッファーのサイズ (バイト単位) |
| outputBuffer | Output復号化されたコンテンツのコピー先のバッファー |
| outputBufferSize | 出力バッファーのサイズ (バイト単位) |
| isFinal | 入力バッファーに最後の暗号化されたバイトが含まれているかどうか |
| actualDecryptedSize | Output暗号化されたコンテンツの実際のサイズ (バイト単位) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionHandler_DecryptBuffer(
    const mip_cc_protection_handler handler,
    const int64_t offsetFromStart,
    const uint8_t* inputBuffer,
    const int64_t inputBufferSize,
    uint8_t* outputBuffer,
    const int64_t outputBufferSize,
    const bool isFinal,
    int64_t *actualDecryptedSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionhandlerpublishingsettings"></a>MIP_CC_ReleaseProtectionHandlerPublishingSettings

保護ハンドラーの設定に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 解放する保護ハンドラーの設定 |

```c
void MIP_CC_ReleaseProtectionHandlerPublishingSettings(mip_cc_protection_handler_publishing_settings settings);
```

## <a name="mip_cc_releaseprotectionhandlerconsumptionsettings"></a>MIP_CC_ReleaseProtectionHandlerConsumptionSettings

保護ハンドラーの設定に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| settings | 解放する保護ハンドラーの設定 |

```c
void MIP_CC_ReleaseProtectionHandlerConsumptionSettings(mip_cc_protection_handler_consumption_settings settings);
```

## <a name="mip_cc_releaseprotectionhandler"></a>MIP_CC_ReleaseProtectionHandler

保護ハンドラーに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| handler | 解放される保護ハンドラー |

```c
void MIP_CC_ReleaseProtectionHandler(mip_cc_protection_handler handler);
```

## <a name="mip_cc_loadprotectionprofile"></a>MIP_CC_LoadProtectionProfile

プロファイルの読み込み

**パラメーター**

パラメーター | 説明
|---|---|
| settings | プロファイルの設定 |
| profile | Output新しく作成された保護プロファイルインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_LoadProtectionProfile(
    const mip_cc_protection_profile_settings settings,
    mip_cc_protection_profile* profile,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionprofile"></a>MIP_CC_ReleaseProtectionProfile

保護プロファイルに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| profile | リリースされる保護プロファイル |

```c
void MIP_CC_ReleaseProtectionProfile(mip_cc_protection_profile profile);
```

## <a name="mip_cc_createprotectionprofilesettings"></a>MIP_CC_CreateProtectionProfileSettings

保護プロファイルの作成に使用する設定オブジェクトを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| mipContext | すべてのプロファイルで共有するグローバルコンテキスト |
| cacheStorageType | ストレージキャッシュの構成 |
| authCallback | クライアントアプリケーションによって実装される認証に使用されるコールバックオブジェクト |
| consentCallback | 同意に使用されるコールバックオブジェクト。クライアントアプリケーションによって実装されます。 |
| settings | Output新しく作成された設定インスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreateProtectionProfileSettings(
    const mip_cc_mip_context mipContext,
    const mip_cc_cache_storage_type cacheStorageType,
    const mip_cc_auth_callback authCallback,
    const mip_cc_consent_callback consentCallback,
    mip_cc_protection_profile_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setsessionid"></a>MIP_CC_ProtectionProfileSettings_SetSessionId

ログとテレメトリを関連付けるために使用できるセッション ID を設定します。

**パラメーター**

パラメーター | 説明
|---|---|
| settings | プロファイルの設定 |
| sessionID | 保護プロファイルの有効期間を表すセッション ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetSessionId(
    const mip_cc_protection_profile_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setcancachelicenses"></a>MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses

エンドユーザーライセンス (Eul) をローカルにキャッシュするかどうかを構成します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | プロファイルの設定 |
| canCacheLicenses | 保護されたコンテンツを開くときにエンジンがライセンスをキャッシュする必要があるかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses(
    const mip_cc_protection_profile_settings settings,
    const bool canCacheLicenses,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_sethttpdelegate"></a>MIP_CC_ProtectionProfileSettings_SetHttpDelegate

既定の HTTP スタックをクライアント独自にオーバーライドする

**パラメーター**

パラメーター | 説明
|---|---|
| settings | HTTP デリゲートが割り当てられるプロファイル設定 |
| httpDelegate | クライアントアプリケーションによって実装される HTTP コールバックインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetHttpDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate

既定の非同期タスクディスパッチャーをクライアント独自にオーバーライドする

**パラメーター**

パラメーター | 説明
|---|---|
| settings | タスクディスパッチャーデリゲートが割り当てられるプロファイル設定 |
| taskDispatcherDelegate | クライアントアプリケーションによって実装されたタスクディスパッチャーコールバックインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setcustomsettings"></a>MIP_CC_ProtectionProfileSettings_SetCustomSettings

機能のゲートとテストに使用されるカスタム設定を構成します。

**パラメーター**

パラメーター | 説明
|---|---|
| settings | プロファイルの設定 |
| Customsettings.ini | カスタム設定のキーと値のペア |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCustomSettings(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionprofilesettings"></a>MIP_CC_ReleaseProtectionProfileSettings

保護プロファイル設定に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| settings | リリースされる保護プロファイルの設定 |

```c
void MIP_CC_ReleaseProtectionProfileSettings(mip_cc_protection_profile_settings profilsettingseSettings);
```

## <a name="mip_cc_templatedescriptor_getid"></a>MIP_CC_TemplateDescriptor_GetId

テンプレート ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| protectionDescriptor | 保護されたコンテンツに関連付けられた記述子 |
| templateId | Output保護に関連付けられているテンプレート ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetId(
    const mip_cc_template_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getnamesize"></a>MIP_CC_TemplateDescriptor_GetNameSize

名前を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| templateDescriptor | テンプレートに関連付けられた記述子 |
| nameSize | Output名前を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetNameSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getname"></a>MIP_CC_TemplateDescriptor_GetName

テンプレート名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| templateDescriptor | テンプレートに関連付けられた記述子 |
| nameBuffer | Output名前がコピーされるバッファー。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetName(
    const mip_cc_template_descriptor templateDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescriptionsize"></a>MIP_CC_TemplateDescriptor_GetDescriptionSize

説明を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| templateDescriptor | テンプレートに関連付けられた記述子 |
| 説明のサイズ | Output説明を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescriptionSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescription"></a>MIP_CC_TemplateDescriptor_GetDescription

テンプレートの説明を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| templateDescriptor | テンプレートに関連付けられた記述子 |
| descriptionBuffer | Output説明のコピー先となるバッファー。 |
| descriptionBufferSize | DescriptionBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: descriptionbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualdescriptionsize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescription(
    const mip_cc_template_descriptor templateDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasetemplatedescriptor"></a>MIP_CC_ReleaseTemplateDescriptor

テンプレート記述子に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| templateDescriptor | 解放されるテンプレート記述子 |

```c
void MIP_CC_ReleaseTemplateDescriptor(mip_cc_template_descriptor templateDescriptor);
```

## <a name="mip_cc_action_gettype"></a>MIP_CC_Action_GetType

アクションの型を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | アクション |
| actionType | Outputアクションの種類 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Action_GetType(
    const mip_cc_action action,
    mip_cc_action_type* actionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_action_getid"></a>MIP_CC_Action_GetId

アクションの ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | アクション |
| id | Output一意のアクション ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Action_GetId(
    const mip_cc_action action,
    mip_cc_guid* id,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_actionresult_getactions"></a>MIP_CC_ActionResult_GetActions

アクションの結果を構成するアクションを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| actionResult | ソースアクションの結果 |
| actions | Outputアクションの配列、mip_cc_action_result オブジェクトによって所有されているメモリ |
| count | Outputキー/値ペアの数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' actions ' のメモリは mip_cc_action_result オブジェクトによって所有されているため、個別に解放しないでください。 

```c
mip_cc_result MIP_CC_ActionResult_GetActions(
    const mip_cc_action_result actionResult,
    mip_cc_action** actions,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseactionresult"></a>MIP_CC_ReleaseActionResult

アクションの結果に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| actionResult | リリースされるアクションの結果 |

```c
void MIP_CC_ReleaseActionResult(mip_cc_action_result actionResult);
```

## <a name="mip_cc_addcontentfooteraction_getuielementnamesize"></a>MIP_CC_AddContentFooterAction_GetUIElementNameSize

"コンテンツフッターの追加" アクションの UI 要素名を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| nameSize | OutputUI 要素名を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getuielementname"></a>MIP_CC_AddContentFooterAction_GetUIElementName

"コンテンツフッターの追加" アクションの UI 要素名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| nameBuffer | OutputUI 要素名がコピーされるバッファーです。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettextsize"></a>MIP_CC_AddContentFooterAction_GetTextSize

"コンテンツフッターの追加" アクションのテキストを格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| nameSize | Outputテキストを保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettext"></a>MIP_CC_AddContentFooterAction_GetText

"コンテンツフッターの追加" アクションのテキストを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| textBuffer | Outputテキストがコピーされるバッファー。 |
| textBufferSize | TextBuffer のサイズ (文字数)。 |
| actualTextSize 場合 | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: textBuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualtextsize 値が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontnamesize"></a>MIP_CC_AddContentFooterAction_GetFontNameSize

"コンテンツフッターの追加" アクションのフォント名を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| nameSize | Outputフォント名を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontname"></a>MIP_CC_AddContentFooterAction_GetFontName

"コンテンツフッターの追加" アクションのフォント名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| nameBuffer | Outputフォント名がコピーされるバッファーです。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontsize"></a>MIP_CC_AddContentFooterAction_GetFontSize

整数のフォントサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| fontSize | Outputフォントサイズ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolorsize"></a>MIP_CC_AddContentFooterAction_GetFontColorSize

"コンテンツフッターの追加" アクションのフォントの色を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| colorSize | Outputフォントの色を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolor"></a>MIP_CC_AddContentFooterAction_GetFontColor

"コンテンツフッターの追加" アクションのフォントの色 (例、"#000000") を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| colorBuffer | Outputフォントの色がにコピーされるバッファー。 |
| colorBufferSize | ColorBuffer のサイズ (文字数)。 |
| actualColorSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: colorbuffer が null または不十分な場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualcolorsize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getalignment"></a>MIP_CC_AddContentFooterAction_GetAlignment

配置を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| 配置 (alignment) | Output配置 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getmargin"></a>MIP_CC_AddContentFooterAction_GetMargin

余白のサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの追加" アクション |
| marginSize | Output余白のサイズ (mm) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementnamesize"></a>MIP_CC_AddContentHeaderAction_GetUIElementNameSize

"コンテンツヘッダーの追加" アクションの UI 要素名を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| nameSize | OutputUI 要素名を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementname"></a>MIP_CC_AddContentHeaderAction_GetUIElementName

"コンテンツヘッダーの追加" アクションの UI 要素名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| nameBuffer | OutputUI 要素名がコピーされるバッファーです。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettextsize"></a>MIP_CC_AddContentHeaderAction_GetTextSize

"コンテンツヘッダーの追加" アクションのテキストを格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| nameSize | Outputテキストを保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettext"></a>MIP_CC_AddContentHeaderAction_GetText

"コンテンツヘッダーの追加" アクションのテキストを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| textBuffer | Outputテキストがコピーされるバッファー。 |
| textBufferSize | TextBuffer のサイズ (文字数)。 |
| actualTextSize 場合 | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: textBuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualtextsize 値が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontnamesize"></a>MIP_CC_AddContentHeaderAction_GetFontNameSize

"コンテンツヘッダーの追加" アクションのフォント名を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| nameSize | Outputフォント名を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontname"></a>MIP_CC_AddContentHeaderAction_GetFontName

"コンテンツヘッダーの追加" アクションのフォント名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| nameBuffer | Outputフォント名がコピーされるバッファーです。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontsize"></a>MIP_CC_AddContentHeaderAction_GetFontSize

整数のフォントサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| fontSize | Outputフォントサイズ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolorsize"></a>MIP_CC_AddContentHeaderAction_GetFontColorSize

"コンテンツヘッダーの追加" アクションのフォントの色を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| colorSize | Outputフォントの色を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolor"></a>MIP_CC_AddContentHeaderAction_GetFontColor

"コンテンツヘッダーの追加" アクションのフォントの色 (例、"#000000") を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| colorBuffer | Outputフォントの色がにコピーされるバッファー。 |
| colorBufferSize | ColorBuffer のサイズ (文字数)。 |
| actualColorSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: colorbuffer が null または不十分な場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualcolorsize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getalignment"></a>MIP_CC_AddContentHeaderAction_GetAlignment

配置を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| 配置 (alignment) | Output配置 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getmargin"></a>MIP_CC_AddContentHeaderAction_GetMargin

余白のサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの追加" アクション |
| marginSize | Output余白のサイズ (mm) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementnamesize"></a>MIP_CC_AddWatermarkAction_GetUIElementNameSize

"透かしの追加" アクションの UI 要素名を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| nameSize | OutputUI 要素名を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementname"></a>MIP_CC_AddWatermarkAction_GetUIElementName

"透かしの追加" アクションの UI 要素名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| nameBuffer | OutputUI 要素名がコピーされるバッファーです。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getlayout"></a>MIP_CC_AddWatermarkAction_GetLayout

透かしのレイアウトを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| レイアウト | Output透かしのレイアウト |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetLayout(
    const mip_cc_action action,
    mip_cc_watermark_layout* layout,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettextsize"></a>MIP_CC_AddWatermarkAction_GetTextSize

"透かしの追加" アクションのテキストを格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| textSize | Outputテキストを保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettext"></a>MIP_CC_AddWatermarkAction_GetText

"透かしの追加" アクションのテキストを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| textBuffer | Outputテキストがコピーされるバッファー。 |
| textBufferSize | TextBuffer のサイズ (文字数)。 |
| actualTextSize 場合 | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: textBuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualtextsize 値が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontnamesize"></a>MIP_CC_AddWatermarkAction_GetFontNameSize

"透かしの追加" アクションのフォント名を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| nameSize | Outputフォント名を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontname"></a>MIP_CC_AddWatermarkAction_GetFontName

"透かしの追加" アクションのフォント名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| nameBuffer | Outputフォント名がコピーされるバッファーです。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontsize"></a>MIP_CC_AddWatermarkAction_GetFontSize

整数のフォントサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| fontSize | Outputフォントサイズ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolorsize"></a>MIP_CC_AddWatermarkAction_GetFontColorSize

"透かしの追加" アクションのフォントの色を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| colorSize | Outputフォントの色を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolor"></a>MIP_CC_AddWatermarkAction_GetFontColor

"透かしの追加" アクションのフォントの色 (例、"#000000") を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしの追加" アクション |
| colorBuffer | Outputフォントの色がにコピーされるバッファー。 |
| colorBufferSize | ColorBuffer のサイズ (文字数)。 |
| actualColorSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: colorbuffer が null または不十分な場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualcolorsize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasecontentlabel"></a>MIP_CC_ReleaseContentLabel

コンテンツラベルに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| contentLabel | リリースされるラベル |

```c
void MIP_CC_ReleaseContentLabel(mip_cc_content_label contentLabel);
```

## <a name="mip_cc_contentlabel_getcreationtime"></a>MIP_CC_ContentLabel_GetCreationTime

ラベルが適用された時刻を取得します

**パラメーター**

パラメーター | 説明
|---|---|
| contentLabel | ラベル |
| creationTime | Outputラベルがドキュメントに適用された時刻 (エポックからの秒単位) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ContentLabel_GetCreationTime(
    const mip_cc_content_label contentLabel,
    int64_t* creationTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getassignmentmethod"></a>MIP_CC_ContentLabel_GetAssignmentMethod

ラベルの割り当て方法を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| contentLabel | ラベル |
| assignmentMethod | Output割り当て方法 (例: ' standard ' または ' privileged ') |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ContentLabel_GetAssignmentMethod(
    const mip_cc_content_label contentLabel,
    mip_cc_label_assignment_method* assignmentMethod,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getextendedproperties"></a>MIP_CC_ContentLabel_GetExtendedProperties

拡張プロパティを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| contentLabel | ラベル |
| properties | Output拡張プロパティのディクショナリ、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' properties ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_ContentLabel_GetExtendedProperties(
    const mip_cc_content_label contentLabel,
    mip_cc_metadata_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_isprotectionappliedfromlabel"></a>MIP_CC_ContentLabel_IsProtectionAppliedFromLabel

ラベルによって保護が適用されたかどうかを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| contentLabel | ラベル |
| Isprotectionの Edbylabel | Outputドキュメントが保護されていて、このラベルによって保護が明示的に適用されている場合。 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ContentLabel_IsProtectionAppliedFromLabel(
    const mip_cc_content_label contentLabel,
    bool* isProtectionAppliedByLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getlabel"></a>MIP_CC_ContentLabel_GetLabel

コンテンツラベルのインスタンスから汎用ラベルのプロパティを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| contentLabel | ラベル |
| label | Output汎用ラベル、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' label ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseLabel 

```c
mip_cc_result MIP_CC_ContentLabel_GetLabel(
    const mip_cc_content_label contentLabel,
    mip_cc_label* label,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getnamesize"></a>MIP_CC_CustomAction_GetNameSize

"カスタム" アクションの名前を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "カスタム" アクション |
| nameSize | Output名前を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CustomAction_GetNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getname"></a>MIP_CC_CustomAction_GetName

"カスタム" アクションの名前を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "カスタム" アクション |
| nameBuffer | Output名前がコピーされるバッファー。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_CustomAction_GetName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getproperties"></a>MIP_CC_CustomAction_GetProperties

"カスタム" アクションのプロパティを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "カスタム" アクション |
| properties | Outputプロパティのディクショナリ、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' properties ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CustomAction_GetProperties(
    const mip_cc_action action,
    mip_cc_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadata_callback"></a>mip_cc_metadata_callback

名前/プレフィックスでフィルター処理されたドキュメント metatdata を取得するためのコールバック関数定義

**パラメーター**

パラメーター | 説明
|---|---|
| names | 結果に含めるメタデータキー名の配列 |
| namesSize | ' Names ' 配列内の値の数 |
| namePrefixes | 結果に含めるメタデータキー名プレフィックスの配列 |
| namePrefixesSize | ' NamesPrefixes ' 配列内の値の数 |
| context | API 呼び出しからコールバックに渡されたアプリケーションコンテキスト不透明 |
| metadata | Outputクライアントアプリケーションによって作成されたメタデータキー/値のディクショナリ。 このディクショナリは MIP によって解放されます。 |

```c
MIP_CC_CALLBACK(mip_cc_metadata_callback,
    void,
    const char**,
    const int64_t,
    const char**,
    const int64_t,
    const void*,
    mip_cc_metadata_dictionary*);
```

## <a name="mip_cc_releaselabel"></a>MIP_CC_ReleaseLabel

ラベルに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| label | リリースされるラベル |

```c
void MIP_CC_ReleaseLabel(mip_cc_label label);
```

## <a name="mip_cc_label_getid"></a>MIP_CC_Label_GetId

ラベル ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| labelId | Outputラベル ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetId(
    const mip_cc_label label,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getnamesize"></a>MIP_CC_Label_GetNameSize

名前を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| nameSize | Output名前を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetNameSize(
    const mip_cc_label label,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getname"></a>MIP_CC_Label_GetName

ラベル名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| nameBuffer | Output名前がコピーされるバッファー。 |
| nameBufferSize | NameBuffer のサイズ (文字数)。 |
| actualNameSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: namebuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualNameSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_Label_GetName(
    const mip_cc_label label,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescriptionsize"></a>MIP_CC_Label_GetDescriptionSize

説明を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| 説明のサイズ | Output説明を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetDescriptionSize(
    const mip_cc_label label,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescription"></a>MIP_CC_Label_GetDescription

ラベルの説明を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| descriptionBuffer | Output説明のコピー先となるバッファー。 |
| descriptionBufferSize | DescriptionBuffer のサイズ (文字数)。 |
| actualDescriptionSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: descriptionbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualdescriptionsize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_Label_GetDescription(
    const mip_cc_label label,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolorsize"></a>MIP_CC_Label_GetColorSize

色を格納するために必要なバッファーのサイズを取得します

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| colorSize | Output色を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetColorSize(
    const mip_cc_label label,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolor"></a>MIP_CC_Label_GetColor

ラベルの色を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| colorBuffer | Output色のコピー先となるバッファー (#RRGGBB 形式)。 |
| colorBufferSize | ColorBuffer のサイズ (文字数)。 |
| actualColorSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: colorbuffer が null または不十分な場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualcolorsize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_Label_GetColor(
    const mip_cc_label label,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getsensitivity"></a>MIP_CC_Label_GetSensitivity

ラベルの感度レベルを取得します。 値が大きいほど、より機密性が高いことを意味します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| 区別 | Output感度レベル |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetSensitivity(
    const mip_cc_label label,
    int32_t* sensitivity,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltipsize"></a>MIP_CC_Label_GetTooltipSize

ツールヒントを格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| tooltipSize | Outputツールヒントを保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltip"></a>MIP_CC_Label_GetTooltip

ラベルのツールヒントを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| tooltipBuffer | Outputツールヒントがにコピーされるバッファー。 |
| tooltipBufferSize | TooltipBuffer のサイズ (文字数)。 |
| actualTooltipSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: tooltipBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualTooltipSize は必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_Label_GetTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltipsize"></a>MIP_CC_Label_GetAutoTooltipSize

自動分類ツールヒントを格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| tooltipSize | Outputツールヒントを保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetAutoTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltip"></a>MIP_CC_Label_GetAutoTooltip

ラベルの自動分類ツールヒントを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| tooltipBuffer | Outputツールヒントがにコピーされるバッファー。 |
| tooltipBufferSize | TooltipBuffer のサイズ (文字数)。 |
| actualTooltipSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: tooltipBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualTooltipSize は必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_Label_GetAutoTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_isactive"></a>MIP_CC_Label_IsActive

ラベルがアクティブかどうかを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| isActive | Outputラベルがアクティブであると見なされるかどうか。 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 適用できるのはアクティブなラベルのみです。 Inactivte ラベルは適用できず、表示目的でのみ使用されます。 

```c
mip_cc_result MIP_CC_Label_IsActive(
    const mip_cc_label label,
    bool* isActive,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getparent"></a>MIP_CC_Label_GetParent

親ラベル (存在する場合) を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| parent | Output親ラベル (存在する場合)、それ以外の場合は null |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetParent(
    const mip_cc_label label,
    mip_cc_label* parent,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildrensize"></a>MIP_CC_Label_GetChildrenSize

子ラベルの数を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| childrenSize | Output子の数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_Label_GetChildrenSize(
    const mip_cc_label label,
    int64_t* childrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildren"></a>MIP_CC_Label_GetChildren

子ラベルを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| childrenBuffer | Output子ラベルをコピーするバッファー。 子ラベル |
| childrenBufferSize | ChildrenBuffer のサイズ (ラベルの数)。 |
| actualChildrenSize | Outputバッファーに書き込まれた子ラベルの数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: childrenBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualChildrenSize は必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_Label_GetChildren(
    const mip_cc_label label,
    mip_cc_label* childrenBuffer,
    const int64_t childrenBufferSize,
    int64_t* actualChildrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcustomsettings"></a>MIP_CC_Label_GetCustomSettings

ラベルのポリシーで定義されたカスタム設定を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| label | ラベル |
| settings | Output呼び出し元が所有する設定のディクショナリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' settings ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_Label_GetCustomSettings(
    const mip_cc_label label,
    mip_cc_dictionary* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoremove"></a>MIP_CC_MetadataAction_GetMetadataToRemove

削除する "メタデータ" アクションのメタデータを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "メタデータ" アクション |
| metadataNames | Output削除するメタデータのキー名、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: メタデータを @note 追加する前にメタデータを削除する必要がある MIP_CC_ReleaseStringList を呼び出すことによって、呼び出し元によって ' metadatanames 変数 ' 変数を解放する必要があります 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToRemove(
    const mip_cc_action action,
    mip_cc_string_list* metadataNames,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoadd"></a>MIP_CC_MetadataAction_GetMetadataToAdd

追加する "メタデータ" アクションのメタデータを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "メタデータ" アクション |
| metadata | [出力] 追加するメタデータエントリの一覧、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: メタデータを @note 追加する前にメタデータを削除する必要がある MIP_CC_ReleaseDictionary を呼び出すことによって、' metadata ' 変数を呼び出し元が解放する必要があります 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToAdd(
    const mip_cc_action action,
    mip_cc_metadata_dictionary* metadata,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmetadatadictionary"></a>MIP_CC_CreateMetadataDictionary

文字列のキー/値の辞書を作成する

**パラメーター**

パラメーター | 説明
|---|---|
| entries | メタデータエントリの配列 |
| count | メタデータエントリの数 |
| ディクショナリ | Output新しく作成されたディクショナリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: mip_cc_dictionary は、を呼び出して解放する必要があり MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CreateMetadataDictionary(
    const mip_cc_metadata_entry* entries,
    const int64_t count,
    mip_cc_metadata_dictionary* dictionary,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadatadictionary_getentries"></a>MIP_CC_MetadataDictionary_GetEntries

ディクショナリを構成するメタデータエントリを取得する

**パラメーター**

パラメーター | 説明
|---|---|
| ディクショナリ | ソースディクショナリ |
| entries | Outputメタデータエントリの配列、mip_cc_dictionary オブジェクトによって所有されているメモリ |
| count | Outputメタデータエントリの数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' entries ' のメモリは mip_cc_dictionary オブジェクトによって所有されているため、個別に解放しないでください。 

```c
mip_cc_result MIP_CC_MetadataDictionary_GetEntries(
    const mip_cc_metadata_dictionary dictionary,
    mip_cc_metadata_entry** entries,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasemetadatadictionary"></a>MIP_CC_ReleaseMetadataDictionary

ディクショナリに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| ディクショナリ | リリースされるディクショナリ |

```c
void MIP_CC_ReleaseMetadataDictionary(mip_cc_metadata_dictionary dictionary);
```

## <a name="mip_cc_releasepolicyengine"></a>MIP_CC_ReleasePolicyEngine

ポリシーエンジンに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジンを解放する |

```c
void MIP_CC_ReleasePolicyEngine(mip_cc_policy_engine engine);
```

## <a name="mip_cc_policyengine_getengineidsize"></a>MIP_CC_PolicyEngine_GetEngineIdSize

エンジン ID に必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| idSize | Outputエンジン ID を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineIdSize(
    const mip_cc_policy_engine engine,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getengineid"></a>MIP_CC_PolicyEngine_GetEngineId

エンジン ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| idBuffer | OutputId がコピーされるバッファー。 |
| idBufferSize | IdBuffer のサイズ (文字数)。 |
| actualIdSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: idbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualIdSize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineId(
    const mip_cc_policy_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getmoreinfourlsize"></a>MIP_CC_PolicyEngine_GetMoreInfoUrlSize

ポリシーエンジンに関連付けられているクライアントデータのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| よりよい Infourlsize | Outputクライアントデータのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrlSize(
    const mip_cc_policy_engine engine,
    int64_t* moreInfoUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getmoreinfourl"></a>MIP_CC_PolicyEngine_GetMoreInfoUrl

ポリシーエンジンに関連付けられているクライアントデータを取得する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| その他の Infourlbuffer | Outputクライアントデータがコピーされるバッファー |
| その他の Infourlbuffersize | より多くの Infourlbuffer のサイズ (文字数)。 |
| Actualのよりよい Infourlsize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: それよりも後の Infourlbuffer が null または不十分な場合は、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualのより適切なバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrl(
    const mip_cc_policy_engine engine,
    char* moreInfoUrlBuffer,
    const int64_t moreInfoUrlBufferSize,
    int64_t* actualMoreInfoUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_islabelingrequired"></a>MIP_CC_PolicyEngine_IsLabelingRequired

ドキュメントにラベルを付ける必要があるかどうかをポリシーが指示するかどうかを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| isLabelingRequired | Outputポリシーによってドキュメントにラベルを付ける必要があるかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_IsLabelingRequired(
    const mip_cc_policy_engine engine,
    bool* isLabelingRequired,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicyfileidsize"></a>MIP_CC_PolicyEngine_GetPolicyFileIdSize

ポリシーエンジンに関連付けられているクライアントデータのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| policyFileIdSize | Outputクライアントデータのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* policyFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicyfileid"></a>MIP_CC_PolicyEngine_GetPolicyFileId

ポリシーエンジンに関連付けられているクライアントデータを取得する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| policyFileIdBuffer | Outputクライアントデータがコピーされるバッファー |
| policyFileIdBufferSize | PolicyFileIdBuffer のサイズ (文字数)。 |
| actualPolicyFileIdSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: policyFileIdBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualPolicyFileIdSize は必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileId(
    const mip_cc_policy_engine engine,
    char* policyFileIdBuffer,
    const int64_t policyFileIdBufferSize,
    int64_t* actualPolicyFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivityfileidsize"></a>MIP_CC_PolicyEngine_GetSensitivityFileIdSize

ポリシーエンジンに関連付けられているクライアントデータのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| sensitivityFileIdSize | Outputクライアントデータのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivityfileid"></a>MIP_CC_PolicyEngine_GetSensitivityFileId

ポリシーエンジンに関連付けられているクライアントデータを取得する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| sensitivityFileIdBuffer | Outputクライアントデータがコピーされるバッファー |
| sensitivityFileIdBufferSize | SensitivityFileIdBuffer のサイズ (文字数)。 |
| actualSensitivityFileIdSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: sensitivityFileIdBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualSensitivityFileIdSize は必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileId(
    const mip_cc_policy_engine engine,
    char* sensitivityFileIdBuffer,
    const int64_t sensitivityFileIdBufferSize,
    int64_t* actualSensitivityFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_hasclassificationrules"></a>MIP_CC_PolicyEngine_HasClassificationRules

ポリシーに自動または推奨規則があるかどうかを取得します

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| hasClassificationRules | Outputポリシーに自動または推奨規則があるかどうか |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_HasClassificationRules(
    const mip_cc_policy_engine engine,
    bool* hasClassificationRules,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getlastpolicyfetchtime"></a>MIP_CC_PolicyEngine_GetLastPolicyFetchTime

ポリシーが最後にフェッチされた時刻を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| lastPolicyFetchTime | Outputポリシーが最後にフェッチされた時刻 (エポックからの秒) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetLastPolicyFetchTime(
    const mip_cc_policy_engine engine,
    int64_t* lastPolicyFetchTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitylabelssize"></a>MIP_CC_PolicyEngine_GetSensitivityLabelsSize

ポリシーエンジンに関連付けられている秘密度ラベルの数を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| ラベルのサイズ | Outputラベル数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabelsSize(
    const mip_cc_policy_engine engine,
    int64_t* labelsSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitylabels"></a>MIP_CC_PolicyEngine_GetSensitivityLabels

ポリシーエンジンに関連付けられている機密ラベルを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| labelBuffer | Outputラベルをコピーするバッファー。 ラベルはクライアントによって所有されています |
| labelBufferSize | LabelBuffer のサイズ (ラベルの数)。 |
| actualLabelsSize | Outputバッファーに書き込まれたラベルの数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: labelbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualLabelsSize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabels(
    const mip_cc_policy_engine engine,
    mip_cc_label* labelBuffer,
    const int64_t labelBufferSize,
    int64_t* actualLabelsSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getlabelbyid"></a>MIP_CC_PolicyEngine_GetLabelById

ID で感度ラベルを取得します

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| labelId | ラベル ID |
| label | Output感度ラベル。 この値は呼び出し元によって所有されており、MIP_CC_ReleaseLabel と共に解放する必要があります。 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetLabelById(
    const mip_cc_policy_engine engine,
    const char* labelId,
    mip_cc_label* label,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypessize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesSize

ポリシーエンジンに関連付けられている感度の種類の数を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| sensitivityTypesSize | Output感度の種類の数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityTypesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypes"></a>MIP_CC_PolicyEngine_GetSensitivityTypes

ポリシーエンジンに関連付けられている感度の種類を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| sensitivityTypeBuffer | Output感度の種類がにコピーされるバッファー。 感度 |
| sensitivityTypeBufferSize | SensitivityTypeBuffer のサイズ (感度の種類の数)。 |
| actualSensitivityTypesSize | Outputバッファーに書き込まれた感度の種類の数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: sensitivityTypeBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualSensitivityTypesSize は必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypes(
    const mip_cc_policy_engine engine,
    mip_cc_sensitivity_type* sensitivityTypeBuffer,
    const int64_t sensitivityTypeBufferSize,
    int64_t* actualSensitivityTypesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_createpolicyhandler"></a>MIP_CC_PolicyEngine_CreatePolicyHandler

ポリシー関連の関数を実行するポリシーハンドラーを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| isAuditDiscoveryEnabled | 監査検出が有効かどうか |
| handler | Output新しく作成されたポリシーハンドラーインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_CreatePolicyHandler(
    const mip_cc_policy_engine engine,
    const bool isAuditDiscoveryEnabled,
    mip_cc_policy_handler* handler,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_sendapplicationauditevent"></a>MIP_CC_PolicyEngine_SendApplicationAuditEvent

アプリケーション固有のイベントを監査パイプラインに記録します。

**パラメーター**

パラメーター | 説明
|---|---|
| レベル | イベントのレベル: 情報/エラー/警告 |
| eventType | イベントの種類の説明 |
| eventData | イベントに関連付けられているデータ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_SendApplicationAuditEvent(
    const mip_cc_policy_engine engine,
    const char* level,
    const char* eventType,
    const char* eventData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_gettenantidsize"></a>MIP_CC_PolicyEngine_GetTenantIdSize

テナント ID のサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| アンチサイズ | Outputテナント ID のサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetTenantIdSize(
    const mip_cc_policy_engine engine,
    int64_t* tenantIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_gettenantid"></a>MIP_CC_PolicyEngine_GetTenantId

テナント ID を取得します

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| このようにして、 | Outputテナント ID がコピーされるバッファー。 |
| このようにして、 | 表示されていない Dbuffer のサイズ (文字数)。 |
| Actualdsize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: "格納されていない dbuffer" が null または "不十分" の場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、Actualのアンチサイズは必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetTenantId(
    const mip_cc_policy_engine engine,
    char* tenantIdBuffer,
    const int64_t tenantIdBufferSize,
    int64_t* actualTenantIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicydataxmlsize"></a>MIP_CC_PolicyEngine_GetPolicyDataXmlSize

ポリシーデータ xml のサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| xmlSize | Outputポリシーデータ xml のサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicydataxml"></a>MIP_CC_PolicyEngine_GetPolicyDataXml

ポリシーデータ xml を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| xmlBuffer | OutputXml がコピーされるバッファー。 |
| xmlBufferSize | XmlBuffer のサイズ (文字数)。 |
| actualXmlSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: xmlbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualxmlsize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxmlsize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize

感度の種類のデータ xml のサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| xmlSize | Outputポリシーデータ xml のサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxml"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXml

感度の種類のデータ xml を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| xmlBuffer | OutputXml がコピーされるバッファー。 |
| xmlBufferSize | XmlBuffer のサイズ (文字数)。 |
| actualXmlSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: xmlbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualxmlsize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getclientdatasize"></a>MIP_CC_PolicyEngine_GetClientDataSize

ポリシーエンジンに関連付けられているクライアントデータのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| clientDataSize | Outputクライアントデータのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientDataSize(
    const mip_cc_policy_engine engine,
    int64_t* clientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getclientdata"></a>MIP_CC_PolicyEngine_GetClientData

ポリシーエンジンに関連付けられているクライアントデータを取得する

**パラメーター**

パラメーター | 説明
|---|---|
| エンジン | ポリシーエンジン |
| clientDataBuffer | Outputクライアントデータがコピーされるバッファー |
| clientDataBufferSize | ClientDataBuffer のサイズ (文字数)。 |
| actualClientDataSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: clientDataBuffer が null または不足している場合は MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualClientDataSize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientData(
    const mip_cc_policy_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createpolicyenginesettingswithidentity"></a>MIP_CC_CreatePolicyEngineSettingsWithIdentity

新しいポリシーエンジンを作成するために使用される設定オブジェクトを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| ID | PolicyEngine に関連付けられる id |
| clientData | エンジンと共に保存されるカスタマイズ可能なクライアントデータ |
| locale | テキスト結果が出力されるロケール |
| loadSensitivityTypes | 感度の種類のデータ (分類の場合) も読み込むかどうか |
| settings | Output新しく作成された設定インスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: アプリケーションが後で MIP_CC_PolicyEngine_GetSensitivityTypes を呼び出す必要がある場合にのみ、' loadSensitivityTypes ' を ' true ' にする必要があります。 それ以外の場合、不要な HTTP 操作を回避するには、false にする必要があります。 

```c
mip_cc_result MIP_CC_CreatePolicyEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    bool loadSensitivityTypes,
    mip_cc_policy_engine_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setclientdata"></a>MIP_CC_PolicyEngineSettings_SetClientData

このエンジンと共に不透明に格納され、セッション間で保持されるクライアントデータを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| clientData | クライアントデータ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetClientData(
    const mip_cc_policy_engine_settings settings,
    const char* clientData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcustomsettings"></a>MIP_CC_PolicyEngineSettings_SetCustomSettings

機能のゲートとテストに使用されるカスタム設定を構成します。

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| Customsettings.ini | カスタム設定のキーと値のペア |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCustomSettings(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setsessionid"></a>MIP_CC_PolicyEngineSettings_SetSessionId

ログとテレメトリを関連付けるために使用できるセッション ID を設定します。

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| sessionID | ポリシーエンジンの有効期間を表すセッション ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetSessionId(
    const mip_cc_policy_engine_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcloud"></a>MIP_CC_PolicyEngineSettings_SetCloud

すべてのサービス要求のエンドポイント Url に影響するクラウドを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| cloud | クラウド識別子 (既定 = 不明) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: cloud が指定されていない場合、既定ではグローバルクラウドになります。 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloud(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_cloud cloud,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcloudendpointbaseurl"></a>MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl

すべてのサービス要求のベース URL を設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| cloudEndpointBaseUrl | ベース URL (例: ' https://dataservice.protection.outlook.com ') |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: この値は読み取り専用であり、Cloud = MIP_CLOUD_CUSTOM に設定する必要があります 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_policy_engine_settings settings,
    const char* cloudEndpointBaseUrl,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setdelegateduseremail"></a>MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail

委任されたユーザーを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| delegatedUserEmail | 委任されたユーザーの電子メールアドレス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作しているときに指定します。 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail(
    const mip_cc_policy_engine_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setlabelfilter"></a>MIP_CC_PolicyEngineSettings_SetLabelFilter

ラベルフィルターを設定します

**パラメーター**

パラメーター | 説明
|---|---|
| settings | エンジンの設定 |
| labelFilter | ラベルフィルターを表す列挙型の既定値が設定されていない場合、hyok、doublekeyencryption |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetLabelFilter(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_label_filter labelFilter,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyenginesettings"></a>MIP_CC_ReleasePolicyEngineSettings

ポリシーエンジン設定に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| settings | リリースされるポリシーエンジンの設定 |

```c
void MIP_CC_ReleasePolicyEngineSettings(mip_cc_policy_engine_settings settings);
```

## <a name="mip_cc_releasepolicyhandler"></a>MIP_CC_ReleasePolicyHandler

ポリシーハンドラーに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| handler | リリースするポリシーハンドラー |

```c
void MIP_CC_ReleasePolicyHandler(mip_cc_policy_handler handler);
```

## <a name="mip_cc_policyhandler_getsensitivitylabel"></a>MIP_CC_PolicyHandler_GetSensitivityLabel

ドキュメントの現在のラベルを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | ポリシーハンドラー |
| documentState | ドキュメントの状態 |
| context | アプリケーションコンテキスト不透明が任意のコールバックに転送される |
| contentLabel | ドキュメントに現在適用されているラベル |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyHandler_GetSensitivityLabel(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const void* context,
    mip_cc_content_label* contentLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyhandler_computeactions"></a>MIP_CC_PolicyHandler_ComputeActions

指定された状態に基づいてポリシー規則を実行し、対応するアクションを決定します。

**パラメーター**

パラメーター | 説明
|---|---|
| handler | ポリシーハンドラー |
| documentState | ドキュメントの状態 |
| applicationState | アプリケーションアクションの状態 |
| context | アプリケーションコンテキスト不透明が任意のコールバックに転送される |
| actionResult | Outputアプリケーションで実行する必要があるアクション、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' actionresult ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseActionResult 

```c
mip_cc_result MIP_CC_PolicyHandler_ComputeActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_action_result* actionResult,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyhandler_notifycommittedactions"></a>MIP_CC_PolicyHandler_NotifyCommittedActions

計算されたアクションが適用され、データがディスクにコミットされた後に、アプリケーションによって呼び出されます

**パラメーター**

パラメーター | 説明
|---|---|
| handler | ポリシーハンドラー |
| documentState | ドキュメントの状態 |
| applicationState | アプリケーションアクションの状態 |
| context | アプリケーションコンテキスト不透明が任意のコールバックに転送される |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: 完全なラベルの監査データを送信するには、この関数を呼び出す必要があります。 

```c
mip_cc_result MIP_CC_PolicyHandler_NotifyCommittedActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofile_acquireauthtoken"></a>MIP_CC_PolicyProfile_AcquireAuthToken

認証コールバックをトリガーする

**パラメーター**

パラメーター | 説明
|---|---|
| profile | プロファイル |
| cloud | Azure cloud |
| authCallback | 呼び出される認証コールバック |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: MIP は、auth デリゲートによって返された値を使用してキャッシュしたり他の操作を実行したりすることはありません。 この関数は、MIP が認証トークンを要求するまで "ログイン" されていないアプリケーションに推奨されます。 これにより、アプリケーションは、MIP が実際に必要とする前にトークンをフェッチできます。 

```c
mip_cc_result MIP_CC_PolicyProfile_AcquireAuthToken(
    const mip_cc_policy_profile profile,
    const mip_cc_cloud cloud,
    const mip_cc_auth_callback authCallback,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_loadpolicyprofile"></a>MIP_CC_LoadPolicyProfile

プロファイルの読み込み

**パラメーター**

パラメーター | 説明
|---|---|
| settings | プロファイルの設定 |
| profile | Output新しく作成されたポリシープロファイルインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_LoadPolicyProfile(
    const mip_cc_policy_profile_settings settings,
    mip_cc_policy_profile* profile,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyprofile"></a>MIP_CC_ReleasePolicyProfile

ポリシープロファイルに関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| profile | リリースされるポリシープロファイル |

```c
void MIP_CC_ReleasePolicyProfile(mip_cc_policy_profile profile);
```

## <a name="mip_cc_createpolicyprofilesettings"></a>MIP_CC_CreatePolicyProfileSettings

ポリシープロファイルの作成に使用される設定オブジェクトを作成する

**パラメーター**

パラメーター | 説明
|---|---|
| mipContext | すべてのプロファイルで共有するグローバルコンテキスト |
| cacheStorageType | ストレージキャッシュの構成 |
| authCallback | クライアントアプリケーションによって実装される認証に使用されるコールバックオブジェクト |
| settings | Output新しく作成された設定インスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_CreatePolicyProfileSettings(
    const mip_cc_mip_context mipContext,
    const mip_cc_cache_storage_type cacheStorageType,
    const mip_cc_auth_callback authCallback,
    mip_cc_policy_profile_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_setsessionid"></a>MIP_CC_PolicyProfileSettings_SetSessionId

ログとテレメトリを関連付けるために使用できるセッション ID を設定します。

**パラメーター**

パラメーター | 説明
|---|---|
| settings | プロファイルの設定 |
| sessionID | ポリシープロファイルの有効期間を表すセッション ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetSessionId(
    const mip_cc_policy_profile_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_sethttpdelegate"></a>MIP_CC_PolicyProfileSettings_SetHttpDelegate

既定の HTTP スタックをクライアント独自にオーバーライドする

**パラメーター**

パラメーター | 説明
|---|---|
| settings | HTTP デリゲートが割り当てられるプロファイル設定 |
| httpDelegate | クライアントアプリケーションによって実装される HTTP コールバックインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetHttpDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate

既定の非同期タスクディスパッチャーをクライアント独自にオーバーライドする

**パラメーター**

パラメーター | 説明
|---|---|
| settings | タスクディスパッチャーデリゲートが割り当てられるプロファイル設定 |
| taskDispatcherDelegate | クライアントアプリケーションによって実装されたタスクディスパッチャーコールバックインスタンス |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_setcustomsettings"></a>MIP_CC_PolicyProfileSettings_SetCustomSettings

機能のゲートとテストに使用されるカスタム設定を構成します。

**パラメーター**

パラメーター | 説明
|---|---|
| settings | プロファイルの設定 |
| Customsettings.ini | カスタム設定のキーと値のペア |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetCustomSettings(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyprofilesettings"></a>MIP_CC_ReleasePolicyProfileSettings

ポリシープロファイル設定に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| settings | リリースされるポリシープロファイルの設定 |

```c
void MIP_CC_ReleasePolicyProfileSettings(mip_cc_policy_profile_settings profileSettings);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize

2つのキー暗号化 url を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "二重キーによるアドホックポリシーによる保護" アクション |
| urlSize | OutputUrl を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl

二重キー暗号化 url を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "二重キーによるアドホックポリシーによる保護" アクション |
| urlBuffer | OutputUrl がコピーされるバッファー。 |
| urlBufferSize | UrlBuffer のサイズ (文字数)。 |
| actualUrlSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: urlbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualurlsize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplateaction_gettemplateid"></a>MIP_CC_ProtectByTemplateAction_GetTemplateId

"テンプレートによる保護" アクションのテンプレート ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "テンプレートによる保護" アクション |
| templateId | Output保護を定義するテンプレートの ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectByTemplateAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_gettemplateid"></a>MIP_CC_ProtectByTemplateDkAction_GetTemplateId

"2 つのキーで保護されるテンプレートによる保護" アクションのテンプレート ID を取得します

**パラメーター**

パラメーター | 説明
|---|---|
| action | "テンプレートによる保護" アクション |
| templateId | Output保護を定義するテンプレートの ID |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize

2つのキー暗号化 url を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "二重キーによるテンプレートによる保護" アクション |
| urlSize | OutputUrl を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl

二重キー暗号化 url を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "二重キーによるテンプレートによる保護" アクション |
| urlBuffer | OutputUrl がコピーされるバッファー。 |
| urlBufferSize | UrlBuffer のサイズ (文字数)。 |
| actualUrlSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: urlbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualurlsize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize

2つのキー暗号化 url を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "2 つのキーによる dp 非転送ポリシーによる保護" アクション |
| urlSize | OutputUrl を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl

二重キー暗号化 url を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "2 つのキーによる dp 非転送ポリシーによる保護" アクション |
| urlBuffer | OutputUrl がコピーされるバッファー。 |
| urlBufferSize | UrlBuffer のサイズ (文字数)。 |
| actualUrlSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: urlbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualurlsize は必要最小限のバッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removecontentfooteraction_getuielementnames"></a>MIP_CC_RemoveContentFooterAction_GetUIElementNames

削除する "コンテンツフッターの削除" アクションの UI 要素名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツフッターの削除" アクション |
| names | Output削除する UI 要素の名前、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' names ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentFooterAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removecontentheaderaction_getuielementnames"></a>MIP_CC_RemoveContentHeaderAction_GetUIElementNames

削除する "コンテンツヘッダーの削除" アクションの UI 要素名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "コンテンツヘッダーの削除" アクション |
| names | Output削除する UI 要素の名前、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' names ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentHeaderAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removewatermarkaction_getuielementnames"></a>MIP_CC_RemoveWatermarkAction_GetUIElementNames

削除する "透かしの削除" アクションの UI 要素名を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| action | "透かしフッターの削除" アクション |
| names | Output削除する UI 要素の名前、呼び出し元によって所有されているメモリ |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: ' names ' 変数は、呼び出し元がを呼び出すことによって解放する必要があり MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveWatermarkAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasesensitivitytype"></a>MIP_CC_ReleaseSensitivityType

秘密度の種類に関連付けられているリソースを解放する

**パラメーター**

パラメーター | 説明
|---|---|
| sensitivityType | リリースされる感度の種類 |

```c
void MIP_CC_ReleaseSensitivityType(mip_cc_sensitivity_type sensitivityType);
```

## <a name="mip_cc_sensitivitytype_getrulepackageidsize"></a>MIP_CC_SensitivityType_GetRulePackageIdSize

秘密度の種類の規則パッケージ ID を格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| sensitivityType | 感度の種類 |
| idSize | Output規則パッケージ ID を保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageIdSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackageid"></a>MIP_CC_SensitivityType_GetRulePackageId

感度の種類の規則パッケージ ID を取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| sensitivityType | 感度の種類 |
| idBuffer | OutputID がコピーされるバッファー。 |
| idBufferSize | IdBuffer のサイズ (文字数)。 |
| actualIdSize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: idbuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、actualIdSize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageId(
    const mip_cc_sensitivity_type sensitivityType,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackagesize"></a>MIP_CC_SensitivityType_GetRulePackageSize

感度の種類の規則パッケージを格納するために必要なバッファーのサイズを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| sensitivityType | 感度の種類 |
| rulePackageSize | Output規則パッケージを保持するバッファーのサイズ (文字数) |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* rulePackageSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackage"></a>MIP_CC_SensitivityType_GetRulePackage

感度の種類の規則パッケージを取得します。

**パラメーター**

パラメーター | 説明
|---|---|
| sensitivityType | 感度の種類 |
| rulePackageBuffer | Outputルールパッケージがコピーされるバッファー。 |
| rulePackageBufferSize | RulePackageBuffer のサイズ (文字数)。 |
| Actualruleパッケージ Esize | Outputバッファーに書き込まれた文字数 |
| errorInfo | OutputOptional操作の結果がエラーの場合のエラー情報 |

**Return**: 成功または失敗を示す結果コード

**注**: rulePackageBuffer が null または不十分な場合、MIP_RESULT_ERROR_INSUFFICIENT_BUFFER が返され、Actualruleの esize が必要な最小バッファーサイズに設定されます。 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackage(
    const mip_cc_sensitivity_type sensitivityType,
    char* rulePackageBuffer,
    const int64_t rulePackageBufferSize,
    int64_t* actualRulePackageSize,
    mip_cc_error* errorInfo);
```

