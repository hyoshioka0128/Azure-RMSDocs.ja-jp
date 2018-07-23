# <a name="mip-sdk-for-c-preview-reference"></a>MIP SDK for C++ (プレビュー) リファレンス

Microsoft Information Protection (MIP) SDK for C++ (プレビュー) では、データおよびその他のデジタル資産に対するデータ保護ポリシーを管理、適用できます。  

詳しくは、[MIP 開発者向けブログ](https://aka.ms/MIPDevelopers)<!-- and [MIP samples](https://aka.ms/mipsdksamples)-->をご覧ください。

MIP SDK for C++ には次が含まれます。

- [列挙型と構造体](mip-enums-and-structs.md)
- [関数](mip-functions.md)
- 次のクラス:

| クラス名 | 説明 |
| :----------|:------------|
[ConsentDelegate](class_consentdelegate.md)  |  同意に関連する操作の委任。
[mip::AccessDeniedError](class_mip_accessdeniederror.md)  |  ユーザーは、アクセス拒否、コンテンツ取り消しなどにより、コンテンツにアクセスできませんでした。
[mip::Action](class_mip_action.md)  |  アクションのインターフェイス。 各アクションは、(ポリシーで定義されているように) アプリケーションがラベルを適用するために実行する必要がある手順に対応します
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  ドキュメントに追加されるコンテンツ フッターを指定するアクション クラス。
[mip::AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  コンテンツ ヘッダーの追加を指定するアクション クラス。
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md)  |  ウォーターマークの追加を指定するアクション クラス。
[mip::ApplyLabelAction](class_mip_applylabelaction.md)  |  ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
[mip::BadInputError](class_mip_badinputerror.md)  |  無効な入力エラー。SDK の API への入力が無効だった場合にスローされます。
[mip::ClassificationResult](class_mip_classificationresult.md)  |  実行状態での分類呼び出しの結果を含むクラス。
[mip::ContentLabel](class_mip_contentlabel.md)  |  コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
[mip::CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
[mip::Error](class_mip_error.md)  |  MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
[mip::ExecutionState](class_mip_executionstate.md)  |  エンジンの実行に必要なすべての状態のインターフェイス。
[mip::FileEngine](class_mip_fileengine.md)  |  すべてのエンジン関数のインターフェイス。
[mip::FileEngine::Settings](class_mip_fileengine::settings.md)  | _まだ文書化されていません。_
[mip::FileHandler](class_mip_filehandler.md)  |  すべてのファイル処理関数のインターフェイス。
[mip::FileHandler::Observer](class_mip_filehandler::observer.md)  |  クライアントがファイル ハンドラー関連のイベントに関する通知を取得するための [Observer](class_mip_filehandler_observer.md) インターフェイス。
[mip::FileIOError](class_mip_fileioerror.md)  |  ファイル IO エラー。
[mip::FileProfile](class_mip_fileprofile.md)  |  [FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md)  |  クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_fileprofile_observer.md) インターフェイス。
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md)  |  作成時および有効期間全体にわたって [FileProfile](class_mip_fileprofile.md) に使用される[設定](class_mip_fileprofile_settings.md)。
[mip::InternalError](class_mip_internalerror.md)  |  内部エラー。 このエラーは、実行中に予期しない事態が発生するとスローされます。
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md)  | _まだ文書化されていません。_
[mip::JustifyAction](class_mip_justifyaction.md)  |  正当化[アクション](class_mip_action.md)は、ラベルをダウングレードする理由の提供と実行状態での応答の設定を要求します。
[mip::Label](class_mip_label.md)  |  単一の Microsoft Information Protection ラベルの抽象化。
[mip::LabelingOptions](class_mip_labelingoptions.md)  |  SetLabel メソッドのラベル付けオプションを構成するためのインターフェイス。
[mip::LoggerDelegate](class_mip_loggerdelegate.md)  |  MIP SDK のロガーに対してインターフェイスを定義するクラス。
[mip::MetadataAction](class_mip_metadataaction.md)  |  コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
[mip::NetworkError](class_mip_networkerror.md)  |  ネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。
[mip::NotSupportedError](class_mip_notsupportederror.md)  |  アプリケーションによって要求された操作は、SDK ではサポートされていません。
[mip::PolicyEngine](class_mip_policyengine.md)  |  このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  エンジンを開始するには、適切なパラメーターを指定したこのクラスのインスタンスを提供する必要があります。
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  現在のラベルは特権操作 (管理者の操作と同等) として割り当てられています。このため、オーバーライドできません。
[mip::Profile](class_mip_profile.md)  |  [Profile](class_mip_profile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは[プロファイル](class_mip_profile.md)は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
[mip::Profile::Observer](class_mip_profile_observer.md)  |  クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_profile_observer.md) インターフェイス。
[mip::Profile::Settings](class_mip_profile_settings.md)  |  作成時および有効期間全体にわたって [Profile](class_mip_profile.md) に使用される[設定](class_mip_profile_settings.md)。
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md)  |  アドホック保護をドキュメントに追加することを指定するアクション クラス。
[mip::ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  追加によって保護がドキュメントに転送されないことを指定するアクション クラス。
[mip::ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  保護されたコンテンツに関連付けられているアドホック ポリシーを表します。
[mip::ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  保護されたコンテンツに関連付けられているアドホック ポリシーを表します。
[mip::ProtectionEngine](class_mip_protectionengine.md)  |  特定の ID に関連した、保護に関連するアクションを実行します。
[mip::ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  [ProtectionEngine](class_mip_protectionengine.md) に関連する通知を受け取るインターフェイス。
[mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  作成時および有効期間全体にわたって [ProtectionEngine](class_mip_protectionengine.md) によって使用される[設定](class_mip_protectionengine_settings.md)。
[mip::ProtectionHandler](class_mip_protectionhandler.md)  |  特定の保護構成 (つまりユーザー、権限、ロールなど) に向けた、保護に関連するアクションを実行します。
[mip::ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)  |  [ProtectionHandler](class_mip_protectionhandler.md) に関連する通知を受け取るインターフェイス。
[mip::ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) に関連する通知を受け取るインターフェイス。
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  作成時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)。
[mip::RecommendLabelAction](class_mip_recommendlabelaction.md)  |  このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  ドキュメントからのコンテンツ ヘッダーの削除を指定するアクション クラス。
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  ドキュメントからの保護の削除を指定するアクション クラス。
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  ドキュメントからのウォーターマークの削除を指定するアクション クラス。
[mip::Stream](class_mip_stream.md)  |  MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
[mip::UserRights](class_mip_userrights.md)  |  ユーザーのグループおよびそれらに関連付けられている権限を表します。
[mip::UserRoles](class_mip_userroles.md)  |  ユーザーのグループおよびそれらに関連付けられているロールを表します。

 
