# <a name="class-miprmsofficefileexception"></a>class mip::RMSOfficeFileException 
RMS Office ファイルの例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSOfficeFileException(const std::string& message, Reason reason)  |  [RMSOfficeFileException](class_mip_rmsofficefileexception.md) コンストラクター。
 public RMSOfficeFileException(const char*const& message, Reason reason)  |  [RMSOfficeFileException](class_mip_rmsofficefileexception.md) コンストラクター。
 public virtual Reason reason() const  |  Office ファイル エラー分類を取得します。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
[RMSOfficeFileException](class_mip_rmsofficefileexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ 


* **reason**: Office ファイル エラー分類


  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
[RMSOfficeFileException](class_mip_rmsofficefileexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ 


* **reason**: Office ファイル エラー分類


  
### <a name="reason"></a>理由
Office ファイル エラー分類を取得します。

  
**戻り値**: Office ファイル エラー分類
  
### <a name="what"></a>what
例外メッセージを取得します。

  
**戻り値**: 例外メッセージ
  
### <a name="exceptiontypes"></a>ExceptionTypes
例外の種類を取得します。

  
**戻り値**: 例外の種類
  
### <a name="error"></a>エラー
エラー コードを取得します。

  
**戻り値**: [エラー](class_mip_error.md) コード