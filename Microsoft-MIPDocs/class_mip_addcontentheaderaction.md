# <a name="class-mipaddcontentheaderaction"></a>class mip::AddContentHeaderAction 
コンテンツ ヘッダーの追加を指定するアクション クラス。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string & GetUIElementName | コンテンツ ヘッダー要素をマークするために使用する API。
public const std::string & GetText | コンテンツ ヘッダーに移動されるテキストを取得します。
public const std::string & GetFontName | コンテンツ ヘッダーの表示に使用されるフォント名を取得します。
public int GetFontSize | コンテンツ ヘッダーの表示に使用されるフォント サイズを取得します。
public const std::string & GetFontColor | コンテンツ ヘッダーの表示に使用されるフォントの色を取得します。
public ContentMarkAlignment GetAlignment | ヘッダーの配置を取得します。
public int GetMargin | 一番下からのヘッダーの余白を取得します。
public ActionType GetType
## <a name="members"></a>メンバー
### <a name="getuielementname"></a>GetUIElementName
コンテンツ ヘッダー要素をマークするために使用する API。
#### <a name="returns"></a>戻り値
コンテンツ ヘッダーを保持する UI 要素に使用する必要のある名前。 コンテンツ ヘッダーを削除する必要がある場合は、[RemoveContentHeaderAction](#classmip_1_1_remove_content_header_action) に同じ名前が返されます。
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
### <a name="getalignment"></a>GetAlignment
ヘッダーの配置を取得します。
#### <a name="returns"></a>戻り値
ContentMarkAlignment 列挙子 LEFT|RIGHT|CENTER。 
**関連項目**: ContentMarkAlignment
### <a name="getmargin"></a>GetMargin
一番下からのヘッダーの余白を取得します。
#### <a name="returns"></a>戻り値
ドキュメントの一番下からの余白を表す整数 (例: 10 mm)。
### <a name="actiontype"></a>ActionType
[アクション](#classmip_1_1_action)の種類を取得します。
#### <a name="returns"></a>戻り値
ActionType: この基底クラスをキャストできる派生アクションの種類。