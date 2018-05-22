# <a name="class-mippolicyengine"></a>class mip::PolicyEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  ポリシー エンジン[設定](class_mip_policyengine_settings.md)を取得します。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  既存のコンテンツから機密ラベルを取得します。
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  既定の機密ラベルを取得します。
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  指定された状態に基づいてエンジン内でルールを実行し、実行するアクションの一覧を返します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
ポリシー エンジン[設定](class_mip_policyengine_settings.md)を取得します。

  
**戻り値**: ポリシー エンジン設定。 
**関連項目**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Label
ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。

  
**戻り値**: 機密ラベルの一覧。
  
### <a name="contentlabel"></a>ContentLabel
既存のコンテンツから機密ラベルを取得します。
ラベルの取得に必要な情報は、指定された実行状態を使用して取得されます。 

パラメーター:  
* **state**: 



  
**戻り値**: 機密ラベルと追加情報を格納するコンテンツ ラベル オブジェクト。 存在しない場合は空白を返します。 
**関連項目**: [mip::ContentLabel](class_mip_contentlabel.md)。
  
### <a name="label"></a>Label
既定の機密ラベルを取得します。

  
**戻り値**: 既定の機密ラベル (存在する場合) または既定のラベルが設定されていない場合は nullptr。
  
### <a name="action"></a>操作
指定された状態に基づいてエンジン内でルールを実行し、実行するアクションの一覧を返します。

パラメーター:  
* **state**: ルールが実行されているコンテンツの現在の実行状態。 



  
**戻り値**: コンテンツに適用する必要のあるアクションの一覧。