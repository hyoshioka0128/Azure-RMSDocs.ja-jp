# <a name="class-miprmsrightsexception"></a>class mip::RMSRightsException 
RMS 権限の例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSRightsException(const std::string& message)  |  [RMSRightsException](class_mip_rmsrightsexception.md) コンストラクター。
 public RMSRightsException(const char*const& message)  |  [RMSRightsException](class_mip_rmsrightsexception.md) コンストラクター。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsrightsexception"></a>RMSRightsException
[RMSRightsException](class_mip_rmsrightsexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ


  
### <a name="rmsrightsexception"></a>RMSRightsException
[RMSRightsException](class_mip_rmsrightsexception.md) コンストラクター。

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