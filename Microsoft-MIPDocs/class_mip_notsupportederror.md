# <a name="class-mipnotsupportederror"></a>class mip::NotSupportedError 
サポートされていない操作のエラー。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline char const  * what | cstring のエラー メッセージを取得します。
public std::shared_ptr< Error > Clone | エラーを複製します。
public inline virtual ErrorType GetErrorType | エラーの種類を取得します。
public inline virtual const std::string & GetErrorName | エラー名を取得します。
public inline virtual const std::string & GetMessage | エラー メッセージを取得します。
public inline virtual void SetMessage | エラー メッセージを設定します。
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