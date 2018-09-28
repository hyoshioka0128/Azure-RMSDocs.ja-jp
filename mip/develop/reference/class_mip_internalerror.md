# <a name="class-mipinternalerror"></a>class mip::InternalError 
内部エラー。 このエラーは、実行中に予期しない事態が発生するとスローされます。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public char const* what() const  |  cstring のエラー メッセージを取得します。
public std::shared_ptr<Error> Clone() const  |  エラーを複製します。
 public virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
 public virtual const std::string& GetErrorName() const  |  エラー名を取得します。
 public virtual const std::string& GetMessage() const  |  エラー メッセージを取得します。
 public virtual void SetMessage(const std::string& msg)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="what"></a>what
cstring のエラー メッセージを取得します。

  
**戻り値**: cstring のエラー メッセージ
  
### <a name="error"></a>エラー
エラーを複製します。

  
**戻り値**: エラーの複製。
  
### <a name="errortype"></a>ErrorType
エラーの種類を取得します。

  
**戻り値**: エラーの種類。
  
### <a name="geterrorname"></a>GetErrorName
エラー名を取得します。

  
**戻り値**: エラー名。
  
### <a name="getmessage"></a>GetMessage
エラー メッセージを取得します。

  
**戻り値**: エラー メッセージ。
  
### <a name="setmessage"></a>SetMessage
エラー メッセージを設定します。

パラメーター:  
* **msg**: エラー メッセージ。

