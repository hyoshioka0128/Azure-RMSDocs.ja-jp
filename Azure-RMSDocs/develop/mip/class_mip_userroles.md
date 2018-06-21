# <a name="class-mipuserroles"></a>class mip::UserRoles 
ユーザーのグループおよびそれらに関連付けられているロールを表します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public MIP_EXPORT UserRoles(const UserList& users, const RoleList& roles)  |  [UserRoles](class_mip_userroles.md) コンストラクター。
 public const UserList& Users() const  |  ロールのセットに関連付けられているユーザーを取得します。
 public const RoleList& Roles() const  |  ユーザーのグループに関連付けられているロールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userroles"></a>UserRoles
[UserRoles](class_mip_userroles.md) コンストラクター。

パラメーター:  
* **users**: 同じロールを共有するユーザーのグループ 


* **roles**: ユーザーのグループによって共有されている [Roles](class_mip_roles.md)


  
### <a name="userlist"></a>UserList
ロールのセットに関連付けられているユーザーを取得します。

  
**戻り値**: ロールのセットに関連付けられているユーザー
  
### <a name="rolelist"></a>RoleList
ユーザーのグループに関連付けられているロールを取得します。

  
**戻り値**: ユーザーのグループに関連付けられている [Roles](class_mip_roles.md)