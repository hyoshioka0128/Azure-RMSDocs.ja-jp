# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  プロファイルを構成するためのインターフェイス。
public inline ~Settings()  |  
public inline const std::string& GetPath() const  |  
public inline bool GetUseInMemoryStorage() const  |  
public inline std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  
public inline std::shared_ptr<Observer> GetObserver() const  |  
public inline const ApplicationInfo GetApplicationInfo() const  |  
public inline bool GetSkipTelemetryInit() const  |  
public inline void SetSkipTelemetryInit()  |  
public inline void SetSessionId(const std::string& sessionId)  |  プロファイル セッション ID を設定します。
public inline const std::string& GetSessionId() const  |  プロファイル セッション ID を返します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
プロファイルを構成するためのインターフェイス。
  
#### <a name="parameters"></a>パラメーター
* observer: [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) インターフェイスを実装するクラス。 nullptr にすることができます。
  
### <a name="settings"></a>~Settings
  
### <a name="getpath"></a>GetPath
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
  
### <a name="getauthdelegate"></a>GetAuthDelegate
  
### <a name="observer"></a>オブザーバー
  
### <a name="applicationinfo"></a>ApplicationInfo
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
  
### <a name="setsessionid"></a>SetSessionId
プロファイル セッション ID を設定します。
  
### <a name="getsessionid"></a>GetSessionId
プロファイル セッション ID を返します。