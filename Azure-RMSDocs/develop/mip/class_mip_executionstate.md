# <a name="class-mipexecutionstate"></a>class mip::ExecutionState 
エンジンの実行に必要なすべての状態のインターフェイス。
クライアントでは、必要な状態を取得するメソッドのみを呼び出す必要があります。 そのため、効率を高めるために、クライアントは対応する状態が事前に計算されるのではなく動的に計算されるようにこのインターフェイスを実装できます。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  ドキュメントに適用される必要のある機密ラベル ID を取得します。
 public bool IsDowngradeJustified() const  |  実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  新しいラベルの割り当て方法を取得します。
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  コンテンツからメタデータ項目を取得します。
 public std::string GetTemplateId() const  |  権限管理サービス保護テンプレート ID を取得します。
 public ContentFormat GetContentFormat() const  |  コンテンツの形式を取得します。
 public const ActionType GetSupportedActions() const  |  アプリケーションがサポートするアクションの一覧を返します。 すべてのアクションの種類は、[mip/upe/action.h](#action) に一覧表示されています。
  
## <a name="members"></a>メンバー
  
### <a name="getnewlabelid"></a>GetNewLabelId
ドキュメントに適用される必要のある機密ラベル ID を取得します。

  
**戻り値**: コンテンツに適用される機密ラベル ID が存在する場合はその ID、それ以外でラベルを削除する場合は空。
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。

  
**戻り値**: ダウングレードの理由が既に示されている場合は true、まだ示されていない場合は false。 
**関連項目**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
新しいラベルの割り当て方法を取得します。

  
**戻り値**: 割り当て方法: STANDARD、PRIVILEGED、AUTO。 
**関連項目**: mip::AssignmentMethod
  
### <a name="getcontentmetadata"></a>GetContentMetadata
コンテンツからメタデータ項目を取得します。

  
**戻り値**: コンテンツに適用するメタデータを表すキーと値のペアのベクター。 各メタデータ項目は名前と値のペアです。
  
### <a name="gettemplateid"></a>GetTemplateId
権限管理サービス保護テンプレート ID を取得します。

  
**戻り値**: 権限管理サービス保護テンプレート ID が存在する場合はその ID、それ以外の場合は中かっこのない guid 形式で空の文字列を返します。
  
### <a name="getcontentformat"></a>GetContentFormat
コンテンツの形式を取得します。

  
**戻り値**: DEFAULT、EMAIL。**関連項目**: mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
アプリケーションがサポートするアクションの一覧を返します。 すべてのアクションの種類は、[mip/upe/action.h](#action) に一覧表示されています。