# <a name="class-miprmsnotfoundexception"></a>class mip::RMSNotFoundException 
RMS が見つからないことを示す例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSNotFoundException(const std::string& message)  |  [RMSNotFoundException](class_mip_rmsnotfoundexception.md) コンストラクター。
 public RMSNotFoundException(const char*const& message)  |  [RMSNotFoundException](class_mip_rmsnotfoundexception.md) コンストラクター。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsnotfoundexception"></a>RMSNotFoundException
[RMSNotFoundException](class_mip_rmsnotfoundexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ


  
### <a name="rmsnotfoundexception"></a>RMSNotFoundException
[RMSNotFoundException](class_mip_rmsnotfoundexception.md) コンストラクター。

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