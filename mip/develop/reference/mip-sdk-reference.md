---
title: 参照用C++ MIP SDK
description: 参照用C++ MIP SDK
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 69896e60fcf8aa33b2181fd22aeda803ab35b1cf
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555995"
---
# <a name="mip-sdk-for-c-reference"></a>参照用C++ MIP SDK

のC++ Microsoft INFORMATION PROTECTION (MIP) SDK を使用すると、開発者はデータやその他のデジタル資産にデータ保護ポリシーを管理して適用することができます。

MIP SDK for C++ には次が含まれます。

- [列挙型と構造体](mip-enums-and-structs.md)
- [関数](mip-functions.md)
- 次のクラス:

 インスタンス                         | Description                                
--------------------------------|---------------------------------------------
[クラス mip:: AccessDeniedError](class_mip_accessdeniederror.md)  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
[クラス mip:: Action](class_mip_action.md)  |  アクションのインターフェイス。 各アクションは、(ポリシーで定義されているように) アプリケーションがラベルを適用するために実行する必要がある手順に対応します
[クラス mip:: ActionData](class_mip_actiondata.md)  | まだ文書化されていません。
[クラス mip:: Addcontentフッターアクション](class_mip_addcontentfooteraction.md)  |  コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
[クラス mip:: AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  コンテンツ ヘッダーの追加を指定するアクション クラス。
[クラス mip:: AddWatermarkAction](class_mip_addwatermarkaction.md)  |  ウォーターマークの追加を指定するアクション クラス。
[クラス mip:: AddWatermarkActionData](class_mip_addwatermarkactiondata.md)  | まだ文書化されていません。
[クラス mip:: AdhocProtectionRequiredError](class_mip_adhocprotectionrequirederror.md)  |  ファイルに対する操作を完了するには、アドホック保護を設定する必要があります。
[クラス mip:: ApplicationActionState](class_mip_applicationactionstate.md)  | まだ文書化されていません。
[クラス mip:: ApplyLabelAction](class_mip_applylabelaction.md)  |  ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
[クラス mip:: ArgumentData](class_mip_argumentdata.md)  | まだ文書化されていません。
[クラス mip:: AuthDelegate](class_mip_authdelegate.md)  |  認証関連の操作のデリゲート。
[クラス mip:: AuthDelegate:: OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)  |  oauth2 トークンを生成するために、呼び出し元アプリケーションから必要なすべての情報を含むクラス。
[クラス mip:: AuthDelegate:: OAuth2Token](class_mip_authdelegate_oauth2token.md)  |  Mipmap SDK が oauth2 トークンを SDK に渡すことを要求する方法を定義するクラス。
[クラス mip:: BadInputError](class_mip_badinputerror.md)  |  無効な入力エラー。SDK の API への入力が無効だった場合にスローされます。
[クラス mip:: ClassificationData](class_mip_classificationdata.md)  | まだ文書化されていません。
[クラス mip:: ClassificationRequest](class_mip_classificationrequest.md)  |  実行状態に対する分類呼び出しの要求を含むクラス。
[クラス mip:: ClassificationResult](class_mip_classificationresult.md)  |  実行状態での分類呼び出しの結果を含むクラス。
[クラス mip:: ComputeEngine](class_mip_computeengine.md)  | まだ文書化されていません。
[クラス mip:: ComputeEngine:: Settings](class_mip_computeengine_settings.md)  | まだ文書化されていません。
[クラス mip:: ComputeEngineContext](class_mip_computeenginecontext.md)  | まだ文書化されていません。
[クラス mip:: ConditionData](class_mip_conditiondata.md)  | まだ文書化されていません。
[クラス mip:: Conのデリゲート](class_mip_consentdelegate.md)  |  同意に関連する操作の委任。
[クラス mip:: ConsentDeniedError](class_mip_consentdeniederror.md)  |  ユーザーに同意を求めた操作で、同意が得られませんでした。
[クラス mip:: ContentLabel](class_mip_contentlabel.md)  |  コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
[クラス mip:: ContentMarkingActionData](class_mip_contentmarkingactiondata.md)  | まだ文書化されていません。
[クラス mip:: CustomAction](class_mip_customaction.md)  |  CustomAction は、アクションのすべてのサブプロパティをプロパティバッグとしてキャプチャする汎用アクションクラスです。 呼び出し元は、アクションの意味を理解する必要があります。
[クラス mip::D eprecatedApiError](class_mip_deprecatedapierror.md)  |  呼び出し元が非推奨の API を呼び出しました。
[クラス mip::D ocumentState](class_mip_documentstate.md)  | まだ文書化されていません。
[クラス mip:: Error](class_mip_error.md)  |  MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
[クラス mip:: ExecutionState](class_mip_executionstate.md)  |  エンジンの実行に必要なすべての状態のインターフェイス。
[クラス mip:: FileEngine](class_mip_fileengine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[クラス mip:: FileEngine:: Settings](class_mip_fileengine_settings.md)  | まだ文書化されていません。
[クラス mip:: FileExecutionState](class_mip_fileexecutionstate.md)  | まだ文書化されていません。
[クラス mip:: FileHandler](class_mip_filehandler.md)  |  すべてのファイル処理関数のインターフェイス。
[クラス mip:: FileHandler:: オブザーバー](class_mip_filehandler_observer.md)  |  クライアントがファイルハンドラーに関連する通知イベントを取得するためのオブザーバーインターフェイス。
[クラス mip:: FileInspector](class_mip_fileinspector.md)  | まだ文書化されていません。
[クラス mip:: FileIOError](class_mip_fileioerror.md)  |  ファイル IO エラー。
[クラス mip:: FileProfile](class_mip_fileprofile.md)  |  FileProfile クラスは、Microsoft Information Protection 操作を使用するためのルートクラスです。
[クラス mip:: FileProfile:: オブザーバー](class_mip_fileprofile_observer.md)  |  クライアントがプロファイル関連イベントの通知を取得するためのオブザーバーインターフェイス。
[クラス mip:: FileProfile:: Settings](class_mip_fileprofile_settings.md)  |  作成時および有効期間全体にわたって FileProfile によって使用される設定。
[クラス mip:: HttpDelegate](class_mip_httpdelegate.md)  |  HTTP の処理をオーバーライドするインターフェイス。
[クラス mip:: HttpOperation](class_mip_httpoperation.md)  |  HttpDelegate をオーバーライドするときにクライアントアプリによって実装される、単一の HTTP 操作を記述するインターフェイス。
[クラス mip:: HttpRequest](class_mip_httprequest.md)  |  1 つの HTTP 要求を表すインターフェイス。
[クラス mip:: Httpresponse.cache](class_mip_httpresponse.md)  |  HttpDelegate をオーバーライドするときにクライアントアプリによって実装される、単一の HTTP 応答を記述するインターフェイス。
[クラス mip:: Identity](class_mip_identity.md)  |  Id の抽象化。
[クラス mip:: InternalError](class_mip_internalerror.md)  |  内部エラー。 このエラーは、実行中に予期しない事態が発生するとスローされます。
[クラス mip:: JustificationRequiredError](class_mip_justificationrequirederror.md)  | まだ文書化されていません。
[クラス mip:: ジャスト Ifyaction](class_mip_justifyaction.md)  |  ジャスティフィケーションアクションでは、ラベルダウングレードに対する根拠を提示し、応答を実行状態に設定する必要があります。
[クラス mip:: Label](class_mip_label.md)  |  単一の Microsoft Information Protection ラベルの抽象化。
[クラス mip:: LabelActionData](class_mip_labelactiondata.md)  | まだ文書化されていません。
[クラス mip:: LabelDisabledError](class_mip_labeldisablederror.md)  |  ラベルが無効または非アクティブです。
[クラス mip:: LabelGroupData](class_mip_labelgroupdata.md)  | まだ文書化されていません。
[クラス mip:: LabelingOptions](class_mip_labelingoptions.md)  |  SetLabel/DeleteLabel メソッドのラベル付けオプションを構成するためのインターフェイス。
[クラス mip:: Labelnotfound エラー](class_mip_labelnotfounderror.md)  |  ラベル ID が認識されていません。
[クラス mip:: LoggerDelegate](class_mip_loggerdelegate.md)  |  MIP SDK のロガーに対してインターフェイスを定義するクラス。
[クラス mip:: MetadataAction](class_mip_metadataaction.md)  |  コンテンツにメタデータ情報を追加するアクション。
[クラス mip:: MipContext](class_mip_mipcontext.md)  |  MipContext は、すべてのプロファイル、エンジン、ハンドラー間で共有される状態を表します。
[クラス mip:: MsgAttachmentData](class_mip_msgattachmentdata.md)  | まだ文書化されていません。
[クラス mip:: MsgInspector](class_mip_msginspector.md)  | まだ文書化されていません。
[クラス mip:: NetworkError](class_mip_networkerror.md)  |  ネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。
[クラス mip:: NoAuthTokenError](class_mip_noauthtokenerror.md)  |  認証トークンがないため、ユーザーはコンテンツにアクセスできませんでした。
[クラス mip:: NoPermissionsError](class_mip_nopermissionserror.md)  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
[クラス mip:: NoPolicyError](class_mip_nopolicyerror.md)  |  テナントポリシーが分類/ラベルに対して構成されていません。
[クラス mip:: NotSupportedError](class_mip_notsupportederror.md)  |  アプリケーションによって要求された操作は、SDK ではサポートされていません。
[クラス mip:: Operationcancel-Error](class_mip_operationcancellederror.md)  |  操作が取り消されました。
[クラス mip::P olicyEngine](class_mip_policyengine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[クラス mip::P olicyEngine:: Settings](class_mip_policyengine_settings.md)  |  PolicyEngine に関連付けられた設定を定義します。
[クラス mip::P olicyHandler](class_mip_policyhandler.md)  |  このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
[クラス mip::P olicyPackageData](class_mip_policypackagedata.md)  | まだ文書化されていません。
[クラス mip::P olicyProfile](class_mip_policyprofile.md)  |  PolicyProfile クラスは、Microsoft Information Protection 操作を使用するためのルートクラスです。 一般的なアプリケーションで必要な PolicyProfile は1つだけですが、必要に応じて複数のプロファイルを作成できます。
[クラス mip::P olicyProfile:: オブザーバー](class_mip_policyprofile_observer.md)  |  クライアントがプロファイル関連イベントの通知を取得するためのオブザーバーインターフェイス。
[クラス mip::P olicyProfile:: Settings](class_mip_policyprofile_settings.md)  |  作成時および有効期間全体にわたって PolicyProfile によって使用される設定。
[クラス mip::P olicyRuleData](class_mip_policyruledata.md)  | まだ文書化されていません。
[クラス mip::P olicySyncError](class_mip_policysyncerror.md)  |  ポリシー データを同期しようとして失敗しました。
[クラス mip::P rivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  現在のラベルは特権操作 (管理者の操作と同等) として割り当てられています。このため、オーバーライドできません。
[クラス mip::P ropertyData](class_mip_propertydata.md)  | まだ文書化されていません。
[クラス mip::P rotectAdhocAction](class_mip_protectadhocaction.md)  |  アドホック保護をドキュメントに追加することを指定するアクション クラス。
[クラス mip::P rotectByTemplateAction](class_mip_protectbytemplateaction.md)  |  テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
[クラス mip::P rotectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  追加によって保護がドキュメントに転送されないことを指定するアクション クラス。
[クラス mip::P rotectionActionData](class_mip_protectionactiondata.md)  | まだ文書化されていません。
[クラス mip::P rotectionDescriptor](class_mip_protectiondescriptor.md)  |  コンテンツの一部に関連付けられている保護の説明。
[クラス mip::P rotectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  コンテンツの一部に関連付けられた保護を記述する ProtectionDescriptor を構築します。
[クラス mip::P rotectionEngine](class_mip_protectionengine.md)  |  特定の ID に関連する、保護関連のアクションを管理します。
[クラス mip::P rotectionEngine:: オブザーバー](class_mip_protectionengine_observer.md)  |  ProtectionEngine に関連する通知を受信するインターフェイスです。
[クラス mip::P rotectionEngine:: Settings](class_mip_protectionengine_settings.md)  |  作成時および有効期間全体にわたって ProtectionEngine によって使用される設定。
[クラス mip::P rotectionHandler](class_mip_protectionhandler.md)  |  特定の保護構成のための保護に関連するアクションを管理します。
[クラス mip::P rotectionHandler:: ConsumptionSettings](class_mip_protectionhandler_consumptionsettings.md)  |  既存のコンテンツを使用する ProtectionHandler を作成するために使用される設定。
[クラス mip::P rotectionHandler:: オブザーバー](class_mip_protectionhandler_observer.md)  |  ProtectionHandler に関連する通知を受信するインターフェイスです。
[クラス mip::P rotectionHandler::P ublishingSettings](class_mip_protectionhandler_publishingsettings.md)  |  新しいコンテンツを保護する ProtectionHandler を作成するために使用される設定。
[クラス mip::P rotectionProfile](class_mip_protectionprofile.md)  |  ProtectionProfile は、保護操作を実行するためのルートクラスです。
[クラス mip::P rotectionProfile:: オブザーバー](class_mip_protectionprofile_observer.md)  |  ProtectionProfile に関連する通知を受信するインターフェイスです。
[クラス mip::P rotectionProfile:: Settings](class_mip_protectionprofile_settings.md)  |  作成時および有効期間全体にわたって ProtectionProfile によって使用される設定。
[クラス mip::P rotectionSettings](class_mip_protectionsettings.md)  |  SetLabel メソッドの保護オプションを構成するためのインターフェイスです。
[クラス mip::P roxyAuthenticationError](class_mip_proxyauthenticationerror.md)  |  プロキシ認証エラーです。
[クラス mip::P ublishingLicenseInfo](class_mip_publishinglicenseinfo.md)  |  保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。
[クラス mip:: RecommendLabelAction](class_mip_recommendlabelaction.md)  |  このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
[クラス mip:: RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
[クラス mip:: RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  ドキュメントからのコンテンツ ヘッダーの削除を指定するアクション クラス。
[クラス mip:: RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  ドキュメントからの保護の削除を指定するアクション クラス。
[クラス mip:: RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  ドキュメントからのウォーターマークの削除を指定するアクション クラス。
[クラス mip:: RulePackageData](class_mip_rulepackagedata.md)  | まだ文書化されていません。
[クラス mip:: SensitivityConditionData](class_mip_sensitivityconditiondata.md)  | まだ文書化されていません。
[クラス mip:: SensitivityTypesRulePackage](class_mip_sensitivitytypesrulepackage.md)  | まだ文書化されていません。
[クラス mip:: ServiceDisabledError](class_mip_servicedisablederror.md)  |  サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした。
[クラス mip:: Stream](class_mip_stream.md)  |  MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
[クラス mip:: SyncFileBaseData](class_mip_syncfilebasedata.md)  | まだ文書化されていません。
[クラス mip:: SyncFilePolicyData](class_mip_syncfilepolicydata.md)  | まだ文書化されていません。
[クラス mip:: SyncFileSensitivityData](class_mip_syncfilesensitivitydata.md)  | まだ文書化されていません。
[クラス mip:: TaskDispatcherDelegate](class_mip_taskdispatcherdelegate.md)  |  MIP SDK タスクディスパッチャーへのインターフェイスを定義するクラス。
[クラス mip:: Templatenotfound エラー](class_mip_templatenotfounderror.md)  |  テンプレート ID は RMS サービスによって認識されません。
[クラス mip:: 遷移 Entnetworkerror](class_mip_transientnetworkerror.md)  |  一時的なネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。 このエラーは一時的なエラーであるため、この操作は再試行できます。
[クラス mip:: UserRights](class_mip_userrights.md)  |  ユーザーのグループおよびそれらに関連付けられている権限。
[クラス mip:: UserRoles](class_mip_userroles.md)  |  ユーザーのグループおよびそれらに関連付けられているロール。