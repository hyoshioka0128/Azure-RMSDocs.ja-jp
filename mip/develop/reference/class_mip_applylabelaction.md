# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetLabelId() const  |  必要なラベル ID を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabelid"></a>GetLabelId
必要なラベル ID を取得します。

  
**戻り値**: ラベル ID。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。