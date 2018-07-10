# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
作成時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
 public const std::string& GetPath() const  |  ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。
 public bool GetUseInMemoryStorage() const  |  キャッシュが (ディスク上ではなく) メモリにのみ格納されているかどうかを取得します
 public bool IsLicenseCachingEnabled() const  |  ライセンスのキャッシュが有効かどうかを取得します。
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  認証トークンを取得するために使用する認証委任を取得します。
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  サービスに接続するために使用する同意委任を取得します。
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。
 public const ApplicationInfo& GetApplicationInfo() const  |  保護 SDK を利用しているアプリケーションに関する情報を取得します。
 public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
 public bool IsTelemetryOptedOut() const  |  テレメトリの収集が無効になっているかどうかを取得します。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  外部のロガーの実装を使用します。
 public bool GetSkipTelemetryInit() const  |  テレメトリ初期化をスキップするかどうかを取得します。
 public void SetSkipTelemetryInit()  |  テレメトリ初期化を無効にします。
 public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
 public const std::string& GetSessionId() const  |  セッション ID を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **path**: ログ、テレメトリ、その他の保護関連資料が格納されるファイル パス 


* **useInMemoryStorage**: 状態のキャッシュをディスクではなくメモリに格納します 


* **isLicenseCachingEnabled**: 保護 SDK ライセンスのキャッシュを有効または無効にします 


* **authDelegate**: 認証に使用される callback オブジェクト (クライアント アプリケーションで実装されます) 


* **observer**: [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信する [Observer](class_mip_protectionprofile_observer.md) インスタンス


* **applicationInfo**: 保護 SDK を利用しているアプリケーションに関する情報


  
### <a name="getpath"></a>GetPath
ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。

  
**戻り値**: ログ、テレメトリ、その他の保護関連資料が格納されるパス
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
キャッシュが (ディスク上ではなく) メモリにのみ格納されているかどうかを取得します

  
**戻り値**: キャッシュがメモリにのみ格納される場合は true
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
ライセンスのキャッシュが有効かどうかを取得します。

  
**戻り値**: 保護 SDK ライセンスのキャッシュが有効の場合は true
  
### <a name="getauthdelegate"></a>GetAuthDelegate
認証トークンを取得するために使用する認証委任を取得します。

  
**戻り値**: 認証トークンを取得するために使用する認証委任
  
### <a name="consentdelegate"></a>ConsentDelegate
サービスに接続するために使用する同意委任を取得します。

  
**戻り値**: サービスに接続するために使用する同意委任
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
[ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。

  
**戻り値**: [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信する[オブザーバー](class_mip_protectionprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
保護 SDK を利用しているアプリケーションに関する情報を取得します。

  
**戻り値**: 保護 SDK を利用しているアプリケーションに関する情報
  
### <a name="optouttelemetry"></a>OptOutTelemetry
テレメトリの収集をすべて無効にします。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
テレメトリの収集が無効になっているかどうかを取得します。

  
**戻り値**: テレメトリの収集が無効になっているかどうか
  
### <a name="loggerdelegate"></a>LoggerDelegate
アプリケーションによって提供されるロガー委任を取得します (提供される場合)。

  
**戻り値**: ログの記録に使用されるロガー委任
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
外部のロガーの実装を使用します。
クライアント アプリケーションで独自のロガー実装を使用する場合は、これを呼び出す必要があります
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
テレメトリ初期化をスキップするかどうかを取得します。

  
**戻り値**: テレメトリ初期化をスキップするかどうか
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
テレメトリ初期化を無効にします。
これは通常クライアント アプリケーションによって呼び出されず、重複する初期化を防ぐために (テレメトリを既に初期化している) File SDK によって使用されます
  
### <a name="setsessionid"></a>SetSessionId
セッション ID を設定します。

パラメーター:  
* **sessionId**: ログ/テレメトリを関連付けるために使用されるセッション ID


  
### <a name="getsessionid"></a>GetSessionId
セッション ID を取得します。

  
**戻り値**: ログ/テレメトリを関連付けるために使用されるセッション ID