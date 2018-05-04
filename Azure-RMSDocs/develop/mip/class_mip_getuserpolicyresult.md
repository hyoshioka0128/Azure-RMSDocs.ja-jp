# <a name="class-mipgetuserpolicyresult"></a>class mip::GetUserPolicyResult 
ユーザー ポリシーの取得要求の結果について説明します。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public GetUserPolicyResultStatus GetResultStatus | ポリシーの取得要求の状態を取得します。
public std::shared_ptr< std::string > GetReferrer | ポリシーの参照元アドレスを取得します。
public std::shared_ptr< UserPolicy > GetPolicy
## <a name="members"></a>メンバー
### <a name="getuserpolicyresultstatus"></a>GetUserPolicyResultStatus
ポリシーの取得要求の状態を取得します。
#### <a name="returns"></a>戻り値
ポリシーの取得要求の状態
### <a name="getreferrer"></a>GetReferrer
ポリシーの参照元アドレスを取得します。
#### <a name="returns"></a>戻り値
ポリシーの参照元アドレス。参照元は、ポリシーの取得に失敗したときにユーザーに表示できる URI であり、ユーザーがコンテンツへのアクセス許可を取得する方法についての情報を含みます。
### <a name="userpolicy"></a>UserPolicy
[UserPolicy](#classmip_1_1_user_policy) インスタンスを取得します。
#### <a name="returns"></a>戻り値
取得に成功した場合は [UserPolicy](#classmip_1_1_user_policy) インスタンス、それ以外の場合は nullptr