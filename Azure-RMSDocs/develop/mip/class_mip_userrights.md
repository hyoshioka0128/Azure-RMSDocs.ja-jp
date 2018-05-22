# <a name="class-mipuserrights"></a>class mip::UserRights 
ユーザーのグループおよびそれらに関連付けられている権限を表します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public UserRights(const UserList& users, const RightList& rights)  |  [UserRights](class_mip_userrights.md) コンストラクター。
 public const UserList& Users() const  |  権限のセットに関連付けられているユーザーを取得します。
 public const RightList& Rights() const  |  ユーザーのグループに関連付けられている権限を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userrights"></a>UserRights
[UserRights](class_mip_userrights.md) コンストラクター。

パラメーター:  
* **users**: 同じ権限を共有するユーザーのグループ 


* **rights**: ユーザーのグループによって共有されている権限


  
### <a name="userlist"></a>UserList
権限のセットに関連付けられているユーザーを取得します。

  
**戻り値**: 権限のセットに関連付けられているユーザー
  
### <a name="rightlist"></a>RightList
ユーザーのグループに関連付けられている権限を取得します。

  
**戻り値**: ユーザーのグループに関連付けられている権限