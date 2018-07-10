# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
アプリケーションでは、保護操作を実行する前に [ProtectionProfile](class_mip_protectionprofile.md) を作成する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  エンジンの一覧操作を開始します。
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  プロファイルへの新しい保護エンジンの追加を開始します。
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  指定した ID を持つ保護エンジンの削除を開始します。指定したエンジンのすべてのデータが完全に削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。

  
**戻り値**: 初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される [Settings](class_mip_protectionprofile_settings.md)
  
### <a name="listenginesasync"></a>ListEnginesAsync
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバー関数に渡されるパラメーター。 


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="addengineasync"></a>AddEngineAsync
プロファイルへの新しい保護エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジン パラメーターを指定する [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) オブジェクト。 


* **context**: オブザーバー関数に渡されるパラメーター。 


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
指定した ID を持つ保護エンジンの削除を開始します。指定したエンジンのすべてのデータが完全に削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に渡されるパラメーター。 


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。