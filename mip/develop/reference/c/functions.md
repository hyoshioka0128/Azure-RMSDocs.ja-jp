---
title: 関数
description: 関数
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 9/22/2020
ms.openlocfilehash: 8cb8d6550ecdc0d7ea342c3e6484a7a23b7f590d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569414"
---
# <a name="functions"></a>関数

## <a name="mip_cc_auth_callback"></a>mip_cc_auth_callback

OAuth2 トークンを取得するためのコールバック関数の定義

**パラメーター**

パラメーター | 説明
|---|---|
| identity | トークンを取得する対象の電子メールアドレス |
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
| contentLabel | Label |
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
| contentLabel | Label |
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
| contentLabel | Label |
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
| contentLabel | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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
| label | Label |
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

