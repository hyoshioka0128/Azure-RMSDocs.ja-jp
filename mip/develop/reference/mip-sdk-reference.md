---
title: MIP SDK for C リファレンス
description: MIP SDK for C リファレンス
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 1db2faeca6c2ff00a0053a7d65d16872190d306f
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574059"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for C リファレンス

Microsoft Information Protection (MIP) SDK for C では、管理、およびデータとその他のデジタル資産へのデータ保護ポリシーを適用する開発者ができます。

MIP SDK for C++ には次が含まれます。

- [列挙型と構造体](mip-enums-and-structs.md)
- [関数](mip-functions.md)
- 次のクラス:

 クラス                         | 説明                                
--------------------------------|---------------------------------------------
class mip::AccessDeniedError  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
class mip::Action  |  アクションのインターフェイス。 各アクションは、(ポリシーで定義されているように) アプリケーションがラベルを適用するために実行する必要がある手順に対応します
class mip::AddContentFooterAction  |  コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
class mip::AddContentHeaderAction  |  コンテンツ ヘッダーの追加を指定するアクション クラス。
class mip::AddWatermarkAction  |  ウォーターマークの追加を指定するアクション クラス。
class mip::AdhocProtectionRequiredError  |  ファイルの操作を完了するには、アドホック保護を設定してください。
class mip::ApplyLabelAction  |  ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
mip::AuthDelegate をクラスします。  |  認証用のデリゲートに関連する操作。
クラスの mip::AuthDelegate::OAuth2Challenge  |  oauth2 トークンを生成するために呼び出し元アプリケーションに必要なすべての情報を含むクラスです。
クラスの mip::AuthDelegate::OAuth2Token  |  MIP SDK で oauth2 トークンを SDK に渡す必要がある方法を定義するクラス。
class mip::BadInputError  |  無効な入力エラー。SDK の API への入力が無効だった場合にスローされます。
mip::ClassificationRequest をクラスします。  |  実行状態の分類の呼び出しの要求を含むクラスです。
class mip::ClassificationResult  |  実行状態での分類呼び出しの結果を含むクラス。
mip::ConsentDelegate をクラスします。  |  同意に関連する操作の委任。
class mip::ConsentDeniedError  |  ユーザーに同意を求めた操作で、同意が得られませんでした。
class mip::ContentLabel  |  コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
class mip::CustomAction  |  [CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
class mip::Error  |  MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
class mip::ExecutionState  |  エンジンの実行に必要なすべての状態のインターフェイス。
class mip::FileEngine  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
class mip::FileEngine::Settings  | _まだ文書化されていません。_
mip::FileExecutionState をクラスします。  | _まだ文書化されていません。_
class mip::FileHandler  |  すべてのファイル処理関数のインターフェイス。
class mip::FileHandler::Observer  |  クライアントがファイル ハンドラーに関連する通知イベントを取得するための [Observer](class_mip_filehandler_observer.md) インターフェイス。
class mip::FileIOError  |  ファイル IO エラー。
class mip::FileProfile  |  [FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
class mip::FileProfile::Observer  |  クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_fileprofile_observer.md) インターフェイス。
class mip::FileProfile::Settings  |  作成時および有効期間全体にわたって [FileProfile](class_mip_fileprofile.md) に使用される[設定](class_mip_fileprofile_settings.md)。
class mip::HttpDelegate  |  HTTP の処理をオーバーライドするインターフェイス。
mip::HttpOperation をクラスします。  |  オーバーライドする場合、クライアント アプリケーションによって実装される単一の HTTP 操作を表すインターフェイスを[HttpDelegate](class_mip_httpdelegate.md)します。
class mip::HttpRequest  |  1 つの HTTP 要求を表すインターフェイス。
class mip::HttpResponse  |  [HttpDelegate](class_mip_httpdelegate.md) をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
クラスの:identity  |  Id の抽象化です。
class mip::InternalError  |  内部エラー。 このエラーは、実行中に予期しない事態が発生するとスローされます。
class mip::JustificationRequiredError  | _まだ文書化されていません。_
class mip::JustifyAction  |  正当化[アクション](class_mip_action.md)は、ラベルをダウングレードする理由の提供と実行状態での応答の設定を要求します。
class mip::Label  |  単一の Microsoft Information Protection ラベルの抽象化。
class mip::LabelingOptions  |  SetLabel/DeleteLabel メソッドのラベル付けオプションを構成するためのインターフェイス。
class mip::LoggerDelegate  |  MIP SDK のロガーに対してインターフェイスを定義するクラス。
class mip::MetadataAction  |  コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
class mip::NetworkError  |  ネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。
mip::NoAuthTokenError をクラスします。  |  ユーザーは、認証トークンがないため、コンテンツへのアクセスを取得できませんでした。
mip::NoPermissionsError をクラスします。  |  ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
mip::NoPolicyError をクラスします。  |  分類とラベルは、テナントのポリシーが構成されていません。
class mip::NotSupportedError  |  アプリケーションによって要求された操作は、SDK ではサポートされていません。
mip::OperationCancelledError をクラスします。  |  操作が取り消されました。
class mip::PolicyEngine  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
class mip::PolicyEngine::Settings  |  [PolicyEngine](class_mip_policyengine.md) に関連付けられている設定を定義します。
class mip::PolicyHandler  |  このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
class mip::PolicyProfile  |  [PolicyProfile](class_mip_policyprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは [PolicyProfile](class_mip_policyprofile.md) は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
class mip::PolicyProfile::Observer  |  クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_policyprofile_observer.md) インターフェイス。
class mip::PolicyProfile::Settings  |  作成時および有効期間全体にわたって [PolicyProfile](class_mip_policyprofile.md) に使用される[設定](class_mip_policyprofile_settings.md)。
class mip::PolicySyncError  |  ポリシー データを同期しようとして失敗しました。
class mip::PrivilegedRequiredError  |  現在のラベルは特権操作 (管理者の操作と同等) として割り当てられています。このため、オーバーライドできません。
class mip::ProtectAdhocAction  |  アドホック保護をドキュメントに追加することを指定するアクション クラス。
class mip::ProtectByTemplateAction  |  テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
class mip::ProtectDoNotForwardAction  |  追加によって保護がドキュメントに転送されないことを指定するアクション クラス。
class mip::ProtectionDescriptor  |  コンテンツの一部に関連付けられている保護の説明。
class mip::ProtectionDescriptorBuilder  |  コンテンツの一部に関連付けられている保護を説明する、[ProtectionDescriptor](class_mip_protectiondescriptor.md) を構築します。
class mip::ProtectionEngine  |  特定の ID に関連する、保護関連のアクションを管理します。
class mip::ProtectionEngine::Observer  |  [ProtectionEngine](class_mip_protectionengine.md) に関連する通知を受け取るインターフェイス。
class mip::ProtectionEngine::Settings  |  作成時および有効期間全体にわたって [ProtectionEngine](class_mip_protectionengine.md) によって使用される[設定](class_mip_protectionengine_settings.md)。
class mip::ProtectionHandler  |  特定の保護構成のための保護に関連するアクションを管理します。
class mip::ProtectionHandler::Observer  |  [ProtectionHandler](class_mip_protectionhandler.md) に関連する通知を受け取るインターフェイス。
class mip::ProtectionProfile  |  [ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
class mip::ProtectionProfile::Observer  |  [ProtectionProfile](class_mip_protectionprofile.md) に関連する通知を受け取るインターフェイス。
class mip::ProtectionProfile::Settings  |  作成時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)。
mip::ProxyAuthenticationError をクラスします。  |  プロキシ認証に失敗しました。
class mip::RecommendLabelAction  |  このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
class mip::RemoveContentFooterAction  |  ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
class mip::RemoveContentHeaderAction  |  ドキュメントからのコンテンツ ヘッダーの削除を指定するアクション クラス。
class mip::RemoveProtectionAction  |  ドキュメントからの保護の削除を指定するアクション クラス。
class mip::RemoveWatermarkAction  |  ドキュメントからのウォーターマークの削除を指定するアクション クラス。
mip::SensitivityTypesRulePackage をクラスします。  | _まだ文書化されていません。_
mip::ServiceDisabledError をクラスします。  |  ユーザーは、サービスを無効になっているため、コンテンツへのアクセスを取得できませんでした。
class mip::Stream  |  MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
mip::TaskDispatcherDelegate をクラスします。  |  MIP SDK タスク ディスパッチャーにインターフェイスを定義するクラス。
class mip::TransientNetworkError  |  一時的なネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。 このエラーは一時的なエラーであるため、この操作は再試行できます。
class mip::UserRights  |  ユーザーのグループおよびそれらに関連付けられている権限。
class mip::UserRoles  |  ユーザーのグループおよびそれらに関連付けられているロール。