# <a name="class-mipprofileobserver"></a>class mip::Profile::Observer 
クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_profile_observer.md) インターフェイス。
*Error イベントが発生した場合、エラー オブジェクトは内部 [mip::Error](class_mip_error.md) クラスを保持します。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<Profile>& profile, const std::shared_ptr<void>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エラーの原因となったエンジンを一覧表示するときに呼び出されます。
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  エンジンが正常にアンロードされたときに呼び出されます。
public virtual void OnUnloadEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エンジンのアンロードがエラーの原因となったときに呼び出されます。
public virtual void OnAddEngineSuccess(const std::shared_ptr<PolicyEngine>& engine, const std::shared_ptr<void>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  新しいエンジンの追加がエラーの原因となったときに呼び出されます。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  エンジンの削除がエラーの原因となったときに呼び出されます。
 public virtual void OnPolicyChanged(const std::string& engineId)  |  指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess"></a>OnLoadSuccess
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 操作の開始に使用された現在のプロファイル。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onloadfailure"></a>OnLoadFailure
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **error**: 読み込み操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
エンジンの一覧が正常に生成されたときに呼び出されます。

パラメーター:  
* **engineIds**: 使用可能なエンジン ID の一覧。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onlistengineserror"></a>OnListEnginesError
エラーの原因となったエンジンを一覧表示するときに呼び出されます。

パラメーター:  
* **error**: エンジンの一覧操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
エンジンが正常にアンロードされたときに呼び出されます。

パラメーター:  
* **context**: 操作に渡されたコンテキスト。


  
### <a name="onunloadengineerror"></a>OnUnloadEngineError
エンジンのアンロードがエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンのアンロード操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
新しいエンジンが正常に追加されたときに呼び出されます。
  
### <a name="onaddengineerror"></a>OnAddEngineError
新しいエンジンの追加がエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンの追加操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
エンジンが正常に削除されたときに呼び出されます。

パラメーター:  
* **context**: 操作に渡されたコンテキスト。


  
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
エンジンの削除がエラーの原因となったときに呼び出されます。

パラメーター:  
* **error**: エンジンの削除操作が失敗する原因となったエラー。 


* **context**: 操作に渡されたコンテキスト。


  
### <a name="onpolicychanged"></a>OnPolicyChanged
指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。

パラメーター:  
* **engineId**: エンジン 


新しいポリシーを読み込むには、指定されたエンジン ID を使用して AddEngineAsync をもう一度呼び出す必要があります。