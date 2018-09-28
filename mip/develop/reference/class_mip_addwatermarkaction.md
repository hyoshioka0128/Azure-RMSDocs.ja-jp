# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
ウォーターマークの追加を指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  ウォーターマーク要素を示すために使用される API。
 public WatermarkLayout GetLayout() const  |  ウォーターマーク レイアウトを取得するために使用される API。
 public const std::string& GetText() const  |  ウォーターマークに移動されるテキストを取得します。
 public const std::string& GetFontName() const  |  ウォーターマークの表示に使用されるフォント名を取得します。
 public int GetFontSize() const  |  ウォーターマークの表示に使用されるフォント サイズを取得します。
 public const std::string& GetFontColor() const  |  ウォーターマークの表示に使用されるフォントの色を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname"></a>GetUIElementName
ウォーターマーク要素を示すために使用される API。

  
**戻り値**: ウォーターマークを保持する UI 要素に使用する必要のある名前。 ウォーターマークを削除する必要がある場合は、RemoveWatermarkingAction でも同じ名前が返されます。
  
### <a name="getlayout"></a>GetLayout
ウォーターマーク レイアウトを取得するために使用される API。

  
**戻り値**: WatermarkLayout: 列挙型 HORIZONTAL|DIAGONAL の形式のウォーターマーク レイアウト。 、
  
### <a name="gettext"></a>GetText
ウォーターマークに移動されるテキストを取得します。

  
**戻り値**: コンテンツ ヘッダーのテキスト。
  
### <a name="getfontname"></a>GetFontName
ウォーターマークの表示に使用されるフォント名を取得します。

  
**戻り値**: フォント名。 ポリシーで何も設定されていない場合、規定値は Calibri です。
  
### <a name="getfontsize"></a>GetFontSize
ウォーターマークの表示に使用されるフォント サイズを取得します。

  
**戻り値**: 整数値としてのフォント サイズ。
  
### <a name="getfontcolor"></a>GetFontColor
ウォーターマークの表示に使用されるフォントの色を取得します。

  
**戻り値**: 文字列としてのフォントの色 (例: "#000000")。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。