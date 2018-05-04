# <a name="class-mipuserroles"></a>class mip::UserRoles 
ユーザーのグループおよびそれらに関連付けられているロールを表します。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public MIP_EXPORT UserRolesUserList & users,const RoleList & roles) public inline const UserList & Users | ロールのセットに関連付けられているユーザーを取得します。
public inline const RoleList & Roles | ユーザーのグループに関連付けられているロールを取得します。
## <a name="members"></a>メンバー
### <a name="userroles"></a>UserRoles
[UserRoles](#classmip_1_1_user_roles) コンストラクター。
#### <a name="parameters"></a>パラメーター
* users: 同じロールを共有するユーザーのグループ 
* roles: ユーザーのグループによって共有されている[ロール](#classmip_1_1_roles)
### <a name="userlist"></a>UserList
ロールのセットに関連付けられているユーザーを取得します。
#### <a name="returns"></a>戻り値
ロールのセットに関連付けられているユーザー
### <a name="rolelist"></a>RoleList
ユーザーのグループに関連付けられているロールを取得します。
#### <a name="returns"></a>戻り値
ユーザーのグループに関連付けられている[ロール](#classmip_1_1_roles)