# <a name="class-mipprotectbytemplateaction"></a>class mip::ProtectByTemplateAction 
テンプレートによる保護をドキュメントに追加することを指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetTemplateId() const  |  アクションに関連付けられている保護テンプレート ID を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="gettemplateid"></a>GetTemplateId
アクションに関連付けられている保護テンプレート ID を取得します。

  
**戻り値**: 保護テンプレート ID を含む文字列。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。