# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
作成時および有効期間全体にわたって [ProtectionProfile](#classmip_1_1_protection_profile) によって使用される[設定](#classmip_1_1_protection_profile_1_1_settings)。
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline  SettingsProtectionProfile::Observer > & observer,const ApplicationInfo & applicationInfo) public inline const std::string & GetPath | ログ、テレメトリ、その他の保護関連資料が格納されるパスを取得します。
public inline const std::shared_ptr< ProtectionProfile::Observer > & GetObserver public inline const ApplicationInfo & GetApplicationInfo | 保護 SDK を利用するアプリケーションに関連する情報を取得します。
public inline bool GetSkipTelemetryInit | テレメトリ初期化をスキップする必要があるかどうかを取得します。
public inline void SetSkipTelemetryInit | テレメトリ初期化を無効にします。
public inline void SetSessionId | Sets the session id. public inline const std::string & GetSessionId | セッション ID を取得します。
## <a name="members"></a>メンバー
### <a name="settings"></a>Settings
[ProtectionProfile::Settings](#classmip_1_1_protection_profile_1_1_settings) コンストラクター。
#### <a name="parameters"></a>パラメーター
* path: ログ、テレメトリ、その他の保護関連資料が格納されるファイル パス 
* observer: [ProtectionProfile](#classmip_1_1_protection_profile) に関連するイベントの通知を受信する [Observer](#classmip_1_1_protection_profile_1_1_observer) インスタンス
* applicationInfo: 保護 SDK を利用しているアプリケーションに関する情報
### <a name="getpath"></a>GetPath
ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。
#### <a name="returns"></a>戻り値
ログ、テレメトリ、その他の保護関連資料が格納されるパス
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
[ProtectionProfile](#classmip_1_1_protection_profile) に関連するイベントの通知を受信するオブザーバーを取得します。
#### <a name="returns"></a>戻り値
[ProtectionProfile](#classmip_1_1_protection_profile) に関連するイベントの通知を受信する[オブザーバー](#classmip_1_1_protection_profile_1_1_observer)
### <a name="applicationinfo"></a>ApplicationInfo
保護 SDK を利用しているアプリケーションに関する情報を取得します。
#### <a name="returns"></a>戻り値
保護 SDK を利用しているアプリケーションに関する情報
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
テレメトリ初期化をスキップするかどうかを取得します。
#### <a name="returns"></a>戻り値
テレメトリ初期化をスキップするかどうか
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
テレメトリ初期化を無効にします。
これは通常クライアント アプリケーションによって呼び出されず、重複する初期化を防ぐために (テレメトリを既に初期化している) File SDK によって使用されます
### <a name="setsessionid"></a>SetSessionId
セッション ID を設定します。
#### <a name="parameters"></a>パラメーター
* sessionId: ログ/テレメトリを関連付けるために使用されるセッション ID
### <a name="getsessionid"></a>GetSessionId
セッション ID を取得します。
#### <a name="returns"></a>戻り値
ログ/テレメトリを関連付けるために使用されるセッション ID