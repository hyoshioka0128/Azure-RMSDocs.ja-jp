# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
作成時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
 public const std::string& GetPath() const  |  ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。
 public const ApplicationInfo& GetApplicationInfo() const  |  保護 SDK を利用しているアプリケーションに関する情報を取得します。
 public bool GetSkipTelemetryInit() const  |  テレメトリ初期化をスキップするかどうかを取得します。
 public void SetSkipTelemetryInit()  |  テレメトリ初期化を無効にします。
 public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
 public const std::string& GetSessionId() const  |  セッション ID を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **path**: ログ、テレメトリ、その他の保護関連資料が格納されるファイル パス 


* **observer**: [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信する [Observer](class_mip_protectionprofile_observer.md) インスタンス


* **applicationInfo**: 保護 SDK を利用しているアプリケーションに関する情報


  
### <a name="getpath"></a>GetPath
ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。

  
**戻り値**: ログ、テレメトリ、その他の保護関連資料が格納されるパス
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
[ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。

  
**戻り値**: [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信する [Observer](class_mip_protectionprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
保護 SDK を利用しているアプリケーションに関する情報を取得します。

  
**戻り値**: 保護 SDK を利用しているアプリケーションに関する情報
  
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