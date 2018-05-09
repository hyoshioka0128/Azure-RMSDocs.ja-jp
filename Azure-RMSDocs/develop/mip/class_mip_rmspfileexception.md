# <a name="class-miprmspfileexception"></a>class mip::RMSPFileException 
RMS PFile の例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline RMSPFileException(const std::string& message, Reason reason)  |  [RMSPFileException](#classmip_1_1_r_m_s_p_file_exception) コンストラクター。
public inline RMSPFileException(const char*const& message, Reason reason)  |  [RMSPFileException](#classmip_1_1_r_m_s_p_file_exception) コンストラクター。
public inline virtual Reason reason() const  |  PFile エラー分類を取得します。
public inline virtual const char* what() const  |  例外メッセージを取得します。
public inline virtual ExceptionTypes type() const  |  例外の種類を取得します。
public inline virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmspfileexception"></a>RMSPFileException
[RMSPFileException](#classmip_1_1_r_m_s_p_file_exception) コンストラクター。
  
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ 
* reason: PFile エラー分類
  
### <a name="rmspfileexception"></a>RMSPFileException
[RMSPFileException](#classmip_1_1_r_m_s_p_file_exception) コンストラクター。
  
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ 
* reason: PFile エラー分類
  
### <a name="reason"></a>理由
PFile エラー分類を取得します。
  
#### <a name="returns"></a>戻り値
PFile エラー分類
  
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