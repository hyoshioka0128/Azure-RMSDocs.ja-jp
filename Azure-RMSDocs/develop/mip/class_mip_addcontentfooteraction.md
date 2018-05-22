# <a name="class-mipaddcontentfooteraction"></a>class mip::AddContentFooterAction 
コンテンツ フッターをドキュメントに追加することを指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  コンテンツ フッター要素をマークするために使用する API。
 public const std::string& GetText() const  |  コンテンツ フッターに移動されるテキストを取得します。
 public const std::string& GetFontName() const  |  コンテンツ フッターの表示に使用されるフォント名を取得します。
 public int GetFontSize() const  |  コンテンツ フッターの表示に使用されるフォント サイズを取得します。
 public const std::string& GetFontColor() const  |  コンテンツ フッターの表示に使用されるフォントの色を取得します。
 public ContentMarkAlignment GetAlignment() const  |  フッターの配置を取得します。
 public int GetMargin() const  |  一番下からのフッターの余白を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementname"></a>GetUIElementName
コンテンツ フッター要素をマークするために使用する API。

  
**戻り値**: コンテンツ フッターを保持する UI 要素に使用する必要のある名前。 コンテンツ フッターを削除する必要がある場合は、[RemoveContentFooterAction](class_mip_removecontentfooteraction.md) でも同じ名前が返されます。
  
### <a name="gettext"></a>GetText
コンテンツ フッターに移動されるテキストを取得します。

  
**戻り値**: コンテンツ フッターのテキスト。
  
### <a name="getfontname"></a>GetFontName
コンテンツ フッターの表示に使用されるフォント名を取得します。

  
**戻り値**: フォント名。ポリシー Calibri で設定されていない場合は既定値です。
  
### <a name="getfontsize"></a>GetFontSize
コンテンツ フッターの表示に使用されるフォント サイズを取得します。

  
**戻り値**: 整数値としてのフォント サイズ。
  
### <a name="getfontcolor"></a>GetFontColor
コンテンツ フッターの表示に使用されるフォントの色を取得します。

  
**戻り値**: 文字列としてのフォントの色 (例: "#000000")。
  
### <a name="getalignment"></a>GetAlignment
フッターの配置を取得します。

  
**戻り値**: ContentMarkAlignment 列挙子、LEFT|RIGHT|CENTER。 
**関連項目**: ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
一番下からのフッターの余白を取得します。

  
**戻り値**: ドキュメントの一番下からの余白を表す整数 (例: 10 mm)。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。