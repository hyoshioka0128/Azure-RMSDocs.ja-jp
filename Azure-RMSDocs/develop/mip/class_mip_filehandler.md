# <a name="class-mipfilehandler"></a>class mip::FileHandler 
すべてのファイル処理関数のインターフェイス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  ファイルからの機密ラベルの取得を開始します。
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  ファイルからの保護ポリシーの取得を開始します。
 public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  機密ラベルをファイルに設定します。
 public void DeleteLabel(AssignmentMethod method, const std::string& justificationMessage)  |  ファイルから機密ラベルを削除します。
public void SetCustomPermissions(const std::shared_ptr<PolicyDescriptor>& policyDescriptor)  |  ファイルにカスタムのアクセス許可を設定します。
 public void RemoveProtection()  |  ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | \|outputFilePath\ で指定されたファイルに変更を書き込みます。 |  パラメーターに渡します。
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | \|outputStream\ で指定されたストリームに変更を書き込みます。 |  パラメーターに渡します。
 public std::string GetOutputFileName()  |  元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。
 public virtual ~FileHandler()  | _まだ文書化されていません。_
 protected FileHandler()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="getlabelasync"></a>GetLabelAsync
ファイルからの機密ラベルの取得を開始します。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。

パラメーター:  
* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="getprotectionasync"></a>GetProtectionAsync
ファイルからの保護ポリシーの取得を開始します。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。

パラメーター:  
* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="setlabel"></a>SetLabel
機密ラベルをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
ラベルの設定に理由が必要で、labelingOptions パラメーターを介して理由メッセージが指定されなかった場合は、[JustificationRequiredError](class_mip_justificationrequirederror.md) をスローします。
  
### <a name="deletelabel"></a>DeleteLabel
ファイルから機密ラベルを削除します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privilegd および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に理由が必要で、justificationMessage パラメーターを介して理由メッセージが指定されなかった場合は、[JustificationRequiredError](class_mip_justificationrequirederror.md) をスローします。
  
### <a name="setcustompermissions"></a>SetCustomPermissions
ファイルにカスタムのアクセス許可を設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="removeprotection"></a>RemoveProtection
ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="commitasync"></a>CommitAsync
|outputFilePath| パラメーターで指定されたファイルに変更を書き込みます。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="commitasync"></a>CommitAsync
|outputStream| パラメーターで指定されたストリームに変更を書き込みます。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="getoutputfilename"></a>GetOutputFileName
元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。
  
### <a name="filehandler"></a>~FileHandler
_まだ文書化されていません。_

  
### <a name="filehandler"></a>FileHandler
_まだ文書化されていません。_
