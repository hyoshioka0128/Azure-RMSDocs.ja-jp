# <a name="class-miprmsexception"></a>class mip::RMSException 
ベース RMS の例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSException(const ExceptionTypes type, const int error, const std::string& message)  |  [RMSException](class_mip_rmsexception.md) コンストラクター。
 public RMSException(const ExceptionTypes type, const int error, const char*const& message)  |  [RMSException](class_mip_rmsexception.md) コンストラクター。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsexception"></a>RMSException
[RMSException](class_mip_rmsexception.md) コンストラクター。

パラメーター:  
* **type**: 例外の種類 


* **error**: [エラー](class_mip_error.md) コード 


* **message**: 例外メッセージ


  
### <a name="rmsexception"></a>RMSException
[RMSException](class_mip_rmsexception.md) コンストラクター。

パラメーター:  
* **type**: 例外の種類 


* **error**: [エラー](class_mip_error.md) コード 


* **message**: 例外メッセージ


  
### <a name="what"></a>what
例外メッセージを取得します。

  
**戻り値**: 例外メッセージ
  
### <a name="exceptiontypes"></a>ExceptionTypes
例外の種類を取得します。

  
**戻り値**: 例外の種類
  
### <a name="error"></a>エラー
エラー コードを取得します。

  
**戻り値**: [エラー](class_mip_error.md) コード