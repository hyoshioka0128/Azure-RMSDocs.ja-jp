---
title: 参照用C++ MIP SDK
description: 参照用C++ MIP SDK
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2fab85dfd5b5d0d1103f9c3ee4b0d3725a10cb8f
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884829"
---
# <a name="mip-sdk-for-c-reference"></a>参照用C++ MIP SDK

のC++ Microsoft INFORMATION PROTECTION (MIP) SDK を使用すると、開発者はデータやその他のデジタル資産にデータ保護ポリシーを管理して適用することができます。

MIP SDK for C++ には次が含まれます。

- [列挙型と構造体](mip-enums-and-structs.md)
- [関数](mip-functions.md)
- 次のクラス:

 クラス                         | 説明                                
--------------------------------|---------------------------------------------
class mip::AccessDeniedError  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
class mip::Action  |  アクションのインターフェイス。 各アクションは、(ポリシーで定義されているように) アプリケーションがラベルを適用するために実行する必要がある手順に対応します
クラス mip:: ActionData  | _まだ文書化されていません。_
class mip::AddContentFooterAction  |  コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
class mip::AddContentHeaderAction  |  コンテンツ ヘッダーの追加を指定するアクション クラス。
class mip::AddWatermarkAction  |  ウォーターマークの追加を指定するアクション クラス。
クラス mip:: AddWatermarkActionData  | _まだ文書化されていません。_
クラス mip:: AdhocProtectionRequiredError  |  ファイルに対する操作を完了するには、アドホック保護を設定する必要があります。
クラス mip:: ApplicationActionState  | _まだ文書化されていません。_
class mip::ApplyLabelAction  |  ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
クラス mip:: ArgumentData  | _まだ文書化されていません。_
クラス mip:: AuthDelegate  |  認証関連の操作のデリゲート。
class mip::BadInputError  |  無効な入力エラー。SDK の API への入力が無効だった場合にスローされます。
クラス mip:: ClassificationData  | _まだ文書化されていません。_
クラス mip:: ClassificationRequest  |  実行状態に対する分類呼び出しの要求を含むクラス。
class mip::ClassificationResult  |  実行状態での分類呼び出しの結果を含むクラス。
クラス mip:: ComputeEngine  | _まだ文書化されていません。_
クラス mip:: ComputeEngineContext  | _まだ文書化されていません。_
クラス mip:: ConditionData  | _まだ文書化されていません。_
クラス mip:: Conのデリゲート  |  同意に関連する操作の委任。
class mip::ConsentDeniedError  |  ユーザーに同意を求めた操作で、同意が得られませんでした。
class mip::ContentLabel  |  コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
クラス mip:: ContentMarkingActionData  | _まだ文書化されていません。_
class mip::CustomAction  |  [CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
クラス mip::D eprecatedApiError  |  呼び出し元が非推奨の API を呼び出しました。
クラス mip::D ocumentState  | _まだ文書化されていません。_
class mip::Error  |  MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
class mip::ExecutionState  |  エンジンの実行に必要なすべての状態のインターフェイス。
class mip::FileEngine  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
クラス mip:: FileExecutionState  | _まだ文書化されていません。_
class mip::FileHandler  |  すべてのファイル処理関数のインターフェイス。
クラス mip:: FileInspector  | _まだ文書化されていません。_
class mip::FileIOError  |  ファイル IO エラー。
class mip::FileProfile  |  [FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
class mip::HttpDelegate  |  HTTP の処理をオーバーライドするインターフェイス。
クラス mip:: HttpOperation  |  [Httpdelegate](class_mip_httpdelegate.md)をオーバーライドするときにクライアントアプリによって実装される、単一の HTTP 操作を記述するインターフェイス。
class mip::HttpRequest  |  1 つの HTTP 要求を表すインターフェイス。
class mip::HttpResponse  |  [HttpDelegate](class_mip_httpdelegate.md) をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
クラス mip:: Identity  |  Id の抽象化。
class mip::InternalError  |  内部エラー。 このエラーは、実行中に予期しない事態が発生するとスローされます。
class mip::JustificationRequiredError  | _まだ文書化されていません。_
class mip::JustifyAction  |  正当化[アクション](class_mip_action.md)は、ラベルをダウングレードする理由の提供と実行状態での応答の設定を要求します。
class mip::Label  |  単一の Microsoft Information Protection ラベルの抽象化。
クラス mip:: LabelActionData  | _まだ文書化されていません。_
クラス mip:: LabelDisabledError  |  [ラベル](class_mip_label.md)が無効または非アクティブです。
クラス mip:: LabelGroupData  | _まだ文書化されていません。_
class mip::LabelingOptions  |  SetLabel/DeleteLabel メソッドのラベル付けオプションを構成するためのインターフェイス。
クラス mip:: Labelnotfound エラー  |  [ラベル](class_mip_label.md)ID が認識されません。
class mip::LoggerDelegate  |  MIP SDK のロガーに対してインターフェイスを定義するクラス。
class mip::MetadataAction  |  コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
クラス mip:: MipContext  | MipContext は、すべてのプロファイル、エンジン、ハンドラー間で共有される状態を表します。
クラス mip:: MsgAttachmentData  | _まだ文書化されていません。_
クラス mip:: MsgInspector  | _まだ文書化されていません。_
class mip::NetworkError  |  ネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。
クラス mip:: NoAuthTokenError  |  認証トークンがないため、ユーザーはコンテンツにアクセスできませんでした。
クラス mip:: NoPermissionsError  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
クラス mip:: NoPolicyError  |  テナントポリシーが分類/ラベルに対して構成されていません。
class mip::NotSupportedError  |  アプリケーションによって要求された操作は、SDK ではサポートされていません。
クラス mip:: Operationcancel-Error  |  操作が取り消されました。
class mip::PolicyEngine  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
class mip::PolicyHandler  |  このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
クラス mip::P olicyPackageData  | _まだ文書化されていません。_
class mip::PolicyProfile  |  [PolicyProfile](class_mip_policyprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは [PolicyProfile](class_mip_policyprofile.md) は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
クラス mip::P olicyRuleData  | _まだ文書化されていません。_
class mip::PolicySyncError  |  ポリシー データを同期しようとして失敗しました。
class mip::PrivilegedRequiredError  |  現在のラベルは特権操作 (管理者の操作と同等) として割り当てられています。このため、オーバーライドできません。
クラス mip::P ropertyData  | _まだ文書化されていません。_
class mip::ProtectAdhocAction  |  アドホック保護をドキュメントに追加することを指定するアクション クラス。
class mip::ProtectByTemplateAction  |  テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
class mip::ProtectDoNotForwardAction  |  追加によって保護がドキュメントに転送されないことを指定するアクション クラス。
クラス mip::P rotectionActionData  | _まだ文書化されていません。_
class mip::ProtectionDescriptor  |  コンテンツの一部に関連付けられている保護の説明。
class mip::ProtectionDescriptorBuilder  |  コンテンツの一部に関連付けられている保護を説明する、[ProtectionDescriptor](class_mip_protectiondescriptor.md) を構築します。
class mip::ProtectionEngine  |  特定の ID に関連する、保護関連のアクションを管理します。
class mip::ProtectionHandler  |  特定の保護構成のための保護に関連するアクションを管理します。
class mip::ProtectionProfile  |  [ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
クラス mip::P rotectionSettings  |  SetLabel メソッドの保護オプションを構成するためのインターフェイスです。
クラス mip::P roxyAuthenticationError  |  プロキシ認証エラーです。
クラス mip::P ublishingLicenseInfo  |  保護ハンドラーを作成するために使用する発行ライセンスの詳細を保持します。
class mip::RecommendLabelAction  |  このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
class mip::RemoveContentFooterAction  |  ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
class mip::RemoveContentHeaderAction  |  ドキュメントからのコンテンツ ヘッダーの削除を指定するアクション クラス。
class mip::RemoveProtectionAction  |  ドキュメントからの保護の削除を指定するアクション クラス。
class mip::RemoveWatermarkAction  |  ドキュメントからのウォーターマークの削除を指定するアクション クラス。
クラス mip:: RulePackageData  | _まだ文書化されていません。_
クラス mip:: SensitivityConditionData  | _まだ文書化されていません。_
クラス mip:: SensitivityTypesRulePackage  | _まだ文書化されていません。_
クラス mip:: ServiceDisabledError  |  サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした。
class mip::Stream  |  MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
クラス mip:: SyncFileBaseData  | _まだ文書化されていません。_
クラス mip:: SyncFilePolicyData  | _まだ文書化されていません。_
クラス mip:: SyncFileSensitivityData  | _まだ文書化されていません。_
クラス mip:: TaskDispatcherDelegate  |  MIP SDK タスクディスパッチャーへのインターフェイスを定義するクラス。
クラス mip:: Templatenotfound エラー  |  テンプレート ID は RMS サービスによって認識されません。
class mip::TransientNetworkError  |  一時的なネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。 このエラーは一時的なエラーであるため、この操作は再試行できます。
class mip::UserRights  |  ユーザーのグループおよびそれらに関連付けられている権限。
class mip::UserRoles  |  ユーザーのグループおよびそれらに関連付けられているロール。
