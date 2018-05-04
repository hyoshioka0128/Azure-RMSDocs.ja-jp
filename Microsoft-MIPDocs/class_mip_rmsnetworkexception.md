# <a name="class-miprmsnetworkexception"></a>class mip::RMSNetworkException 
RMS ネットワークの例外。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline  RMSNetworkExceptionReason reason) public inline  RMSNetworkExceptionReason reason) public inline virtual Reason reason | ネットワーク エラー分類を取得します。
public inline virtual const char * what | 例外メッセージを取得します。
public inline virtual ExceptionTypes type | 例外の種類を取得します。
public inline virtual int error | エラー コードを取得します。
## <a name="members"></a>メンバー
### <a name="rmsnetworkexception"></a>RMSNetworkException
[RMSNetworkException](#classmip_1_1_r_m_s_network_exception) コンストラクター。
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ 
* reason: ネットワーク エラー分類
### <a name="rmsnetworkexception"></a>RMSNetworkException
[RMSNetworkException](#classmip_1_1_r_m_s_network_exception) コンストラクター。
#### <a name="parameters"></a>パラメーター
* message: 例外メッセージ 
* reason: ネットワーク エラー分類
### <a name="reason"></a>理由
ネットワーク エラー分類を取得します。
#### <a name="returns"></a>戻り値
ネットワーク エラー分類
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