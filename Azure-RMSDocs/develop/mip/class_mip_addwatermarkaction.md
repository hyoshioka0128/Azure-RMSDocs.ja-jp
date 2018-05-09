# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
ウォーターマークの追加を指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  ウォーターマーク要素を示すために使用される API。
public WatermarkLayout GetLayout() const  |  ウォーターマーク レイアウトを取得するために使用される API。
public const std::string& GetText() const  |  コンテンツ ヘッダーに移動されるテキストを取得します。
public const std::string& GetFontName() const  |  コンテンツ ヘッダーの表示に使用されるフォント名を取得します。
public int GetFontSize() const  |  コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。
public const std::string& GetFontColor() const  |  コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。
public ActionType GetType() const  |  [アクション](#classmip_1_1_action)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname"></a>GetUIElementName
ウォーターマーク要素を示すために使用される API。
  
#### <a name="returns"></a>戻り値
ウォーターマークを保持する UI 要素に使用する必要のある名前。 ウォーターマークを削除する必要がある場合は、RemoveWatermarkingAction でも同じ名前が返されます。
  
### <a name="getlayout"></a>GetLayout
ウォーターマーク レイアウトを取得するために使用される API。
  
#### <a name="returns"></a>戻り値
WatermarkLayout: 列挙型 HORIZONTAL|DIAGONAL の形式のウォーターマーク レイアウト。 、
  
### <a name="gettext"></a>GetText
コンテンツ ヘッダーに移動されるテキストを取得します。
  
#### <a name="returns"></a>戻り値
コンテンツ ヘッダーのテキスト。
  
### <a name="getfontname"></a>GetFontName
コンテンツ ヘッダーの表示に使用されるフォント名を取得します。
  
#### <a name="returns"></a>戻り値
フォント名。ポリシー Calibri で設定されていない場合は既定値です。
  
### <a name="getfontsize"></a>GetFontSize
コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。
  
#### <a name="returns"></a>戻り値
整数値としてのフォント サイズ。
  
### <a name="getfontcolor"></a>GetFontColor
コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。
  
#### <a name="returns"></a>戻り値
文字列としてのフォントの色 (例: "#000000")。
  
### <a name="actiontype"></a>ActionType
[アクション](#classmip_1_1_action)の種類を取得します。
  
#### <a name="returns"></a>戻り値
ActionType: この基底クラスをキャストできる派生アクションの種類。