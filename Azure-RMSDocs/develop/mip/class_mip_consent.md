# <a name="class-mipconsent"></a>class mip::Consent 
アクションの許可に対するユーザーの同意/拒否を表します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const mip::ConsentResult& Result() const  |  同意要求の結果を取得します。
public void Result(const ConsentResult& value)  |  同意要求の結果を設定します。
public mip::ConsentType Type() const  |  同意の種類を取得します。
public const std::vector<std::string> Urls() const  |  同意要求に関連する URL を取得します。
public const std::string User() const  |  同意が要求されたユーザー (メール アドレス) を取得します。
public const std::string Domain() const  |  同意が要求されたユーザーに関連付けられているドメインを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="mipconsentresult"></a>mip::ConsentResult
同意要求の結果を取得します。
  
#### <a name="returns"></a>戻り値
同意要求の結果
  
### <a name="result"></a>Result
同意要求の結果を設定します。
  
#### <a name="parameters"></a>パラメーター
* value: 同意要求の結果
  
### <a name="mipconsenttype"></a>mip::ConsentType
同意の種類を取得します。
  
#### <a name="returns"></a>戻り値
同意の種類
  
### <a name="urls"></a>Urls
同意要求に関連する URL を取得します。
  
#### <a name="returns"></a>戻り値
同意要求に関連する URL
  
### <a name="user"></a>User
同意が要求されたユーザー (メール アドレス) を取得します。
  
#### <a name="returns"></a>戻り値
同意が要求されたユーザー
  
### <a name="domain"></a>ドメイン
同意が要求されたユーザーに関連付けられているドメインを取得します。
  
#### <a name="returns"></a>戻り値
同意が要求されたユーザーに関連付けられているドメイン