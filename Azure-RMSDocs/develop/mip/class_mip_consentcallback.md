# <a name="class-mipconsentcallback"></a>class mip::ConsentCallback 
同意要求通知のインターフェイス。
このコールバックは、同意通知をユーザーに表示する必要がある場合に、それを認識するためにクライアント アプリケーションによって実装されます。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public ConsentList ConsentsConsentList & consents) | SDK が操作に対するユーザーの同意を必要とする場合に呼び出されます。
## <a name="members"></a>メンバー
### <a name="consentlist"></a>ConsentList
SDK が操作に対するユーザーの同意を必要とする場合に呼び出されます。
#### <a name="parameters"></a>パラメーター
* consents: SDK によって要求された同意の一覧
#### <a name="returns"></a>戻り値
[同意](#classmip_1_1_consent)結果。SDK によって同意が要求された場合、クライアント アプリケーションはユーザーから同意を得る必要があります。各同意の結果は、[Consent::Result(const ConsentResult&)](#classmip_1_1_consent_1ad6c17d9af548a40b2fe854fe0d9bca64) を介して格納するか、解決された同意の一覧を返す必要があります。