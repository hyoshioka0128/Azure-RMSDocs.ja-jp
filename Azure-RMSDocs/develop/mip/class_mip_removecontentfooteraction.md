# <a name="class-mipremovecontentfooteraction"></a>class mip::RemoveContentFooterAction 
ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetUIElementNames()  |  削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。
public ActionType GetType() const  |  [アクション](#classmip_1_1_action)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementnames"></a>GetUIElementNames
削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。
  
#### <a name="returns"></a>戻り値
ui 要素名の一覧。
  
### <a name="actiontype"></a>ActionType
[アクション](#classmip_1_1_action)の種類を取得します。
  
#### <a name="returns"></a>戻り値
ActionType: この基底クラスをキャストできる派生アクションの種類。