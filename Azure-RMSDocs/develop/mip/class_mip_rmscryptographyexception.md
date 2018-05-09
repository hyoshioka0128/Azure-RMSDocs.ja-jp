# <a name="class-miprmscryptographyexception"></a>class mip::RMSCryptographyException 
RMS 暗号の例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline RMSCryptographyException(const std::string& message)  |  [RMSCryptographyException](#classmip_1_1_r_m_s_cryptography_exception) コンストラクター。
public inline RMSCryptographyException(const char*const& message)  |  [RMSCryptographyException](#classmip_1_1_r_m_s_cryptography_exception) コンストラクター。
public inline virtual const char* what() const  |  例外メッセージを取得します。
public inline virtual ExceptionTypes type() const  |  例外の種類を取得します。
public inline virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmscryptographyexception"></a>RMSCryptographyException
[RMSCryptographyException](#classmip_1_1_r_m_s_cryptography_exception) コンストラクター。
  
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ
  
### <a name="rmscryptographyexception"></a>RMSCryptographyException
[RMSCryptographyException](#classmip_1_1_r_m_s_cryptography_exception) コンストラクター。
  
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