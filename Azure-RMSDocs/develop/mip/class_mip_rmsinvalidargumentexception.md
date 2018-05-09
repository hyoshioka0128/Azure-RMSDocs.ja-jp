# <a name="class-miprmsinvalidargumentexception"></a>class mip::RMSInvalidArgumentException 
RMS の無効な引数の例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline RMSInvalidArgumentException(const std::string& message)  |  [RMSInvalidArgumentException](#classmip_1_1_r_m_s_invalid_argument_exception) コンストラクター。
public inline RMSInvalidArgumentException(const char*const& message)  |  [RMSInvalidArgumentException](#classmip_1_1_r_m_s_invalid_argument_exception) コンストラクター。
public inline virtual const char* what() const  |  例外メッセージを取得します。
public inline virtual ExceptionTypes type() const  |  例外の種類を取得します。
public inline virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsinvalidargumentexception"></a>RMSInvalidArgumentException
[RMSInvalidArgumentException](#classmip_1_1_r_m_s_invalid_argument_exception) コンストラクター。
  
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ
  
### <a name="rmsinvalidargumentexception"></a>RMSInvalidArgumentException
[RMSInvalidArgumentException](#classmip_1_1_r_m_s_invalid_argument_exception) コンストラクター。
  
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ
  
### <a name="what"></a>what
例外メッセージを取得します。
  
#### <a name="returns"></a>戻り値
例外メッセージ
  
### <a name="exceptiontypes"></a>ExceptionTypes
例外の種類を取得します。
  
#### <a name="returns"></a>戻り値
例外の種類
  
### <a name="error"></a>エラー
エラー コードを取得します。
  
#### <a name="returns"></a>戻り値
[エラー](#classmip_1_1_error) コード