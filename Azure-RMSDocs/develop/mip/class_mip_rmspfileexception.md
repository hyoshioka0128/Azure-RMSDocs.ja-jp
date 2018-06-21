# <a name="class-miprmspfileexception"></a>class mip::RMSPFileException 
RMS PFile の例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSPFileException(const std::string& message, Reason reason)  |  [RMSPFileException](class_mip_rmspfileexception.md) コンストラクター。
 public RMSPFileException(const char*const& message, Reason reason)  |  [RMSPFileException](class_mip_rmspfileexception.md) コンストラクター。
 public virtual Reason reason() const  |  PFile エラー分類を取得します。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmspfileexception"></a>RMSPFileException
[RMSPFileException](class_mip_rmspfileexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ 


* **reason**: PFile エラー分類


  
### <a name="rmspfileexception"></a>RMSPFileException
[RMSPFileException](class_mip_rmspfileexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ 


* **reason**: PFile エラー分類


  
### <a name="reason"></a>理由
PFile エラー分類を取得します。

  
**戻り値**: PFile エラー分類
  
### <a name="what"></a>what
例外メッセージを取得します。

  
**戻り値**: 例外メッセージ
  
### <a name="exceptiontypes"></a>ExceptionTypes
例外の種類を取得します。

  
**戻り値**: 例外の種類
  
### <a name="error"></a>エラー
エラー コードを取得します。

  
**戻り値**: [エラー](class_mip_error.md) コード