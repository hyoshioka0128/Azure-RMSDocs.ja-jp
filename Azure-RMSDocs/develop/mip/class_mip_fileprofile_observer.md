# <a name="class-mipfileprofileobserver"></a>class mip::FileProfile::Observer 
クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](#classmip_1_1_file_profile_1_1_observer) インターフェイス。
*Error イベントが発生した場合、エラー オブジェクトは内部 [mip::Error](#classmip_1_1_error) クラスを保持します。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline virtual ~Observer()  |  
public inline virtual void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public inline virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public inline virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public inline virtual void OnListEnginesError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エラーの原因となったエンジンを一覧表示するときに呼び出されます。
public inline virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  エンジンが正常にアンロードされたときに呼び出されます。
public inline virtual void OnUnloadEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エンジンのアンロードがエラーの原因となったときに呼び出されます。
public inline virtual void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public inline virtual void OnAddEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  新しいエンジンの追加がエラーの原因となったときに呼び出されます。
public inline virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public inline virtual void OnDeleteEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エンジンの削除がエラーの原因となったときに呼び出されます。
public inline virtual void OnPolicyChanged(const std::string& engineId)  |  指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。
protected inline Observer()  |  
  
## <a name="members"></a>メンバー
  
### <a name="observer"></a>~Observer
  
### <a name="onloadsuccess"></a>OnLoadSuccess
プロファイルが正常に読み込まれたときに呼び出されます。
  
### <a name="onloadfailure"></a>OnLoadFailure
プロファイルの読み込みでエラーが発生したときに呼び出されます。
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
エンジンの一覧が正常に生成されたときに呼び出されます。
  
### <a name="onlistengineserror"></a>OnListEnginesError
エラーの原因となったエンジンを一覧表示するときに呼び出されます。
  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
エンジンが正常にアンロードされたときに呼び出されます。
  
### <a name="onunloadengineerror"></a>OnUnloadEngineError
エンジンのアンロードがエラーの原因となったときに呼び出されます。
  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
新しいエンジンが正常に追加されたときに呼び出されます。
  
### <a name="onaddengineerror"></a>OnAddEngineError
新しいエンジンの追加がエラーの原因となったときに呼び出されます。
  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
エンジンが正常に削除されたときに呼び出されます。
  
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
エンジンの削除がエラーの原因となったときに呼び出されます。
  
### <a name="onpolicychanged"></a>OnPolicyChanged
指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。
  
### <a name="observer"></a>オブザーバー