---
title: MIP SDK for C リファレンス
description: MIP SDK for C リファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: cae7955684d0fae0f61e2a7319cbb036263e129b
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650590"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for C リファレンス

Microsoft Information Protection (MIP) SDK for C では、管理、およびデータとその他のデジタル資産へのデータ保護ポリシーを適用する開発者ができます。  

MIP SDK for C++ には次が含まれます。

- [列挙型と構造体](mip-enums-and-structs.md)
- [関数](mip-functions.md)
- 次のクラス:

| Namespace::Class 名 | 説明 |
| :----------|:------------|
[mip::AccessDeniedError](class_mip_AccessDeniedError.md)  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
[mip::Action](class_mip_Action.md)  |  アクションのインターフェイス。 各アクションは、(ポリシーで定義されているように) アプリケーションがラベルを適用するために実行する必要がある手順に対応します
[mip::AddContentFooterAction](class_mip_AddContentFooterAction.md)  |  コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
[mip::AddContentHeaderAction](class_mip_AddContentHeaderAction.md)  |  コンテンツ ヘッダーの追加を指定するアクション クラス。
[mip::AddWatermarkAction](class_mip_AddWatermarkAction.md)  |  ウォーターマークの追加を指定するアクション クラス。
[mip::ApplyLabelAction](class_mip_ApplyLabelAction.md)  |  ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
[mip::AuthDelegate](class_mip_AuthDelegate.md)  |  認証用のデリゲートに関連する操作。
[mip::BadInputError](class_mip_BadInputError.md)  |  無効な入力エラー。SDK の API への入力が無効だった場合にスローされます。
[mip::ClassificationRequest](class_mip_ClassificationRequest.md)  |  実行状態の分類の呼び出しの要求を含むクラスです。
[mip::ClassificationResult](class_mip_ClassificationResult.md)  |  実行状態での分類呼び出しの結果を含むクラス。
[mip::ConsentDelegate](class_mip_ConsentDelegate.md)  |  同意に関連する操作の委任。
[mip::ConsentDeniedError](class_mip_ConsentDeniedError.md)  |  ユーザーに同意を求めた操作で、同意が得られませんでした。
[mip::ContentLabel](class_mip_ContentLabel.md)  |  コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
[mip::CustomAction](class_mip_CustomAction.md)  |  [CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
[mip::Error](class_mip_Error.md)  |  MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
[mip::ExecutionState](class_mip_ExecutionState.md)  |  エンジンの実行に必要なすべての状態のインターフェイス。
[mip::FileEngine](class_mip_FileEngine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[mip::FileExecutionState](class_mip_FileExecutionState.md)  | _まだ文書化されていません。_
[mip::FileHandler](class_mip_FileHandler.md)  |  すべてのファイル処理関数のインターフェイス。
[mip::FileIOError](class_mip_FileIOError.md)  |  ファイル IO エラー。
[mip::FileProfile](class_mip_FileProfile.md)  |  [FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
[mip::HttpDelegate](class_mip_HttpDelegate.md)  |  HTTP の処理をオーバーライドするインターフェイス。
[mip::HttpRequest](class_mip_HttpRequest.md)  |  1 つの HTTP 要求を表すインターフェイス。
[mip::HttpResponse](class_mip_HttpResponse.md)  |  [HttpDelegate](class_mip_httpdelegate.md) をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
[mip::Identity](class_mip_Identity.md)  |  Id の抽象化です。
[mip::InternalError](class_mip_InternalError.md)  |  内部エラーです。 このエラーは、実行中に予期しない事態が発生するとスローされます。
[mip::JustificationRequiredError](class_mip_JustificationRequiredError.md)  | _まだ文書化されていません。_
[mip::JustifyAction](class_mip_JustifyAction.md)  |  正当化[アクション](class_mip_action.md)は、ラベルをダウングレードする理由の提供と実行状態での応答の設定を要求します。
[mip::Label](class_mip_Label.md)  |  単一の Microsoft Information Protection ラベルの抽象化。
[mip::LabelingOptions](class_mip_LabelingOptions.md)  |  SetLabel/DeleteLabel メソッドのラベル付けオプションを構成するためのインターフェイス。
[mip::LoggerDelegate](class_mip_LoggerDelegate.md)  |  MIP SDK のロガーに対してインターフェイスを定義するクラス。
[mip::MetadataAction](class_mip_MetadataAction.md)  |  コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
[mip::NetworkError](class_mip_NetworkError.md)  |  ネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。
[mip::NoAuthTokenError](class_mip_NoAuthTokenError.md)  |  ユーザーは、認証トークンがないため、コンテンツへのアクセスを取得できませんでした。
[mip::NoPermissionsError](class_mip_NoPermissionsError.md)  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
[mip::NoPolicyError](class_mip_NoPolicyError.md)  |  分類とラベルは、テナントのポリシーが構成されていません。
[mip::NotSupportedError](class_mip_NotSupportedError.md)  |  アプリケーションによって要求された操作は、SDK ではサポートされていません。
[mip::PolicyEngine](class_mip_PolicyEngine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[mip::PolicyHandler](class_mip_PolicyHandler.md)  |  このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
[mip::PolicyProfile](class_mip_PolicyProfile.md)  |  [PolicyProfile](class_mip_policyprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは [PolicyProfile](class_mip_policyprofile.md) は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
[mip::PolicySyncError](class_mip_PolicySyncError.md)  |  ポリシー データを同期しようとして失敗しました。
[mip::PrivilegedRequiredError](class_mip_PrivilegedRequiredError.md)  |  現在のラベルは特権操作 (管理者の操作と同等) として割り当てられています。このため、オーバーライドできません。
[mip::ProtectAdhocAction](class_mip_ProtectAdhocAction.md)  |  アドホック保護をドキュメントに追加することを指定するアクション クラス。
[mip::ProtectByTemplateAction](class_mip_ProtectByTemplateAction.md)  |  テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
[mip::ProtectDoNotForwardAction](class_mip_ProtectDoNotForwardAction.md)  |  追加によって保護がドキュメントに転送されないことを指定するアクション クラス。
[mip::ProtectionDescriptor](class_mip_ProtectionDescriptor.md)  |  コンテンツの一部に関連付けられている保護の説明。
[mip::ProtectionDescriptorBuilder](class_mip_ProtectionDescriptorBuilder.md)  |  コンテンツの一部に関連付けられている保護を説明する、[ProtectionDescriptor](class_mip_protectiondescriptor.md) を構築します。
[mip::ProtectionEngine](class_mip_ProtectionEngine.md)  |  特定の ID に関連する、保護関連のアクションを管理します。
[mip::ProtectionHandler](class_mip_ProtectionHandler.md)  |  特定の保護構成のための保護に関連するアクションを管理します。
[mip::ProtectionProfile](class_mip_ProtectionProfile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
[mip::ProxyAuthenticationError](class_mip_ProxyAuthenticationError.md)  |  プロキシ認証に失敗しました。
[mip::RecommendLabelAction](class_mip_RecommendLabelAction.md)  |  このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
[mip::RemoveContentFooterAction](class_mip_RemoveContentFooterAction.md)  |  ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
[mip::RemoveContentHeaderAction](class_mip_RemoveContentHeaderAction.md)  |  ドキュメントからのコンテンツ ヘッダーの削除を指定するアクション クラス。
[mip::RemoveProtectionAction](class_mip_RemoveProtectionAction.md)  |  ドキュメントからの保護の削除を指定するアクション クラス。
[mip::RemoveWatermarkAction](class_mip_RemoveWatermarkAction.md)  |  ドキュメントからのウォーターマークの削除を指定するアクション クラス。
[mip::SensitivityTypesRulePackage](class_mip_SensitivityTypesRulePackage.md)  | _まだ文書化されていません。_
[mip::ServiceDisabledError](class_mip_ServiceDisabledError.md)  |  ユーザーは、サービスを無効になっているため、コンテンツへのアクセスを取得できませんでした。
[mip::Stream](class_mip_Stream.md)  |  MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
[mip::TransientNetworkError](class_mip_TransientNetworkError.md)  |  一時的なネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。 このエラーは一時的なエラーであるため、この操作は再試行できます。
[mip::UserRights](class_mip_UserRights.md)  |  ユーザーのグループおよびそれらに関連付けられている権限。
[mip::UserRoles](class_mip_UserRoles.md)  |  ユーザーのグループおよびそれらに関連付けられているロール。