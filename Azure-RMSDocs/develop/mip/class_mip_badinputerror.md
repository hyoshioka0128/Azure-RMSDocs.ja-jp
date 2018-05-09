# <a name="class-mipbadinputerror"></a>class mip::BadInputError 
無効な入力エラーです。sdk api への入力が無効でした。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline char const* what() const  |  cstring のエラー メッセージを取得します。
public std::shared_ptr<Error> Clone() const  |  エラーを複製します。
public inline virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
public inline virtual const std::string& GetErrorName() const  |  エラー名を取得します。
public inline virtual const std::string& GetMessage() const  |  エラー メッセージを取得します。
public inline virtual void SetMessage(const std::string& msg)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="what"></a>what
cstring のエラー メッセージを取得します。
  
#### <a name="returns"></a>戻り値
cstring のエラー メッセージ
  
### <a name="error"></a>エラー
エラーを複製します。
  
#### <a name="returns"></a>戻り値
エラーの複製。
  
### <a name="errortype"></a>ErrorType
エラーの種類を取得します。
  
#### <a name="returns"></a>戻り値
エラーの種類。
  
### <a name="geterrorname"></a>GetErrorName
エラー名を取得します。
  
#### <a name="returns"></a>戻り値
エラー名。
  
### <a name="getmessage"></a>GetMessage
エラー メッセージを取得します。
  
#### <a name="returns"></a>戻り値
エラー メッセージ。
  
### <a name="setmessage"></a>SetMessage
エラー メッセージを設定します。
  
#### <a name="parameters"></a>パラメーター
* msg: エラー メッセージ。