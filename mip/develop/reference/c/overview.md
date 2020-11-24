---
title: MIP SDK for C リファレンス
description: MIP SDK for C リファレンス
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 9/22/2020
ms.openlocfilehash: 6269921c14b0ac284aab501253d07bea416ef137
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569391"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for C リファレンス

Microsoft Information Protection (MIP) SDK for C を使用すると、開発者はデータやその他のデジタル資産にデータ保護ポリシーを管理して適用できます。

MIP SDK for C には、

- [列挙型](enumerations.md)
- [構造体](structures.md)
- 次の関数:

関数 | 簡単な説明 |
|---|---|
| [mip_cc_auth_callback](functions.md#mip_cc_auth_callback) | OAuth2 トークンを取得するためのコールバック関数の定義 |
| [mip_cc_consent_callback](functions.md#mip_cc_consent_callback) | ユーザーから外部サービスエンドポイントへのアクセスに同意するためのコールバック関数定義 |
| [MIP_CC_CreateDictionary](functions.md#mip_cc_createdictionary) | 文字列のキー/値の辞書を作成する |
| [MIP_CC_Dictionary_GetEntries](functions.md#mip_cc_dictionary_getentries) | ディクショナリを構成するキーと値のペアを取得する |
| [MIP_CC_ReleaseDictionary](functions.md#mip_cc_releasedictionary) | ディクショナリに関連付けられているリソースを解放する |
| [mip_cc_http_send_callback_fn](functions.md#mip_cc_http_send_callback_fn) | HTTP 要求を発行するためのコールバック関数の定義 |
| [mip_cc_http_cancel_callback_fn](functions.md#mip_cc_http_cancel_callback_fn) | HTTP 要求をキャンセルするためのコールバック関数の定義 |
| [MIP_CC_CreateHttpDelegate](functions.md#mip_cc_createhttpdelegate) | MIP の既定の HTTP スタックをオーバーライドするために使用できる HTTP デリゲートを作成します。 |
| [MIP_CC_NotifyHttpDelegateResponse](functions.md#mip_cc_notifyhttpdelegateresponse) | Http 応答の準備ができていることを HTTP デリゲートに通知します |
| [MIP_CC_ReleaseHttpDelegate](functions.md#mip_cc_releasehttpdelegate) | HTTP デリゲートハンドルに関連付けられているリソースを解放する |
| [mip_cc_logger_init_callback_fn](functions.md#mip_cc_logger_init_callback_fn) | Logger を初期化するためのコールバック関数の定義 |
| [mip_cc_logger_write_callback_fn](functions.md#mip_cc_logger_write_callback_fn) | Log ステートメントを記述するためのコールバック関数の定義 |
| [MIP_CC_CreateLoggerDelegate](functions.md#mip_cc_createloggerdelegate) | Mipmap の既定のロガーをオーバーライドするために使用できる logger デリゲートを作成します。 |
| [MIP_CC_ReleaseLoggerDelegate](functions.md#mip_cc_releaseloggerdelegate) | Logger デリゲートハンドルに関連付けられているリソースを解放する |
| [MIP_CC_CreateMipContext](functions.md#mip_cc_createmipcontext) | すべてのプロファイルインスタンス間で共有される状態を管理する MIP コンテキストを作成する |
| [MIP_CC_CreateMipContextWithCustomFeatureSettings](functions.md#mip_cc_createmipcontextwithcustomfeaturesettings) | すべてのプロファイルインスタンス間で共有される状態を管理する MIP コンテキストを作成する |
| [MIP_CC_ReleaseMipContext](functions.md#mip_cc_releasemipcontext) | Mipmap コンテキストに関連付けられているリソースを解放する |
| [MIP_CC_ProtectionDescriptor_GetProtectionType](functions.md#mip_cc_protectiondescriptor_getprotectiontype) | RMS テンプレートによって定義されているかどうかにかかわらず、保護の種類を取得します。 |
| [MIP_CC_ProtectionDescriptor_GetOwnerSize](functions.md#mip_cc_protectiondescriptor_getownersize) | 所有者を格納するために必要なバッファーのサイズを取得します |
| [MIP_CC_ProtectionDescriptor_GetOwner](functions.md#mip_cc_protectiondescriptor_getowner) | 保護所有者を取得します。 |
| [MIP_CC_ProtectionDescriptor_GetNameSize](functions.md#mip_cc_protectiondescriptor_getnamesize) | 名前を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_ProtectionDescriptor_GetName](functions.md#mip_cc_protectiondescriptor_getname) | 保護名を取得します。 |
| [MIP_CC_ProtectionDescriptor_GetDescriptionSize](functions.md#mip_cc_protectiondescriptor_getdescriptionsize) | 説明を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_ProtectionDescriptor_GetDescription](functions.md#mip_cc_protectiondescriptor_getdescription) | 保護の説明を取得します。 |
| [MIP_CC_ProtectionDescriptor_GetTemplateId](functions.md#mip_cc_protectiondescriptor_gettemplateid) | テンプレート ID を取得します。 |
| [MIP_CC_ProtectionDescriptor_GetLabelId](functions.md#mip_cc_protectiondescriptor_getlabelid) | ラベル ID を取得します。 |
| [MIP_CC_ProtectionDescriptor_GetContentId](functions.md#mip_cc_protectiondescriptor_getcontentid) | コンテンツ ID を取得します。 |
| [MIP_CC_ProtectionDescriptor_DoesContentExpire](functions.md#mip_cc_protectiondescriptor_doescontentexpire) | コンテンツの有効期限が切れているかどうかを取得します。 |
| [MIP_CC_ProtectionDescriptor_GetContentValidUntil](functions.md#mip_cc_protectiondescriptor_getcontentvaliduntil) | 保護の有効期限 (エポックからの秒数) を取得します。 |
| [MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess](functions.md#mip_cc_protectiondescriptor_doesallowofflineaccess) | オフラインアクセスが許可されているかどうかを取得します。 |
| [MIP_CC_ProtectionDescriptor_GetReferrerSize](functions.md#mip_cc_protectiondescriptor_getreferrersize) | 参照元を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_ProtectionDescriptor_GetReferrer](functions.md#mip_cc_protectiondescriptor_getreferrer) | 保護参照元を取得します |
| [MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize](functions.md#mip_cc_protectiondescriptor_getdoublekeyurlsize) | 2つのキーの URL を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl](functions.md#mip_cc_protectiondescriptor_getdoublekeyurl) | 2つのキーの URL を取得します |
| [MIP_CC_ReleaseProtectionDescriptor](functions.md#mip_cc_releaseprotectiondescriptor) | 保護記述子に関連付けられているリソースを解放する |
| [MIP_CC_CreateStringList](functions.md#mip_cc_createstringlist) | 文字列リストの作成 |
| [MIP_CC_StringList_GetStrings](functions.md#mip_cc_stringlist_getstrings) | 文字列リストを構成する文字列を取得します。 |
| [MIP_CC_ReleaseStringList](functions.md#mip_cc_releasestringlist) | 文字列リストに関連付けられているリソースを解放する |
| [mip_cc_dispatch_task_callback_fn](functions.md#mip_cc_dispatch_task_callback_fn) | 非同期タスクをディスパッチするためのコールバック関数の定義 |
| [mip_cc_cancel_task_callback_fn](functions.md#mip_cc_cancel_task_callback_fn) | バックグラウンドタスクをキャンセルするためのコールバック関数 |
| [MIP_CC_CreateTaskDispatcherDelegate](functions.md#mip_cc_createtaskdispatcherdelegate) | MIP の既定の非同期タスク処理をオーバーライドするために使用できるタスクディスパッチャーデリゲートを作成します。 |
| [MIP_CC_ExecuteDispatchedTask](functions.md#mip_cc_executedispatchedtask) | タスクが現在のスレッドで実行するようにスケジュールされていることを TaskDispatcher デリゲートに通知します |
| [MIP_CC_ReleaseTaskDispatcherDelegate](functions.md#mip_cc_releasetaskdispatcherdelegate) | タスクディスパッチャーデリゲートハンドルに関連付けられているリソースの解放 |
| [MIP_CC_CreateTelemetryConfiguration](functions.md#mip_cc_createtelemetryconfiguration) | 保護プロファイルの作成に使用する設定オブジェクトを作成する |
| [MIP_CC_TelemetryConfiguration_SetHostName](functions.md#mip_cc_telemetryconfiguration_sethostname) | 内部テレメトリ設定を上書きするテレメトリホスト名を設定する |
| [MIP_CC_TelemetryConfiguration_SetLibraryName](functions.md#mip_cc_telemetryconfiguration_setlibraryname) | テレメトリ共有ライブラリオーバーライドの設定 |
| [MIP_CC_TelemetryConfiguration_SetHttpDelegate](functions.md#mip_cc_telemetryconfiguration_sethttpdelegate) | 既定のテレメトリ HTTP スタックをクライアント独自にオーバーライドする |
| [MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate](functions.md#mip_cc_telemetryconfiguration_settaskdispatcherdelegate) | 既定の非同期タスクディスパッチャーをクライアント独自にオーバーライドする |
| [MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled](functions.md#mip_cc_telemetryconfiguration_setisnetworkdetectionenabled) | バックグラウンドスレッドでテレメトリコンポーネントがネットワークステータスに ping を実行できるかどうかを設定します。 |
| [MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled](functions.md#mip_cc_telemetryconfiguration_setislocalcachingenabled) | テレメトリコンポーネントでディスクへのキャッシュの書き込みが許可されているかどうかを設定します。 |
| [MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled](functions.md#mip_cc_telemetryconfiguration_setistraceloggingenabled) | テレメトリコンポーネントでディスクへのログの書き込みが許可されているかどうかを設定します |
| [MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut](functions.md#mip_cc_telemetryconfiguration_setistelemetryoptedout) | アプリケーション/ユーザーがオプションのテレメトリをオプトアウトしたかどうかを設定します。 |
| [MIP_CC_TelemetryConfiguration_SetCustomSettings](functions.md#mip_cc_telemetryconfiguration_setcustomsettings) | カスタムテレメトリ設定を設定します |
| [MIP_CC_TelemetryConfiguration_AddMaskedProperty](functions.md#mip_cc_telemetryconfiguration_addmaskedproperty) | テレメトリプロパティを mask に設定します |
| [MIP_CC_ReleaseTelemetryConfiguration](functions.md#mip_cc_releasetelemetryconfiguration) | 保護プロファイル設定に関連付けられているリソースを解放する |
| [MIP_CC_TemplateDescriptor_GetId](functions.md#mip_cc_templatedescriptor_getid) | テンプレート ID を取得します。 |
| [MIP_CC_TemplateDescriptor_GetNameSize](functions.md#mip_cc_templatedescriptor_getnamesize) | 名前を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_TemplateDescriptor_GetName](functions.md#mip_cc_templatedescriptor_getname) | テンプレート名を取得します。 |
| [MIP_CC_TemplateDescriptor_GetDescriptionSize](functions.md#mip_cc_templatedescriptor_getdescriptionsize) | 説明を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_TemplateDescriptor_GetDescription](functions.md#mip_cc_templatedescriptor_getdescription) | テンプレートの説明を取得します。 |
| [MIP_CC_ReleaseTemplateDescriptor](functions.md#mip_cc_releasetemplatedescriptor) | テンプレート記述子に関連付けられているリソースを解放する |
| [MIP_CC_ActionResult_GetActions](functions.md#mip_cc_actionresult_getactions) | アクションの結果を構成するアクションを取得します。 |
| [MIP_CC_ReleaseActionResult](functions.md#mip_cc_releaseactionresult) | アクションの結果に関連付けられているリソースを解放する |
| [MIP_CC_AddContentFooterAction_GetUIElementNameSize](functions.md#mip_cc_addcontentfooteraction_getuielementnamesize) | "コンテンツフッターの追加" アクションの UI 要素名を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddContentFooterAction_GetUIElementName](functions.md#mip_cc_addcontentfooteraction_getuielementname) | "コンテンツフッターの追加" アクションの UI 要素名を取得します。 |
| [MIP_CC_AddContentFooterAction_GetTextSize](functions.md#mip_cc_addcontentfooteraction_gettextsize) | "コンテンツフッターの追加" アクションのテキストを格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddContentFooterAction_GetText](functions.md#mip_cc_addcontentfooteraction_gettext) | "コンテンツフッターの追加" アクションのテキストを取得します。 |
| [MIP_CC_AddContentFooterAction_GetFontNameSize](functions.md#mip_cc_addcontentfooteraction_getfontnamesize) | "コンテンツフッターの追加" アクションのフォント名を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddContentFooterAction_GetFontName](functions.md#mip_cc_addcontentfooteraction_getfontname) | "コンテンツフッターの追加" アクションのフォント名を取得します。 |
| [MIP_CC_AddContentFooterAction_GetFontSize](functions.md#mip_cc_addcontentfooteraction_getfontsize) | 整数のフォントサイズを取得します。 |
| [MIP_CC_AddContentFooterAction_GetFontColorSize](functions.md#mip_cc_addcontentfooteraction_getfontcolorsize) | "コンテンツフッターの追加" アクションのフォントの色を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddContentFooterAction_GetFontColor](functions.md#mip_cc_addcontentfooteraction_getfontcolor) | "コンテンツフッターの追加" アクションのフォントの色 (例、"#000000") を取得します。 |
| [MIP_CC_AddContentFooterAction_GetAlignment](functions.md#mip_cc_addcontentfooteraction_getalignment) | 配置を取得します。 |
| [MIP_CC_AddContentFooterAction_GetMargin](functions.md#mip_cc_addcontentfooteraction_getmargin) | 余白のサイズを取得します。 |
| [MIP_CC_AddContentHeaderAction_GetUIElementNameSize](functions.md#mip_cc_addcontentheaderaction_getuielementnamesize) | "コンテンツヘッダーの追加" アクションの UI 要素名を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddContentHeaderAction_GetUIElementName](functions.md#mip_cc_addcontentheaderaction_getuielementname) | "コンテンツヘッダーの追加" アクションの UI 要素名を取得します。 |
| [MIP_CC_AddContentHeaderAction_GetTextSize](functions.md#mip_cc_addcontentheaderaction_gettextsize) | "コンテンツヘッダーの追加" アクションのテキストを格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddContentHeaderAction_GetText](functions.md#mip_cc_addcontentheaderaction_gettext) | "コンテンツヘッダーの追加" アクションのテキストを取得します。 |
| [MIP_CC_AddContentHeaderAction_GetFontNameSize](functions.md#mip_cc_addcontentheaderaction_getfontnamesize) | "コンテンツヘッダーの追加" アクションのフォント名を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddContentHeaderAction_GetFontName](functions.md#mip_cc_addcontentheaderaction_getfontname) | "コンテンツヘッダーの追加" アクションのフォント名を取得します。 |
| [MIP_CC_AddContentHeaderAction_GetFontSize](functions.md#mip_cc_addcontentheaderaction_getfontsize) | 整数のフォントサイズを取得します。 |
| [MIP_CC_AddContentHeaderAction_GetFontColorSize](functions.md#mip_cc_addcontentheaderaction_getfontcolorsize) | "コンテンツヘッダーの追加" アクションのフォントの色を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddContentHeaderAction_GetFontColor](functions.md#mip_cc_addcontentheaderaction_getfontcolor) | "コンテンツヘッダーの追加" アクションのフォントの色 (例、"#000000") を取得します。 |
| [MIP_CC_AddContentHeaderAction_GetAlignment](functions.md#mip_cc_addcontentheaderaction_getalignment) | 配置を取得します。 |
| [MIP_CC_AddContentHeaderAction_GetMargin](functions.md#mip_cc_addcontentheaderaction_getmargin) | 余白のサイズを取得します。 |
| [MIP_CC_AddWatermarkAction_GetUIElementNameSize](functions.md#mip_cc_addwatermarkaction_getuielementnamesize) | "透かしの追加" アクションの UI 要素名を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddWatermarkAction_GetUIElementName](functions.md#mip_cc_addwatermarkaction_getuielementname) | "透かしの追加" アクションの UI 要素名を取得します。 |
| [MIP_CC_AddWatermarkAction_GetLayout](functions.md#mip_cc_addwatermarkaction_getlayout) | 透かしのレイアウトを取得します。 |
| [MIP_CC_AddWatermarkAction_GetTextSize](functions.md#mip_cc_addwatermarkaction_gettextsize) | "透かしの追加" アクションのテキストを格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddWatermarkAction_GetText](functions.md#mip_cc_addwatermarkaction_gettext) | "透かしの追加" アクションのテキストを取得します。 |
| [MIP_CC_AddWatermarkAction_GetFontNameSize](functions.md#mip_cc_addwatermarkaction_getfontnamesize) | "透かしの追加" アクションのフォント名を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddWatermarkAction_GetFontName](functions.md#mip_cc_addwatermarkaction_getfontname) | "透かしの追加" アクションのフォント名を取得します。 |
| [MIP_CC_AddWatermarkAction_GetFontSize](functions.md#mip_cc_addwatermarkaction_getfontsize) | 整数のフォントサイズを取得します。 |
| [MIP_CC_AddWatermarkAction_GetFontColorSize](functions.md#mip_cc_addwatermarkaction_getfontcolorsize) | "透かしの追加" アクションのフォントの色を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_AddWatermarkAction_GetFontColor](functions.md#mip_cc_addwatermarkaction_getfontcolor) | "透かしの追加" アクションのフォントの色 (例、"#000000") を取得します。 |
| [MIP_CC_ReleaseContentLabel](functions.md#mip_cc_releasecontentlabel) | コンテンツラベルに関連付けられているリソースを解放する |
| [MIP_CC_ContentLabel_GetCreationTime](functions.md#mip_cc_contentlabel_getcreationtime) | ラベルが適用された時刻を取得します |
| [MIP_CC_ContentLabel_GetAssignmentMethod](functions.md#mip_cc_contentlabel_getassignmentmethod) | ラベルの割り当て方法を取得します。 |
| [MIP_CC_ContentLabel_GetExtendedProperties](functions.md#mip_cc_contentlabel_getextendedproperties) | 拡張プロパティを取得します。 |
| [MIP_CC_ContentLabel_IsProtectionAppliedFromLabel](functions.md#mip_cc_contentlabel_isprotectionappliedfromlabel) | ラベルによって保護が適用されたかどうかを取得します。 |
| [MIP_CC_ContentLabel_GetLabel](functions.md#mip_cc_contentlabel_getlabel) | コンテンツラベルのインスタンスから汎用ラベルのプロパティを取得します。 |
| [MIP_CC_CustomAction_GetNameSize](functions.md#mip_cc_customaction_getnamesize) | "カスタム" アクションの名前を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_CustomAction_GetName](functions.md#mip_cc_customaction_getname) | "カスタム" アクションの名前を取得します。 |
| [MIP_CC_CustomAction_GetProperties](functions.md#mip_cc_customaction_getproperties) | "カスタム" アクションのプロパティを取得します。 |
| [MIP_CC_ReleaseLabel](functions.md#mip_cc_releaselabel) | ラベルに関連付けられているリソースを解放する |
| [MIP_CC_Label_GetId](functions.md#mip_cc_label_getid) | ラベル ID を取得します。 |
| [MIP_CC_Label_GetNameSize](functions.md#mip_cc_label_getnamesize) | 名前を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_Label_GetName](functions.md#mip_cc_label_getname) | ラベル名を取得します。 |
| [MIP_CC_Label_GetDescriptionSize](functions.md#mip_cc_label_getdescriptionsize) | 説明を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_Label_GetDescription](functions.md#mip_cc_label_getdescription) | ラベルの説明を取得します。 |
| [MIP_CC_Label_GetColorSize](functions.md#mip_cc_label_getcolorsize) | 色を格納するために必要なバッファーのサイズを取得します |
| [MIP_CC_Label_GetColor](functions.md#mip_cc_label_getcolor) | ラベルの色を取得します。 |
| [MIP_CC_Label_GetSensitivity](functions.md#mip_cc_label_getsensitivity) | ラベルの感度レベルを取得します。 値が大きいほど、より機密性が高いことを意味します。 |
| [MIP_CC_Label_GetTooltipSize](functions.md#mip_cc_label_gettooltipsize) | ツールヒントを格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_Label_GetTooltip](functions.md#mip_cc_label_gettooltip) | ラベルのツールヒントを取得します。 |
| [MIP_CC_Label_GetAutoTooltipSize](functions.md#mip_cc_label_getautotooltipsize) | 自動分類ツールヒントを格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_Label_GetAutoTooltip](functions.md#mip_cc_label_getautotooltip) | ラベルの自動分類ツールヒントを取得します。 |
| [MIP_CC_Label_IsActive](functions.md#mip_cc_label_isactive) | ラベルがアクティブかどうかを取得します。 |
| [MIP_CC_Label_GetParent](functions.md#mip_cc_label_getparent) | 親ラベル (存在する場合) を取得します。 |
| [MIP_CC_Label_GetChildrenSize](functions.md#mip_cc_label_getchildrensize) | 子ラベルの数を取得します。 |
| [MIP_CC_Label_GetChildren](functions.md#mip_cc_label_getchildren) | 子ラベルを取得します。 |
| [MIP_CC_Label_GetCustomSettings](functions.md#mip_cc_label_getcustomsettings) | ラベルのポリシーで定義されたカスタム設定を取得します。 |
| [MIP_CC_MetadataAction_GetMetadataToRemove](functions.md#mip_cc_metadataaction_getmetadatatoremove) | 削除する "メタデータ" アクションのメタデータを取得します。 |
| [MIP_CC_MetadataAction_GetMetadataToAdd](functions.md#mip_cc_metadataaction_getmetadatatoadd) | 追加する "メタデータ" アクションのメタデータを取得します。 |
| [MIP_CC_CreateMetadataDictionary](functions.md#mip_cc_createmetadatadictionary) | 文字列のキー/値の辞書を作成する |
| [MIP_CC_MetadataDictionary_GetEntries](functions.md#mip_cc_metadatadictionary_getentries) | ディクショナリを構成するメタデータエントリを取得する |
| [MIP_CC_ReleaseMetadataDictionary](functions.md#mip_cc_releasemetadatadictionary) | ディクショナリに関連付けられているリソースを解放する |
| [MIP_CC_ReleasePolicyHandler](functions.md#mip_cc_releasepolicyhandler) | ポリシーハンドラーに関連付けられているリソースを解放する |
| [MIP_CC_PolicyHandler_GetSensitivityLabel](functions.md#mip_cc_policyhandler_getsensitivitylabel) | ドキュメントの現在のラベルを取得します。 |
| [MIP_CC_PolicyHandler_ComputeActions](functions.md#mip_cc_policyhandler_computeactions) | 指定された状態に基づいてポリシー規則を実行し、対応するアクションを決定します。 |
| [MIP_CC_PolicyHandler_NotifyCommittedActions](functions.md#mip_cc_policyhandler_notifycommittedactions) | 計算されたアクションが適用され、データがディスクにコミットされた後に、アプリケーションによって呼び出されます |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize) | 2つのキー暗号化 url を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurl) | 二重キー暗号化 url を取得します。 |
| [MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize) | 2つのキー暗号化 url を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurl) | 二重キー暗号化 url を取得します。 |
| [MIP_CC_RemoveContentFooterAction_GetUIElementNames](functions.md#mip_cc_removecontentfooteraction_getuielementnames) | 削除する "コンテンツフッターの削除" アクションの UI 要素名を取得します。 |
| [MIP_CC_RemoveContentHeaderAction_GetUIElementNames](functions.md#mip_cc_removecontentheaderaction_getuielementnames) | 削除する "コンテンツヘッダーの削除" アクションの UI 要素名を取得します。 |
| [MIP_CC_RemoveWatermarkAction_GetUIElementNames](functions.md#mip_cc_removewatermarkaction_getuielementnames) | 削除する "透かしの削除" アクションの UI 要素名を取得します。 |
| [MIP_CC_ReleaseSensitivityType](functions.md#mip_cc_releasesensitivitytype) | 秘密度の種類に関連付けられているリソースを解放する |
| [MIP_CC_SensitivityType_GetRulePackageIdSize](functions.md#mip_cc_sensitivitytype_getrulepackageidsize) | 秘密度の種類の規則パッケージ ID を格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_SensitivityType_GetRulePackageId](functions.md#mip_cc_sensitivitytype_getrulepackageid) | 感度の種類の規則パッケージ ID を取得します。 |
| [MIP_CC_SensitivityType_GetRulePackageSize](functions.md#mip_cc_sensitivitytype_getrulepackagesize) | 感度の種類の規則パッケージを格納するために必要なバッファーのサイズを取得します。 |
| [MIP_CC_SensitivityType_GetRulePackage](functions.md#mip_cc_sensitivitytype_getrulepackage) | 感度の種類の規則パッケージを取得します。 |
