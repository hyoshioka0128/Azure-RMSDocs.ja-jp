---
title: MIP SDK for C++ (プレビュー) リファレンス
description: MIP SDK for C++ (プレビュー) リファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 06d8bb26a8e3026562006d68d4ae8d1630eba81c
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446330"
---
# <a name="mip-sdk-for-c-preview-reference"></a>MIP SDK for C++ (プレビュー) リファレンス

Microsoft Information Protection (MIP) SDK for C++ (プレビュー) では、データおよびその他のデジタル資産に対するデータ保護ポリシーを管理、適用できます。  

詳しくは、[MIP 開発者向けブログ](https://aka.ms/MIPDevelopers)<!-- and [MIP samples](https://aka.ms/mipsdksamples)-->をご覧ください。

MIP SDK for C++ には次が含まれます。

- [列挙型と構造体](mip-enums-and-structs.md)
- [関数](mip-functions.md)
- 次のクラス:

| クラス名 | 説明 |
| :----------|:------------|
[AccessDeniedError](class_mip_accessdeniederror.md)  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
[操作](class_mip_action.md)  |  アクションのインターフェイス。 各アクションは、(ポリシーで定義されているように) アプリケーションがラベルを適用するために実行する必要がある手順に対応します
[AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
[AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  コンテンツ ヘッダーの追加を指定するアクション クラス。
[AddWatermarkAction](class_mip_addwatermarkaction.md)  |  ウォーターマークの追加を指定するアクション クラス。
[ApplyLabelAction](class_mip_applylabelaction.md)  |  ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
[BadInputError](class_mip_badinputerror.md)  |  無効な入力エラー。SDK の API への入力が無効だった場合にスローされます。
[ClassificationResult](class_mip_classificationresult.md)  |  実行状態での分類呼び出しの結果を含むクラス。
[ConsentDelegate](class_consentdelegate.md)  |  同意に関連する操作の委任。
[ConsentDeniedError](class_mip_consentdeniederror.md)  |  ユーザーに同意を求めた操作で、同意が得られませんでした。
[ContentLabel](class_mip_contentlabel.md)  |  コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
[CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
[エラー](class_mip_error.md)  |  MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
[ExecutionState](class_mip_executionstate.md)  |  エンジンの実行に必要なすべての状態のインターフェイス。
[FileEngine::Settings](class_mip_fileengine_settings.md)  | _まだ文書化されていません。_
[FileEngine](class_mip_fileengine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[FileHandler::Observer](class_mip_filehandler_observer.md)  |  クライアントがファイル ハンドラーに関連する通知イベントを取得するための [Observer](class_mip_filehandler_observer.md) インターフェイス。
[FileHandler](class_mip_filehandler.md)  |  すべてのファイル処理関数のインターフェイス。
[FileIOError](class_mip_fileioerror.md)  |  ファイル IO エラー。
[FileProfile::Observer](class_mip_fileprofile_observer.md)  |  クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_fileprofile_observer.md) インターフェイス。
[FileProfile::Settings](class_mip_fileprofile_settings.md)  |  作成時および有効期間全体にわたって [FileProfile](class_mip_fileprofile.md) に使用される[設定](class_mip_fileprofile_settings.md)。
[FileProfile](class_mip_fileprofile.md)  |  [FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
[HttpDelegate](class_mip_httpdelegate.md)  |  HTTP の処理をオーバーライドするインターフェイス。
[HttpRequest](class_mip_httprequest.md)  |  1 つの HTTP 要求を表すインターフェイス。
[HttpResponse](class_mip_httpresponse.md)  |  [HttpDelegate](class_mip_httpdelegate.md) をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
[InternalError](class_mip_internalerror.md)  |  内部エラー。 このエラーは、実行中に予期しない事態が発生するとスローされます。
[JustificationRequiredError](class_mip_justificationrequirederror.md)  | _まだ文書化されていません。_
[JustifyAction](class_mip_justifyaction.md)  |  正当化[アクション](class_mip_action.md)は、ラベルをダウングレードする理由の提供と実行状態での応答の設定を要求します。
[Label](class_mip_label.md)  |  単一の Microsoft Information Protection ラベルの抽象化。
[LabelingOptions](class_mip_labelingoptions.md)  |  SetLabel/DeleteLabel メソッドのラベル付けオプションを構成するためのインターフェイス。
[LoggerDelegate](class_mip_loggerdelegate.md)  |  MIP SDK のロガーに対してインターフェイスを定義するクラス。
[MetadataAction](class_mip_metadataaction.md)  |  コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
[NetworkError](class_mip_networkerror.md)  |  ネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。
[NotSupportedError](class_mip_notsupportederror.md)  |  アプリケーションによって要求された操作は、SDK ではサポートされていません。
[PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  [PolicyEngine](class_mip_policyengine.md) に関連付けられている設定を定義します。
[PolicyEngine](class_mip_policyengine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[PolicyHandler](class_mip_policyhandler.md)  |  このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
[PolicyProfile::Observer](class_mip_policyprofile_observer.md)  |  クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_policyprofile_observer.md) インターフェイス。
[PolicyProfile::Settings](class_mip_policyprofile_settings.md)  |  作成時および有効期間全体にわたって [PolicyProfile](class_mip_policyprofile.md) に使用される[設定](class_mip_policyprofile_settings.md)。
[PolicyProfile](class_mip_policyprofile.md)  |  [PolicyProfile](class_mip_policyprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは [PolicyProfile](class_mip_policyprofile.md) は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
[PolicySyncError](class_mip_policysyncerror.md)  |  ポリシー データを同期しようとして失敗しました。
[PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  現在のラベルは特権操作 (管理者の操作と同等) として割り当てられています。このため、オーバーライドできません。
[ProtectAdhocAction](class_mip_protectadhocaction.md)  |  アドホック保護をドキュメントに追加することを指定するアクション クラス。
[ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
[ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  追加によって保護がドキュメントに転送されないことを指定するアクション クラス。
[ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  コンテンツの一部に関連付けられている保護の説明。
[ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  コンテンツの一部に関連付けられている保護を説明する、[ProtectionDescriptor](class_mip_protectiondescriptor.md) を構築します。
[ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  [ProtectionEngine](class_mip_protectionengine.md) に関連する通知を受け取るインターフェイス。
[ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  作成時および有効期間全体にわたって [ProtectionEngine](class_mip_protectionengine.md) によって使用される[設定](class_mip_protectionengine_settings.md)。
[ProtectionEngine](class_mip_protectionengine.md)  |  特定の ID に関連する、保護関連のアクションを管理します。
[ProtectionHandler::Observer](class_mip_protectionhandler.md)  |  [ProtectionHandler](class_mip_protectionhandler.md) に関連する通知を受け取るインターフェイス。
[ProtectionHandler](class_mip_protectionhandler.md)  |  特定の保護構成のための保護に関連するアクションを管理します。
[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) に関連する通知を受け取るインターフェイス。
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  作成時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)。
[ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
[RecommendLabelAction](class_mip_recommendlabelaction.md)  |  このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
[RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
[RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  ドキュメントからのコンテンツ ヘッダーの削除を指定するアクション クラス。
[RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  ドキュメントからの保護の削除を指定するアクション クラス。
[RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  ドキュメントからのウォーターマークの削除を指定するアクション クラス。
[Stream](class_mip_stream.md)  |  MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
[TransientNetworkError](class_mip_transientnetworkerror.md)  |  一時的なネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。 このエラーは一時的なエラーであるため、この操作は再試行できます。
[UserRights](class_mip_userrights.md)  |  ユーザーのグループおよびそれらに関連付けられている権限。
[UserRoles](class_mip_userroles.md)  |  ユーザーのグループおよびそれらに関連付けられているロール。
