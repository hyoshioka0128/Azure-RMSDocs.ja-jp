# <a name="class-miprmslogicexception"></a>class mip::RMSLogicException 
RMS ロジックの例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline RMSLogicException(const ErrorTypes error, const std::string& message)  |  [RMSLogicException](#classmip_1_1_r_m_s_logic_exception) コンストラクター。
public inline RMSLogicException(const ErrorTypes error, const char*const& message)  |  [RMSLogicException](#classmip_1_1_r_m_s_logic_exception) コンストラクター。
public inline virtual const char* what() const  |  例外メッセージを取得します。
public inline virtual ExceptionTypes type() const  |  例外の種類を取得します。
public inline virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmslogicexception"></a>RMSLogicException
[RMSLogicException](#classmip_1_1_r_m_s_logic_exception) コンストラクター。
  
#### <a name="parameters"></a>パラメーター
* error: [エラー](#classmip_1_1_error) コード 
* message: 例外メッセージ
  
### <a name="rmslogicexception"></a>RMSLogicException
[RMSLogicException](#classmip_1_1_r_m_s_logic_exception) コンストラクター。
  
#### <a name="parameters"></a>パラメーター
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