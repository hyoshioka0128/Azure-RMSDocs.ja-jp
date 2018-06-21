# <a name="class-miprmsnullpointerexception"></a>class mip::RMSNullPointerException 
RMS Null ポインターの例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSNullPointerException(const std::string& message)  |  [RMSNullPointerException](class_mip_rmsnullpointerexception.md) コンストラクター。
 public RMSNullPointerException(const char*const& message)  |  [RMSNullPointerException](class_mip_rmsnullpointerexception.md) コンストラクター。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsnullpointerexception"></a>RMSNullPointerException
[RMSNullPointerException](class_mip_rmsnullpointerexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ


  
### <a name="rmsnullpointerexception"></a>RMSNullPointerException
[RMSNullPointerException](class_mip_rmsnullpointerexception.md) コンストラクター。

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