# <a name="class-miprmsnetworkexception"></a>class mip::RMSNetworkException 
RMS ネットワークの例外。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public RMSNetworkException(const std::string& message, Reason reason)  |  [RMSNetworkException](class_mip_rmsnetworkexception.md) コンストラクター。
 public RMSNetworkException(const char*const& message, Reason reason)  |  [RMSNetworkException](class_mip_rmsnetworkexception.md) コンストラクター。
 public virtual Reason reason() const  |  ネットワーク エラー分類を取得します。
 public virtual const char* what() const  |  例外メッセージを取得します。
 public virtual ExceptionTypes type() const  |  例外の種類を取得します。
 public virtual int error() const  |  エラー コードを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="rmsnetworkexception"></a>RMSNetworkException
[RMSNetworkException](class_mip_rmsnetworkexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ 


* **reason**: ネットワーク エラー分類


  
### <a name="rmsnetworkexception"></a>RMSNetworkException
[RMSNetworkException](class_mip_rmsnetworkexception.md) コンストラクター。

パラメーター:  
* **message**: 例外メッセージ 


* **reason**: ネットワーク エラー分類


  
### <a name="reason"></a>理由
ネットワーク エラー分類を取得します。

  
**戻り値**: ネットワーク エラー分類
  
### <a name="what"></a>what
例外メッセージを取得します。

  
**戻り値**: 例外メッセージ
  
### <a name="exceptiontypes"></a>ExceptionTypes
例外の種類を取得します。

  
**戻り値**: 例外の種類
  
### <a name="error"></a>エラー
エラー コードを取得します。

  
**戻り値**: [エラー](class_mip_error.md) コード