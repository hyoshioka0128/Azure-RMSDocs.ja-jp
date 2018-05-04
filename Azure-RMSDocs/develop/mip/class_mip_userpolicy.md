# <a name="class-mipuserpolicy"></a>class mip::UserPolicy 
保護されたコンテンツに関連付けられているポリシーを表します。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public bool AccessCheck | ポリシーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。
public UserPolicyType GetType | ポリシーの種類を取得します。
public std::string GetName | ポリシー名を取得します。
public std::string GetDescription | ポリシーの説明を取得します。
public std::shared_ptr< TemplateDescriptor > GetTemplateDescriptor public std::shared_ptr< PolicyDescriptor > GetPolicyDescriptor public std::string GetOwner | コンテンツ所有者のメール アドレスを取得します。
public std::string GetIssuedTo | 保護ポリシーに関連付けられているユーザーを取得します。
public bool IsIssuedToOwner | 現在のユーザーがコンテンツの所有者かどうかを取得します。
public std::string GetContentId | ドキュメント/コンテンツの一意識別子を取得します。
public const mip::AppDataHashMap GetEncryptedAppData | 暗号化されたアプリ固有のデータを取得します。
public const mip::AppDataHashMap GetSignedAppData | 署名されたアプリ固有のデータを取得します。
public std::chrono::time_point< std::chrono::system_clock > GetContentValidUntil | ポリシーの有効期限を取得します。
public bool DoesUseDeprecatedAlgorithms | ポリシーで下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。
public bool IsAuditedExtractAllowed | ポリシーがユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。
public const std::vector< unsigned char > GetSerializedPolicy public std::shared_ptr< rmscore::core::ProtectionPolicy > GetImpl
## <a name="members"></a>メンバー
### <a name="accesscheck"></a>AccessCheck
ポリシーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。
#### <a name="parameters"></a>パラメーター
* right: 確認する権限
#### <a name="returns"></a>戻り値
ポリシーが指定された権限へのアクセス権をユーザーに付与するかどうか
### <a name="userpolicytype"></a>UserPolicyType
ポリシーの種類を取得します。
#### <a name="returns"></a>戻り値
ポリシーの種類
### <a name="getname"></a>GetName
ポリシー名を取得します。
#### <a name="returns"></a>戻り値
ポリシー名
### <a name="getdescription"></a>GetDescription
ポリシーの説明を取得します。
#### <a name="returns"></a>戻り値
ポリシーの説明
### <a name="templatedescriptor"></a>TemplateDescriptor
テンプレート ベースの [UserPolicy](#classmip_1_1_user_policy) の [TemplateDescriptor](#classmip_1_1_template_descriptor) を取得します。
#### <a name="returns"></a>戻り値
[UserPolicy](#classmip_1_1_user_policy) がテンプレート ベースの場合は [TemplateDescriptor](#classmip_1_1_template_descriptor)、それ以外の場合は nullptr
### <a name="policydescriptor"></a>PolicyDescriptor
アドホック [UserPolicy](#classmip_1_1_user_policy) の [PolicyDescriptor](#classmip_1_1_policy_descriptor) を取得します。
#### <a name="returns"></a>戻り値
[UserPolicy](#classmip_1_1_user_policy) がアドホックの場合は [PolicyDescriptor](#classmip_1_1_policy_descriptor)、それ以外の場合は nullptr
### <a name="getowner"></a>GetOwner
コンテンツ所有者のメール アドレスを取得します。
#### <a name="returns"></a>戻り値
コンテンツ所有者のメール アドレス
### <a name="getissuedto"></a>GetIssuedTo
保護ポリシーに関連付けられているユーザーを取得します。
#### <a name="returns"></a>戻り値
保護ポリシーに関連付けられているユーザー
### <a name="isissuedtoowner"></a>IsIssuedToOwner
現在のユーザーがコンテンツの所有者かどうかを取得します。
#### <a name="returns"></a>戻り値
現在のユーザーがコンテンツの所有者かどうか
### <a name="getcontentid"></a>GetContentId
ドキュメント/コンテンツの一意識別子を取得します。
#### <a name="returns"></a>戻り値
一意のコンテンツ識別子
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
暗号化されたアプリ固有のデータを取得します。
[UserPolicy](#classmip_1_1_user_policy) には、RMS サービスによって暗号化されたアプリ固有のデータのディクショナリが含まれる場合があります。 この暗号化データは、[UserPolicy::GetSignedAppData](#classmip_1_1_user_policy_1a1c8a284d50adcac1a0a09316afa1d43e) を使用してアクセスできる署名済みデータに依存しません
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
署名されたアプリ固有のデータを取得します。
[UserPolicy](#classmip_1_1_user_policy) には、RMS サービスによって署名されたアプリ固有のデータのディクショナリが含まれる場合があります。 この署名済みデータは、[UserPolicy::GetEncryptedAppData](#classmip_1_1_user_policy_1a610fbc799284ab0ce4354c0611ece0e8) を使用してアクセスできる暗号化データに依存しません
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
ポリシーの有効期限を取得します。
#### <a name="returns"></a>戻り値
ポリシーの有効期限
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
ポリシーで下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。
#### <a name="returns"></a>戻り値
ポリシーで非推奨の暗号アルゴリズムを使用するかどうか
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
ポリシーがユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。
#### <a name="returns"></a>戻り値
ポリシーがユーザーに '監査済み抽出' 権限を付与するかどうか
### <a name="getserializedpolicy"></a>GetSerializedPolicy
[UserPolicy](#classmip_1_1_user_policy) を発行ライセンス (PL) にシリアル化します
#### <a name="returns"></a>戻り値
シリアル化された [UserPolicy](#classmip_1_1_user_policy)
### <a name="getimpl"></a>GetImpl
[UserPolicy](#classmip_1_1_user_policy) の内部派生クラスの実装を取得します。
#### <a name="returns"></a>戻り値
[UserPolicy](#classmip_1_1_user_policy) の派生クラスの実装。内部的にのみ使用されます