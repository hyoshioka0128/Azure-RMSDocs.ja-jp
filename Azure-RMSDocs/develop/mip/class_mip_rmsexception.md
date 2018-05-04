# <a name="class-miprmsexception"></a>class mip::RMSException 
ベース RMS の例外。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline  RMSExceptionExceptionTypes type,const int error,const std::string & message) public inline  RMSExceptionExceptionTypes type,const int error,const char *const & message) public inline virtual const char * what | 例外メッセージを取得します。
public inline virtual ExceptionTypes type | 例外の種類を取得します。
public inline virtual int error | エラー コードを取得します。
## <a name="members"></a>メンバー
### <a name="rmsexception"></a>RMSException
[RMSException](#classmip_1_1_r_m_s_exception) コンストラクター。
#### <a name="parameters"></a>パラメーター
* type: 例外の種類 
* error: [エラー](#classmip_1_1_error) コード 
* message: 例外メッセージ
### <a name="rmsexception"></a>RMSException
[RMSException](#classmip_1_1_r_m_s_exception) コンストラクター。
#### <a name="parameters"></a>パラメーター
* type: 例外の種類 
* error: [エラー](#classmip_1_1_error) コード 
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