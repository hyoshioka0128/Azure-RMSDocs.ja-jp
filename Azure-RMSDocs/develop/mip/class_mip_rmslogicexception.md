# <a name="class-miprmslogicexception"></a>class mip::RMSLogicException 
RMS ロジックの例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSLogicException(const ErrorTypes error, const std::string& message)  |  [RMSLogicException](class_mip_rmslogicexception.md) コンストラクター。
 public RMSLogicException(const ErrorTypes error, const char*const& message)  |  [RMSLogicException](class_mip_rmslogicexception.md) コンストラクター。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmslogicexception"></a>RMSLogicException
[RMSLogicException](class_mip_rmslogicexception.md) コンストラクター。

パラメーター:  
* **error**: [エラー](class_mip_error.md) コード 


* **message**: 例外メッセージ


  
### <a name="rmslogicexception"></a>RMSLogicException
[RMSLogicException](class_mip_rmslogicexception.md) コンストラクター。

パラメーター:  
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