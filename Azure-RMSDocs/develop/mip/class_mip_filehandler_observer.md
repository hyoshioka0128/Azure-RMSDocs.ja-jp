# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
クライアントがファイル ハンドラー関連のイベントに関する通知を取得するための [Observer](#classmip_1_1_file_handler_1_1_observer) インターフェイス。
*Error イベントが発生した場合、エラー オブジェクトは内部 [mip::Error](#classmip_1_1_error) クラスを保持します。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline virtual  ~Observer | 
public void OnGetLabelSuccessContentLabel > & label,const std::shared_ptr< void > & context) | ラベルが (ファイルから) 正常に取得されたときに呼び出されます。
public void OnGetLabelFailure | (ファイルからの) ラベルの取得がエラーにより失敗した場合に呼び出されます。
public void OnGetProtectionSuccessUserPolicy > & userPolicy,const std::shared_ptr< void > & context) | 保護ポリシーが (ファイルから) 正常に取得されたときに呼び出されます。
public void OnGetProtectionFailure | (ファイルからの) 保護ポリシーの取得がエラーにより失敗したア場合に呼び出されます。
public void OnCommitSuccess | ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
public void OnCommitFailure | ファイルに対する変更のコミットがエラーにより失敗した場合に呼び出されます。
protected inline  Observer | 
## <a name="members"></a>メンバー
### <a name="observer"></a>~Observer
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
ラベルが (ファイルから) 正常に取得されたときに呼び出されます。
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
(ファイルからの) ラベルの取得がエラーにより失敗した場合に呼び出されます。
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
保護ポリシーが (ファイルから) 正常に取得されたときに呼び出されます。
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
(ファイルからの) 保護ポリシーの取得がエラーにより失敗したア場合に呼び出されます。
### <a name="oncommitsuccess"></a>OnCommitSuccess
ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
### <a name="oncommitfailure"></a>OnCommitFailure
ファイルに対する変更のコミットがエラーにより失敗した場合に呼び出されます。
### <a name="observer"></a>オブザーバー