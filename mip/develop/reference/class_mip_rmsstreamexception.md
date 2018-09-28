# <a name="class-miprmsstreamexception"></a>class mip::RMSStreamException 
RMS ストリームの例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSStreamException(const std::string& message)  |  [RMSStreamException](class_mip_rmsstreamexception.md) コンストラクター。
 public RMSStreamException(const char*const& message)  |  [RMSStreamException](class_mip_rmsstreamexception.md) コンストラクター。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsstreamexception"></a>RMSStreamException
[RMSStreamException](class_mip_rmsstreamexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ


  
### <a name="rmsstreamexception"></a>RMSStreamException
[RMSStreamException](class_mip_rmsstreamexception.md) コンストラクター。

パラメーター:  
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