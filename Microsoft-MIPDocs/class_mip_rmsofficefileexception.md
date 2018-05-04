# <a name="class-miprmsofficefileexception"></a>class mip::RMSOfficeFileException 
RMS Office ファイルの例外。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline  RMSOfficeFileExceptionReason reason) public inline  RMSOfficeFileExceptionReason reason) public inline virtual Reason reason | Office ファイルのエラー分類を取得します。
public inline virtual const char * what | 例外メッセージを取得します。
public inline virtual ExceptionTypes type | 例外の種類を取得します。
public inline virtual int error | エラー コードを取得します。
## <a name="members"></a>メンバー
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
[RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception) コンストラクター。
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ 
* reason: Office ファイル エラー分類
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
[RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception) コンストラクター。
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ 
* reason: Office ファイル エラー分類
### <a name="reason"></a>理由
Office ファイル エラー分類を取得します。
#### <a name="returns"></a>戻り値
Office ファイル エラー分類
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