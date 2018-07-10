# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
クライアントがファイル ハンドラー関連のイベントに関する通知を取得するための [Observer](class_mip_filehandler_observer.md) インターフェイス。
*Error イベントが発生した場合、エラー オブジェクトは内部 [mip::Error](class_mip_error.md) クラスを保持します。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public virtual ~Observer()  | _まだ文書化されていません。_
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr<FileHandler>& fileHandler, const std::shared_ptr<void>& context)  |  ハンドラーが正しく作成されると呼び出されます。
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  ハンドラーの作成がエラーによって失敗すると呼び出されます。
public virtual void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  ラベルが (ファイルから) 正常に取得されたときに呼び出されます。
public virtual void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  (ファイルからの) ラベルの取得がエラーにより失敗した場合に呼び出されます。
public virtual void OnGetProtectionSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  保護ポリシーが (ファイルから) 正常に取得されたときに呼び出されます。
public virtual void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  (ファイルからの) 保護ポリシーの取得がエラーにより失敗したア場合に呼び出されます。
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context)  |  ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  ファイルに対する変更のコミットがエラーにより失敗した場合に呼び出されます。
 protected Observer()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="observer"></a>~Observer
_まだ文書化されていません。_

  
### <a name="oncreatefilehandlersuccess"></a>OnCreateFileHandlerSuccess
ハンドラーが正しく作成されると呼び出されます。
  
### <a name="oncreatefilehandlerfailure"></a>OnCreateFileHandlerFailure
ハンドラーの作成がエラーによって失敗すると呼び出されます。
  
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
_まだ文書化されていません。_
