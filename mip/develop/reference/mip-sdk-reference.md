---
title: MIP SDK for C++ リファレンス
description: MIP SDK for C++ リファレンス
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: da5ee17fbb177fe9b6e37461a5d35425a3945e59
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566758"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for C++ リファレンス

C++ 用 Microsoft Information Protection (MIP) SDK を使用すると、開発者はデータやその他のデジタル資産にデータ保護ポリシーを管理して適用できます。

MIP SDK for C++ には次が含まれます。

- [列挙型と構造体](mip-enums-and-structs.md)
- [関数](mip-functions.md)
- 次のクラス:

## <a name="namespace-mip-classes"></a>名前空間 mip クラス

 クラス                         | 説明                                
--------------------------------|---------------------------------------------
[AccessDeniedError クラス](class_mip_accessdeniederror.md)  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
[クラスアクション](class_mip_action.md)  |  アクションのインターフェイス。 各アクションは、(ポリシーで定義されているように) アプリケーションがラベルを適用するために実行する必要がある手順に対応します
[クラス ActionData](class_mip_actiondata.md)  | まだ文書化されていません。
[クラス Addcontentフッターアクション](class_mip_addcontentfooteraction.md)  |  コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
[AddContentHeaderAction クラス](class_mip_addcontentheaderaction.md)  |  コンテンツ ヘッダーの追加を指定するアクション クラス。
[AddWatermarkAction クラス](class_mip_addwatermarkaction.md)  |  ウォーターマークの追加を指定するアクション クラス。
[AddWatermarkActionData クラス](class_mip_addwatermarkactiondata.md)  | まだ文書化されていません。
[AdhocProtectionRequiredError クラス](class_mip_adhocprotectionrequirederror.md)  |  ファイルに対する操作を完了するには、アドホック保護を設定する必要があります。
[クラス ApplicationActionState](class_mip_applicationactionstate.md)  | まだ文書化されていません。
[クラス ApplyLabelAction](class_mip_applylabelaction.md)  |  ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
[クラス引数データ](class_mip_argumentdata.md)  | まだ文書化されていません。
[クラス AsyncControl](class_mip_asynccontrol.md)  |  非同期操作を取り消すために使用されるクラスです。
[クラス AuthDelegate](class_mip_authdelegate.md)  |  認証関連の操作のデリゲート。
[BadInputError クラス](class_mip_badinputerror.md)  |  無効な入力エラー。SDK の API への入力が無効だった場合にスローされます。
[ClassificationData クラス](class_mip_classificationdata.md)  | まだ文書化されていません。
[ClassificationRequest クラス](class_mip_classificationrequest.md)  |  実行状態に対する分類呼び出しの要求を含むクラス。
[ClassificationResult クラス](class_mip_classificationresult.md)  |  実行状態での分類呼び出しの結果を含むクラス。
[クラス ComputeEngine](class_mip_computeengine.md)  | まだ文書化されていません。
[ComputeEngineContext クラス](class_mip_computeenginecontext.md)  | まだ文書化されていません。
[クラス ConditionData](class_mip_conditiondata.md)  | まだ文書化されていません。
[class ConsentDelegate](class_mip_consentdelegate.md)  |  同意に関連する操作の委任。
[ConsentDeniedError クラス](class_mip_consentdeniederror.md)  |  ユーザーに同意を求めた操作で、同意が得られませんでした。
[クラス ProtectionHandler:: ConsumptionSettings](class_mip_protectionhandler_consumptionsettings.md)  |  既存のコンテンツを使用する ProtectionHandler を作成するために使用される設定。
[クラス ContentLabel](class_mip_contentlabel.md)  |  コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
[クラス ContentMarkingActionData](class_mip_contentmarkingactiondata.md)  | まだ文書化されていません。
[CustomAction クラス](class_mip_customaction.md)  |  CustomAction は、アクションのすべてのサブプロパティをプロパティバッグとしてキャプチャする汎用アクションクラスです。 呼び出し元は、アクションの意味を理解する必要があります。
[DeprecatedApiError クラス](class_mip_deprecatedapierror.md)  |  呼び出し元が非推奨の API を呼び出しました。
[DetailedClassificationResult クラス](class_mip_detailedclassificationresult.md)  |  実行状態での分類呼び出しの結果を含むクラス。
[クラス DocumentState](class_mip_documentstate.md)  | まだ文書化されていません。
[クラスエラー](class_mip_error.md)  |  MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
[クラス ExecutionState](class_mip_executionstate.md)  |  エンジンの実行に必要なすべての状態のインターフェイス。
[クラス FileEngine](class_mip_fileengine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[クラス FileExecutionState](class_mip_fileexecutionstate.md)  | まだ文書化されていません。
[クラス FileHandler](class_mip_filehandler.md)  |  すべてのファイル処理関数のインターフェイス。
[クラス FileInspector](class_mip_fileinspector.md)  | まだ文書化されていません。
[FileIOError クラス](class_mip_fileioerror.md)  |  ファイル IO エラー。
[クラス FileProfile](class_mip_fileprofile.md)  |  FileProfile クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
[クラス HttpDelegate](class_mip_httpdelegate.md)  |  HTTP の処理をオーバーライドするインターフェイス。
[HttpOperation クラス](class_mip_httpoperation.md)  |  HttpDelegate をオーバーライドするときにクライアントアプリによって実装される、単一の HTTP 操作を記述するインターフェイス。
[クラス HttpRequest](class_mip_httprequest.md)  |  1 つの HTTP 要求を表すインターフェイス。
[Httpresponse.cache クラス](class_mip_httpresponse.md)  |  HttpDelegate をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
[クラス Id](class_mip_identity.md)  |  Id の抽象化。
[InsufficientBufferError クラス](class_mip_insufficientbuffererror.md)  |  バッファーエラーが不足しています。
[クラス InternalError](class_mip_internalerror.md)  |  内部エラーです。 このエラーは、実行中に予期しない事態が発生するとスローされます。
[JustificationRequiredError クラス](class_mip_justificationrequirederror.md)  | まだ文書化されていません。
[クラスジャスト Ifyaction](class_mip_justifyaction.md)  |  正当化アクションは、ラベルをダウングレードする理由の提供と実行状態での応答の設定を要求します。
[クラスラベル](class_mip_label.md)  |  単一の Microsoft Information Protection ラベルの抽象化。
[クラス LabelActionData](class_mip_labelactiondata.md)  | まだ文書化されていません。
[LabelDisabledError クラス](class_mip_labeldisablederror.md)  |  ラベルが無効または非アクティブです。
[クラス LabelGroupData](class_mip_labelgroupdata.md)  | まだ文書化されていません。
[クラス LabelingOptions](class_mip_labelingoptions.md)  |  SetLabel/DeleteLabel メソッドのラベル付けオプションを構成するためのインターフェイス。
[クラス Labelnotfound エラー](class_mip_labelnotfounderror.md)  |  ラベル ID が認識されていません。
[LicenseNotRegisteredError クラス](class_mip_licensenotregisterederror.md)  |  ライセンスが登録されていません。
[LoggerDelegate クラス](class_mip_loggerdelegate.md)  |  MIP SDK のロガーに対してインターフェイスを定義するクラス。
[クラス MetadataAction](class_mip_metadataaction.md)  |  コンテンツにメタデータ情報を追加するアクション。
[クラス MetadataEntry](class_mip_metadataentry.md)  |  メタデータエントリの抽象クラス。
[クラス MetadataVersion](class_mip_metadataversion.md)  |  MetadataVersion のインターフェイスです。 MetadataVersion は、アクティブなメタデータとその処理方法を決定します。
[MipContext クラス](class_mip_mipcontext.md)  |  MipContext は、すべてのプロファイル、エンジン、ハンドラー間で共有される状態を表します。
[クラス MsgAttachmentData](class_mip_msgattachmentdata.md)  | まだ文書化されていません。
[クラス MsgInspector](class_mip_msginspector.md)  | まだ文書化されていません。
[クラス NetworkError](class_mip_networkerror.md)  |  ネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。
[クラス NoAuthTokenError](class_mip_noauthtokenerror.md)  |  認証トークンがないため、ユーザーはコンテンツにアクセスできませんでした。
[NoPermissionsError クラス](class_mip_nopermissionserror.md)  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
[クラス NoPolicyError](class_mip_nopolicyerror.md)  |  テナントポリシーが分類/ラベルに対して構成されていません。
[クラス NotSupportedError](class_mip_notsupportederror.md)  |  アプリケーションによって要求された操作は、SDK ではサポートされていません。
[クラス AuthDelegate:: OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)  |  oauth2 トークンを生成するために、呼び出し元アプリケーションから必要なすべての情報を含むクラス。
[クラス AuthDelegate:: OAuth2Token](class_mip_authdelegate_oauth2token.md)  |  アプリケーションによって提供されるアクセストークン情報を格納しているクラス。
[クラス FileHandler:: オブザーバー](class_mip_filehandler_observer.md)  |  クライアントがファイル ハンドラーに関連する通知イベントを取得するための Observer インターフェイス。
[クラス ProtectionEngine:: オブザーバー](class_mip_protectionengine_observer.md)  |  ProtectionEngine に関連する通知を受け取るインターフェイス。
[クラス FileProfile:: オブザーバー](class_mip_fileprofile_observer.md)  |  クライアントがプロファイル関連のイベントに関する通知を取得するための Observer インターフェイス。
[クラス PolicyProfile:: オブザーバー](class_mip_policyprofile_observer.md)  |  クライアントがプロファイル関連のイベントに関する通知を取得するための Observer インターフェイス。
[クラス ProtectionHandler:: オブザーバー](class_mip_protectionhandler_observer.md)  |  ProtectionHandler に関連する通知を受け取るインターフェイス。
[クラス ProtectionProfile:: オブザーバー](class_mip_protectionprofile_observer.md)  |  ProtectionProfile に関連する通知を受け取るインターフェイス。
[クラス操作キャンセルエラー](class_mip_operationcancellederror.md)  |  操作が取り消されました。
[クラス PolicyEngine](class_mip_policyengine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[クラス PolicyHandler](class_mip_policyhandler.md)  |  このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
[クラス PolicyPackageData](class_mip_policypackagedata.md)  | まだ文書化されていません。
[クラス PolicyProfile](class_mip_policyprofile.md)  |  PolicyProfile クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは PolicyProfile は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
[クラス PolicyRuleData](class_mip_policyruledata.md)  | まだ文書化されていません。
[PrivilegedRequiredError クラス](class_mip_privilegedrequirederror.md)  |  現在のラベルは特権操作 (管理者の操作と同等) として割り当てられています。このため、オーバーライドできません。
[クラスの PropertyData](class_mip_propertydata.md)  | まだ文書化されていません。
[ProtectAdhocAction クラス](class_mip_protectadhocaction.md)  |  アドホック保護をドキュメントに追加することを指定するアクション クラス。
[ProtectAdhocDkAction クラス](class_mip_protectadhocdkaction.md)  |  アドホックダブルキー保護を文書に追加することを指定するアクションクラス。
[ProtectByEncryptOnlyAction クラス](class_mip_protectbyencryptonlyaction.md)  |  ドキュメントに暗号化のみの保護を追加することを指定するアクションクラス。
[ProtectByTemplateAction クラス](class_mip_protectbytemplateaction.md)  |  テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
[ProtectDoNotForwardAction クラス](class_mip_protectdonotforwardaction.md)  |  追加によって保護がドキュメントに転送されないことを指定するアクション クラス。
[ProtectDoNotForwardDkAction クラス](class_mip_protectdonotforwarddkaction.md)  |  追加を指定するアクションクラスは、ダブルキー保護をドキュメントに転送しません。
[クラス ProtectionActionData](class_mip_protectionactiondata.md)  | まだ文書化されていません。
[クラス ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  コンテンツの一部に関連付けられている保護の説明。
[クラス Protection記述子ビルダー](class_mip_protectiondescriptorbuilder.md)  |  コンテンツの一部に関連付けられている保護を説明する、ProtectionDescriptor を構築します。
[クラス ProtectionEngine](class_mip_protectionengine.md)  |  特定の ID に関連する、保護関連のアクションを管理します。
[クラス ProtectionHandler](class_mip_protectionhandler.md)  |  特定の保護構成のための保護に関連するアクションを管理します。
[クラス ProtectionProfile](class_mip_protectionprofile.md)  |  ProtectionProfile は、保護操作を実行するためのルート クラスです。
[クラス ProtectionSettings](class_mip_protectionsettings.md)  |  SetLabel メソッドの保護オプションを構成するためのインターフェイスです。
[クラス ProxyAuthenticationError](class_mip_proxyauthenticationerror.md)  |  プロキシ認証エラーです。
[クラス発行 Licenseinfo](class_mip_publishinglicenseinfo.md)  |  保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。
[クラス ProtectionHandler::P ublishingSettings](class_mip_protectionhandler_publishingsettings.md)  |  新しいコンテンツを保護する ProtectionHandler を作成するために使用される設定。
[RecommendLabelAction クラス](class_mip_recommendlabelaction.md)  |  このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
[RemoveContentFooterAction クラス](class_mip_removecontentfooteraction.md)  |  ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
[RemoveContentHeaderAction クラス](class_mip_removecontentheaderaction.md)  |  ドキュメントからのコンテンツ ヘッダーの削除を指定するアクション クラス。
[クラス RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  ドキュメントからの保護の削除を指定するアクション クラス。
[RemoveWatermarkAction クラス](class_mip_removewatermarkaction.md)  |  ドキュメントからのウォーターマークの削除を指定するアクション クラス。
[クラス RulePackageData](class_mip_rulepackagedata.md)  | まだ文書化されていません。
[SensitiveTypeClassificationData クラス](class_mip_sensitivetypeclassificationdata.md)  | まだ文書化されていません。
[SensitivityConditionData クラス](class_mip_sensitivityconditiondata.md)  | まだ文書化されていません。
[SensitivityTypesRulePackage クラス](class_mip_sensitivitytypesrulepackage.md)  | まだ文書化されていません。
[ServiceDisabledError クラス](class_mip_servicedisablederror.md)  |  サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした。
[クラス FileEngine:: Settings](class_mip_fileengine_settings.md)  | まだ文書化されていません。
[クラス PolicyEngine:: Settings](class_mip_policyengine_settings.md)  |  PolicyEngine に関連付けられている設定を定義します。
[クラス PolicyProfile:: Settings](class_mip_policyprofile_settings.md)  |  作成時および有効期間全体にわたって PolicyProfile に使用される設定。
[クラス ProtectionProfile:: Settings](class_mip_protectionprofile_settings.md)  |  作成時および有効期間全体にわたって ProtectionProfile によって使用される設定。
[クラス FileProfile:: Settings](class_mip_fileprofile_settings.md)  |  作成時および有効期間全体にわたって FileProfile に使用される設定。
[クラス ComputeEngine:: Settings](class_mip_computeengine_settings.md)  | まだ文書化されていません。
[クラス ProtectionEngine:: Settings](class_mip_protectionengine_settings.md)  |  作成時および有効期間全体にわたって ProtectionEngine によって使用される設定。
[クラスストリーム](class_mip_stream.md)  |  MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
[クラス SyncFileBaseData](class_mip_syncfilebasedata.md)  | まだ文書化されていません。
[クラス SyncFilePolicyData](class_mip_syncfilepolicydata.md)  | まだ文書化されていません。
[SyncFileSensitivityData クラス](class_mip_syncfilesensitivitydata.md)  | まだ文書化されていません。
[TaskDispatcherDelegate クラス](class_mip_taskdispatcherdelegate.md)  |  MIP SDK タスクディスパッチャーへのインターフェイスを定義するクラス。
[クラステンプレート記述子](class_mip_templatedescriptor.md)  | まだ文書化されていません。
[クラス Templatenotfound エラー](class_mip_templatenotfounderror.md)  |  テンプレート ID は RMS サービスによって認識されません。
[クラス UserRights](class_mip_userrights.md)  |  ユーザーのグループおよびそれらに関連付けられている権限。
[クラス UserRoles](class_mip_userroles.md)  |  ユーザーのグループおよびそれらに関連付けられているロール。