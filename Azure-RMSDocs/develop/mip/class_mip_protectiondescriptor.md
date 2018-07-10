# <a name="class-mipprotectiondescriptor"></a>class mip::ProtectionDescriptor 
保護されたコンテンツに関連付けられているアドホック ポリシーを表します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public ProtectionType GetProtectionType() const  |  保護の種類を (保護 SDK テンプレートが基になっているかどうかに関係なく) 取得します。
 public const std::string& GetName() const  |  ポリシー名を取得します。
 public const std::string& GetDescription() const  |  ポリシーの説明を取得します。
 public const std::string& GetTemplateId() const  |  保護テンプレート ID を取得します。
public const std::vector<UserRights>& GetUserRights() const  |  ユーザーから権限へのマッピングのコレクションを取得します。
public const std::vector<UserRoles>& GetUserRoles() const  |  ユーザーからロールへのマッピングのコレクションを取得します。
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil() const  |  ポリシーの有効期限を取得します。
 public bool DoesAllowOfflineAccess() const  |  ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを取得します。
 public const std::string& GetReferrer() const  |  ポリシーの参照元のアドレスを取得します。
public const std::map<std::string, std::string>& GetEncryptedAppData() const  |  暗号化されたアプリ固有のデータを取得します。
public const std::map<std::string, std::string>& GetSignedAppData() const  |  署名されたアプリ固有のデータを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="protectiontype"></a>ProtectionType
保護の種類を (保護 SDK テンプレートが基になっているかどうかに関係なく) 取得します。

  
**戻り値**: 保護の種類
  
### <a name="getname"></a>GetName
ポリシー名を取得します。

  
**戻り値**: ポリシー名
  
### <a name="getdescription"></a>GetDescription
ポリシーの説明を取得します。

  
**戻り値**: ポリシーの説明
  
### <a name="gettemplateid"></a>GetTemplateId
保護テンプレート ID を取得します。

  
**戻り値**: テンプレート ID
  
### <a name="userrights"></a>UserRights
ユーザーから権限へのマッピングのコレクションを取得します。

  
**戻り値**: ユーザーから権限へのマッピングのコレクション。現在のユーザーがユーザー権限情報へのアクセス権を持っていない (つまり、所有者ではなく VIEWRIGHTSDATA 権限がない) 場合、[UserRights](class_mip_userrights.md) プロパティの値は空になります。
  
### <a name="userroles"></a>UserRoles
ユーザーからロールへのマッピングのコレクションを取得します。

  
**戻り値**: ユーザーからロールへのマッピングのコレクション
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
ポリシーの有効期限を取得します。

  
**戻り値**: ポリシーの有効期限
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを取得します。

  
**戻り値**: ポリシーがオフライン コンテンツへのアクセスを許可するかどうか (既定値 = true)
  
### <a name="getreferrer"></a>GetReferrer
ポリシーの参照元のアドレスを取得します。

  
**戻り値**: ポリシーの参照元アドレス。参照元は、ポリシーの取得に失敗したときにユーザーに表示できる URI であり、ユーザーがコンテンツへのアクセス許可を取得する方法についての情報を含みます。
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
暗号化されたアプリ固有のデータを取得します。

  
**戻り値**: アプリ固有のデータ。[ProtectionHandler](class_mip_protectionhandler.md) には、保護サービスによって暗号化されたアプリ固有のデータのディクショナリが含まれる場合があります。この暗号化データは、[ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata) 経由でアクセスできる署名済みデータに依存しません
  
### <a name="getsignedappdata"></a>GetSignedAppData
署名されたアプリ固有のデータを取得します。

  
**戻り値**: アプリ固有のデータ。[ProtectionHandler](class_mip_protectionhandler.md) には、保護サービスが署名したアプリ固有のデータのディクショナリが含まれる場合があります。 この署名済みデータは、[ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata) 経由でアクセスできる暗号化データに依存しません