# <a name="class-mipprofileobserver"></a>class mip::Profile::Observer 
クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](#classmip_1_1_profile_1_1_observer) インターフェイス。
*Error イベントが発生した場合、エラー オブジェクトは内部 [mip::Error](#classmip_1_1_error) クラスを保持します。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccessProfile > & profile,const std::shared_ptr< void > & context) | プロファイルが正常に読み込まれたときに呼び出されます。
public inline virtual void OnLoadFailure | プロファイルの読み込みでエラーが発生したときに呼び出されます。
public inline virtual void OnListEnginesSuccess | エンジンの一覧が正常に生成されたときに呼び出されます。
public inline virtual void OnListEnginesError | エラーの原因となったエンジンを一覧表示するときに呼び出されます。
public inline virtual void OnUnloadEngineSuccess | エンジンが正常にアンロードされたときに呼び出されます。
public inline virtual void OnUnloadEngineError | エンジンのアンロードがエラーの原因となったときに呼び出されます。
public inline virtual void OnAddEngineSuccessPolicyEngine > & engine,const std::shared_ptr< void > & context) | 新しいエンジンが正常に追加されたときに呼び出されます。
public inline virtual void OnAddEngineError | 新しいエンジンの追加がエラーの原因となったときに呼び出されます。
public inline virtual void OnDeleteEngineSuccess | エンジンが正常に削除されたときに呼び出されます。
public inline virtual void OnDeleteEngineError | エンジンの削除がエラーの原因となったときに呼び出されます。
public inline virtual void OnPolicyChanged | 指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。
## <a name="members"></a>メンバー
### <a name="onloadsuccess"></a>OnLoadSuccess
プロファイルが正常に読み込まれたときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* profile: 操作の開始に使用された現在のプロファイル。 
* context: 操作に渡されたコンテキスト。
### <a name="onloadfailure"></a>OnLoadFailure
プロファイルの読み込みでエラーが発生したときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* error: 読み込み操作が失敗する原因となったエラー。 
* context: 操作に渡されたコンテキスト。
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
エンジンの一覧が正常に生成されたときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* engineIds: 使用可能なエンジン ID の一覧。 
* context: 操作に渡されたコンテキスト。
### <a name="onlistengineserror"></a>OnListEnginesError
エラーの原因となったエンジンを一覧表示するときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* error: エンジンの一覧操作が失敗する原因となったエラー。 
* context: 操作に渡されたコンテキスト。
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
エンジンが正常にアンロードされたときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* context: 操作に渡されたコンテキスト。
### <a name="onunloadengineerror"></a>OnUnloadEngineError
エンジンのアンロードがエラーの原因となったときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* error: エンジンのアンロード操作が失敗する原因となったエラー。 
* context: 操作に渡されたコンテキスト。
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
新しいエンジンが正常に追加されたときに呼び出されます。
### <a name="onaddengineerror"></a>OnAddEngineError
新しいエンジンの追加がエラーの原因となったときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* error: エンジンの追加操作が失敗する原因となったエラー。 
* context: 操作に渡されたコンテキスト。
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
エンジンが正常に削除されたときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* context: 操作に渡されたコンテキスト。
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
エンジンの削除がエラーの原因となったときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* error: エンジンの削除操作が失敗する原因となったエラー。 
* context: 操作に渡されたコンテキスト。
### <a name="onpolicychanged"></a>OnPolicyChanged
指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。
#### <a name="parameters"></a>パラメーター
* engineId: エンジン。新しいポリシーを読み込むには、指定されたエンジン ID を使用して AddEngineAsync をもう一度呼び出す必要があります。