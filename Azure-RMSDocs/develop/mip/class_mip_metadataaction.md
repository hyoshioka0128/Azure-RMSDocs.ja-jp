# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  キーと値のペアとしてメタデータの一覧を取得します。 メタデータは、コンテンツのメタデータに追加する必要があります。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。

  
**戻り値**: 削除する文字列のベクター。 メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
キーと値のペアとしてメタデータの一覧を取得します。 メタデータは、コンテンツのメタデータに追加する必要があります。

  
**戻り値**: const std::vector<std::pair<std::string, std::string>>& メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。