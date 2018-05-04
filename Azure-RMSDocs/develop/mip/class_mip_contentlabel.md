# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
コンテンツの一部 (通常はドキュメント) に適用される Microsoft Information Protection ラベルの抽象化。
ラベル情報だけでなく、特定の適用済みラベルのプロパティを保持します。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string & GetCreationTime | ラベルの作成時間を取得します。
public AssignmentMethod GetAssignmentMethod | ラベルの割り当て方法を取得します。
public std::shared_ptr< Label > GetLabel | コンテンツに適用された実際のラベル オブジェクトを取得します。
## <a name="members"></a>メンバー
### <a name="getcreationtime"></a>GetCreationTime
ラベルの作成時間を取得します。
#### <a name="returns"></a>戻り値
gmt 文字列としての作成時間。
### <a name="getassignmentmethod"></a>GetAssignmentMethod
ラベルの割り当て方法を取得します。
#### <a name="returns"></a>戻り値
AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
**関連項目**: mip::AssignmentMethod
### <a name="label"></a>Label
コンテンツに適用された実際のラベル オブジェクトを取得します。
#### <a name="returns"></a>戻り値
コンテンツに適用されたラベル オブジェクト。 
**関連項目**: [mip::Label](#classmip_1_1_label)