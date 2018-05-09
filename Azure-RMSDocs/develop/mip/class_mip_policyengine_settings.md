# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
エンジンを開始するには、適切なパラメーターを指定したこのクラスのインスタンスを提供する必要があります。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
`public inline Settings(const std::string& id, const std::string& clientData, const std::string& locale)`  |  指定されたパラメーターを使用してインスタンスを作成します。 これを使用して、既存のエンジンを読み込むために LoadEngineAsync を呼び出す[設定](#classmip_1_1_policy_engine_1_1_settings)を作成します。
`public inline Settings(const Identity& identity, const std::string& clientData, const std::string& locale)`  |  これを使用して、新しいエンジンを追加するために AddEngineAsync を呼び出す[設定](#classmip_1_1_policy_engine_1_1_settings)を作成します。
`public inline const std::string& GetId() const`  |  エンジン ID を取得します。
`public inline void SetId(const std::string& id)`  |  エンジン ID を設定します。
`public inline const Identity& GetIdentity() const`  |  ID オブジェクトを取得します。
`public inline void SetIdentity(const Identity& identity)`  |  ID オブジェクトを設定します。
`public inline const std::string& GetClientData() const`  |  設定で設定されたクライアント データを取得します。
`public inline void SetClientData(const std::string& clientData)`  |  クライアント データ文字列を設定します。
`public inline const std::string& GetLocale() const`  |  設定で設定されたロケールを取得します。
`public inline void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)`  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
`public inline const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const`  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
`public inline void SetSessionId(const std::string& sessionId)`  |  クライアントによって定義されたテレメトリに使用するセッション ID を設定します。
`public inline const std::string& GetSessionId() const`  |  セッション ID、一意識別子を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
指定されたパラメーターを使用してインスタンスを作成します。 これを使用して、既存のエンジンを読み込むために LoadEngineAsync を呼び出す[設定](#classmip_1_1_policy_engine_1_1_settings)を作成します。
  
#### <a name="parameters"></a>パラメーター
* id: AddEngineAsync によって生成されるか自分で生成した一意のエンジン ID に設定します。 既存のエンジンを読み込む場合は id を再利用し、それ以外の場合は新しいエンジンが作成されます。 
* clientData: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 
* locale: エンジンのローカライズ可能な出力はこのロケールで提供されます。既定値は "en-US" です。
  
### <a name="settings"></a>Settings
これを使用して、新しいエンジンを追加するために AddEngineAsync を呼び出す[設定](#classmip_1_1_policy_engine_1_1_settings)を作成します。
  
#### <a name="parameters"></a>パラメーター
* identity: エンジンを追加する必要がある対象ユーザーの一意識別子。 
* clientData: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 
* locale: エンジンのローカライズ可能な出力はこのロケールで提供されます。既定値は `en-US` です。
  
### <a name="getid"></a>GetId
エンジン ID を取得します。
  
#### <a name="returns"></a>戻り値
エンジンを識別する一意の文字列。
  
### <a name="setid"></a>SetId
エンジン ID を設定します。
  
#### <a name="parameters"></a>パラメーター
* エンジン ID を識別します。
  
### <a name="getidentity"></a>GetIdentity
ID オブジェクトを取得します。
  
#### <a name="returns"></a>戻り値
設定オブジェクト内の ID への参照。 
**関連項目**: mip::Identity
  
### <a name="setidentity"></a>SetIdentity
ID オブジェクトを設定します。
  
#### <a name="parameters"></a>パラメーター
* identity: ユーザーの一意の ID。 
**関連項目**: mip::Identity
  
### <a name="getclientdata"></a>GetClientData
設定で設定されたクライアント データを取得します。
  
#### <a name="returns"></a>戻り値
クライアントで指定されたデータの文字列。
  
### <a name="setclientdata"></a>SetClientData
クライアント データ文字列を設定します。
  
#### <a name="parameters"></a>パラメーター
* clientData: ユーザーが指定したデータ。
  
### <a name="getlocale"></a>GetLocale
設定で設定されたロケールを取得します。
  
#### <a name="returns"></a>戻り値
ロケール。
  
### <a name="setcustomsettings"></a>SetCustomSettings
機能のゲーティングとテストに使用するカスタム設定を設定します。
  
#### <a name="parameters"></a>パラメーター
* customSettings: 名前と値のペアの一覧。
  
### <a name="getcustomsettings"></a>GetCustomSettings
機能のゲーティングとテストに使用するカスタム設定を設定します。
  
#### <a name="parameters"></a>パラメーター
* 名前と値のペアの一覧。
  
### <a name="setsessionid"></a>SetSessionId
クライアントによって定義されたテレメトリに使用するセッション ID を設定します。
  
#### <a name="parameters"></a>パラメーター
* sessionId: テレメトリ イベントを接続する一意の文字列。
  
### <a name="getsessionid"></a>GetSessionId
セッション ID、一意識別子を取得します。
  
#### <a name="returns"></a>戻り値
セッション ID。