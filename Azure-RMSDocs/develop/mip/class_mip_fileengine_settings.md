# <a name="class-mipfileenginesettings"></a>class mip::FileEngine::Settings 
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  指定されたパラメーターを使用してインスタンスを作成します。
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  指定されたパラメーターを使用してインスタンスを作成します。
 public const std::string& GetEngineId() const  |  エンジン ID を返します。
 public const Identity& GetIdentity() const  |  エンジン ID を返します。
 public void SetIdentity(const Identity& identity)  |  エンジン ID を設定します。
 public const std::string& GetClientData() const  |  エンジンのクライアント データを返します。
 public const std::string& GetLocale() const  |  エンジンのロケールを返します。
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  テストや実験に使用する名前と値のペアの一覧を設定します。
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  テストや実験に使用する名前と値のペアの一覧を取得します。
 public void SetSessionId(const std::string& sessionId)  |  エンジンのセッション ID を設定します。
 public const std::string& GetSessionId() const  |  エンジンのセッション ID を返します。
 public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  クラウド境界を指定するために使用する、保護クラウド エンドポイント ベース URL を設定します。
 public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  cloudEndpointBaseUrl を取得します。
 public void SetProtectionOnlyEngine(const bool protectionOnly)  |  保護のみのエンジン インジケーターを設定します (ポリシー/ラベルなし)。
 public const bool IsProtectionOnlyEngine() const  |  保護のみのエンジン インジケーターを返します (ポリシー/ラベルなし)。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
指定されたパラメーターを使用してインスタンスを作成します。
これを使用して、(AddEngineAsync を使用して追加した) 既存のエンジンを読み込むために LoadEngineAsync を呼び出す[設定](class_mip_fileengine_settings.md)を作成します。

パラメーター:  
* **engineId**: AddEngineAsync によって生成される一意のエンジン ID に設定します。


  
### <a name="settings"></a>Settings
指定されたパラメーターを使用してインスタンスを作成します。
これを使用して、新しいエンジンを追加するために AddEngineAsync を呼び出す[設定](class_mip_fileengine_settings.md)を作成します。

パラメーター:  
* **identity**: エンジンを追加する必要がある対象ユーザーの ID 情報。


  
### <a name="getengineid"></a>GetEngineId
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
  
### <a name="setprotectioncloudendpointbaseurl"></a>SetProtectionCloudEndpointBaseUrl
クラウド境界を指定するために使用する、保護クラウド エンドポイント ベース URL を設定します。

パラメーター:  
* **protectionCloudEndpointBaseUrl**: 保護エンドポイントに関連付けられたベース URL


  
### <a name="getprotectioncloudendpointbaseurl"></a>GetProtectionCloudEndpointBaseUrl
cloudEndpointBaseUrl を取得します。

  
**戻り値**: 保護エンドポイントに関連付けられたベース URL
  
### <a name="setprotectiononlyengine"></a>SetProtectionOnlyEngine
保護のみのエンジン インジケーターを設定します (ポリシー/ラベルなし)。
  
### <a name="isprotectiononlyengine"></a>IsProtectionOnlyEngine
保護のみのエンジン インジケーターを返します (ポリシー/ラベルなし)。