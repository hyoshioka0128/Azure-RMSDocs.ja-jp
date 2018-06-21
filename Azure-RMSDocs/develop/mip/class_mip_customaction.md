# <a name="class-mipcustomaction"></a>class mip::CustomAction 
[CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector<std::pair<std::string, std::string>>& GetProperties() const  |  プロパティ キーと値のペアの一覧を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getproperties"></a>GetProperties
プロパティ キーと値のペアの一覧を取得します。

  
**戻り値**: キーと値のペアの一覧。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。