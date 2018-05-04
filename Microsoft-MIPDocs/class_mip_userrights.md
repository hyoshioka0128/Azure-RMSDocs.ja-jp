# <a name="class-mipuserrights"></a>class mip::UserRights 
ユーザーのグループおよびそれらに関連付けられている権限を表します。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline  UserRightsUserList & users,const RightList & rights) public inline const UserList & Users | 権限のセットに関連付けられているユーザーを取得します。
public inline const RightList & Rights | ユーザーのグループに関連付けられている権限を取得します。
## <a name="members"></a>メンバー
### <a name="userrights"></a>UserRights
[UserRights](#classmip_1_1_user_rights) コンストラクター。
#### <a name="parameters"></a>パラメーター
* users: 同じ権限を共有するユーザーのグループ 
* rights: ユーザーのグループによって共有されている権限
### <a name="userlist"></a>UserList
権限のセットに関連付けられているユーザーを取得します。
#### <a name="returns"></a>戻り値
権限のセットに関連付けられているユーザー
### <a name="rightlist"></a>RightList
ユーザーのグループに関連付けられている権限を取得します。
#### <a name="returns"></a>戻り値
ユーザーのグループに関連付けられている権限