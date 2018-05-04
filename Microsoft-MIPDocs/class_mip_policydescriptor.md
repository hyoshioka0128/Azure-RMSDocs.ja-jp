# <a name="class-mippolicydescriptor"></a>class mip::PolicyDescriptor 
保護されたコンテンツに関連付けられているアドホック ポリシーを表します。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string & GetName | ポリシー名を取得します。
public void SetName | ポリシー名を設定します。
public const std::string & GetDescription | ポリシーの説明を取得します。
public void SetDescription | ポリシーの説明を設定します。
public const std::vector< UserRights > & GetUserRightsList | ユーザーから権限へのマッピングのコレクションを取得します。
public const std::vector< mip::UserRoles > & GetUserRolesList | ユーザーからロールへのマッピングのコレクションを取得します。
public const std::chrono::time_point< std::chrono::system_clock > & GetContentValidUntil | ポリシーの有効期限を取得します。
public void SetContentValidUntil | ポリシーの有効期限を設定します。
public bool DoesAllowOfflineAccess | ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを取得します。
public void SetAllowOfflineAccess | ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。
public const std::string & GetReferrer | ポリシーの参照元のアドレスを取得します。
public void SetReferrer | ポリシーの参照元のアドレスを設定します。
public const AppDataHashMap & GetEncryptedAppData | 暗号化されたアプリ固有のデータを取得します。
public void SetEncryptedAppDataAppDataHashMap & value) | 暗号化する必要のあるアプリ固有のデータを設定します。
public const AppDataHashMap & GetSignedAppData | 署名されたアプリ固有のデータを取得します。
public void SetSignedAppDataAppDataHashMap & value) | 署名する必要があるアプリ固有のデータを設定します。
## <a name="members"></a>メンバー
### <a name="getname"></a>GetName
ポリシー名を取得します。
#### <a name="returns"></a>戻り値
ポリシー名
### <a name="setname"></a>SetName
ポリシー名を設定します。
#### <a name="parameters"></a>パラメーター
* value: ポリシー名
### <a name="getdescription"></a>GetDescription
ポリシーの説明を取得します。
#### <a name="returns"></a>戻り値
ポリシーの説明
### <a name="setdescription"></a>SetDescription
ポリシーの説明を設定します。
#### <a name="parameters"></a>パラメーター
* value: ポリシーの説明
### <a name="userrights"></a>UserRights
ユーザーから権限へのマッピングのコレクションを取得します。
#### <a name="returns"></a>戻り値
ユーザーから権限へのマッピングのコレクション。現在のユーザーがユーザー権限情報へのアクセス権を持っていない (つまり、所有者ではなく VIEWRIGHTSDATA 権限がない) 場合、UserRightsList プロパティの値は空になります。
### <a name="mipuserroles"></a>mip::UserRoles
ユーザーからロールへのマッピングのコレクションを取得します。
#### <a name="returns"></a>戻り値
ユーザーからロールへのマッピングのコレクション
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
ポリシーの有効期限を取得します。
#### <a name="returns"></a>戻り値
ポリシーの有効期限
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
ポリシーの有効期限を設定します。
#### <a name="parameters"></a>パラメーター
* value: ポリシーの有効期限
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを取得します。
#### <a name="returns"></a>戻り値
ポリシーがオフライン コンテンツへのアクセスを許可するかどうか (既定値 = true)
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。
#### <a name="parameters"></a>パラメーター
* value: ポリシーがオフライン コンテンツへのアクセスを許可するかどうか
### <a name="getreferrer"></a>GetReferrer
ポリシーの参照元のアドレスを取得します。
#### <a name="returns"></a>戻り値
ポリシーの参照元アドレス。参照元は、ポリシーの取得に失敗したときにユーザーに表示できる URI であり、ユーザーがコンテンツへのアクセス許可を取得する方法についての情報を含みます。
### <a name="setreferrer"></a>SetReferrer
ポリシーの参照元のアドレスを設定します。
#### <a name="parameters"></a>パラメーター
* uri: ポリシーの参照元アドレス。参照元は、ポリシーの取得に失敗したときにユーザーに表示できる URI であり、ユーザーがコンテンツへのアクセス許可を取得する方法についての情報を含みます。
### <a name="appdatahashmap"></a>AppDataHashMap
暗号化されたアプリ固有のデータを取得します。
#### <a name="returns"></a>戻り値
アプリ固有のデータ。[UserPolicy](#classmip_1_1_user_policy) には、RMS サービスによって暗号化されたアプリ固有のデータのディクショナリが含まれる場合があります。 この暗号化データは、[PolicyDescriptor::GetSignedAppData](#classmip_1_1_policy_descriptor_1ad523870efc92f9f81c82121a054d74d4) を使用してアクセスできる署名済みデータに依存しません
### <a name="setencryptedappdata"></a>SetEncryptedAppData
暗号化する必要のあるアプリ固有のデータを設定します。
#### <a name="parameters"></a>パラメーター
* value: アプリ固有のデータ。アプリケーションでは、RMS サービスによって暗号化されるアプリ固有のデータのディクショナリを指定できます。 この暗号化データは、[PolicyDescriptor::GetSignedAppData](#classmip_1_1_policy_descriptor_1a00f35c0b91e48ccdcc6387466a61f362) によって設定される署名済みデータに依存しません。
### <a name="appdatahashmap"></a>AppDataHashMap
署名されたアプリ固有のデータを取得します。
#### <a name="returns"></a>戻り値
アプリ固有のデータ。[UserPolicy](#classmip_1_1_user_policy) には、RMS サービスによって署名されたアプリ固有のデータのディクショナリが含まれる場合があります。 この署名済みデータは、[PolicyDescriptor::GetEncryptedAppData](#classmip_1_1_policy_descriptor_1a9a5bcf9d1bf7357de549429179197ab6) を使用してアクセスできる暗号化データに依存しません
### <a name="setsignedappdata"></a>SetSignedAppData
署名する必要があるアプリ固有のデータを設定します。
#### <a name="parameters"></a>パラメーター
* value: アプリ固有のデータ。アプリケーションでは、RMS サービスによって署名されるアプリ固有のデータのディクショナリを指定できます。 この署名済みデータは、[PolicyDescriptor::SetEncryptedAppData](#classmip_1_1_policy_descriptor_1a5275224932dc17319092304497e59eb2) によって設定される暗号化データに依存しません。