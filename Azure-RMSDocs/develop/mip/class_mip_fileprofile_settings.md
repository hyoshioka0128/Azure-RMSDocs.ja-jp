# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
作成時および有効期間全体にわたって [FileProfile](class_mip_fileprofile.md) に使用される[設定](class_mip_fileprofile_settings.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  [FileProfile::Settings](class_mip_fileprofile_settings.md) コンストラクター。
 public const std::string& GetPath() const  |  ログ、テレメトリ、その他の継続状態が格納されるファイル パスを取得します。
 public bool GetUseInMemoryStorage() const  |  状態がすべて (ディスク上ではなく) メモリに格納されるかどうかを取得します。
 public bool IsLicenseCachingEnabled() const  |  ライセンスのキャッシュが有効かどうかを取得します。
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  認証トークンを取得するために使用する認証委任を取得します。
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  サービスに接続しているユーザーの同意を要求するために使用する同意委任を取得します。
public std::shared_ptr<Observer> GetObserver() const  |  [FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。
 public const ApplicationInfo GetApplicationInfo() const  |  SDK を利用しているアプリケーションに関する情報を取得します。
 public bool GetSkipTelemetryInit() const  |  テレメトリ初期化をスキップするかどうかを取得します。
 public void SetSkipTelemetryInit()  |  テレメトリ初期化を無効にします。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  外部のロガーの実装を使用します。
 public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
 public bool IsTelemetryOptedOut() const  |  テレメトリの収集が無効になっているかどうかを取得します。
 public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
 public const std::string& GetSessionId() const  |  セッション ID を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
[FileProfile::Settings](class_mip_fileprofile_settings.md) コンストラクター。

パラメーター:  
* **path**: ログ、テレメトリ、その他の継続状態が格納されるファイル パス 


* **useInMemoryStorage**: 状態がすべて (ディスク上ではなく) メモリに格納されるかどうか 


* **isLicenseCachingEnabled**: 保護ライセンスのキャッシュを有効または無効にします 


* **authDelegate**: 認証トークンを取得するために使用する認証委任 


* **observer**: [FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信する[オブザーバー](class_mip_fileprofile_observer.md) インスタンス


* **applicationInfo**: SDK を利用しているアプリケーションに関する情報


  
### <a name="getpath"></a>GetPath
ログ、テレメトリ、その他の継続状態が格納されるファイル パスを取得します。

  
**戻り値**: ログ、テレメトリ、その他の継続状態が格納されるファイル パス
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
状態がすべて (ディスク上ではなく) メモリに格納されるかどうかを取得します。

  
**戻り値**: 状態がすべて (ディスク上ではなく) メモリに格納されるかどうか
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
ライセンスのキャッシュが有効かどうかを取得します。

  
**戻り値**: キャッシュがメモリにのみ格納される場合は true
  
### <a name="getauthdelegate"></a>GetAuthDelegate
認証トークンを取得するために使用する認証委任を取得します。

  
**戻り値**: 認証トークンを取得するために使用する認証委任
  
### <a name="consentdelegate"></a>ConsentDelegate
サービスに接続しているユーザーの同意を要求するために使用する同意委任を取得します。

  
**戻り値**: ユーザーの同意を要求するために使用する同意委任
  
### <a name="observer"></a>オブザーバー
[FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。

  
**戻り値**: [FileProfile](class_mip_fileprofile.md) に関連するイベントの通知を受信する[オブザーバー](class_mip_fileprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
SDK を利用しているアプリケーションに関する情報を取得します。

  
**戻り値**: SDK を利用しているアプリケーションに関する情報
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
テレメトリ初期化をスキップするかどうかを取得します。

  
**戻り値**: テレメトリ初期化をスキップするかどうか
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
テレメトリ初期化を無効にします。
これは通常クライアント アプリケーションによって呼び出されず、重複する初期化を防ぐために (テレメトリを既に初期化している) File SDK によって使用されます
  
### <a name="loggerdelegate"></a>LoggerDelegate
アプリケーションによって提供されるロガー委任を取得します (提供される場合)。

  
**戻り値**: ログの記録に使用されるロガー委任
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
外部のロガーの実装を使用します。
クライアント アプリケーションで独自のロガー実装を使用する場合は、これを呼び出す必要があります
  
### <a name="optouttelemetry"></a>OptOutTelemetry
テレメトリの収集をすべて無効にします。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
テレメトリの収集が無効になっているかどうかを取得します。

  
**戻り値**: テレメトリの収集が無効になっているかどうか
  
### <a name="setsessionid"></a>SetSessionId
セッション ID を設定します。

パラメーター:  
* **sessionId**: ログ/テレメトリを関連付けるために使用されるセッション ID


  
### <a name="getsessionid"></a>GetSessionId
セッション ID を取得します。

  
**戻り値**: ログ/テレメトリを関連付けるために使用されるセッション ID