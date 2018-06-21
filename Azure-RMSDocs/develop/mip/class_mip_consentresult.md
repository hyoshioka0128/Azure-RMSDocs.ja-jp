# <a name="class-mipconsentresult"></a>class mip::ConsentResult 
ユーザー操作の後の同意要求の結果について説明します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public ConsentResult(bool accepted, bool showAgain, const std::string& userId)  |  [ConsentResult](class_mip_consentresult.md) コンストラクター。
 public bool Accepted() const  |  ユーザーがアクションに同意したかどうかを取得します。
 public bool ShowAgain() const  |  今後の要求について明示的な同意が必要かどうかを取得します。
 public const std::string& UserId() const  |  同意が要求されたユーザー (メール アドレス) を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="consentresult"></a>ConsentResult
[ConsentResult](class_mip_consentresult.md) コンストラクター。

パラメーター:  
* **accepted**: ユーザーがアクションに同意したかどうか 


* **showAgain**: 今後のアクション要求について明示的な同意が必要かどうか 


* **userId**: 同意が要求されたユーザー (メール アドレス)


  
### <a name="accepted"></a>Accepted
ユーザーがアクションに同意したかどうかを取得します。

  
**戻り値**: ユーザーがアクションに同意したかどうか
  
### <a name="showagain"></a>ShowAgain
今後の要求について明示的な同意が必要かどうかを取得します。

  
**戻り値**: 今後の要求について明示的な同意が必要かどうか。これが true の場合、SDK はこの同意の結果を記憶し、今後クライアント アプリケーションに同意を要求しません。
  
### <a name="userid"></a>UserId
同意が要求されたユーザー (メール アドレス) を取得します。

  
**戻り値**: 同意が要求されたユーザー