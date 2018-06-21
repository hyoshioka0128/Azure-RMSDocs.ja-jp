# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  プロファイルを構成するためのインターフェイス。
 public ~Settings()  | _まだ文書化されていません。_
 public const std::string& GetPath() const  | _まだ文書化されていません。_
 public bool GetUseInMemoryStorage() const  | _まだ文書化されていません。_
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  | _まだ文書化されていません。_
public std::shared_ptr<Observer> GetObserver() const  | _まだ文書化されていません。_
 public const ApplicationInfo GetApplicationInfo() const  | _まだ文書化されていません。_
 public bool GetSkipTelemetryInit() const  | _まだ文書化されていません。_
 public void SetSkipTelemetryInit()  | _まだ文書化されていません。_
 public void SetSessionId(const std::string& sessionId)  |  プロファイル セッション ID を設定します。
 public const std::string& GetSessionId() const  |  プロファイル セッション ID を返します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
プロファイルを構成するためのインターフェイス。

パラメーター:  
* **observer**: [FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。 nullptr にすることができます。


  
### <a name="settings"></a>~Settings
_まだ文書化されていません。_

  
### <a name="getpath"></a>GetPath
_まだ文書化されていません。_

  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
_まだ文書化されていません。_

  
### <a name="getauthdelegate"></a>GetAuthDelegate
_まだ文書化されていません。_

  
### <a name="observer"></a>オブザーバー
_まだ文書化されていません。_

  
### <a name="applicationinfo"></a>ApplicationInfo
_まだ文書化されていません。_

  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
_まだ文書化されていません。_

  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
_まだ文書化されていません。_

  
### <a name="setsessionid"></a>SetSessionId
プロファイル セッション ID を設定します。
  
### <a name="getsessionid"></a>GetSessionId
プロファイル セッション ID を返します。