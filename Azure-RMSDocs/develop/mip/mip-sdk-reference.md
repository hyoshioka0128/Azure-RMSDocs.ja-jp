# <a name="mip-sdk-for-c-preview-reference"></a>MIP SDK for C++ (プレビュー) リファレンス

Microsoft Information Protection (MIP) SDK for C++ (プレビュー) では、データおよびその他のデジタル資産に対するデータ保護ポリシーを管理、適用できます。  

詳しくは、[MIP 開発者向けブログ](https://aka.ms/MIPDevelopers)と [MIP サンプル](https://aka.ms/mipsdksamples)をご覧ください。

MIP SDK for C++ には、以下のクラスが含まれています。

| クラス名 | 説明 |
| :----------|:------------|
[mip::Action](class_mip_action.md) | すべてのアクションの基底クラス。 |
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md) | コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
[mip::addContentHeaderAction](class_mip_addcontentheaderaction.md) | コンテンツ ヘッダーの追加を指定するアクション クラス。
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md) | ウォーターマークの追加を指定するアクション クラス。
[mip::BadInputError](class_mip_badinputerror.md) | 無効な入力エラー。API への入力が無効でした。
[mip::CommonRights](class_mip_commonrights.md) | 広くサポートされている権限。
[mip::Consent](class_mip_consent.md) | アクションの許可に対するユーザーの同意/拒否を表します。
[mip::ConsentCallback](class_mip_consentcallback.md) | 同意要求通知のインターフェイス。
[mip::ConsentResult](class_mip_consentresult.md) | ユーザー操作の後の同意要求の結果について説明します。
[mip::ContentLabel](class_mip_contentlabel.md) | コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
[mip::CustomAction](class_mip_customaction.md) | アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラス。
[mip::CustomProtectedStream](class_mip_customprotectedstream.md) | ストリームをラップして、読み取りと書き込みに対して透過的な暗号化と復号化を提供します。
[mip::EditableDocumentRights](class_mip_editabledocumentrights.md) | 編集可能なドキュメントに適用される権限。
[mip::EmailRights](class_mip_emailrights.md) | 電子メールに適用される権限。
[mip::Error](class_mip_error.md) | MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
[mip::ExecutionState](class_mip_executionstate.md) | エンジンの実行に必要なすべての状態のインターフェイス。
[mip::FileEngine](class_mip_fileengine.md) | すべてのエンジン関数のインターフェイス。
[mip::FileEngine::Settings](class_mip_fileengine_settings.md) | 
[mip::FileHandler](class_mip_filehandler.md) | すべてのファイル処理関数のインターフェイス。
[mip::FileHandler::Observer](class_mip_filehandler_observer.md) | クライアントがファイル ハンドラー関連のイベントに関する通知を取得するための Observer インターフェイス。
[mip::FileIOError](class_mip_fileioerror.md) | ファイル IO エラー。
[mip::FileProfile](class_mip_fileprofile.md) | Microsoft Information Protection 操作のルート クラス。
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md) | プロファイル関連のイベント通知を受信するために使用される Observer インターフェイス。
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md) | ファイルのプロファイル設定を管理するためのインターフェイス。
[mip::GetUserPolicyResult](class_mip_getuserpolicyresult.md) | ユーザー ポリシーの取得要求の結果について説明します。
[mip::InternalError](class_mip_internalerror.md) | 内部 SDK エラー。 予期せぬ事態が発生しました。
[mip::IStream](class_mip_istream.md) | 保護されたストリーム用の基底インターフェイス。
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md) | 要求された変更には、変更の説明が必要です。
[mip::JustifyAction](class_mip_justifyaction.md) | 要求には、ラベルをダウングレードする理由と実行状態での応答の設定が必要です。
[mip::Label](class_mip_label.md) | 単一の Microsoft Information Protection ラベルの抽象化。
[mip::LabelingOptions](class_mip_labelingoptions.md) | SetLabel メソッドのラベル付けオプションを構成するためのインターフェイス。
[mip::MetadataAction](class_mip_metadataaction.md) | コンテンツに追加するメタデータ情報を指定するアクション。
[mip::NetworkError](class_mip_networkerror.md) | ネットワーク エラー。
[mip::NotSupportedError](class_mip_notsupportederror.md) | サポートされていない操作のエラー。
[mip::PolicyDescriptor](class_mip_policydescriptor.md) | 保護されたコンテンツに関連付けられているアドホック ポリシーを表します。
[mip::PolicyEngine](class_mip_policyengine.md) | このクラスは、すべてのエンジン関数のインターフェイスを提供します。
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) | エンジンを開始するには、適切なパラメーターを指定したこのクラスのインスタンスを提供する必要があります。
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md) | 現在のラベルは特権割り当てメソッドによって設定されており、オーバーライドできません。
[mip::Profile](class_mip_profile.md) | Microsoft Information Protection 操作のルート クラス。
[mip::Profile::Observer](class_mip_profile_observer.md) | プロファイル関連のイベント通知の通知を受信するために使用されるインターフェイス。
[mip::Profile::Settings](class_mip_profile_settings.md) | プロファイル設定を構成します。
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md) | アドホック保護をドキュメントに追加することを指定するアクション クラス。  
[mip::ProtectbyTemplateAction](class_mip_protectbytemplateaction.md) | テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md) | 追加によって保護がドキュメントに転送されないことを指定するアクション クラス。
[mip::ProtectionProfile](class_mip_protectionprofile.md) | 保護操作の実行に使用される基底クラス。
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) | 保護プロファイル通知の受信に使用されます。
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) | インスタンスの有効期間全体にわたって使用される保護プロファイル設定。
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md) | ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) | ドキュメントからのコンテンツ ヘッダーの削除を指定するアクション クラス。
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md) | ドキュメントからの保護の削除を指定するアクション クラス。
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md) | ドキュメントからのウォーターマークの削除を指定するアクション クラス。
[mip::RMSCryptographyException](class_mip_rmscryptographyexception.md) | RMS 暗号の例外。
[mip::RMSException](class_mip_rmsexception.md) | ベース RMS の例外。
[mip::RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) | RMS の無効な引数の例外。
[mip::RMSLogicException](class_mip_rmslogicexception.md) | RMS ロジックの例外。
[mip::RMSNetworkException](class_mip_rmsnetworkexception.md) | RMS ネットワークの例外。
[mip::RMSNotFoundException](class_mip_rmsnotfoundexception.md) | RMS が見つからないことを示す例外。
[mip::RMSNullPointerException](class_mip_rmsnullpointerexception.md) | RMS Null ポインターの例外。
[mip::RMSOfficeFileException](class_mip_rmsofficefileexception.md) | RMS Office ファイルの例外。
[mip::RMSPFileException](class_mip_rmspfileexception.md) | RMS PFile の例外。
[mip::RMSRightsException](class_mip_rmsrightsexception.md) | RMS 権限の例外。
[mip::RMSStreamException](class_mip_rmsstreamexception.md) | RMS ストリームの例外。
[mip::Roles](class_mip_roles.md) | データを保護するためのロールを定義します。
[mip::Stream](class_mip_stream.md) | MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
[mip::TemplateDescriptor](class_mip_templatedescriptor.md) | RMS テンプレートについて説明します。
[mip::UserPolicy](class_mip_userpolicy.md) | 保護されたコンテンツに関連付けられているポリシーを表します。
[mip::UserRights](class_mip_userrights.md) | ユーザーのグループおよびそれらに関連付けられている権限を表します。
[mip::UserRoles](class_mip_userroles.md) | ユーザーのグループおよびそれらに関連付けられているロールを表します。
 
