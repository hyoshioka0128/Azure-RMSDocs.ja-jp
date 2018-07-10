# <a name="class-mipprotectionenginesettings"></a>class mip::ProtectionEngine::Settings 
作成時および有効期間全体にわたって [ProtectionEngine](class_mip_protectionengine.md) によって使用される[設定](class_mip_protectionengine_settings.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  新しいエンジンを作成するための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  既存のエンジンを読み込むための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。
 public const std::string& GetEngineId() const  |  エンジン ID を取得します。
 public void SetEngineId(const std::string& engineId)  |  エンジン ID を設定します。
 public const Identity& GetIdentity() const  |  エンジンに関連付けられたユーザー ID を取得します。
 public void SetIdentity(const Identity& identity)  |  エンジンに関連付けられるユーザー ID を設定します。
 public const std::string& GetClientData() const  |  クライアントに指定されたカスタム データを取得します。
 public const std::string& GetLocale() const  |  エンジン データが書き込まれるロケールを取得します。
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  テストや実験に使用する名前と値のペアを設定します。
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  テストや実験に使用する名前と値のペアを取得します。
 public void SetSessionId(const std::string& sessionId)  |  ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。
 public const std::string& GetSessionId() const  |  エンジンのセッション ID を取得します。
 public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  クラウド境界を指定するために使用する、クラウド エンドポイント ベース URL を設定します。
 public const std::string& GetCloudEndpointBaseUrl() const  |  cloudEndpointBaseUrl を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
新しいエンジンを作成するための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。

パラメーター:  
* **identity**: [ProtectionEngine](class_mip_protectionengine.md) に関連付けられる ID


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **locale**: エンジンの出力のロケール (既定値は "en-US")。


  
### <a name="settings"></a>Settings
既存のエンジンを読み込むための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。

パラメーター:  
* **engineId**: 読み込まれるエンジンの一意識別子 


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **locale**: エンジンの出力のロケール (既定値は "en-US")。


  
### <a name="getengineid"></a>GetEngineId
エンジン ID を取得します。

  
**戻り値**: エンジン ID
  
### <a name="setengineid"></a>SetEngineId
エンジン ID を設定します。

パラメーター:  
* **engineId**: エンジン ID。


  
### <a name="getidentity"></a>GetIdentity
エンジンに関連付けられたユーザー ID を取得します。

  
**戻り値**: エンジンに関連付けられたユーザー ID
  
### <a name="setidentity"></a>SetIdentity
エンジンに関連付けられるユーザー ID を設定します。

パラメーター:  
* **identity**: エンジンに関連付けられるユーザー ID


  
### <a name="getclientdata"></a>GetClientData
クライアントに指定されたカスタム データを取得します。

  
**戻り値** クライアントに指定されたカスタム データ
  
### <a name="getlocale"></a>GetLocale
エンジン データが書き込まれるロケールを取得します。

  
**戻り値**: エンジン データが書き込まれるロケール
  
### <a name="setcustomsettings"></a>SetCustomSettings
テストや実験に使用する名前と値のペアを設定します。

パラメーター:  
* **customSettings**: テストや実験に使用する名前と値のペア


  
### <a name="getcustomsettings"></a>GetCustomSettings
テストや実験に使用する名前と値のペアを取得します。

  
**戻り値**: テストや実験に使用する名前と値のペア
  
### <a name="setsessionid"></a>SetSessionId
ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。

パラメーター:  
* **sessionId**: ログ/テレメトリの相関関係に使用するエンジンのセッション ID


  
### <a name="getsessionid"></a>GetSessionId
エンジンのセッション ID を取得します。

  
**戻り値** エンジンのセッション ID
  
### <a name="setcloudendpointbaseurl"></a>SetCloudEndpointBaseUrl
クラウド境界を指定するために使用する、クラウド エンドポイント ベース URL を設定します。

パラメーター:  
* **cloudEndpointBaseUrl**: 保護エンドポイントに関連付けられたベース URL


  
### <a name="getcloudendpointbaseurl"></a>GetCloudEndpointBaseUrl
cloudEndpointBaseUrl を取得します。

  
**戻り値**: 保護エンドポイントに関連付けられたベース URL