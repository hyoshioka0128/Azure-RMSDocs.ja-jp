# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
コンテンツに追加する必要のあるメタデータ情報を指定するための[アクション](#classmip_1_1_action)。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector< std::string > & GetMetadataToRemove | コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std::vector< std::pair< std::string, std::string > > & GetMetadataToAdd | キーと値のペアとしてのメタデータの一覧を取得します。 メタデータは、コンテンツ メタデータに追加する必要があります。
public ActionType GetType
## <a name="members"></a>メンバー
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
#### <a name="returns"></a>戻り値
削除する文字列のベクター。 メタデータを追加する前にメタデータの削除を実行する必要があります。
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
キーと値のペアとしてのメタデータの一覧を取得します。 メタデータは、コンテンツ メタデータに追加する必要があります。
#### <a name="returns"></a>戻り値
const std::vector<std::pair<std::string, std::string>>& メタデータを追加する前にメタデータの削除を実行する必要があります。
### <a name="actiontype"></a>ActionType
[アクション](#classmip_1_1_action)の種類を取得します。
#### <a name="returns"></a>戻り値
ActionType: この基底クラスをキャストできる派生アクションの種類。