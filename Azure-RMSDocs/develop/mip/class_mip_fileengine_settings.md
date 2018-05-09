# <a name="class-mipfileenginesettings"></a>class mip::FileEngine::Settings 
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline Settings(const std::string& id, const std::string& clientData, const std::string& locale)  |  指定されたパラメーターを使用してインスタンスを作成します。
public inline Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  指定されたパラメーターを使用してインスタンスを作成します。
public inline const std::string& GetId() const  |  エンジン ID を返します。
public inline const Identity& GetIdentity() const  |  エンジン ID を返します。
public inline void SetIdentity(const Identity& identity)  |  エンジン ID を設定します。
public inline const std::string& GetClientData() const  |  エンジンのクライアント データを返します。
public inline const std::string& GetLocale() const  |  エンジンのロケールを返します。
public inline void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  テストや実験に使用する名前と値のペアの一覧を設定します。
public inline const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  テストや実験に使用する名前と値のペアの一覧を取得します。
public inline void SetSessionId(const std::string& sessionId)  |  エンジンのセッション ID を設定します。
public inline const std::string& GetSessionId() const  |  エンジンのセッション ID を返します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
指定されたパラメーターを使用してインスタンスを作成します。
これを使用して、(AddEngineAsync を使用して追加した) 既存のエンジンを読み込むために LoadEngineAsync を呼び出す[設定](#classmip_1_1_file_engine_1_1_settings)を作成します。
  
#### <a name="parameters"></a>パラメーター
* id: AddEngineAsync によって生成される一意のエンジン ID に設定します。
  
### <a name="settings"></a>Settings
指定されたパラメーターを使用してインスタンスを作成します。
これを使用して、新しいエンジンを追加するために AddEngineAsync を呼び出す[設定](#classmip_1_1_file_engine_1_1_settings)を作成します。
  
#### <a name="parameters"></a>パラメーター
* identity: エンジンを追加する必要がある対象ユーザーの ID 情報。
  
### <a name="getid"></a>GetId
エンジン ID を返します。
  
### <a name="getidentity"></a>GetIdentity
エンジン ID を返します。
  
### <a name="setidentity"></a>SetIdentity
エンジン ID を設定します。
  
### <a name="getclientdata"></a>GetClientData
エンジンのクライアント データを返します。
  
### <a name="getlocale"></a>GetLocale
エンジンのロケールを返します。
  
### <a name="setcustomsettings"></a>SetCustomSettings
テストや実験に使用する名前と値のペアの一覧を設定します。
  
### <a name="getcustomsettings"></a>GetCustomSettings
テストや実験に使用する名前と値のペアの一覧を取得します。
  
### <a name="setsessionid"></a>SetSessionId
エンジンのセッション ID を設定します。
  
### <a name="getsessionid"></a>GetSessionId
エンジンのセッション ID を返します。