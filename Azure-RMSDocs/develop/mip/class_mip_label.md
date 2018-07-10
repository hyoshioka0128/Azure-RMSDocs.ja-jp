# <a name="class-miplabel"></a>class mip::Label 
単一の Microsoft Information Protection ラベルの抽象化。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetId() const  |  ラベル ID を取得します。
 public const std::string& GetName() const  |  ラベル名を取得します。
 public const std::string& GetDescription() const  |  ラベルの説明を取得します。
 public const std::string& GetColor() const  |  ラベルの表示色を取得します。
 public int GetSensitivity() const  |  ラベルの秘密度を取得します。
 public const std::string& GetTooltip() const  |  ラベルのヒントの説明を取得します。
 public bool IsActive() const  |  ラベルがアクティブかどうかを示すブール値を取得します。
public std::weak_ptr<Label> GetParent() const  |  親ラベルを取得します。
public const std::vector<std::shared_ptr<Label>>& GetChildren() const  |  現在のラベルの子ラベルを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid"></a>GetId
ラベル ID を取得します。

  
**戻り値**: ラベル ID。
  
### <a name="getname"></a>GetName
ラベル名を取得します。

  
**戻り値**: ラベル名。
  
### <a name="getdescription"></a>GetDescription
ラベルの説明を取得します。

  
**戻り値**: ラベルの説明。
  
### <a name="getcolor"></a>GetColor
ラベルの表示色を取得します。

  
**戻り値**: 文字列形式での色の値。 "#RRGGBB" で、RR、GG、BB は 16 進数の 0 ～ f です。
  
### <a name="getsensitivity"></a>GetSensitivity
ラベルの秘密度を取得します。

  
**戻り値**: 数値。 大きい値は高い秘密度を意味します。
  
### <a name="gettooltip"></a>GetTooltip
ラベルのヒントの説明を取得します。

  
**戻り値**: ヒントの文字列。
  
### <a name="isactive"></a>IsActive
ラベルがアクティブかどうかを示すブール値を取得します。
アクティブなラベルのみを適用できます。 非アクティブなラベルは適用できず、表示目的でのみ使用されます。 

  
**戻り値**: ラベルがアクティブな場合は true、それ以外の場合は false。
  
### <a name="label"></a>Label
親ラベルを取得します。

  
**戻り値**: 親ラベルが存在する場合は親ラベルへの弱いポインター、存在しない場合は空のポインターです。
  
### <a name="label"></a>Label
現在のラベルの子ラベルを取得します。

  
**戻り値**: ラベルへの共有ポインターのベクター。