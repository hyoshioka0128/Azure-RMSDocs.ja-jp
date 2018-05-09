# <a name="class-miprmsnotfoundexception"></a>class mip::RMSNotFoundException 
RMS が見つからないことを示す例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline RMSNotFoundException(const std::string& message)  |  [RMSNotFoundException](#classmip_1_1_r_m_s_not_found_exception) コンストラクター。
public inline RMSNotFoundException(const char*const& message)  |  [RMSNotFoundException](#classmip_1_1_r_m_s_not_found_exception) コンストラクター。
public inline virtual const char* what() const  |  例外メッセージを取得します。
public inline virtual ExceptionTypes type() const  |  例外の種類を取得します。
public inline virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsnotfoundexception"></a>RMSNotFoundException
[RMSNotFoundException](#classmip_1_1_r_m_s_not_found_exception) コンストラクター。
  
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ
  
### <a name="rmsnotfoundexception"></a>RMSNotFoundException
[RMSNotFoundException](#classmip_1_1_r_m_s_not_found_exception) コンストラクター。
  
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