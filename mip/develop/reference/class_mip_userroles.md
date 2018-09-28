# <a name="class-mipuserroles"></a>class mip::UserRoles 
ユーザーのグループおよびそれらに関連付けられているロールを表します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public UserRoles(const std::vector<std::string>& users, const std::vector<std::string>& roles)  |  [UserRoles](class_mip_userroles.md) コンストラクター。
public const std::vector<std::string>& Users() const  |  ロールのセットに関連付けられているユーザーを取得します。
public const std::vector<std::string>& Roles() const  |  ユーザーのグループに関連付けられているロールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userroles"></a>UserRoles
[UserRoles](class_mip_userroles.md) コンストラクター。

パラメーター:  
* **users**: 同じロールを共有するユーザーのグループ 


* **roles**: ユーザーのグループによって共有されているロール


  
### <a name="users"></a>Users
ロールのセットに関連付けられているユーザーを取得します。

  
**戻り値**: ロールのセットに関連付けられているユーザー
  
### <a name="roles"></a>役割
ユーザーのグループに関連付けられているロールを取得します。

  
**戻り値**: ユーザーのグループに関連付けられているロール