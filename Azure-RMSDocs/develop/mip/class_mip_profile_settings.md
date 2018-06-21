# <a name="class-mipprofilesettings"></a>class mip::Profile::Settings 
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  プロファイルを構成するためのインターフェイス。
 public const std::string& GetPath() const  |  保存された状態へのパスを取得します。
 public bool GetUseInMemoryStorage() const  |  Use In Memory Storage フラグを取得します。
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  認証委任を取得します。
public const std::shared_ptr<Profile::Observer>& GetObserver() const  |  イベント オブザーバーを取得します。
 public const ApplicationInfo GetApplicationInfo() const  |  アプリケーション情報を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
プロファイルを構成するためのインターフェイス。

パラメーター:  
* **path**: sdk がプロファイル状態を格納するディレクトリへのパス。 


* **useInMemoryStorage**: 状態をディスクに保存する必要があるかどうかを示すフラグ。 


* **authDelegate**: 認証トークンを取得するために SDK によって使用される認証委任。 


* **observer**: [Profile::Observer](class_mip_profile_observer.md) インターフェイスを実装するクラス。 nullptr にすることができます。 


* **applicationInfo**: サービスへのアクセスに使用されるアプリケーション識別子。


  
### <a name="getpath"></a>GetPath
保存された状態へのパスを取得します。

  
**戻り値**: 保存された状態へのパス。
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Use In Memory Storage フラグを取得します。

  
**戻り値**: メモリでの使用が設定されている場合は true、それ以外の場合は false。
  
### <a name="getauthdelegate"></a>GetAuthDelegate
認証委任を取得します。

  
**戻り値**: 認証委任。
  
### <a name="profileobserver"></a>Profile::Observer
イベント オブザーバーを取得します。

  
**戻り値**: イベント オブザーバー。
  
### <a name="applicationinfo"></a>ApplicationInfo
アプリケーション情報を取得します。

  
**戻り値**: アプリケーション情報。